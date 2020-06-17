<template>
  <div id="app">
    <Header/>
    <!-- <TweetTextArea v-on:submit-tweet="submitTweet"/> -->
    <Profile v-bind:profile="profile"/>
    <TweetList v-bind:tweets='tweets'/>
  </div>
</template>

<script>
import Header from './components/layout/Header.vue';
import Profile from './components/layout/Profile.vue';

import TweetList from './components/TweetList.vue';
import TweetTextArea from './components/TweetTextArea.vue';

import axios from 'axios';

import 'bootstrap/dist/css/bootstrap.css'
import 'bootstrap-vue/dist/bootstrap-vue.css'

export default {
  name: 'app',
  components: {
    Header,
    Profile,
    TweetList,
    TweetTextArea
  },
  data(){
    return{
      tweets: [],
      profile: {}
    };
  },
  methods:{
    submitTweet(){
      // create a tweet object using the message tweeted
      let msg = document.getElementById('tweet').value;
      if(msg != ''){
        let tweet={
          id: this.tweets.length + 1,
          msg: msg,
          author: '@aninarj',
          timestamp: new Date()
        };
        this.tweets.push(tweet);
        document.getElementById('tweet').value = "";
      }
    }
  },
  created(){
    axios({
      method: 'GET',
      url: 'https://morning-headland-68889.herokuapp.com/https://api.twitter.com/1.1/search/tweets.json?q=from%3Aaninarj',
      headers: {
        'Authorization': 'Bearer AAAAAAAAAAAAAAAAAAAAAICpFAEAAAAAMYYy3I%2F%2BFrsZU6SZ12x%2FQuOvfiM%3DciqEC9FnXygv2Xk1ETTyojENsgkGNvrbHp5lJBcCBC5KXTfwWk',
        'Content-Type': 'application/json'
      }
    })
      .then(res => {this.tweets=res.data.statuses; this.profile = res.data.statuses[0].user;})
      .catch(err => console.log(err));
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.lightBg{
  background-color: #ffffff;
}

.darkBg{
  background-color: #000000;
}

.primary-btn{
  background-color: rosybrown;
  font-size: 15px;
  color: #ffffff;
  font-weight: bold;
  border: transparent;
  border-radius: 5px;
  box-shadow: none;
  text-transform: uppercase;
}

.btn-medium{
  width: 140px;
  height: 40px;
}

button:hover{
  cursor: pointer;
}

</style>
