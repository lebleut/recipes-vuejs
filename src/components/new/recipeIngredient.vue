<template>
  <div class="container">

    <div v-if="isNew">
      <label>
        <select v-model="newRecIngredient.name">
          <option v-for="ing in ingredients">{{ ing }}</option>
        </select>
      </label>

      <label>Qty: 
        <input v-model="newRecIngredient.quantity" />
      </label>

      <label>Unity: 
        <select v-model="newRecIngredient.unity" >
          <option v-for="unity in unities">{{ unity }}</option>
        </select>
      </label>
      <button @click="addIngredient()">Add ingredient</button>
    </div>

    <div v-else>
      <label>
        <select v-model="ingredient.name">
          <option v-for="ing in ingredients">{{ ing }}</option>
        </select>
      </label>

      <label>Qty: 
        <input v-model="ingredient.quantity" />
      </label>

      <label>Unity: 
        <select v-model="ingredient.unity" >
          <option v-for="unity in unities">{{ unity }}</option>
        </select>
      </label>
    </div>
  </div>
</template>

<script>
// event bus
import { EventBus } from '../../main.js'

export default {
  props:[ 'unities', 'ingredients', 'ingredient', 'isNew' ],
  data: function() {
    return {
      newRecIngredient:{
        name:'',
        quantity:'',
        unity:'',
      }
    }
  },
  methods:{
    addIngredient: function(){
      EventBus.$emit('newRecIngredientAdded', this.newRecIngredient)
      this.newRecIngredient = {
        name:'',
        quantity:'',
        unity:'',
      }
    },
  }
}
</script>

<style lang="scss">

</style>