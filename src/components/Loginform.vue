<template>
    <div class="login-form">
        <h2>Login</h2>
        <form @submit.prevent="handleLogin">
        <div class="form-group">
            <label for="username">Username:</label>
            <input type="text" id="username" v-model="username" required />
        </div>
        <div class="form-group">
            <label for="password">Password:</label>
            <input type="password" id="password" v-model="password" required />
        </div>
        <button type="submit">Login</button>
       <label class="register-label">
  Don't have an account?
  <router-link to="/register">Register</router-link>
</label>

<label class="register-label">
  <router-link to="/forgot-password">
    Forgot Password?
  </router-link>
</label>        </form>
    </div>
</template>
<script>
import { ref } from 'vue'
import { useAuthStore } from '../stores/auth'
import { useRouter } from 'vue-router'

export default {
  name: 'LoginForm',

 setup() {
  const auth = useAuthStore()
  const router = useRouter()

  const username = ref('')
  const password = ref('')

    const handleLogin = () => {
  auth.login(username.value)

  router.push('/dashboard')
}

    return {
      username,
      password,
      handleLogin
    }
  }
}
</script>

<style scoped>
.login-form {
    max-width: 400px;
    margin: 0 auto;
    padding: 2rem;
    border: 1px solid #ccc;
    border-radius: 8px;
    background-color: #f9f9f9;
}
.form-group {
    margin-bottom: 1rem;
}
label {
    display: block;
    margin-bottom: 0.5rem;
}
input {
    width: 100%;
    padding: 0.5rem;        
    border: 1px solid #ccc;
    border-radius: 4px;
}
button {
    width: 100%;
    padding: 0.75rem;
    border: none;
    border-radius: 4px;
    background-color: #42b983; 
    color: white;
    font-size: 1rem;
    cursor: pointer;
}
button:hover {
    background-color: #38a173;
}       
.register-label {
    display: block;
    margin-top: 1rem;
    text-align: center;
}

.register-label a {
    color: #42b983;
    text-decoration: none;
}

.register-label a:hover {
    text-decoration: underline;
}             
</style>