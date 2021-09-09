<template>
  <view class="container">
    <text class="text-color-primary">Vibration</text>
    <button title="Vibrate" @press="startVibration"></button>
    <button title="Go to menu screen" @press="goToMenuScreen"></button>
  </view>
</template>

<script>
import {Vibration} from 'react-native'
export default {
  // Declare `navigation` as a prop
  props: {
    navigation: {
      type: Object,
    },
  },
  methods: {
    goToMenuScreen() {
      this.navigation.navigate('Menu')
    },
    startVibration() {
      console.log('vibrate')
      Vibration.vibrate(1000);
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
