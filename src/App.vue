<template>
  <div>
    <b-button id="informationButton" v-if="ShowSettings">
      <b-icon
        :icon="ShowAbout ? 'x-circle' : 'info-circle-fill'"
        scale="2"
        variant="info"
        align-v="top"
        align-h="right"
        @click="OpenAboutApp"
      />
    </b-button>
    <AboutApp v-if="ShowAbout"></AboutApp>
    <div v-if="!ShowAbout">
      <Buttons
        v-if="ShowOptions"
        :time="parseInt(this.breakTime)"
        @setTime5min="setTimeParent"
        @resetTimer="setTimeParent"
      />

      <div id="app" :style="`background:${backgroundColor}`">
        <b-row align-v="center" align-h="center">
          <Setup v-if="ShowSettings" @setTime="setTimeParent" id="setup" />

          <Timer
            v-if="ShowTimer"
            @endOfTimer="endOfTimerParent"
            @ChangeBg="changeBackground"
            :time="parseInt(this.time)"
          />
        </b-row>
      </div>
    </div>
  </div>
</template>

<script>
import Timer from "./components/Timer.vue";
import Buttons from "./components/Buttons.vue";
import Setup from "./components/Setup.vue";
import AboutApp from "./components/AboutApp.vue";

export default {
  name: "App",
  components: {
    Timer,
    AboutApp,
    Buttons,
    Setup,
  },
  data() {
    return {
      backgroundColor: "#FFFFFF",
      time: null,
      breakTime: null,
      ShowAbout: false,
      ShowSettings: true,
      ShowTimer: false,
      ShowOptions: false,
    };
  },
  methods: {
    SetBreak5(value) {
      this.time = value;
      this.ShowOptions = false;
      this.ShowSettings = false;
      this.ShowTimer = true;
    },
    // Show/Hide about app page
    OpenAboutApp() {
      this.ShowAbout = !this.ShowAbout;
    },
    // Changing background
    changeBackground(value) {
      this.backgroundColor = value;
    },
    // hide timer show buttons
    endOfTimerParent() {
      this.ShowOptions = true;
      this.ShowTimer = false;
    },
    // Set timer and show it
    setTimeParent(value) {
      this.time = value;
      this.breakTime = value;
      this.ShowOptions = false;
      this.ShowSettings = false;
      this.ShowTimer = true;
    },
  },
};
</script>
<style scoped>
#setup {
  padding-top: 40vh;
}
html,
body,
#app {
  height: 100vh;
}
</style>
<style>
#informationButton {
  top: 15px;
  right: 15px;

  position: absolute;
  border: none;
  background: none;
}
* {
  overflow-x: hidden;
  overflow-y: hidden;
}
body {
  font-family: "Bungee Shade", cursive;
}
</style>
