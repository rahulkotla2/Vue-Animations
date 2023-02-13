<template>
    <transition-group tag="ul" name="user-data">
        <li v-for="user in users" :key="user" @click="removeUser(user)">
            {{ user }}
        </li>
    </transition-group>
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
    margin: 1rem 0;
    padding: 0;
}

li {
    border: 1px solid black;
    padding: 1rem;
    text-align: center;
}

.user-data-enter-from {
    opacity: 0;
    transform: translateX(-30px);
}

.user-data-enter-active {
    transition: all 1s ease-in;
}

.user-data-enter-to,
.user-data-leave-from {
    opacity: 1;
    transform: translateX(0);
}

.user-data-leave-active {
    transition: all 1s ease-in;
    position: absolute;
}

.user-data-leave-to {
    opacity: 0;
    transform: translateX(30px);
}

.user-data-move {
    transition: all 1s ease-in;
}
</style>