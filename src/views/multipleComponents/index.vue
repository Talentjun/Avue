<template>
  <div>
    <son :names="value" age="18" @test="test"></son>
  </div>
</template>

<script>
import son from './son.vue'
export default {
  name: 'multipleComponents',
  components: {
    son,
  },
  data() {
    return {
      value: 'yj',
    }
  },
  methods: {
    test(value) {
      console.log(value)
    },
  },
}
</script>

<style lang="scss" scoped>
</style>