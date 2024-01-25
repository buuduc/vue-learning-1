<template>
    <Header></Header>
    <div>
        <h1>Hello User, Welcome to Add Restaurant Page</h1>
    </div>
    <form @submit="onSubmitForm" class="form-container" action="">
        <input type="text" v-model="name" name="name" placeholder="Enter Name"/>
        <input type="text" v-model="address" name="address" placeholder="Enter Address"/>
        <input type="text" v-model="contact" name="contact" placeholder="Enter Contact"/>
        <button type="submit" >Add new restaurant</button>
    </form>
</template>

<script setup>
import { onMounted, ref } from 'vue';
const name = ref()
const address = ref()
const contact = ref()
import Header from './Header.vue'
import { useRouter } from 'vue-router'
import { BACKEND_URL, STORAGE } from '@/utils/constants'
import axios from 'axios';
const router = useRouter()
console.log('🚀 🚀 file: Add.vue:24 🚀 router:', router)
const onSubmitForm = async (e) => { 
    e.preventDefault()
    const endpoint = `${BACKEND_URL}/restaurants`
    await axios.post(endpoint, {
        name: name.value,
        address: address.value,
        contact: contact.value
    })
    router.push({ name: 'Home' })

 }
// onMounted(() => { 
//     const dataUser = localStorage.getItem(STORAGE.USER_INFO)
//     console.log('🚀 🚀 file: Add.vue:16 🚀 onMounted 🚀 dataUser:', dataUser)
//     if (!dataUser){
//         router.push({ name: 'Login' })
//     }
//  })
</script>

<style lang="scss" scoped>
.form-container{
    display: flex;
    justify-content: center;
    flex-direction: column;
    align-items: center;
    margin-top: 50px;

}
</style>
