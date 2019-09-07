<template>
  <div class="tgl-container">
    <div v-for="(cell, index) in cells">
      <div class="cell cell-1">
        <p class="tgl-num">{{ index + 1 }}</p>
        <p class="tgl-dinpar">{{ capitalizeFirstLetter(cell[index + 1].dinten) }} {{ capitalizeFirstLetter(cell[index +1].pasaran) }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import * as KalenderJawa from '@kalenderjawa/pustaka'

export default {
  name: 'TGL',
  data() {
    return {
      cells: []
    }
  },
  methods: {
    async sasiPenuh() {
      const { k, s } = await KalenderJawa.sasi('mukarom', 1953)
      const _s = s.get(k)
      console.log(_s)
      this.cells = _s
    },
    capitalizeFirstLetter (string) {
      return string.charAt(0).toUpperCase() + string.slice(1)
    }
  },
  created() {
    this.sasiPenuh()
  }
}
</script>

<style>
.tgl-container {
  height: 40vh;
  margin: 1rem;
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr 1fr 1fr 1fr;
  grid-template-rows: 1fr 1fr 1fr 1fr 1fr;
  grid-gap: 1px 1px;
}
.cell {
  color: white;
  font-size: 1rem;
  text-align: center;
  padding: 1rem;
}

.cell .tgl-num {
  font-weight: 700;
  font-size: 2rem;
}

.cell .tgl-dinpar {
  font-weight: 500;
}
.cell-1 {
  background: deepskyblue;
}

</style>
