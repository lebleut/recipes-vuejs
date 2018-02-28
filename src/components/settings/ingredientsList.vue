<template>
  <div class="container">
  	<div class="ingredients" v-if="ingredients.length">
  		<hr>
  		<h2>Ingredients</h2>
  		<ul>
  			<li v-for="ingredient in ingredients">{{ ingredient }}</li>
  		</ul>
  	</div>
  </div>
</template>

<script>

export default {
	props: [ "ingredients" ],
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
