<template>
  <main>
    <h1>AWS Chat</h1>
    <div class="container padded">
      <form @submit.prevent="triggerConfirmRegistration">
        <input type="text" placeholder="username" v-model="usernameC">
        <input type="text" placeholder="enter code" v-model="code">
        <button class="block" type="submit">Confirm Code</button>
      </form>
      <button @click="triggerResendConfirmation" class="block">Resend Code</button> 
    </div>
    <nav class="simple">
      <router-link to="/signin">Sign In</router-link>
      <router-link to="/signup">Sign Up</router-link>
    </nav>
  </main>  
</template>
<script>
import { mapActions } from "vuex";
export default {
  props: ["username"],
  data() {
    return {
      code: "",
      usernameC: ""
    };
  },
  methods: {
    triggerConfirmRegistration() {
      if (!(this.username && this.code)) {
        return alert("Must have both username and code filled out!");
      }
      this.confirmRegistration({
        username: this.usernameC,
        code: this.code
      }).then(
        () => {
          this.$router.push({
            path: "/signin",
            query: { username: this.usernameC }
          });
        },
        () => {
          alert("there was an error");
        }
      );
    },
    triggerResendConfirmation() {
      this.resendConfirmationCode(this.usernameC).then(
        () => {},
        () => {
          alert("there was an error");
        }
      );
    },
    ...mapActions("cognito", {
      confirmRegistration: "confirmRegistration",
      resendConfirmationCode: "resendConfirmationCode"
    })
  },
  created() {
    this.usernameC = this.username;
  }
};
</script>
<style lang="scss" scoped>
nav a {
  display: inline-block;

  &:not(:last-child) {
    margin-right: 1em;
  }
}

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
</style>