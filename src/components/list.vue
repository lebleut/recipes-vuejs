<template>
  <div class="container">
  	<div v-if="!recipes.length">
  		<h3>No Recipes added yet ...</h3>
  	</div>
  	<div v-else>
	  	<h1>Recipes List</h1>
	    <template v-for="recipe in recipes">
	    	<h2>{{ recipe.name }}</h2>
	    	<ul>
	    		<li v-for="ing in recipe.ingredients">{{ ing.name }}</li>
	    	</ul>
	    	<ul>
	    		<li v-for="stp in recipe.steps">{{ stp }}</li>
	    	</ul>
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
