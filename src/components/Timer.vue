<template>
  <div>{{timeElapsed}}</div>
</template>

<script>
import Timer from '../../node_modules/easytimer/dist/easytimer.min.js'

const timer = new Timer()

export default {
  name: 'timer',
  props: ['count', 'seconds'],
  data () {
    return {
      completed: 0
      timeElapsed: ''
    }
  },
  methods: {
    processTick: function () {
      this.completed++
    },
    startTimer: function () {
      timer.start()
      timer.addEventListener('secondsUpdated', function(e) {
        this.timeElapsed = timer.getTimeValues().toString()
      })
    }
  },
  computed: {
    remaining: function () {
      return this.count - this.completed
    }
  }

}
</script>

<style>
</style>
