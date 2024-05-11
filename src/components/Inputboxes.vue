<script>
export default {
  name: 'Input-boxes',
  data() {
    return {
      sports: ['cricket'],
      player: 'finch'
    };
  }
}
</script>
<template>
  <div>

      <h3>Form example</h3>
      <label for="cricket">cricket</label>&nbsp;
      <input type="checkbox" value="cricket" v-model="sports" id="cricket" />
      &nbsp;&nbsp;
        
      <label for="footbal">Footbal</label>&nbsp;
      <input type="checkbox" value="footbal" v-model="sports" id="footbal" />
      &nbsp;&nbsp;
    
      <label for="hockey">Hockey</label>&nbsp;
      <input type="checkbox" value="hockey" v-model="sports" id="hockey" />
      &nbsp;&nbsp;
    
      <h3>Players</h3>
      <label for="john">John</label>&nbsp;
      <input type="radio" value="john" v-model="player" id="john" />
      <br/>
      <label for="finch">Finch</label>&nbsp;
      <input type="radio" value="finch" v-model="player" id="finch" />
      <br/>
    
    
    <h4>Selected Sports {{ sports }}</h4>
    <h4><strong>Player Name</strong>:: {{ player }}</h4>
  </div>
</template>