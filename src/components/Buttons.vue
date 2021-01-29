<template>
  <div>
    <b-button-group vertical>
      <b-button
        block
        @click="resetTimer"
        variant="success"
        class="chooseButton"
      >
        another {{ time }} minutes
      </b-button>

      <b-button
        block
        @click="setBreak5min"
        variant="warning"
        class="chooseButton"
      >
        Give us 5 minute break
      </b-button>
    </b-button-group>
  </div>
</template>

<script>
export default {
  name: "Buttons",
  props: {
    time: {
      required: true,
      type: Number,
    },
  },
  methods: {
    // Emit to parent 5 min break
    setBreak5min() {
      this.$emit("setTime5min", 5);
    },
    // emit to parent {time} break
    resetTimer() {
      this.$emit("resetTimer", this.time);
    },
  },
};
</script>

<style scoped>
.chooseButton {
  border: none;
  height: 50%;
  width: 100%;
  font-size: 300%;
  font-family: "Bungee Shade", cursive;
}
div {
  width: 100vw;
  height: 100vh;
}
</style>