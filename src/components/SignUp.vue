<template>
  <img class="logo" src="../assets/los-mariscos-restaurante-logo.jpg" />
  <h1>Sign Up</h1>
  <div class="register">
    <InputText type="text" v-model="name" placeholder="Enter Name" />
    <InputText type="text" v-model="email" placeholder="Enter email" />
    <InputText type="text" v-model="password" placeholder="Enter Password" />
  </div>

  <Button @click="signUp">Sign Up</Button>
</template>
<script>
import axios from "axios";
export default {
  name: "SignUp",
  data() {
    return {
      name: "",
      email: "",
      password: "",
    }
  },
  methods: {
    async signUp() {
      let result = await axios.post("http://localhost:3000/user", {
        email: this.email,
        password: this.password,
        name: this.name
      });
      console.log(result);
      if (result.status == 201) {       
        localStorage.setItem("user-info",JSON.stringify(result.data))
        this.$router.push({name:'Home'})
      }

    }
  }
}
</script>

<style>
.logo {
  width: 390px;
  height: 390px;
}

.register input {
  width: 300px;
  height: 40px;
  padding-left: 20px;
  display: block;
  margin-bottom: 30px;
  margin-right: auto;
  margin-left: auto;
  border: 1px solid skyblue;
}

.register button {
  width: 320px;
  height: 40px;
  border: 1px solid skyblue;
  background: skyblue;
  color: #fff;
  cursor: pointer;
}
</style>
