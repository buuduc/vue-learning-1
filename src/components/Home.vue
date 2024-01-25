<template>
    <Header></Header>
    <div>
        <h1> Hello {{ name }}, Welcome on Home Page! </h1>
    </div>
    <table border="1">
        <tr v-for="item in restaurants" :key="item.id">
            <td>{{ item.id }}</td>
            <td>{{ item.name }}</td>
            <td>{{ item.contact }}</td>
            <td>{{ item.address }}</td>
            <td>
                <router-link :to="`/update/${item.id}`">Update</router-link>
            </td>
        </tr>
    </table>
</template>

<script setup>
import { onMounted, ref } from 'vue';
import { STORAGE, BACKEND_URL } from '@/utils/constants'
import Header from './Header.vue'
import { useRouter } from 'vue-router';
import axios from 'axios';

const router = useRouter()
const name = ref(null)
const restaurants = ref([])
onMounted(async () => {
    const user = localStorage.getItem(STORAGE.USER_INFO)
    if (!user) {
        router.push({ name: 'Login' })
    }
    name.value = JSON.parse(user).name
    const response = await axios.get(`${BACKEND_URL}/restaurants`)
    console.log('🚀 🚀 file: Home.vue:37 🚀 onMounted 🚀 response.data:', response.data)
    restaurants.value = response.data
    // console.log('🚀 🚀 file: Home.vue:34 🚀 onMounted 🚀 restaurants:', restaurants)

})
</script>


<style lang="scss" scoped>
</style>
