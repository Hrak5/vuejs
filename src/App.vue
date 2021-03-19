<template>
  <div id="app">

    <div class="container">
      <div v-if="user.name" class="text-white" v-bind:class="user.gendre == 'male' ? 'male' : 'female'">

        <p>Name: {{ user.name }}</p>
        <p>Surname: {{ user.surname }}</p>
        <p>Gendre: {{ user.gendre }}</p>
      </div>

      <div>
        <div class="form-group">
          <label>Name</label>
          <input type="text" class="form-control" v-model="newUser.name">
          <div class="text-danger" font-weight-bold v-if="errors.users.name">
              {{errors.users.name}}
          </div>
        </div>
        <div class="form-group">
          <label>Surname</label>
          <input type="text" class="form-control" v-model="newUser.surname">
          <div class="text-danger" font-weight-bold v-if="errors.users.surname">
            {{errors.users.surname}}
          </div>
        </div>
        <div class="form-group">
          <label>Gendre</label>
          <input type="text" class="form-control" v-model="newUser.gendre">
          <div class="text-danger" font-weight-bold v-if="errors.users.gendre">
            {{errors.users.gendre}}
          </div>
        </div>
        <div class="form-group">
          <button class="btn btn-success" @click="saveUser">Change</button>
        </div>
      </div>
    </div>

  </div>
</template>

<script>

export default {
  name: 'App',
  data(){
    return {
      user:{
        name: "",
        surname: "",
        gendre: ""
      },
      newUser:{
        name: "",
        surname: "",
        gendre: ""
      },
      errors: {
        users: {
          name: "",
          surname: "",
          gendre: ""
        }
      }
    }
  },
  methods: {
    saveUser(){
      // if (this.newUser.name == ""){
      //   this.errors.users.name ="Name is required"
      // }else{
      //   this.errors.users.name =""
      // }
      this.errors.users.name = this.newUser.name == "" ? "Name is required" : ""
      this.errors.users.surname = this.newUser.surname == "" ? "Surname is required" : ""
      this.errors.users.gendre = this.newUser.gendre == "" ? "Gendre is required" : ""

      // if (this.newUser.surname == ""){
      //   this.errors.users.surname ="Surname is required"
      // }
      // if (this.newUser.gendre == ""){
      //   this.errors.users.gendre ="Gendre is required"
      // }
      if (this.errors.users.name == "" && this.errors.users.surname == "" && this.errors.users.gendre == ""){

        this.user.name = this.newUser.name
        this.user.surname = this.newUser.surname
        this.user.gendre = this.newUser.gendre
      }
    }
  }
}
</script>

<style>
.male{
  background: blue;
}
.female{
  background: pink;
}
</style>
