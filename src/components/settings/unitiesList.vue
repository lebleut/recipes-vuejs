<template>
  <div class="container">
    <div class="unities" v-if="unities.length">
      <h2>Unities</h2>
      <ul>
        <li v-for="unity in unities">{{ unity }}</li>
      </ul>
    </div>  </div>
</template>

<script>

export default {
	props: [ "unities" ],
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
