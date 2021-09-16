<template>
  <view class="container">
    <text class="text-title-primary">Enter message</text>
    <text-input
      v-model="messageInput"
      :style="{ height: 40, width: 100, borderColor: 'gray', borderWidth: 1 }"
    ></text-input>
    <button title="Send" @press="onSendMessage"></button>

    <text class="text-title-primary">Earlier messages</text>
    <text v-for="message in messages" :key="message.key">{{
      message.text
    }}</text>
    <button title="Sign out" @press="signOut"></button>
  </view>
</template>

<style>
.container {
  background-color: white;
  align-items: center;
  justify-content: center;
  flex: 1;
}
.text-title-primary {
  color: blue;
  margin-top: 10;
  margin-bottom: 5;
  font-size: 25;
}
</style>

<script>
// Firebase App (the core Firebase SDK) is always required and
// must be listed before other Firebase SDKs
import firebase from "firebase/app";

// Add the Firebase products that you want to use
require("firebase/database");
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
  data() {
    return { messageInput: "", messagesRef: "", messages: [] };
  },

  methods: {
    onSendMessage() {
      this.messagesRef.push({ text: this.messageInput }, (err) => {
        if (err) {
          // Alert or show this error to the user if anything goes wrong
          console.log({ err });
        }
      });
    },
    signOut() {
      firebase
        .auth()
        .signOut()
        .then((something) => {
          console.log("Successfully logged out");
         this.navigation.navigate("SignIn")
        })
        .catch((error) => {
          const errorCode = error.code;
          const errorMessage = error.message;
          console.log(errorCode);
          console.log(errorMessage);
          // ..
        });
    },
  },

  mounted() {
    if (!firebase.apps.length) {
      // Prevent "hot reloading" to cause errors
      firebase.initializeApp(firebaseConfig);
    }

    // "messages" is the name of our data collection
    this.messagesRef = firebase.database().ref("messages");

    firebase
      .database()
      .ref("messages") // "messages" is the name of our data collection
      .on("value", (snap) => {
        // "value" is a firebase Query event type, Google "firebase.database.Query" for more

        // Empty the all showing messages to avoid duplicates
        this.messages = [];
        const fbVal = snap.val();

        for (const key in fbVal) {
          const fbMessage = fbVal[key];

          if (fbMessage.text) {
            const text = fbMessage.text;
            console.log(fbMessage.text);
            this.messages.push({ key, text });
          }
        }
      });
  },
};
</script>
