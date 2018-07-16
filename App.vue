<template>
  <nb-container class="container">
    <app-loading v-if="!isAppReady" />
    <nb-header v-if="isAppReady">
      <nb-body>
        <nb-title>Torino Coding Society</nb-title>
      </nb-body>
    </nb-header>
    <nb-content v-if="isAppReady" padder>
      <event-list />
    </nb-content>
  </nb-container>
</template>

<script>
import Vue from "vue-native-core"
import { VueNativeBase } from "native-base"
import { AppLoading } from "expo"

import EventList from "./EventList"

Vue.use(VueNativeBase)

export default {
  components: { AppLoading, EventList },
  data: function() {
    return {
      isAppReady: false
    };
  },
  created: function() {
    this.loadFonts();
  },
  methods: {
    loadFonts: async function() {
      try {
        this.isAppReady = false;
        await Expo.Font.loadAsync({
          Roboto: require("native-base/Fonts/Roboto.ttf"),
          Roboto_medium: require("native-base/Fonts/Roboto_medium.ttf"),
          Ionicons: require("@expo/vector-icons/fonts/Ionicons.ttf")
        });
        this.isAppReady = true;
      } catch (error) {
        console.log("some error occured", error);
        this.isAppReady = true;
      }
    }
  }
}
</script>

<style>
.container {
  padding-top: 24px;
}
</style>
