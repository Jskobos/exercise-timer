<template>
  <div>{{seconds}}</div>
</template>

<script>

export default {
  name: 'timer',
  props: ['count', 'seconds'],
  data () {
    return {
      completed: 0,
      timeElapsed: ''
    }
  },
  methods: {
    tick: function () {
      this.timeElapsed = Date.now() - this.start
    },
    rep: function () {
      this.completed++
    }
  },
  computed: {
    remaining: function () {
      return this.count - this.completed
    },
    elapsed: function () {
      return Math.round(this.timeElapsed / 100)
    },
    seconds: function () {
      return (this.elapsed / 10).toFixed(1);
    }
  },
  mounted () {
    this.start = Date.now()
    this.timer = setInterval(this.tick, 50)
  },
  beforeDestroy () {
    clearInterval(this.timer)
  }

}
</script>

<style>
</style>
