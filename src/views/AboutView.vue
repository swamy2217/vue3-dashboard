<script>
import Child from '../components/child.vue';

export default {
  name: 'ABOUT',
  components: {
    Child
  },
  data() {
    return {
      user: {name: "Tony", email: 'tony@yopmail.com'}
    }
  },
  methods: {
    // getData() {      
    //   alert("Method called");
    // }
  }
}
</script>
<template>
  <div class="about">
    <h1>level 2 page</h1>
    <Child name="swamy" :user="user" />
    <!-- :getData="getData()"  -->
  </div>
</template>

<style>
</style>
