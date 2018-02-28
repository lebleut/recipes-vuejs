<template>
  <div id="app" class="container">
    <div class="nav">
      <button @click="currentComp = 'app-settings'">Settings</button>
      <button @click="currentComp = 'app-new'">Create A New Recipe</button>
      <button @click="currentComp = 'app-list'">Recipes List</button>
    </div>
    <keep-alive>
      <app-settings
        v-if="currentComp == 'app-settings'"
        :ingredients="ingredients"
        :unities="unities"
      />
      <app-new
        v-if="currentComp == 'app-new'"
        :ingredients="ingredients"
        :unities="unities"
      />
      <app-list
        v-if="currentComp == 'app-list'"
        :recipes="recipes"
      />
    </keep-alive>
  </div>
</template>

<script>
// event bus
import { EventBus } from './main.js'

import appSettings from './components/settings.vue'
import appNew from './components/new.vue'
import appList from './components/list.vue'

export default {
  name: 'app',
  data: function() {
    return {
      currentComp: 'app-settings',

      recipes: [],
      ingredients: [
        'Lait',
        'Farine',
        'Huil',
        'Levure',
        'Jus',
      ],
      unities: [
        'Litre',
        'Gramme',
        'Kg',
        'Cuillère à soupe',
        'Cuillère à café',
      ],
    }
  },
  components:{
    'app-settings': appSettings,
    'app-new': appNew,
    'app-list': appList,
  },
  methods:{

  },
  created: function(){
    var self = this
    EventBus.$on('newUnityAdded', function(unity){
      self.unities.push(unity)
    })
    EventBus.$on('newIngredientAdded', function(ingredient){
      self.ingredients.push(ingredient)
    })
    // newRecipeAdded
    EventBus.$on('newRecipeAdded', function(recipe){
      self.recipes.push({
        name: recipe.name,
        ingredients: recipe.ingredients,
        steps: recipe.steps,
      })
    })
  }
}
</script>

<style lang="scss">

</style>
