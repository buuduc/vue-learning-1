<template>
    <Header></Header>
    <div>
        <h1>Hello User, Welcome to Update Restaurant Page</h1>
    </div>
    <form @submit="onSubmitForm" class="form-container">
        <input type="text" v-model="name" name="name" placeholder="Enter Name"/>
        <input type="text" v-model="address" name="address" placeholder="Enter Address"/>
        <input type="text" v-model="contact" name="contact" placeholder="Enter Contact"/>
        <button type="submit" > Update restaurant</button>
    </form>
</template>

<script setup>
import { onMounted, onUpdated, ref, watch } from 'vue';
import Header from './Header.vue'
import { useRoute, useRouter } from 'vue-router'
import { BACKEND_URL, STORAGE } from '@/utils/constants'
import axios from 'axios';
const router = useRouter()
const route = useRoute()
const name = ref()
const address = ref()
const contact = ref()
const id = route.params.id
onMounted(async () => { 

    const {data} = await axios.get(`${BACKEND_URL}/restaurants/${id}`)
    console.log('🚀 🚀 file: Update.vue:30 🚀 onMounted 🚀 data:', data)
    name.value = data.name
    address.value = data.address
    contact.value = data.contact
 onUpdated(() => name, async () => {
     console.log(name)
 })
 })
 const onSubmitForm = async (e) => { 
    e.preventDefault()
    const endpoint = `${BACKEND_URL}/restaurants/${id}`
    await axios.put(endpoint, {
        name: name.value,
        address: address.value,
        contact: contact.value
    })
    router.push({ name: 'Home' })

 }
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
