<template>
  <div id="app">
    <div class="container">

      <div class="search-ui card">
        <div class="form-inline">

          <div class="form-group">
            <input type="text" class="form-control"
              v-model="text_search" value="" placeholder="Filter by title or description">
          </div>

          <div class="form-group">
            <label class="form-check-label ml-5">
              <input class="form-check-input"
                type="checkbox" value="" v-model="pool">
              Has a pool.
            </label>
            <label class="form-check-label ml-5">
              <input class="form-check-input"
                type="checkbox" value="" v-model="near_sea">
              Near the sea.
            </label>
          </div>

        </div>
      </div>

      <div class="search-results row">
        <div v-for="villa in villas" class="col col-12 col-sm-6 col-md-4 col-xl-3">
          <div class="card my-2">
            <div class="card-block">
              <h4 class="card-title">{{ villa.title }}</h4>
              <span class="badge badge-info my-1"
                v-if="villa.pool">Has a pool.<br></span>
              <span class="badge badge-primary my-1"
                v-if="villa.near_sea">Near the sea.<br></span>
              <p>{{ villa.description.substr(0,44)+"..." }}</p>
            </div>
            <div class="card-footer">
              <strong>{{ villa.price_per_week }}</strong> per week.
            </div>
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
    pool: true
    near_sea: false
    text_search: ''
  computed:
    villas: () ->
      Villas.filter (x) =>
        if @pool && !x.pool then return false
        if @near_sea && !x.near_sea then return false
        if @text_search.length > 1
          inDesc = x.description.indexOf(@text_search) != -1
          inTitle = x.title.indexOf(@text_search) != -1
          if !inDesc && !inTitle then return false
        true

export default App
</script>

<style lang="sass">
@import '../node_modules/bootstrap/scss/bootstrap.scss'
@import url('https://fonts.googleapis.com/css?family=Montserrat|Open+Sans|Material+Icons')


body
  background-color: #f2f2f6

.search-ui
  margin-top: 40px
  padding: 20px 15px

.search-results
  background-color: white
  padding: 10px 5px
  margin: 40px 0 80px
  .card
    min-height: 15em


</style>
