<template>
  <view class="container">
    <text class="text-color-primary">Language</text>
    <text class="text-color-primary">Configured language: {{ language }}</text>
    <text class="text-color-primary" v-if="language == 'en_US'">This is an English text!</text>
     <text class="text-color-primary" v-if="language == 'de_DE'">Das ist ein Text in deutscher Sprache!</text>
    <button title="Go to menu screen" @press="goToMenuScreen"></button>
  </view>
</template>

<script>
import { NativeModules, Platform } from 'react-native'
export default {
  // Declare `navigation` as a prop
  props: {
    navigation: {
      type: Object,
    },
  },
  data() {
    return {
     language: '',
    }
  },
  mounted: function () {
    this.language =
      Platform.OS === 'ios'
        ? NativeModules.SettingsManager.settings.AppleLocale ||
          NativeModules.SettingsManager.settings.AppleLanguages[0] // iOS 13
        : NativeModules.I18nManager.localeIdentifier    
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
