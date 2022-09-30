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
          <input type="text" id="phone" class="input" name="phone" placeholder="phoneNumber" @input="acceptNumber"  v-model="phoneData">
          
        </div>
        <div class="title">
          <label class="label" for="email">E_MAIL:</label>
          <input type="email" for="email" id="email" class="input" name="email"
            placeholder="Please enter your email here" @blur="validateEmail" required v-model="emailData">
            <br/>
        </div>
        <span class="text-red-700" v-if="msg">{{msg}}</span>

        <div class="">
          <button class="btn" @click="checkInfo">ADD</button>
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
      phoneData: '',
      emailData: '',
      showModal: false,
      msg: "",
    }
  },
  watch: {
    email(value) {
      // binding this to the data value in the email input
      this.emailData = value;
      this.validateEmail(value);
    }
  },
  methods: {
    validateEmail() {
      if (/^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/.test(this.emailData)) {// eslint-disable-line no-useless-escape
        this.msg = '';
      } else {
        this.msg = 'Please enter a valid email address';
      }
    },
    acceptNumber() {
        var x = this.phoneData.replace(/\D/g, '').match(/(\d{0,3})(\d{0,3})(\d{0,4})/);
  this.phoneData = !x[2] ? x[1] : '(' + x[1] + ') ' + x[2] + (x[3] ? '-' + x[3] : '');
    },
  
    checkInfo() {
     if(this.msg== "" && this.phoneData.length==14 ){
      this.$emit('addUser', {name:this.nameData, phone:this.phoneData, email:this.emailData})
     }
    }
  },
  props: ["usersApi"],
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style >

</style>
