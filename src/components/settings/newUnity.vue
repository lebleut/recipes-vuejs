<template>
  <div class="container">
    <h3>New unity</h3>
    <div class="form">
      <label>
        Name : 
        <input v-model="newUnity" />
      </label>
      <button @click="addUnity()">Add unity</button>
    </div>
  </div>
</template>

<script>
// event bus
import { EventBus } from '../../main.js'

export default {
  data: function() {
    return {
      newUnity:'',
    }
  },
  methods:{
    addUnity: function(){
      if( this.newUnity.trim() != '' ){
        EventBus.$emit('newUnityAdded', this.newUnity)
      }
      this.newUnity = ''
    }
  }
}
</script>

<style lang="scss">

</style>
