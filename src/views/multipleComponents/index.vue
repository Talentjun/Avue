<template>
  <basic-container>
    title: <el-input v-model="title"></el-input>
    <son :names="value" age="18" @test="test" :title="title"></son>
  </basic-container>
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
      title: 'Talent',
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