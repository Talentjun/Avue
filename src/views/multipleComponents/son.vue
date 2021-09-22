<template>
  <div>
    {{ names }}
    <p>$attrs: {{ $attrs }}</p>
    <grand-son v-bind="$attrs" v-on="$listeners"></grand-son>
  </div>
</template>

<script>
import grandSon from './grandSon.vue'
export default {
  props: ['names'],
  components: {
    grandSon,
  },
}
</script>

<style lang="scss" scoped>
</style>