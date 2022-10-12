<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h2 v-if="user">User logged: {{ user }}</h2>

    <br />
    <div id="logout" v-if="isSignedIn">
      <button @click="handleSignOut">Logout</button>
    </div>

    <br />
    <div id="LogingWithGoogle" v-if="!isSignedIn">
      <h3>Google</h3>
      <button @click="handleLogingGoogle">Login</button>
    </div>

    <br />
    <div id="LoginWithTwitter" v-if="!isSignedIn">
      <h3>Twitter</h3>
      <button @click="handleLogingTwitter">Login</button>
    </div>

    <br />
    <div id="LoginWithGitHub" v-if="!isSignedIn">
      <h3>GitHub</h3>
      <button @click="handleLogingGitHub">Login</button>
    </div>
  </div>
</template>

<script>
import firebaseConfig from '../firebaseConfig';
import { getAuth, signOut, signInWithPopup, GoogleAuthProvider, TwitterAuthProvider, GithubAuthProvider  } from "firebase/auth";

firebaseConfig

const provider = new GoogleAuthProvider();
const providerTwitter = new TwitterAuthProvider();
const providerGithub = new GithubAuthProvider();
const auth = getAuth();
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      user: '',
      isSignedIn: false,                    // time 12:00
    }
  },
  methods: {
    handleLogingGoogle() {
      signInWithPopup(auth, provider)
        .then((result) => {
          //const user = result.user;
          console.log(result)

          this.user = result.user.displayName;
          this.isSignedIn = true
        }).catch((error) => {
          console.log(error)
        });
    },
    handleSignOut() {
      const auth = getAuth();
      signOut(auth).then(() => {
        this.user = ''
        this.isSignedIn = false
      }).catch((error) => {
        console.log(error)
      });

    },
    handleLogingTwitter() {
      signInWithPopup(auth, providerTwitter)
      .then((result) => {
          //const user = result.user;
          console.log(result)

          this.user = result.user.displayName;
          this.isSignedIn = true
        }).catch((error) => {
          console.log(error)
        });
    },
    handleLogingGitHub(){
      signInWithPopup(auth, providerGithub)
      .then((result) => {
          //const user = result.user;
          console.log(result)

          this.user = result.user.displayName;
          this.isSignedIn = true
        }).catch((error) => {
          console.log(error)
        });
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
