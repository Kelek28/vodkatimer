<template>
  <div>
    <label for="input-live">Enter break beetwen drinking:</label>
    <b-form-input
      size="lg"
      v-model="time"
      type="number"
      text
      @keyup.enter="setBreak"
    />
    <b-button
      class="mx-5 my-3"
      size="lg"
      variant="success"
      @click="setBreak"
      @keyup.enter="setBreak"
      :disabled="time <= 0"
      >Start caunting</b-button
    >
  </div>
</template>

<script>
export default {
  name: "Setup",
  data() {
    return {
      time: null,
    };
  },

  methods: {
    setBreak() {
      if (this.time > 0) {
        this.$emit("setTime", this.time);
      }
    },
  },
};
</script>
