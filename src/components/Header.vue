<template>
    <div class="nav">
        <router-link to="/">Home</router-link>
        <router-link to="/add">Add Restaurant</router-link>
        <router-link to="/update">Update Restaurant</router-link>
        <a href="#" @click="logoutHandler">Logout</a>
    </div>
</template>

<script setup>
import { useRouter } from 'vue-router';

    const router = useRouter()
    // export default {
        
    // }
    const logoutHandler = () => { 
        router.push({ name: 'Login' })
        localStorage.clear();

     }
</script>

<style lang="scss" scoped>
.nav{
    background-color: #333;
    overflow: hidden;
    a{
        float: left;
        color: #f2f2f2;
        padding: 14px 16px;
        text-align: center;
        font-size: 17;
        text-decoration: none;
        margin-right: 5px;
        &:hover{
            background: #ddd;
            color: #333;
        }
    }
}

</style>
