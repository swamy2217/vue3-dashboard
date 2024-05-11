<script>
import Forloop from '../components/Forloop.vue';
import Ifelse from '../components/Ifelse.vue';
import Inputboxes from '../components/Inputboxes.vue';
export default {
  name: 'HOME',
  components: {
    Inputboxes,
    Ifelse,
    Forloop,
  },
  data() {
    return {
      count: 0,
      email: "abc@gmail.com",
      mobile: "8099111231",
    };
  },
  methods: {
    getName: function(name) {
      return `Hello ${name}`;
    },
    increment() {
      this.count++;
    }
  }
}
</script>

<template>
  <main>
    <h1> {{email}}</h1>
    <h2>Mobile: {{ mobile }}</h2>
    <h3>Name: {{getName('swamy')}}</h3>
    <h3>Name2: {{getName('Anneboina')}}</h3>
    <button @click="increment()">click here</button>
    <hr/>
    <input type="text" v-model="count"/>
    <div>{{ count }}</div>
    <Inputboxes />
    <Ifelse />
    <Forloop />

  </main>
</template>
