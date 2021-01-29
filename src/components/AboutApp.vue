<template>
  <div>
    <p>
      This app is a simple timer which help us track time when we are drinking
      spirits. Choose how many minutes you want to wait beetwen shots. After
      that time you will get two options reset or 5 more minutes. You can use it
      for other things. Feel free to use it as you want.
    </p>
  </div>
</template>

<script>
export default {};
</script>

<style scoped>
div {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
div > p {
  font-family: "Merriweather", serif !important;

  background: #eeeeee;
  padding: 25px;
  font-size: 2vw;
}
</style>