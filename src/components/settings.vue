<template>
  <div class="container">
  	<h1>Settings</h1>
  	<ingredients-list :ingredients="ingredients" />
  	<unities-list :unities="unities" />

  	<hr>

  	<new-unity/>
  	<new-ingredient :unities="unities" />
  </div>
</template>

<script>
import ingredientsList from './settings/ingredientsList.vue'
import unitiesList from './settings/unitiesList.vue'

import newIngredient from './settings/newIngredient.vue'
import newUnity from './settings/newUnity.vue'

export default {
	props: [ "ingredients", "unities" ],
  data: function() {
    return {
    }
  },
  components:{
  	'ingredientsList': ingredientsList,
  	'unitiesList': unitiesList,
  	'newIngredient': newIngredient,
  	'newUnity': newUnity,
  },
  methods:{
  }
}
</script>

<style lang="scss">

</style>
