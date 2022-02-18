<template>
    <v-text-field
      type="number"
      v-model.number="textfield"
      class="mt-8"
      solo
      placeholder="Search streamer's ID to check their schedule"
      prepend-icon="mdi-magnify"
      @click:prepend="ToDetail"
    ></v-text-field>
</template>

<script>
export default {

    data() {
        return {
            textfield: ''
        }
    },
    methods: {
        ToDetail(){
            if (typeof this.textfield == 'number'){
                this.$router.push("/detail/" + this.textfield);
            } else alert("insert an id number, please")
        }
    }
};
</script>
