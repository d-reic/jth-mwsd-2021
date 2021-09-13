<template>
  <view class="container">
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
    <button title="Back to Sign In" @press="signIn"></button>
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
      // initiate signUp Process here
    },
    signIn() {
      this.navigation.navigate("SignIn");
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
