<template>
    <h1>child page</h1>
    <!-- <h5> {{ name }} </h5>
    <h6> User info: {{ user.email }}</h6> -->
    <!-- <button v-on:click="getData()">click here</button> -->
    <ul>
        <li v-for="item in users" :key="item.name">
            <Newuser :data="item"  />
        </li>
    </ul>
</template>

<script>
import Newuser from './Newuser.vue';
export default {
    name: 'child-component',
    props: {
        name: String,
        user: Object,
        // getData: Function,
    },
    data() {
        return {
            users: [
                { name: 'jackson', email: 'jackson@yopmail.com' },
                { name: 'jackson2', email: 'jackson2@yopmail.com' },
                { name: 'jackson3', email: 'jackson3@yopmail.com' },
                { name: 'jackson4', email: 'jackson4@yopmail.com' },
                { name: 'jackson5,', email: 'jackson5@yopmail.com' },
            ],
        }

    },
    components: {
        Newuser,
    }
}
</script>
<style>
li {
    list-style: none;
    border: 1px solid #ccc;
    border-radius: 5px;
    padding: 10px;
    margin-bottom: 1rem;
    background-color: rgb(235, 233, 231);
    font-size: 14px;
    border-left: 5px solid #00ca92;
}
</style>