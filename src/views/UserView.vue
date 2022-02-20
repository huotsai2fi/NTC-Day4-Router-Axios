<template>
    <h1>UserId: {{ userId }}</h1>
    <div>Name: {{ userInfo.name }}</div>
    <div>Email: {{ userInfo.email }}</div>
    <hr>
    <router-link :to="`/users/${userId}/todos`">{{ userInfo.name }}的 todo</router-link>
    <router-view></router-view>
</template>

<script>
import axios from 'axios';

export default ({
    data() {
        return{
            userInfo:{},
            // userId: this.$route.params.userId, //component render時指定一次，所以不能寫在這
        }
    },
    computed:{
        userId(){
            return this.$route.params.userId;
        }
    },
    mounted() { //component render時執行一次
        this.fetchUserInfo(this.userId);
        
    },
    watch: {
        userId(value) {
            this.fetchUserInfo(value);
        }
    },
    methods:{
        fetchUserInfo(userId){
            axios.get(`https://jsonplaceholder.typicode.com/users/${userId}`).then(response => this.userInfo = response.data);
        }
    }
});
</script>
