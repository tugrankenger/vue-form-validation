<template>
  <div class="container">
    <h3 class="text-center my-3">Form Validation With Vuelidate</h3>
    <div class="d-flex justify-content-center align-content-center flex-row">
      <div class="card p-4 my-3 shadow me-4">
        <form @submit.prevent="onSubmit" style="width: 350px">
          <div class="form-group mb-3">
            <label>E-mail</label>
            <input
            @blur="v$.$validate()"
            v-model="email" 
            type="email" 
            class="form-control" 
            :class="{'is-invalid': v$.email.$error}"
            placeholder="Enter your email address">
            <!-- <small class="form-text text-muted">Error message</small> -->
            <div class="input-errors" v-for="error of v$.email.$errors" :key="error.$uid">
              <div class="error-msg text-danger">{{ error.$message }}</div>
            </div>
          </div>
          <div class="form-group mb-3">
            <label>Password</label>
            <input 
            @blur="v$.$validate()"
            v-model="password" 
            type="password" 
            class="form-control" 
            :class="{'is-invalid': v$.password.$error }"
            placeholder="Enter your password">
            <div class="input-errors" v-for="error of v$.password.$errors" :key="error.$uid">
              <div class="error-msg text-danger">{{ error.$message }}</div>
            </div>
          </div>
          <div class="form-group mb-3">
            <label>Password again</label>
            <input 
            @blur="v$.$validate()"
            v-model="repassword" 
            type="password" 
            class="form-control" 
            :class="{'is-invalid': v$.repassword.$error}"
            placeholder="Enter your password again">
            <div class="input-errors" v-for="error of v$.repassword.$errors" :key="error.$uid">
              <div class="error-msg text-danger">{{ error.$message }}</div>
            </div>
          </div>
          <div class="form-group mb-3">
            <label> Select you want to register category </label>
            <select v-model="selectedCategory" class="form-control">
              <option v-for="category in categories" :value="category">{{ category }}</option>
            </select>
          </div>
          <a @click="newHobby" class="text-white btn btn-primary rounded-0 btn-sm">Add Hobby</a>

          <ul class="list-group my-3 border-0">
            <li class="list-group-item d-flex ps-2" v-for="(hobby, index) in hobbies">
              <input type="text" class="form-control me-2" v-model="hobby.value">
              <button class="btn btn-sm btn-danger rounded-0" @click="hobbies.splice(index, 1)">Remove</button>
            </li>
          </ul>

          <button class="btn btn-outline-success rounded-0">Save</button>
        </form>
      </div>
      <div class="card p-4 my-3 shadow" style="width:400px">
        <p>{{ v$.repassword }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import {required, email, minLength, maxLength, sameAs} from '@vuelidate/validators'
import { useVuelidate } from '@vuelidate/core'
export default {
  data() {
    return {
      v$: useVuelidate(),
      email: null,
      password: null,
      repassword: null,
      selectedCategory: null,
      categories: ["Software", "Hardware", "Cloud", "Servers", "Unix", "Linux", "Windows"],
      hobbies: []
    }
  },
  methods: {
    onSubmit() {
      let form = {
        email: this.email,
        password: this.password,
        category: this.category,
        hobbies: this.hobbies
      }
      console.log(form)
    },
    newHobby() {
      let hobby = {
        id: Math.random * Math.random * 1000,
        value: ''
      }
      this.hobbies.push(hobby)
    }
  },
  validations(){
    return{
      email:{
        required,
        email
      },
      password:{
        required,
        minLength: minLength(6),
        maxLength: maxLength(8)
      },
      repassword:{
        required,
        minLength: minLength(6),
        maxLength: maxLength(8),
        sameAs: sameAs('password')
      }
    }
  },
}
</script>

<style>

</style>