<template>
  <div id="app">
    <Home v-if="!isLogin"/>
    <Editor 
      v-if="isLogin" 
      :user="userData"/>
  </div>
</template>

<script>
import Home from "./components/Home.vue";
import Editor from "./components/Editor.vue";

export default {
  name: "App",
  components: {
    Home: Home,
    Editor: Editor
  },
  data() {
    return {
      isLogin: false,
      userData: null
    };
  },
  created: function() {
    firebase.auth().onAuthStateChanged(user => {
      if (user) {
        this.isLogin = true;
        this.userData = user;
      } else {
        this.isLogin = false;
        this.userData = null;
      }
    });
  }
};
</script>
