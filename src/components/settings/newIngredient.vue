<template>
  <div class="container">
    <h3>New Ingredient</h3>
    <div class="form">
      <label>
        Name : 
        <input v-model="newIngredient" />
      </label>
      <button @click="addIngredient()">Add Ingredient</button>
    </div>
  </div>
</template>

<script>
// event bus
import { EventBus } from '../../main.js'

export default {
	props:[ 'unities' ],
	data: function() {
		return {
			newIngredient: '',
		}
	},
	methods:{
		addIngredient: function(){
		  if( this.newIngredient.trim() != '' ){
		    EventBus.$emit('newIngredientAdded', this.newIngredient)
		  }
		  this.newIngredient = ''
		}
	}
}
</script>

<style lang="scss">

</style>