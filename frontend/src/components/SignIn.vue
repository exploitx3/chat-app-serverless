<template>
  <main>
    <h1>AWS Chat</h1>
    <form class="container padded" @submit.prevent="triggerSignIn">
      <input type="text" placeholder="username" v-model="usernameC">
      <input type="password" placeholder="password" v-model="pass">
      <button type="submit" class="block">Sign In</button>
    </form>
    <nav class="simple">
      <div>
        <router-link to="/signup">Sign Up</router-link>
      </div>
      <div>
        <router-link :to="{name: 'ForgotPassword'}">Forgot Password?</router-link>
      </div>
    </nav>
  </main>
</template>
<script>
import { mapActions } from "vuex";
export default {
  props: ["username"],
  data() {
    return {
      usernameC: "",
      pass: ""
    };
  },
  methods: {
    triggerSignIn() {
      this.signIn({ username: this.usernameC, pass: this.pass }).then(
        () => {
          console.log("going to chats now");
          this.$router.push({ name: "Group" });
        },
        () => {
          console.log("there was an error");
          alert("there was an error");
        }
      );
    },

    ...mapActions("cognito", {
      signIn: "signIn"
    })
  },
  created() {
    this.usernameC = this.username;
  }
};
</script>
<style lang="scss" scoped>
main {
 background: linear-gradient(322deg, #0098ff, #0df700, #005cf7);
background-size: 600% 600%;

-webkit-animation: AnimationName 59s ease infinite;
-moz-animation: AnimationName 59s ease infinite;
animation: AnimationName 59s ease infinite;

@-webkit-keyframes AnimationName {
    0%{background-position:9% 0%}
    50%{background-position:92% 100%}
    100%{background-position:9% 0%}
}
@-moz-keyframes AnimationName {
    0%{background-position:9% 0%}
    50%{background-position:92% 100%}
    100%{background-position:9% 0%}
}
@keyframes AnimationName { 
    0%{background-position:9% 0%}
    50%{background-position:92% 100%}
    100%{background-position:9% 0%}
}
}
nav div {
  margin-bottom: 0.5em;
}
</style>