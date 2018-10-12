<template>
  <div id="app">
    <div class="container">
      <div class="columns">
        <div class="column is-half is-offset-one-quarter">
          <input class="input" v-model="keyword" id="search" placeholder="Search">
          <grid :data="gridData" :columns="gridColumns" :keyword="keyword"></grid>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Grid from './components/Grid'

export default {
  name: 'app',
  components: { Grid },
  data() {
    return {
      keyword: '',
      gridColumns: ['name', 'power'],
      gridData: [
        { name: 'Chuck Norris', power: Infinity },
        { name: 'Bruce Lee', power: 9000 },
        { name: 'Jackie Chan', power: 7000 },
        { name: 'Jet Li', power: 8000 }
      ]
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1,
h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
