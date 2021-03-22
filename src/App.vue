<template>
  <div id="app">

    <div class="container">

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
          <label>Age</label>
          <input type="text" class="form-control" v-model="newUser.age">
          <div class="text-danger" font-weight-bold v-if="errors.users.age">
            {{errors.users.age}}
          </div>
        </div>
        <div class="form-group">
          <button class="btn btn-success" @click="saveUser">Change</button>
          <button class="btn btn-danger" @click="randomAge">Random Age</button>
        </div>
      </div>

      <div>
        <table class="table table-dark table-bordered table-hover">
          <tr>
            <th>Name</th>
            <th>Surname</th>
            <th>Gendre</th>
            <th>Age</th>
            <th>Action</th>
          </tr>

            <tr v-for="user in users" :key="user.id">
              <td>{{user.name}}</td>
              <td>{{user.surname}}</td>
              <td>{{user.gendre}}</td>
              <td>{{user.age}} {{user.age > 50 ? "Old" : "Young"}}</td>
              <td>
                <button class="btn btn-danger" @click="deleteUser(user.id)">Delete</button>
              </td>
            </tr>
        </table>
      </div>
    </div>

  </div>
</template>

<script>

export default {
  name: 'App',
  data(){
    return {
      users:[],
      newUser:{
        name: "",
        surname: "",
        gendre: "",
        age: ""
      },
      errors: {
        users: {
          name: "",
          surname: "",
          gendre: "",
          age: ""
        }
      }
    }
  },
  mounted(){
    this.getUsersStorage();
  },
  methods: {
    randomAge(){
        const age = Math.floor(Math.random() * 100);
        this.newUser.age = age;
    },
    deleteUser(id){
      console.log(id)
    },
    saveUser(){
      // if (this.newUser.name == ""){
      //   this.errors.users.name ="Name is required"
      // }else{
      //   this.errors.users.name =""
      // }
      this.errors.users.name = this.newUser.name == "" ? "Name is required" : ""
      this.errors.users.surname = this.newUser.surname == "" ? "Surname is required" : ""
      this.errors.users.gendre = this.newUser.gendre == "" ? "Gendre is required" : ""
      this.errors.users.age = this.newUser.age == "" ? "Age is required" : ""
      // if (this.newUser.surname == ""){
      //   this.errors.users.surname ="Surname is required"
      // }
      // if (this.newUser.gendre == ""){
      //   this.errors.users.gendre ="Gendre is required"
      // }
      if (this.errors.users.name == "" && this.errors.users.surname == "" && this.errors.users.gendre == "" && this.errors.users.age == ""){
        const user = {};

        user.id = this.generateRandomNumber()
        user.name = this.newUser.name;
        user.surname = this.newUser.surname;
        user.gendre = this.newUser.gendre;
        user.age = this.newUser.age;

        this.users.push(user)
        this.setUsersStorage();
      }
    },
    generateRandomNumber(){
      const d = new Date();
      return d.getTime() + Math.floor(Math.random()*1000);
    },
    setUsersStorage(){
      const users = JSON.stringify(this.users)
      localStorage.setItem("users",users);
    },
    getUsersStorage(){
      let users = localStorage.getItem("users") || null;
      users = JSON.parse(users)
      this.users = users ? users : []
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
