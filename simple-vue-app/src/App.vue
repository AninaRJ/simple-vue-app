<template>
  <div id="app">
    <Header v-on:submit-search="submitSearch"/>
    <!-- <TweetTextArea v-on:submit-tweet="submitTweet"/> -->
    <br/>
    <b-spinner variant="warning" class="text-center loading" v-if="!profile.hasOwnProperty('id') && this.search_user != ''" label="Loading..."></b-spinner>
    <b-container v-else-if="this.search_user == ''">
      <b-alert show variant="danger">Search for a user to see their tweets!</b-alert>
    </b-container>
    <b-container v-else class="bv-example-row">
      <b-row>
        <b-col sm="12">
          <b-alert dismissible show variant="success">Showing results for @{{this.search_user}}</b-alert>
        </b-col>
      </b-row>
      <b-row>
        <b-col sm="4">
          <Profile v-bind:profile="profile" v-bind:media="media"/>
        </b-col>
        <b-col sm="8">
          <TweetList v-bind:tweets='tweets'/>
        </b-col>
      </b-row>
    </b-container>
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
      profile: {},
      media: [],
      search_user: ""
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
    },
    submitSearch(){
      this.search_user = document.getElementById("search-user").value;

      axios({
          method: 'GET',
          url: 'https://morning-headland-68889.herokuapp.com/https://api.twitter.com/1.1/search/tweets.json?q=from%3A' + this.search_user + '&count=100',
          headers: {
            'Authorization': 'Bearer AAAAAAAAAAAAAAAAAAAAAICpFAEAAAAAMYYy3I%2F%2BFrsZU6SZ12x%2FQuOvfiM%3DciqEC9FnXygv2Xk1ETTyojENsgkGNvrbHp5lJBcCBC5KXTfwWk',
            'Content-Type': 'application/json'
          }
        })
          .then(res => {
              this.tweets=res.data.statuses; 
              this.profile = res.data.statuses[0].user;
              this.media = [];
          })
          .catch(err => console.log(err));
    }
  },
  created(){
    if(this.search_user != ""){
      axios({
        method: 'GET',
        url: 'https://morning-headland-68889.herokuapp.com/https://api.twitter.com/1.1/search/tweets.json?q=from%3A' + this.search_user + '&count=100',
        headers: {
          'Authorization': 'Bearer AAAAAAAAAAAAAAAAAAAAAICpFAEAAAAAMYYy3I%2F%2BFrsZU6SZ12x%2FQuOvfiM%3DciqEC9FnXygv2Xk1ETTyojENsgkGNvrbHp5lJBcCBC5KXTfwWk',
          'Content-Type': 'application/json'
        }
      })
        .then(res => {
            this.tweets=res.data.statuses; 
            this.profile = res.data.statuses[0].user;
            this.media = [];
        })
        .catch(err => console.log(err));
    }
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

.loading{
  width: 40px;
  height: 40px;
}

</style>
