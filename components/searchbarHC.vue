
<template>
  <v-autocomplete
    clearable
    :loading="isLoading"
    :items="streamers"
    :search-input.sync="search"
    hide-details
    item-text="name"
    item-value="id"
    label="Streamer's name"
    solo-inverted
  ></v-autocomplete>
</template>

<script>

import _ from "lodash";

export default ({
    data: () => ({
    streamers: [], // this is where all the streamer data will be stored
    isLoading: true, // variable to determine if the results are still being fetched from the API
    search: null // this is where the query will be stored
  }),
  async mounted(){
      
  },
  methods: {
      getStreamers(params = "") {
      // this function will fetch game data from URL with whatever api parameters you pass to the parameter `params`
      this.$axios.get("/popstreamers/" + params)
        .then(resp => {
          // fetch data
          let tempStreamers = [...this.streamers.slice(0), ...resp.data.results]; //copy of this.streamers + new data
          this.streamers = _.uniqBy(tempStreamers, "name"); // remove any duplicates
          this.isLoading = false; // now that the data is in the array `streamers`, we can set isLoading to false
        })
        .catch(e => {
          // code to run if there was an error
          console.error(e); // display error message
        });
    },

    searchStreamers(query) {
      // this function will call getStreamers() with the search query formatted as an API parameter (?search=YOUR_QUERY)
      let searchQuery = encodeURI("?search=" + query); // URI encode the query so it is able to be fetched properly
      this.getStreamers(searchQuery);
    },
  },
  
  watch: {
    search: _.debounce(function(query) {
      // debounce with a a value of 250 will allow this function to be every 250 milliseconds at most. So if the user is typing continually, it won't run until the user stops.
      this.searchStreamers(query);
    }, 500)
  },

  created() {
    this.getStreamers(); // load the first 20
  }
})
</script>
