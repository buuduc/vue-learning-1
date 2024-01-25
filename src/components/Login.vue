<template >
    <div class="container">
        <div>
            <img class="logo" src="../assets//logo.svg" alt="">
            <h1>Sign In</h1>
        </div>
        <div class='register'>
            <input type="email" v-model="emailInput" name="email" placeholder="Enter Email">
            <input type="password" v-model="passwordInput" name="password" placeholder="Enter Password">
            <button @click="onLoginHandler">Sign In</button>
            <p>
                <router-link to="/signup">
                    Sign Up
                </router-link>
            </p>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue'
import axios from 'axios'
import { BACKEND_URL, STORAGE } from '@/utils/constants'
import { useRouter, useRoute } from 'vue-router'

// const count = ref(0)
const emailInput = ref(null)
const passwordInput = ref(null)
const router = useRouter()

async function onLoginHandler(){ 
    try {
        if (![emailInput.value, passwordInput.value].every(Boolean)){
            throw new Error('all fields are required')
        }
        const endpoint = `${BACKEND_URL}/users`
        const response = await axios({
            method: 'get',
            url: endpoint,
            params: {
                email: emailInput.value,
                password: passwordInput.value
            }
        })
        if (response.data.length > 0 && response.status===200){
            localStorage.setItem(STORAGE.USER_INFO, JSON.stringify(response.data[0]))
            alert(`User login successfully`)
            router.push({ name: 'Home' })
        } else{
            throw new Error('Login Failed')

        }
    } catch (error) {
        console.log('🚀 🚀 file: Signup.vue:43 🚀 onSignupHandler 🚀 error:', error)
        alert('Login failed')
    }
    }

</script>

<style lang="scss">
.logo {
    width: 100px;
}

.container{
    text-align: center;
}
.register {
    input {
        width: 300px;
        height: 40px;
        padding-left: 20px;
        display: block;
        margin-bottom: 30px;
        margin-right: auto;
        margin-left: auto;
        border: 1px solid skyblue;
    }
    button{
        width: 320px;
        height: 40px;
        border: 1px solid skyblue;
        background: skyblue;
        color: #fff;
        cursor: pointer;
    }
}
</style>
