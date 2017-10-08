<template>
    <div>
      <div class="main-view">
        <timer :count=total_reps :seconds=seconds :stop=stop />
      </div>
    </div>
</template>

<script>
import {
  QBtn,
  QIcon
} from 'quasar'

import Timer from './Timer.vue'

export default {
  name: 'index',
  components: {
    QBtn,
    QIcon,
    Timer
  },
  data () {
    return {
      total_reps: 20,
      seconds: 60,
      stop: false
    }
  }
}
</script>

<style scoped>
  .main-view {
    display: flex;
    flex-flow: row nowrap;
    align-items: center;
    justify-content: center;
    height: 100vh;
  }
</style>
