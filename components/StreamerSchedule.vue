<template>
  <v-row>
    <v-col>
      <v-sheet height="400">
        <v-calendar
          ref="calendar"
          :now="today"
          :value="today"
          :events="events"
          color="primary"
          type="week"
        ></v-calendar>
      </v-sheet>
    </v-col>
  </v-row>
</template>

<script>
export default {
    data() {
        return {
            today: Date.now(),
            events: []
        }
    },
    async mounted() {
        const id = this.$route.params.id;
        const res = await this.$axios.get('/detail/' + id);
        const item = res.data;
        this.id = item.id;
        this.start = item.start;
        this.end = item.end;
    },
    mounted () {
      this.$refs.calendar.scrollToTime('08:00')
    },
}
</script>