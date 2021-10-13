<template>
  <view class="container">
    <text class="heading">SIGN IN!</text>
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
    <touchable-opacity class="button" :on-press="signIn">
      <text>SIGN IN</text>
    </touchable-opacity>
    <touchable-opacity class="button" :on-press="signUp">
      <text>SIGN UP</text>
    </touchable-opacity>
    <text class="text-color-primary" v-if="showError">{{ errorMessage }}</text>
  </view>
</template>

<script>
import firebase from "firebase/app";
require("firebase/auth");

// Your web app's Firebase configuration
const firebaseConfig = {
  apiKey: "AIzaSyBrma7NK0kAccH0lzJD_DvceOTDCSYKKfo",
  authDomain: "jth-mwsd-2021-reda21bw.firebaseapp.com",
  databaseURL:
    "https://jth-mwsd-2021-reda21bw-default-rtdb.europe-west1.firebasedatabase.app/",
  projectId: "jth-mwsd-2021-reda21bw",
  storageBucket: "jth-mwsd-2021-reda21bw.appspot.com",
  messagingSenderId: "934426003388",
  appId: "1:934426003388:web:442447560976af1d818db9",
};

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
      showError: false,
      errorMessage: "",
    };
  },
  methods: {
    signUp() {
      this.navigation.navigate("SignUp");
    },
    signIn() {
      if (this.email == null || this.password == null) {
        console.log("Email or PW are empty!");
      } else {
        firebase
          .auth()
          .signInWithEmailAndPassword(this.email, this.password)
          .then((userCredential) => {
            // Signed in
            console.log("Signed in!");
            const user = userCredential.user;
            this.email = "";
            this.password = "";
            this.showError = false;
            this.errorMessage = "";
            this.navigation.navigate("Chat");
          })
          .catch((error) => {
            this.errorMessage = error.message;
            this.showError = true;
          });
      }
    },
    chat() {
      this.navigation.navigate("Chat");
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
  color: green;
  font-size: 50;
  margin-bottom: 64px;
  background-color: yellow;
  padding: 16;
  border-radius: 50;
}
.button {
  padding: 16px;
  background-color: red;
  border-radius: 50;
  margin: 8px;
}
</style>
