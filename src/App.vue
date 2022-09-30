<template>
  <div class="container">
    <div class="box">
      <h1 class="bg-blue-200 h-20 p-6 italic rounded-xl  shadow-xl shadow-blue-300">USER LIST</h1>
      <br/>
      <div class="grid grid-cols-3 text-blue-600/50">
        <strong>NAME</strong>
        <strong>PHONE</strong>
        <strong>E-MAIL</strong>

      </div>
      <div id="app" v-for="user in usersApi" :key="user.id">
        <div class="userList">
          <div class="name">{{user.name}}</div>
          <div class="phone">{{user.phone}}</div>
          <div class="phone">{{user.email}}</div>


        </div>
      </div>
    </div>
    <UserSection :usersApi="usersApi" @addUser="addUser($event)" />
  </div>
</template>

<script>
import UserSection from './components/UserSection.vue'
import axios from 'axios'
import './assets/tailwind.css'

export default {
  name: 'App',
  components: {
    UserSection
  },
  data() {
    return {
      usersApi: null,
    }
  },
  //methods directive içerisinde kullanıcı ekleme ve get post işlemi yapıldı.
  methods: {
    addUser: function(item) {
        console.log(item)
        axios.post("https://jsonplaceholder.typicode.com/users", item)
          .then( (response) => {
            this.usersApi.unshift(response.data);
          })
          .catch( (error) =>{
            console.log(error);
          })

    }
  },
  created: function () {
    axios.get("https://jsonplaceholder.typicode.com/users")
      .then((res) => {
        this.usersApi = res.data;
        console.log(this.usersApi)
      })
  },

}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: rgb(107, 102, 102);
  
    display: flex;
    flex-direction: column;
    align-items: center;
}
</style>
