<template>
  <div class="login">
     <div class="container-fluid">
        <div class="row mvh-100">
          <div class="col-lg-4 mx-auto my-auto">
            <div class="card w-100" style="border-radius:15px">
              <div class="card-body">
                <div class="row">
                  <div v-if="error" class="col-lg-12">
                    <div class="alert alert-danger text-center" role="alert">
                      {{message}}
                    </div>
                  </div>
                  <form @submit="login"  method="post" class="w-100">
                    <div class="col-lg-12 form-group text-left">
                      <p>Username</p>
                      <input type="text" class="form-control" v-model="post.email" required>
                    </div>
                    <div class="col-lg-12 form-group text-left">
                      <p>Password</p>
                      <input type="password" class="form-control" v-model="post.password" required>
                    </div>
                    <div class="col-lg-12 form-group mb-4">
                      <input type="submit" class="form-control" value="Login" style="background:#4e73df;color:white">
                    </div>
                  </form>
                </div>
              </div>
            </div>
          </div>
        </div>
     </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'Login',
  data(){
    return{
      message: '',
      error: false,
      post: {
        email: null,
        password: null
      }
    }
  },
  methods: {
    login: function(e){
      e.preventDefault()
      axios.post('https://frontend-screening-v1.herokuapp.com/login', this.post, {
        headers:{
          'Content-Type': 'application/json'
        }
      })
      .then((response) => {
        if(response.data.data){
          localStorage.setItem('user', response.data.data.email)
          localStorage.setItem('token', response.data.data.session)
          this.$router.push({name: 'Home'})
        }
      })
      .catch((error) => {
        if(error){
          this.error = true
          this.message = error.response.data.message
        }
      });
    }
  }
}
</script>

<style>
body{
    height: 100%;
}
.login{
     min-height: 100vh;
     background: #4e73df;
}
.mvh-100{
    min-height: 100vh;
}
</style>
