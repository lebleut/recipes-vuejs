<template>
  <div class="container">
  	<div v-if="!recipes.length">
  		<h3>No Recipes added yet ...</h3>
  	</div>
  	<div v-else>
	  	<h1>Recipes List</h1>
	    <template v-for="recipe in recipes">
	    	<h2>{{ recipe.name }}</h2>
        <img :src="recipe.image">
        <div v-if="recipe.ingredients.length">
          <h3>Ingredients</h3>
  	    	<ul>
  	    		<li v-for="ing in recipe.ingredients">{{ ing.quantity }} {{ ing.unity }} {{ ing.name }}</li>
  	    	</ul>
        </div>
        <div v-if="recipe.steps.length">
          <h3>Steps</h3>
  	    	<ol>
  	    		<li v-for="stp in recipe.steps">{{ stp }}</li>
  	    	</ol>
        </div>
	    </template>
  	</div>
  </div>
</template>

<script>

export default {
	props: [ 'recipes' ],
  data: function() {
    return {
    }
  },
  methods:{
  }
}
</script>

<style lang="scss">

</style>
