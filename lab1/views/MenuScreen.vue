<template>
  <view class="container">
    <text class="text-color-primary">Menu</text>
    <button class="button" title="Camera" @press="goToCameraScreen"></button>
    <button
      class="button"
      title="Accelerometer"
      @press="goToAccelerometerScreen"
    ></button>
    <button class="button" title="GPS" @press="goToGPSScreen"></button>
  </view>
</template>

<script>
export default {
  // Declare `navigation` as a prop
  props: {
    navigation: {
      type: Object,
    },
  },
  methods: {
    goToCameraScreen() {
      this.navigation.navigate('Camera')
    },
    goToAccelerometerScreen() {
      this.navigation.navigate('Accelerometer')
    },
    goToGPSScreen() {
      this.navigation.navigate('GPS')
    },
  },
}
</script>

<style>
.container {
  background-color: white;
  align-items: center;
  justify-content: center;
  flex: 1;
}
.text-color-primary {
  color: blue;
}
.button {
  color: red;
}
</style>
