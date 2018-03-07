<template>
  <div class="container">
    <div v-if="isNew">
      <label>
        <input v-model="newRecstep">
      </label>
      <button @click="addstep()">Add step</button>
    </div>

    <div v-else>
      <label>
        <input v-model="step">
      </label>
    </div>
  </div>
</template>

<script>
// event bus
import { EventBus } from '../../main.js'

export default {
  props:[ 'step', 'isNew' ],
  data: function() {
    return {
      newRecstep: '',
    }
  },
  methods:{
    addstep: function(){
      if( this.newRecstep.trim() != '' ){
        EventBus.$emit('newRecstepAdded', this.newRecstep)
        this.newRecstep = ''    
      }
    },
  }
}
</script>

<style lang="scss">

</style>