<template>
  <div class="section ui">
    <nav class="navbar is-fixed-bottom is-transparent">
      <div class="navbar-menu is-active">
        <div class="navbar-end">
          <div class="navbar-item">
            <div class="field has-addons has-addons-centered">
              <div class="control">
                <div class="select">
                  <select v-model="selected" v-on:change="onChangeEventHandler()">
                    <option
                      v-for="prop in props"
                      v-bind:value="prop.urutan"
                      v-bind:key="prop.urutan"
                    >{{capitalizeFirstLetter(prop.wulan)}}</option>
                  </select>
                </div>
              </div>
              <p class="control">
                <input
                  class="input"
                  type="number"
                  placeholder="1867 - 2106"
                  size="4"
                  min="1867"
                  max="2106"
                  required
                  v-model="taunjawa"
                />
              </p>
              <p class="control">
                <a class="button is-primary" v-on:click="cal()">Lihat</a>
              </p>
            </div>
          </div>
        </div>
      </div>
    </nav>
    <div class="container">
      <div class="columns">
        <div class="column"></div>
        <div class="column has-text-centered">
          <div class="columns">
            <div class="column">
              <h3 class="title is-4 tgl-title">{{ sasi }} {{ taun }} J</h3>
              <div class="column tgl-tjk">
                <h4 class="title is-6">{{ taunWindu }}, {{ kurup }}</h4>
              </div>
            </div>
          </div>
        </div>
        <div class="column"></div>
      </div>

      <div class="quick-hack-mobile-version">
        <div class="tgl-container-head is-mobile araning-dino has-text-centered">
          <span class="column"  v-for="(cell, index) in cells" v-if="index < 7">
            <div>{{ capitalizeFirstLetter(cell[index + 1].dinten) }}</div>
          </span>
        </div>
        <div class="tgl-container">
          <div v-for="(cell, index) in cells">
            <div class="cell cell-1" v-on:click.capture="tglEventHandler">
              <p
                class="tgl-num"
                :id="`tgl-${index + 1}`"
                :data-tgl="[index + 1, cell[index+1].dinten, cell[index +1].pasaran]"
              >{{ index + 1 }}</p>
              <p class="tgl-dinpar">
                <!--<span class="tgl-din">{{ capitalizeFirstLetter(cell[index + 1].dinten) }}</span>-->
                
                <span class="tgl-pas">{{ capitalizeFirstLetter(cell[index +1].pasaran) }}</span>
                
              </p>
            </div>
          </div>
        </div>
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
      cells: [],
      taun: '',
      taunWindu: '',
      sasi: '',
      kurup: '',
      props: KalenderJawa.araningSasi,
      selected: 1,
      taunjawa: 1953
    }
  },
  methods: {
    async sasiPenuh(_sasiParam, _taunParam) {
      if (
        parseInt(_taunParam) > 2106 ||
        parseInt(_taunParam) < 1867 ||
        _taunParam.length == 0
      ) {
        alert('Masukkan angka antara 1867 - 2106!')
      } else {
        const { k, s } = await KalenderJawa.sasi(_sasiParam, _taunParam)
        const _s = s.get(k)
        this.cells = _s

        //console.log(_s)

        const _kur = await KalenderJawa.cariKurupTahunJawa(_taunParam)
        // console.log(_kur)
        const _taunWindu = _kur.taun.taun
        const _sasi = KalenderJawa.araningSasi[_sasiParam - 1].wulan
        const _kurup = `${this.capitalizeFirstLetter(
          _kur.kurup.taun
        )} ${this.capitalizeFirstLetter(
          _kur.kurup.dinten.dino
        )} ${this.capitalizeFirstLetter(_kur.kurup.pasaran.pasaran)}`

        this.sasi = this.capitalizeFirstLetter(_sasi)
        this.taun = _taunParam
        this.taunWindu = this.capitalizeFirstLetter(_taunWindu)
        this.kurup = _kurup
      }
    },
    capitalizeFirstLetter(string) {
      return string.charAt(0).toUpperCase() + string.slice(1)
    },
    tglEventHandler(event) {
      if (event.target.hasAttribute('data-tgl')) {
       // console.log(event.target.getAttribute('data-tgl'))
      }
    },
    onChangeEventHandler() {},
    cal() {
      this.sasiPenuh(this.selected, this.taunjawa)
    }
  },
  created() {
    this.sasiPenuh(1, 1953)
  }
}
</script>
