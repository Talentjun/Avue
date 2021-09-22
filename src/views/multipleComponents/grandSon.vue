<template>
  <div>
    {{ age }}
    <el-button @click="test">test</el-button>
  </div>
</template>

<script>
export default {
  props: ['age'],
  methods: {
    test() {
      this.$emit('test', '我是test')
    },
  },
}
</script>

<style lang="scss" scoped>
</style>