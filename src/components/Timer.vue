<template>
  <div>{{count}}</div>
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
    }
  },
  methods: {
    processTick: function () {
      this.completed++
    },
    startTimer: function () {
      timer.start()
    }
  },
  computed: {
    remaining: function () {
      return this.count - this.completed
    }
  },
  mounted () {
    console.log(true)
  }

}
</script>

<style>
</style>
