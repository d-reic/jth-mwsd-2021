<template>
  <view class="container">
    <text class="text-color-primary">GPS</text>
    <button title="Get Location" @press="getLocation">      
    </button>
    <text class="text-field-title">Latitude:</text>
    <text>{{ latitude }}</text>
<text class="text-field-title">Longitude:</text>
    <text>{{ longitude }}</text>
    <text class="text-field-title">Altitude:</text>
    <text>{{ altitude }}</text>
    <text class="text-error">{{ errorMessage }}</text>
    <button title="Go to menu screen" @press="goToMenuScreen"></button>
  </view>
</template>

<script>

import * as Location from "expo-location";
import * as Permissions from "expo-permissions";

export default {
  // Declare `navigation` as a prop
  props: {
    navigation: {
      type: Object,
    },
  },
  data: function () {
    return {
      location: {},
      latitude: '',
      longitude: '',
      altitude: '',
      errorMessage: '',
    }
  },
  methods: {
    goToMenuScreen() {
      this.navigation.navigate('Menu')
    },
    getLocation: function () {
      Location.requestForegroundPermissionsAsync()
        .then((status) => {
          if (!status.granted) {
            this.errorMessage = 'Permission to access location was denied'
          } else if (status.granted) {
            Location.getLastKnownPositionAsync({}).then((location) => {
              this.location = location
              this.latitude = location.coords.latitude
              this.longitude = location.coords.longitude
              this.altitude = location.coords.altitude
              this.errorMessage = ''
            })
          }
        })
        .catch((err) => {
          console.log(err)
        })
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
