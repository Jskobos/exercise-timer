<template>
  <div class="timer-box">
    <div class="rep-count">{{remainingReps}}</div>
    <div class="time-count">{{remainingTime.second()}}</div>
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
  props: ['count', 'duration', 'stop'],
  components: { QBtn },
  data () {
    return {
      completed: 0,
      timeElapsed: moment(0),
      start: moment(),
      timePerRep: (this.duration.asMilliseconds() / this.count)
    }
  },
  methods: {
    tick: function () {
      this.timeElapsed = moment(moment() - this.start)
      if (this.timeElapsed > this.duration) {
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
      this.completed = 0
      this.start = moment()
      clearInterval(this.timer)
      clearInterval(this.repCount)
      this.timer = setInterval(this.tick, 50)
      this.repCount = setInterval(this.rep, this.timePerRep)
    }
  },
  computed: {
    remainingReps: function () {
      return this.count - this.completed
    },
    remainingTime: function () {
      return moment(this.duration - this.timeElapsed)
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
    display: flex;
    flex-flow: column nowrap;
    align-items: center;
    justify-content: center;
  }
  .rep-count {
    height: 300px;
    width: 300px;
    border-radius: 50%;
    font-size: 8em;
    border: solid 12px rgba(26, 184, 237, 0.45);
    display:flex;
    justify-content: center;
    align-items: center;
  }
  .time-count {
    padding: 0.5em;
    font-size: 4em;
  }
</style>
