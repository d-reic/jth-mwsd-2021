<template>
  <view>
    <touchable-opacity class="list-message" :on-press="toggleButtons">
      <text>{{ item.email }} says "{{ item.text }}"</text>
    </touchable-opacity>
    <view v-if="showButtons">
      <button class="button" title="Edit" @press="editMessage"></button>
      <button class="button" title="Delete" @press="deleteMessage"></button>
    </view>
    <view v-if="showEditTextfield">
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
        v-model="text"
      />
      <button
        class="button"
        title="Update message"
        @press="updateMessage"
      ></button>
    </view>
  </view>
</template>

<script>
import firebase from "firebase/app";

// Add the Firebase products that you want to use
require("firebase/database");
require("firebase/auth");
export default {
  props: {
    item: {
      Type: Object,
    },
  },
  data() {
    return {
      showButtons: false,
      text: "",
      showEditTextfield: false,
    };
  },
  methods: {
    toggleButtons() {
      if (
        this.item.email == firebase.auth().currentUser.email &&
        this.showButtons == false
      ) {
        console.log(firebase.auth().currentUser.email);
        this.showButtons = true;
      } else {
        this.showButtons = false;
        this.showEditTextfield = false;
      }
    },
    editMessage() {
      //edit
      this.showEditTextfield = true;
    },
    deleteMessage() {
      // delete message
      const ref = firebase.database().ref("messages");
      var deleteRef = ref.child(this.item.key);
      deleteRef.remove();
    },
    updateMessage() {
      // update message
      const ref = firebase.database().ref("messages");
      var updateRef = ref.child(this.item.key);
      updateRef.update({
        text: this.text,
      });
      this.showButtons = false;
      this.showEditTextfield = false;
    },
  },
};
</script>

<style>
.list-message {
  border-color: red;
  border-style: solid;
  border-radius: 5;
  border-width: 2;
  padding: 10px;
  margin: 4px;
  background-color: white;
  width: 200;
}
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
