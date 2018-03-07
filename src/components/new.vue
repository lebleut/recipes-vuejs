<template>
  <div class="container">
    <h3>New Recipe</h3>
    <div class="form">
      <label>
        Name : 
        <input v-model="newRecipe.name" />
        Image :
        <input v-model="newRecipe.image" /> <br>
        <img :src="newRecipe.image">
      </label>
      <br>
      <div>
        Ingredients : 
        <template v-for="ingredient in newRecipe.ingredients">
          <recipe-ingredient
            :unities="unities"
            :ingredients="ingredients"
            :ingredient="ingredient"
          />
        </template>
        <recipe-ingredient
          :unities="unities"
          :ingredients="ingredients"
          :ingredient="newRecIngredient"
          :isNew="true"
        />
      </div>
      <div>
        Etapes : 
        <template v-for="step in newRecipe.steps">
          <recipe-step
            :step="step"
          />
        </template>
        <recipe-step
          :step="newRecstep"
          :isNew="true"
        />
      </div>
      <br>
      <button @click="addRecipe()">Add Recipe</button>
    </div>
  </div>
</template>

<script>
// event bus
import { EventBus } from '../main.js'

import recipeIngredient from './new/recipeIngredient.vue'
import recipeStep from './new/recipeStep.vue'

export default {
  props:[ 'unities', 'ingredients' ],
  data: function() {
    return {
    	newRecipe: {
        name: '',
        image:'',
        ingredients: [],
        steps: []
      },
      newRecIngredient:{
        name: '',
        quantity:'',
        unity:''
      },
      newRecstep: ''
    }
  },
  components:{
    "recipeIngredient": recipeIngredient,
    "recipeStep": recipeStep
  },
  methods:{
    addRecipe: function(){
      if( this.newRecipe.name.trim() != '' ){
        EventBus.$emit('newRecipeAdded', this.newRecipe)
        this.newRecipe.name = ''
        this.newRecipe.image = ''
        this.newRecipe.ingredients = []
        this.newRecipe.steps = []
      }
    }
  },
  created: function(){
    var self = this
    EventBus.$on('newRecIngredientAdded', function(recIngredient){
      self.newRecipe.ingredients.push({
        name: recIngredient.name,
        quantity: recIngredient.quantity,
        unity: recIngredient.unity,
      })
    })
    EventBus.$on('newRecstepAdded', function(recStep){
      self.newRecipe.steps.push(recStep)
    })
  }
}
</script>

<style lang="scss">

</style>