<template>
  <view class="camera">
    <Camera ref="camera" class="camera" :type="cameraSettings.type" />
    <button :on-press="takePicture" title="Snap"></button>
    <button :on-press="switchCamera" title="Switch camera"></button>
    <button title="Go to menu screen" @press="goToMenuScreen"></button>
  </view>
</template>

<script>
import * as Permissions from 'expo-permissions'
import { Camera } from 'expo-camera'

export default {
  // Declare `navigation` as a prop
  props: {
    navigation: {
      type: Object,
    },
  },
  data: function () {
    return {
      cameraSettings: {
        show: false,
        flash: 'off',
        zoom: 0,
        autoFocus: 'on',
        type: Camera.Constants.Type.back,
        whiteBalance: 'auto',
        ratio: '16:9',
        ratios: [],
        barcodeScanning: false,
        faceDetecting: false,
        faces: [],
        newPhotos: false,
        permissionsGranted: false,
        pictureSize: undefined,
        pictureSizes: [],
        pictureSizeId: 0,
        showGallery: false,
        showMoreOptions: false,
      },
    }
  },
  mounted: function () {
    if (!this.cameraSettings.permissionsGranted) {
      Permissions.askAsync(Permissions.CAMERA)
        .then((status) => {
          this.cameraSettings.permissionsGranted = status.status === 'granted'
          this.cameraSettings.show = true
        })
        .catch((err) => {
          this.cameraSettings.show = false
          console.log(err)
        })
    } else {
      this.cameraSettings.show = !this.cameraSettings.show
    }
  },
  methods: {
    takePicture() {
      this.$refs.camera
        .takePictureAsync()
        .then((pic) => console.log('pic', pic))
    },
    goToMenuScreen() {
      this.navigation.navigate('Menu')
    },
    switchCamera() {
      if (this.cameraSettings.type == Camera.Constants.Type.back) {
        this.cameraSettings.type = Camera.Constants.Type.front
      } else {
        this.cameraSettings.type = Camera.Constants.Type.back
      }
    },
  },
  components: { Camera },
}
</script>
<style>
.container {
  flex: 1;
  background-color: white;
  align-items: center;
  justify-content: center;
}
.camera {
  flex: 1;
}
.text-color-primary {
  color: blue;
}
</style>
