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
        "image": "https://cac.img.pmdstatic.net/fit/http.3A.2F.2Fwww.2Ecuisineactuelle.2Efr.2Fvar.2Fcui.2Fstorage.2Fimages.2Frecettes-de-cuisine.2Frecettes-par-evenements.2Fchandeleur.2Fcrepes-au-chocolat.2F1141872-2-fre-FR.2Fcrepes-au-chocolat.2Ejpg/748x372/quality/80/crop-from/center/crepes-au-chocolat.jpeg",
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
        image: recipe.image,
        ingredients: recipe.ingredients,
        steps: recipe.steps,
      })
    })
  }
}
</script>

<style lang="scss">
  img {
    max-width: 100%;
    max-height:  300px;
  }
</style>
