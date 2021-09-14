<template>
  <view class="container">
    <text class="text-color-primary">SignInComponent</text>
      <text class="text-color-primary">Email</text>
    <text-input
      :style="{ height: 40, width: 100, borderColor: 'gray', borderWidth: 1 }"
      v-model="email"
    />
    <text class="text-color-primary">Password</text>
    <text-input
      :style="{ height: 40, width: 100, borderColor: 'gray', borderWidth: 1 }"
      v-model="password"
    />
    <button title="Sign Up" @press="signUp"></button>
     <button title="Chat" @press="chat"></button>
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
      email: "",
      password: "",
    };
  },
  methods: {
    signUp() {
      this.navigation.navigate("SignUp");
    },
    signIn() {
      // initiate signInProcess
    },
    chat() {
this.navigation.navigate("Chat");
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
