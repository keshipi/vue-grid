<template>
  <table class="grid table is-fullwidth">
    <thead>
      <tr>
        <th v-for="(column, index) in columns" :key="index" @click="sort(column)" :class="{ 'active': sortKey === column }">
          {{ column }}
          <span class="arrow" :class="0 < sortOrders[column] ? 'asc' : 'desc'"></span>
        </th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(d, index) in sorted" :key="index">
        <td>{{ d.name }}</td>
        <td>{{ d.power }}</td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  name: 'grid',
  props: {
    columns: Array,
    data: Array,
    keyword: String
  },
  data() {
    const sortOrders = {}
    this.columns.forEach(column => {
      sortOrders[column] = 1
    })
    return {
      sortKey: '',
      sortOrders: sortOrders
    }
  },
  computed: {
    sorted: function() {
      let data = this.data

      if (this.keyword) {
        data = data.filter(row => {
          return Object.keys(row).some(key => {
            return (
              String(row[key])
                .toLowerCase()
                .indexOf(this.keyword) > -1
            )
          })
        })
      }

      const order = this.sortOrders[this.sortKey]
      const sorted = data.sort((a, b) => {
        a = a[this.sortKey]
        b = b[this.sortKey]
        return (a === b ? 0 : a > b ? 1 : -1) * order
      })
      return sorted
    }
  },
  methods: {
    sort: function(sortKey) {
      this.sortKey = sortKey
      // ソート順を反転させる
      this.sortOrders[sortKey] = this.sortOrders[sortKey] * -1
    }
  }
}
</script>
<style>
.active .arrow {
  display: inline-block;
  vertical-align: middle;
  width: 0;
  height: 0;
  margin-left: 5px;
}
.active .arrow.asc {
  border-left: 4px solid transparent;
  border-right: 4px solid transparent;
  border-bottom: 4px solid #555;
}

.active .arrow.desc {
  border-left: 4px solid transparent;
  border-right: 4px solid transparent;
  border-top: 4px solid #555;
}
</style>
