<template>
  <view class="container">
    <text class="text-color-primary">ChatComponent!</text>
    <text-input
      :style="{ height: 40, width: 100, borderColor: 'gray', borderWidth: 1 }"
      v-model="message"
    />
    <button title="Send message" @press="sendMessage"></button>
    <button title="Sign out" @press="signOut"></button>
  </view>
</template>

<script>
export default {
  props: {
    navigation: {
      type: Object,
    },
  },
  data: function () {
    return {
      message: ""
    };
  },
  methods: {
    signOut() {
      // initiate signOut Process here
    },
    sendMessage() {
     // send message to firebase
    },
  },
};
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
