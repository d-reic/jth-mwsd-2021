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
     <button class="button" title="Vibration" @press="goToVibrationScreen"></button>
     <button class="button" title="Language" @press="goToLanguageScreen"></button>
     <button class="button" title="Movement" @press="goToMovementScreen"></button>
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
     goToVibrationScreen() {
      this.navigation.navigate('Vibrate')
    },
       goToLanguageScreen() {
      this.navigation.navigate('Language')
    },
       goToMovementScreen() {
      this.navigation.navigate('Movement')
    }
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
    background-color: #bbb;
    margin: 10px 0;
    padding: 10px;
    width: 100%;
}
</style>
