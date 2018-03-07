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
      currentComp: 'app-list',

      recipes: [{
        "name": "Crèpes",
        "ingredients": [
          {
            "name": "Lait",
            "quantity": "0.5",
            "unity": "Litre"
          },
          {
            "name": "Sel",
            "quantity": "1",
            "unity": "Pincée"
          },
          {
            "name": "Farine",
            "quantity": "250",
            "unity": "Gramme"
          },
          {
            "name": "Oeuf",
            "quantity": "4",
            "unity": "Pièce"
          },
          {
            "name": "Beurre",
            "quantity": "50",
            "unity": "Gramme"
          },
          {
            "name": "Sucre vanillé",
            "quantity": "1",
            "unity": "Sachet"
          },
          {
            "name": "Rhum",
            "quantity": "1",
            "unity": "Cuillère à soupe"
          }
        ],
        "steps": [
        "Dans un saladier, versez la farine et les oeufs. Puis progressivement ajoutez le lait tout en mélangeant avec votre fouet. Ajoutez le sucre vanillé, la pincée de sel.",
        "Laissez reposer la pâte à crêpe si possible une heure. Faites chauffer une poêle, une fois chaude, versez un peu de beurre pour graisser la poêle.",
        "Versez une demi-louche de votre pâte à crêpe et faites cuire 1 à 2 minutes par face.",
        "Voilà vos crèpes sont prêtes, vous pouvez maintenant les déguster.",
        ]
      }],
      ingredients: [
        'Lait',
        'Farine',
        'Huil',
        'Levure',
        'Jus',
        'Fraise',
        'Oeuf',
        'Sel',
        'Sucre',
        'Sucre vanillé',
        'Rhum'
      ],
      unities: [
        'Litre',
        'Gramme',
        'Kg',
        'Cuillère à soupe',
        'Cuillère à café',        
        'Goute',
        'Pièce',
        'Pincée',
        'Gousse',
        'Boite',
        'Sachet'
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
