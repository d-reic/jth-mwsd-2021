<template>
  <view class="container">
    <text class="text-color-primary">Accelerometer</text>
    <text class="text-color-primary">X: {{ accelerometerData.x }}</text>
    <text class="text-color-primary">Y: {{ accelerometerData.y }}</text>
    <text class="text-color-primary">Z: {{ accelerometerData.z }}</text>
    <button title="Go to menu screen" @press="goToMenuScreen"></button>
  </view>
</template>

<script>
import { Accelerometer } from 'expo-sensors'

export default {
  // Declare `navigation` as a prop
  props: {
    navigation: {
      type: Object,
    },
  },
  data() {
    return {
      accelerometerData: {},
    }
  },
  mounted: function () {
    Accelerometer.setUpdateInterval(500)
    Accelerometer.addListener((accelerometerData) => {
      this.accelerometerData = accelerometerData
    })
  },
  methods: {
    goToMenuScreen() {
      this.navigation.navigate('Menu')
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
</style>
