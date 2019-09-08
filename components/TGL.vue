<template>
  <section>
    <div class="container">
      <div class="columns">
        <div class="column">
          <p>{{ kurup }}</p>
        </div>
        <div class="column has-text-centered">
          <h2 class="title">{{ sasi }} {{ taun }} J</h2>
        </div>
        <div class="column">
          <p>{{ taunWindu }}</p>
        </div>
      </div>
    </div>
    <div class="container">
      <div class="tgl-container">
        <div v-for="(cell, index) in cells">
          <div class="cell cell-1" v-on:click.capture="tglEventHandler">
            <p class="tgl-num" :id="`tgl-${index + 1}`" :data-tgl="[index + 1, cell[index+1].dinten, cell[index +1].pasaran]">{{ index + 1 }}</p>
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
      cells: [],
      taun: '',
      taunWindu: '',
      sasi: '',
      kurup: ''
    }
  },
  methods: {
    async sasiPenuh() {
      const _sasiParam = 1
      const _taunParam = 1953

      const { k, s } = await KalenderJawa.sasi(_sasiParam, _taunParam)
      const _s = s.get(k)
      this.cells = _s

      const _kur = await KalenderJawa.cariKurupTahunJawa(_taunParam)
      // console.log(_kur)
      const _taunWindu = _kur.taun.taun
      const _sasi = KalenderJawa.araningSasi[_sasiParam - 1].wulan
      const _kurup = `${_kur.kurup.taun} ${_kur.kurup.dinten.dino} ${_kur.kurup.pasaran.pasaran}`

      this.sasi = _sasi
      this.taun = _taunParam
      this.taunWindu = _taunWindu
      this.kurup = _kurup
      // console.log(_s)
    },
    capitalizeFirstLetter(string) {
      return string.charAt(0).toUpperCase() + string.slice(1)
    },
    tglEventHandler(event) {
      if(event.target.hasAttribute('data-tgl')) {
        console.log(event.target.getAttribute('data-tgl'))
      }
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
