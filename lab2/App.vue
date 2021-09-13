<template>
  <app-navigator></app-navigator>
</template>

<script>
import { createAppContainer, createStackNavigator } from "vue-native-router";

import SignUpComponent from "./views/SignUpComponent.vue";
import SignInComponent from "./views/SignInComponent.vue";
import ChatComponent from "./views/ChatComponent.vue";

const StackNavigator = createStackNavigator(
  {
    SignUp: SignUpComponent,
    SignIn: SignInComponent,
    Chat: ChatComponent,
  },
  {
    initialRouteName: "SignIn",
  }
);

const AppNavigator = createAppContainer(StackNavigator);

export default {
  components: { AppNavigator },
  data() {
    return {
      currentPage: "Test",
    };
  },
  methods: {
    navigate() {
      console.log("Navigate");
      //this.navigation.navigate('Menu')
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
