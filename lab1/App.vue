<template>
  <app-navigator></app-navigator>
</template>

<script>
import {
  createAppContainer,
  createStackNavigator,
} from "vue-native-router";

import MenuScreen from "./views/MenuScreen.vue";
import CameraScreen from "./views/CameraScreen.vue";
import GPSScreen from "./views/GPSScreen.vue";
import AccelerometerScreen from "./views/AccelerometerScreen.vue"
import VibrateScreen from "./views/VibrateScreen.vue"
import LanguageScreen from "./views/LanguageScreen.vue"
import MovementScreen from "./views/MovementScreen.vue"

const StackNavigator = createStackNavigator(
  {
    Menu: MenuScreen,
    Camera: CameraScreen,
    GPS: GPSScreen,
    Accelerometer: AccelerometerScreen,
    Vibrate: VibrateScreen,
    Language: LanguageScreen,
    Movement: MovementScreen
  },
  {
    initialRouteName: 'Menu',
  }
);

const AppNavigator = createAppContainer(StackNavigator);

export default {
  components: { AppNavigator },
}
</script>