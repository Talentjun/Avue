<template>
  <div>
    sonTitle: {{ sonTitle }} names: {{ names }}
    <p>$attrs: {{ $attrs }}</p>
    <grand-son v-bind="$attrs" v-on="$listeners" @test="test"></grand-son>
  </div>
</template>

<script>
import grandSon from './grandSon.vue'
export default {
  props: ['names', 'title'],
  components: {
    grandSon,
  },
  data() {
    return {
      sonTitle: this.title,
    }
  },
  methods: {
    test(value) {
      console.log('son', value)
    },
  },
}
</script>

<style lang="scss" scoped>
</style>