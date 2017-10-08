<template>
  <div class="timer-box">
    <div>{{second}}:{{tenth}}</div>
    <div>{{remaining}}</div>
    <q-btn glossy color="primary" @click="reset()">
      Reset
    </q-btn>
  </div>
</template>

<script>

import { QBtn } from 'quasar'

import moment from 'moment'

export default {
  name: 'timer',
  props: ['count', 'seconds', 'stop'],
  components: { QBtn },
  data () {
    return {
      completed: 0,
      timeElapsed: moment(0),
      start: moment(),
      timePerRep: (this.seconds / this.count) * 1000
    }
  },
  methods: {
    tick: function () {
      this.timeElapsed = moment(moment() - this.start)
      if (this.second > this.seconds) {
        this.complete()
      }
    },
    rep: function () {
      this.completed++
      if (this.completed === this.count) {
        this.complete()
      }
    },
    complete: function () {
      clearInterval(this.timer)
      clearInterval(this.repCount)
      this.completed = this.count
      this.timeElapsed = moment(0)
    },
    reset: function () {
      console.log('resetting')
      this.completed = 0
      this.start = moment()
      clearInterval(this.timer)
      clearInterval(this.repCount)
      this.timer = setInterval(this.tick, 50)
      this.repCount = setInterval(this.rep, this.timePerRep)
    }
  },
  computed: {
    remaining: function () {
      return this.count - this.completed
    },
    second: function () {
      return this.timeElapsed.second()
    },
    tenth: function () {
      return Math.floor(this.timeElapsed.millisecond() / 100)
    }
  },
  mounted () {
    this.reset()
  },
  beforeDestroy () {
    clearInterval(this.timer)
    clearInterval(this.repCount)
  }

}
</script>

<style scoped>
  .timer-box {
    
  }
</style>
