<template>
  <nav class="navbar is-fixed-bottom">
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
              <input class="input" type="text" placeholder="Tahun Jawa"  required v-model="taunjawa"/>
            </p>
            <p class="control">
              <a class="button is-primary" v-on:click="cal()">Ubah</a>
            </p>
          </div>
        </div>
      </div>
    </div>
  </nav>
</template>

<script>
import * as KalenderJawa from '@kalenderjawa/pustaka'

export default {
  data() {
    return {
      props: KalenderJawa.araningSasi,
      selected: 1,
      taunjawa: 1953
    }
  },
  methods: {
    onChangeEventHandler () {
    
    },
    capitalizeFirstLetter (string) {
      return string.charAt(0).toUpperCase() + string.slice(1)
    },
    cal () {
      console.log(this.selected)
      console.log(this.taunjawa)
    }
  }
}
</script>
