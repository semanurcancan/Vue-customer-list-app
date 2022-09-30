<template>
  <div class="container">
    <div class="box">
      <h1 class="bg-amber-200 h-20 p-6 italic rounded-2xl shadow-xl shadow-yellow-400">COSTUMER LIST</h1>

      <br />
      <div class="grid grid-cols-3">
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
    <UserSection :usersApi="usersApi" @newUser="usersApi.unshift($event)" />
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
  methods: {
    newUser(item) {
      this.usersApi.unshift(item);
    }
  },
  created: function () {
    axios.get("https://jsonplaceholder.typicode.com/users").then((res) => {
      this.usersApi = res.data;
      console.log(this.usersApi)
    })
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: rgb(107, 102, 102)
}
</style>
