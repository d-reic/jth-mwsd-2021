<template>
  <view class="container">
    <text class="text-color-primary">Vibration</text>
    <button title="Vibrate" @press="startVibration"></button>
    <button title="Go to menu screen" @press="goToMenuScreen"></button>
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
  data() {
    return {
      accelerometerData: {},
    }
  },
  methods: {
    goToMenuScreen() {
      this.navigation.navigate('Menu')
    },
    startVibration() {
      console.log('vibrate')
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
