<script>
    export default {
        name: 'foor-loop',
        data() {
            return {
                technologies: ['Javascript', 'Python', 'C++', 'Java']
            }
        }
    }
</script>


<template>
    <h3>For loop block</h3>
    <ul>
        <li v-for="tech in technologies" :key= "tech">
            {{ tech }}
        </li>
    </ul>
</template>