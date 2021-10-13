<template>
  <view class="container">
    <text class="heading">SIGN UP!</text>
    <text class="text-color-primary">Email</text>
    <text-input
      :style="{
        height: 40,
        width: 300,
        borderRadius: 5,
        borderColor: 'black',
        borderWidth: 5,
        backgroundColor: 'white',
        padding: 8,
      }"
      v-model="email"
    />
    <text class="text-color-primary">Password</text>
    <text-input
      :style="{
        height: 40,
        width: 300,
        borderRadius: 5,
        borderColor: 'black',
        borderWidth: 5,
        backgroundColor: 'white',
        padding: 8,
      }"
      v-model="password"
    />
    <touchable-opacity class="button" :on-press="signUp">
      <text>SIGN UP</text>
    </touchable-opacity>
    <touchable-opacity class="button" :on-press="signIn">
      <text>🔙</text>
    </touchable-opacity>
    <text class="text-color-primary" v-if="showError">{{ errorMessage }}</text>
  </view>
</template>

<script>
import firebase from "firebase/app";
require("firebase/auth");

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
      user: {},
      showError: false,
      errorMessage: "",
    };
  },
  methods: {
    signUp() {
      if (this.email == null || this.password == null) {
        console.log("Email or PW are empty!");
      } else {
        firebase
          .auth()
          .createUserWithEmailAndPassword(this.email, this.password)
          .then((userCredential) => {
            // Signed in
            console.log("Signed in!");
            this.email = "";
            this.password = "";
            this.showError = false;
            this.errorMessage = "";
            const user = userCredential.user;
            this.navigation.navigate("Chat");
          })
          .catch((error) => {
            this.errorMessage = error.message;
            this.showError = true;
          });
      }
    },
    signIn() {
      this.navigation.navigate("SignIn");
    },
  },
  mounted() {
    if (!firebase.apps.length) {
      // Prevent "hot reloading" to cause errors
      firebase.initializeApp(firebaseConfig);
    }
  },
};
</script>

<style>
.container {
  background-color: gray;
  align-items: center;
  justify-content: center;
  flex: 1;
}
.text-color-primary {
  color: white;
  padding: 8px;
}
.heading {
  color: yellow;
  font-size: 50;
  margin-bottom: 64px;
  background-color: purple;
  padding: 16;
  border-radius: 50;
}
.button {
  padding: 16px;
  background-color: lightblue;
  border-radius: 50;
  margin: 8px;
}
</style>
