<template>
  <div class="container">
    <h3 class="text-center my-3">Form Validation With Vuelidate</h3>
    <div class="d-flex justify-content-center align-content-center flex-row">
      <div class="card p-4 my-3 shadow me-4">
        <form @submit.prevent="onSubmit" style="width: 350px">
          <div class="form-group mb-3">
            <label>E-mail</label>
            <input v-model="email" type="email" class="form-control" placeholder="Emnter your email address">
            <small class="form-text text-muted">Error message</small>
          </div>
          <div class="form-group mb-3">
            <label>Password</label>
            <input v-model="password" type="password" class="form-control" placeholder="Enter your password">
          </div>
          <div class="form-group mb-3">
            <label>Password again</label>
            <input v-model="repassword" type="password" class="form-control" placeholder="Enter your password again">
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
        <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Natus aspernatur distinctio repellendus quia
          cupiditate necessitatibus. Eius, est inventore vel provident sapiente dolore, libero deleniti, nihil sit
          repellendus animi molestiae ullam.</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
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
  }
}
</script>

<style>

</style>