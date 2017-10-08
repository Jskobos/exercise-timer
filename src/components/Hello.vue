<template>
    <div>
      <div class="main-view">
        <timer :count=total_reps :duration=duration :stop=stop />
      </div>
    </div>
</template>

<script>
import {
  QBtn,
  QIcon
} from 'quasar'

import Timer from './Timer.vue'
import moment from 'moment'

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
      duration: moment.duration(1, 'minutes'),
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
    background: black;
    color: white;
  }
</style>
