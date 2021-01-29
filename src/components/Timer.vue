<template>
  <div id="Timer" :style="myStyle">
    <span v-if="hours">{{ hours | formatTime }}:</span>
    <span v-if="minutes">{{ minutes | formatTime }}:</span>
    <span v-if="currentTime">{{ seconds | formatTime }}</span>
  </div>
</template>

<script>
export default {
  name: "Timer",
  props: {
    time: {
      required: true,
      type: Number,
    },
  },
  data() {
    return {
      myStyle: {
        color: "#000000",
      },
      currentTime: null,
      deadline:
        new Date().setMinutes(new Date().getMinutes() + this.time) + 1000,
    };
  },

  mounted() {
    setTimeout(this.countdown, 1000);
  },
  computed: {
    seconds() {
      const seconds = Math.floor((this.currentTime / 1000) % 60);
      return seconds;
    },
    minutes() {
      const minutes = Math.floor((this.currentTime / 1000 / 60) % 60);
      return minutes;
    },
    hours() {
      const hours = Math.floor((this.currentTime / (1000 * 60 * 60)) % 24);
      return hours;
    },
  },
  filters: {
    formatTime(value) {
      if (value < 10) {
        return "0" + value;
      }
      return value;
    },
  },

  methods: {
    // Generate random RGB color for background
    generateRGB() {
      var num = Math.round(0xffffff * Math.random());
      const red = num >> 16;
      const green = (num >> 8) & 255;
      const blue = num & 255;
      this.myStyle.color = "#000000";
      if ((red + green + blue) / 3 < 120) {
        this.myStyle.color = "#FFFFFF";
      }
      return `rgb(${red},${green},${blue})`;
    },
    // Countdown function
    countdown() {
      this.currentTime = this.deadline - Date.parse(new Date());
      if (this.currentTime > 0) {
        setTimeout(this.countdown, 1000);
        this.$emit("ChangeBg", this.generateRGB());
      } else {
        this.currentTime = null;
        this.$emit("endOfTimer");
      }
    },
  },
};
</script>

<style scoped>
#Timer {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  font-family: "Bungee Shade", cursive;

  font-size: 15vw;
}
</style>
