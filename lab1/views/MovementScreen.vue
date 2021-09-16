<template>
  <view class="container">
    <text class="text-color-primary">Movement</text>
    <text class="text-color-primary">X: {{ accelerometerData.x }}</text>
    <text class="text-color-primary">Y: {{ accelerometerData.y }}</text>
    <text class="text-color-primary">Z: {{ accelerometerData.z }}</text>
        <image
      v-if="accelerometerData.y > 1.2 || accelerometerData.y < 0.8"
      :style="{ height: 150, width: 150 }"
      :source="require('./../img/arrow_up.png')"
    />
        <image
      v-if="accelerometerData.x > 0.2 || accelerometerData.x < -0.2"
      :style="{ height: 150, width: 150 }"
      :source="require('./../img/arrow_left.png')"
    />
        <image
      v-if="accelerometerData.y > 1.2 || accelerometerData.y < 0.8"
      :style="{ height: 150, width: 150 }"
      :source="require('./../img/arrow_down.png')"
    />
        <image
      v-if="accelerometerData.x > 0.2 || accelerometerData.x < -0.2"
      :style="{ height: 150, width: 150 }"
      :source="require('./../img/arrow_right.png')"
    />
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
