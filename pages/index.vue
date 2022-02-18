<template>
  <div>
    <h2 class="text-center mb-2">Popular streamers</h2>
    <v-row>
      <v-col
        cols="auto"
        sm="6"
        lg="3"
        md="4"
        v-for="streamer in popstreamers"
        :key="streamer.id"
      >
        <PreviewPopstreamers :popstreamer="streamer"></PreviewPopstreamers>
      </v-col>
    </v-row>
  </div>
</template>

<script>
import PreviewPopstreamers from "../components/PreviewPopstreamers.vue";
export default {
  components: { PreviewPopstreamers },
  data() {
    return {
      popstreamers: [],
    };
  },
  async mounted() {
    const res = await this.$axios.get("/popstreamers");
    console.log(res.data);
    this.popstreamers = res.data;
  },
};
</script>
