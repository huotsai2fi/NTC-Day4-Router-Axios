<template>
    <h1>User {{ userId }} Todo</h1>
    <ol>
        <li v-for="todo in todos" :key="todo">
            <h4>{{ todo.title }}</h4>
            <div>
                是否完成? <input type="checkbox" v-model="todo.completed">
            </div>
        </li>
    </ol>
</template>

<script>
import axios from 'axios'

export default ({
    data() {
        return{
            todos:[],
        }
    },
    computed: {
        userId(){
            return this.$route.params.userId;
        }
    },
    methods: {
        fetchUserTodos(userId){
            axios.get(`https://jsonplaceholder.typicode.com/users/${userId}/todos`)
           .then(response => this.todos = response.data);
        }
    },
    mounted() {
        this.fetchUserTodos(this.userId);
    }
})
</script>
