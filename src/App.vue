<template>
  <div id="app">
    <div class="container">
      <div class="search-ui row">
        <div class="col-6">
          Filter by price interval: <b>€ 10</b> <input id="ex2" type="text" class="span2" value="" data-slider-min="10" data-slider-max="1000" data-slider-step="5" data-slider-value="[250,450]"/> <b>€ 1000</b>
        </div>
      </div>
      <div class="search-results row">
        <div v-for="villa in villas" class="col-12 col-sm-6 col-md-4 col-lg-3">
          <div class="card my-2 p-3">
            <h2>{{ villa.title }}</h2>
            <span v-if="villa.pool">Has a pool.<br></span>
            <span v-if="villa.near_sea">Near the sea!<br></span>
            <span><strong>{{ villa.price_per_week }}</strong> per week.</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="coffee">
import Villas from './assets/example_data.json'

App =
  name: 'app'
  data: () ->
    msg: 'Welcome to You'
  computed:
    villas: () -> Villas

export default App
</script>

<style lang="sass">
@import '../node_modules/bootstrap/scss/bootstrap.scss'
@import url('https://fonts.googleapis.com/css?family=Montserrat|Open+Sans|Material+Icons')

.card
  min-height: 12em

</style>
