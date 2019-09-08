<template>
  <section>
    <div class="container">
      <div class="columns is-mobile">
        <div class="column has-text-centered">
          <h3 class="title is-5 tag is-success">{{ sasi }} {{ taun }} J</h3>
        </div>
        <div class="column has-text-centered">
          <h3 class="title is-5 tag">{{ taunWindu }}</h3>
        </div>
        <div class="column has-text-centered">
          <h3 class="title is-5 tag">{{ kurup }}</h3>
        </div>
      </div>
    </div>
    <div class="container">
      <div>
      <div class="columns is-mobile araning-dino has-text-centered">
          <div class="column">Akad</div>
        
          <div class="column">Senen</div>
          
          <div class="column">Selasa</div>
          
          <div class="column">Rebo</div>
          
          <div class="column">Kemis</div>
          
          <div class="column">Jemah</div>

          <div class="column">Sebtu</div>

      </div>
      <div class="tgl-container">
        <div v-for="(cell, index) in cells">
          <div class="cell cell-1" v-on:click.capture="tglEventHandler">
            <p class="tgl-num" :id="`tgl-${index + 1}`" :data-tgl="[index + 1, cell[index+1].dinten, cell[index +1].pasaran]">{{ index + 1 }}</p>
            <p class="tgl-dinpar">
              <!--
              <span class="tgl-din">{{ capitalizeFirstLetter(cell[index + 1].dinten) }}</span>
              -->
              <span class="tgl-pas">{{ capitalizeFirstLetter(cell[index +1].pasaran) }}</span>
            </p>
          </div>
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
      const _kurup = `${this.capitalizeFirstLetter(_kur.kurup.taun)} ${this.capitalizeFirstLetter(_kur.kurup.dinten.dino)} ${this.capitalizeFirstLetter(_kur.kurup.pasaran.pasaran)}`

      this.sasi = this.capitalizeFirstLetter(_sasi)
      this.taun = _taunParam
      this.taunWindu = this.capitalizeFirstLetter(_taunWindu)
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
