<template>
  <div>
    <a v-for="item in num" :href="`#${item}`" :key="item.id">跳转</a>
    <ul>
      <li style="height: 500px" v-for="item in num" :id="item" :key="item.id"></li>
    </ul>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        num: [1,2,3,4]
      }
    },
  }
</script>

<style lang="scss" scoped>

</style>
