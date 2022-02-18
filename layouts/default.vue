<template>
  <v-app dark>
    <!--<v-navigation-drawer
      v-model="drawer"
      :mini-variant="miniVariant"
      :clipped="clipped"
      fixed
      app
    >
      <v-list>
        <v-subheader>Popular Right Now</v-subheader>
        <v-list-item two-line v-for="streamer in popstreamers" :key="streamer.id">
          <v-list-item-content>
            <v-list-item-title v-text="streamer.name"></v-list-item-title>
            <v-list-item-subtitle v-text="streamer.ccvthreedays"> viewers </v-list-item-subtitle>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer> -->
    <v-app-bar :clipped-left="clipped" fixed app>
      <!-- <v-app-bar-nav-icon @click.stop="drawer = !drawer" /> -->
      <v-toolbar-title v-text="maintitle" />
      <v-spacer />
      <StreamerSearchBar></StreamerSearchBar>
      <v-menu bottom left>
        <template v-slot:activator="{ on, attrs }">
          <v-btn dark icon v-bind="attrs" v-on="on" color="purple">
            <v-icon>{{ icons.mdiAccount }}</v-icon>
          </v-btn>
        </template>

        <v-list>
          <v-list-item
            v-for="item in menuitems"
            :key="item.title"
            @click="selectSection(item)"
          >
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item>
        </v-list>
      </v-menu>
    </v-app-bar>
    <v-main>
      <v-container>
        <Nuxt />
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import { mdiAccount } from "@mdi/js";
import StreamerSearchBar from "../components/StreamerSearchBar.vue";
export default {
  components: {StreamerSearchBar},
  data() {
    return {
      clipped: true,
      drawer: true,
      fixed: false,
      icons: {
        mdiAccount,
      },
      //popstreamers: [],
      miniVariant: false,
      menuitems: [{ title: "Login or Register" }, { title: "Logout" }],
      right: true,
      rightDrawer: false,
      maintitle: "Livestream schedules",
    };
  },
  /*async mounted() {
    const res = await this.$axios.get("/popstreamers");
    console.log(res.data);
    this.popstreamers = res.data;
  },*/
  methods: {
    selectSection(item) {
      switch (item.title) {
        case "Login or Register":
          this.$router.push("/logreg");
          break;
        case "Logout":
          this.$router.push("/");
      }
    },
  },
};
</script>
