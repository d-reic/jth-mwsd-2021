<template>
  <view class="container">
    <text class="heading">Chat!</text>
    <touchable-opacity :on-press="onPressMessage">
      <text class="message" v-for="message in messages" :key="message.key"
        >User {{ message.email }} sent this message: {{ message.text }}</text
      ></touchable-opacity
    >
    <text class="text-title-primary">Enter message</text>
    <text-input
      class="message-input"
      v-model="messageInput"
      :style="{ height: 40, width: 100, borderColor: 'gray', borderWidth: 1 }"
    ></text-input>
    <button class="send-button" title="Send" @press="onSendMessage"></button>
    <button class="button" title="Sign out" @press="signOut"></button>
    <button
      class="button"
      title="Delete account"
      @press="deleteAccount"
    ></button>
    <text class="text-color-primary" v-if="showError">{{ errorMessage }}</text>
  </view>
</template>

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
    return {
      messageInput: "",
      messagesRef: "messages",
      messages: [],
      showError: false,
      errorMessage: "",
    };
  },

  methods: {
    onSendMessage() {
      var postref = firebase.database().ref("messages").push();
      postref.set(
        { email: firebase.auth().currentUser.email, text: this.messageInput },
        (err) => {
          if (err) {
            // Alert or show this error to the user if anything goes wrong
            console.log({ err });
          }
          this.messageInput = "";
        }
      );
    },
    signOut() {
      firebase
        .auth()
        .signOut()
        .then((something) => {
          console.log("Successfully logged out");
          this.navigation.navigate("SignIn");
        })
        .catch((error) => {
          const errorCode = error.code;
          const errorMessage = error.message;
          console.log(errorCode);
          console.log(errorMessage);
          // ..
        });
    },
    onPressMessage() {
      console.log("Messagepressed");
    },
    deleteAccount() {
      const ref = firebase.database().ref("messages");
      ref
        .orderByChild("email")
        .equalTo(firebase.auth().currentUser.email)
        .once("value")
        .then((snapshot) => {
          snapshot.forEach(function (childSnapshot) {
            var childKey = childSnapshot.key;
            var childData = childSnapshot.val();
            var deleteRef = ref.child(childKey);
            deleteRef.remove();
          });
        });
      firebase
        .auth()
        .currentUser.delete()
        .then((something) => {
          console.log("Successfully deleted account");
          this.navigation.navigate("SignIn");
          this.showError = false;
          this.errorMessage = "";
        })
        .catch((error) => {
          const errorCode = error.code;
          const errorMessage = error.message;
          console.log(errorCode);
          console.log(errorMessage);
          this.errorMessage = error.message;
          this.showError = true;
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
            const email = fbMessage.email;
            console.log(fbMessage.text);
            console.log(fbMessage.email);
            this.messages.push({ key, text, email });
          }
        }
      });
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
.text-title-primary {
  color: blue;
  margin-top: 10;
  margin-bottom: 5;
  font-size: 25;
}
.heading {
  color: green;
  font-size: 25;
}
.message-input {
  width: 55%;
  margin-right: 2%;
}

.send-button {
  width: 42%;
}

.message {
  color: red;
  margin-top: 10;
  margin-bottom: 10;
  font-size: 20;
}
</style>
