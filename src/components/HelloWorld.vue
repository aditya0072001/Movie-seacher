<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
      <ion-item>
    <ion-label position="floating">Enter movie/series name.</ion-label>
    <ion-input :value="mname" @input="mname=$event.target.value"></ion-input>
      </ion-item>
      <ion-button expand="block" @click="feed">Find</ion-button>
      <br>
      <ion-list>
    <ion-item v-for="post in posts" v-bind:key="post.imdbID">
      <ion-label>{{post.Title}}</ion-label>
    </ion-item>
  </ion-list>
  </div>
</template>

<script>
const axios = require('axios');
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data(){
    return{
      mname:'',
      posts:[]
    }
  },
  methods:{
    feed(){
      var url="http://www.omdbapi.com/?apikey=b27cb83d&s="+this.mname;
      axios.get(url)
      .then(data=>{
        this.posts=data.data.Search
       // console.log(data.data.Search)
      }).catch(function (error) {
    // handle error
    alert(error);
    })
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
