<template>
    <ul>
        <li v-for="user in users" :key="user" @click="removeUser(user)">
            {{ user }}
        </li>
    </ul>
    <input type="text" ref="userInput">
    <button @click="AddUser">Add User</button>
</template>

<script>
export default {
    data() {
        return {
            users: ['Max', 'Rahul', 'Sarath', 'Praveen', 'Vivek']
        }
    },
    methods: {
        AddUser() {
            const userValue = this.$refs.userInput.value;
            this.users.unshift(userValue);
            this.$refs.userInput.value = '';
        },
        removeUser(usr) {
            this.users = this.users.filter(user => usr !== user);
        }
    },
}
</script>

<style>
ul {
    list-style: none;
    margin:1rem 0;
    padding: 0;
}

li {
    border: 1px solid black;
    padding: 1rem;
    text-align: center;
}
</style>