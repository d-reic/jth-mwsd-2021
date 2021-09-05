<template>
  <view class="container">
    <text class="text-color-primary">{{ name }}</text>
    <text-input
      :style="{ height: 40, width: 100, borderColor: 'gray', borderWidth: 1 }"
      v-model="text"
    />
    <image
      v-if="imageShown"
      :style="{ height: 150, width: 150 }"
      :source="require('./img/me.jpg')"
    />
    <button :on-press="updateName" title="Update name" color="#841584" />
    <button :on-press="toggleImage" title="Hide your face" />
    <custom-button     
      v-for="example in examples"
      :key="example.text"
      :item="example"
    />
  </view>
</template>

<script>
import CustomButton from './components/CustomButton.vue'
export default {
  components: { CustomButton },
  data() {
    return {
      name: 'Daniel',
      text: '',
      imageShown: true,
      examples: [
        { id: 1, text: 'foo' },
        { id: 2, text: 'bar' },
        { id: 3, text: 'foobar' },
      ],
    }
  },
  methods: {
    updateName() {
      this.name = this.text
    },
    toggleImage() {
      this.imageShown = !this.imageShown
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
