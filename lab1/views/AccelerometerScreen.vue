<template>
  <view class="container">
    <text class="text-color-primary">Accelerometer</text>
    <text class="text-color-primary">{{ accelerometerData.x }}</text>
    <text class="text-color-primary">{{ accelerometerData.y }}</text>
    <text class="text-color-primary">{{ accelerometerData.z }}</text>
    <button title="Go to menu screen" @press="goToMenuScreen"></button>
  </view>
</template>

<script>
import { Accelerometer } from 'expo-sensors'

Accelerometer.setUpdateInterval(1000);
Accelerometer.addListener(accelerometerData => {
  this.accelerometerData = accelerometerData;
});

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
