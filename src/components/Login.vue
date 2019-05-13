<template>
  <div>
    EMAIL: <input type="text" v-model="email"> <br/>
    PASSWORD: <input type="password" v-model="password"> <br/>
    <button @click="login">login</button>
    {{ error }}
  </div>
</template>
<script>
import axios from 'axios';

export default {
  name: 'Login',
  data() {
    return {
      email: '',
      password: '',

      error: '',
    }
  },
  methods: {
    login() {
      let user = {
        email: this.email,
        password: this.password
      }
      axios.post('http://localhost:5000/login', user)
        .then(res => {
          //if successfull
          if (res.status === 200) {
            localStorage.setItem('token', res.data.token);
            this.$router.push('/');
          }
        }, err => {
          console.log(err.response);
          this.error = err.response.data.error
        })
    }
  }
}
</script>

