<template>
  <div class="container">
    <TGL/>
  </div>
</template>

<script>
import * as KalenderJawa from '@kalenderjawa/pustaka'
import TGL from '~/components/TGL.vue'

console.log(KalenderJawa)

export default {
  components: {
    TGL
  }
}
</script>

