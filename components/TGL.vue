<template>
  <section>
    <div class="container">
      <div class="columns">
        <div class="column"></div>
        <div class="column has-text-centered">
          <h2 class="title">Sapar 1953 J</h2>
        </div>
        <div class="column"></div>
      </div>
    </div>
    <div class="container">
      <div class="tgl-container">
        <div v-for="(cell, index) in cells">
          <div class="cell cell-1">
            <p class="tgl-num">{{ index + 1 }}</p>
            <p class="tgl-dinpar">
              <span class="tgl-din">{{ capitalizeFirstLetter(cell[index + 1].dinten) }}</span>
              <span class="tgl-pas">{{ capitalizeFirstLetter(cell[index +1].pasaran) }}</span>
            </p>
          </div>
        </div>
      </div>
    </div>
  </section>
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
      const { k, s } = await KalenderJawa.sasi('sapar', 1953)
      const _s = s.get(k)
      this.cells = _s
    },
    capitalizeFirstLetter(string) {
      return string.charAt(0).toUpperCase() + string.slice(1)
    }
  },
  created() {
    this.sasiPenuh()
  }
}
</script>

<style>
.tgl-id {
  text-transform: uppercase;
  font-weight: 300;
  letter-spacing: 0.08em;
  font-size: 25px;
}

.tgl-container {
  height: 50vh;
  margin: 1rem;
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr 1fr 1fr 1fr;
  grid-template-rows: 1fr 1fr 1fr 1fr 1fr;
  grid-gap: 0px 0px;
}

.tgl-container div {
  border: 0px solid grey;
}

.tgl-container div:hover {
  background-color: antiquewhite;
}

.cell {
  color: black;
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
  background: transparent !important;
}
</style>
