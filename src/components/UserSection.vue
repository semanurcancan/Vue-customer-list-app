<template>
  <div class="card-container">
    <div class="addUser">
      <div id="user" class="text-sm m-8 ">
        <h4 class="mb-4">Add New Custumer</h4>
        <div class="title">
          <label class="label" for="name">NAME:</label>
          <input type="text" id="name" class="input" name="name" placeholder="name" v-model="nameData">
        </div>
        <div class="title">
          <label class="label" for="phone">PHONE:</label>
          <input type="text" id="phone" class="input" name="phone" placeholder="phoneNumber" v-model="phoneData">
        </div>
        <div class="title">
          <label class="label" for="email">E_MAIL:</label>
          <input type="text" id="email" class="input" name="email" placeholder="test@gmail.com" v-model="emailData">
        </div>

        
        <div class="">
          <button class="btn" @click="$emit('addUser', {name:nameData, phone:phoneData, email:emailData})"  >ADD</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      nameData: '',
      phoneData:'',
      emailData:'',
    }
  },
  props: ["usersApi"],
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style >

</style>
