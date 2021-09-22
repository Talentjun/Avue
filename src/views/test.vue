<template>
  <div>
    <div id="box">
      <div
        v-for="item in num"
        :key="item.count"
        :ref="`item${item.count}`"
        class="content-box"
      >
        {{ item.name }}
      </div>
    </div>
    <nav>
      <ul id="side-nav">
        <li
          v-for="item in num"
          :key="item.count"
          :class="{ active: item.count == count ? true : false }"
          @click="go(item.count)"
        >
          {{ item.name }}
        </li>
      </ul>
    </nav>
  </div>
</template>

<script>
export default {
  data() {
    return {
      count: 1,
      num: [
        {
          name: '1',
          count: 1,
        },
        {
          name: '2',
          count: 2,
        },
        {
          name: '3',
          count: 3,
        },
        {
          name: '4',
          count: 4,
        },
        {
          name: '5',
          count: 5,
        },
        {
          name: '6',
          count: 6,
        },
      ],
    }
  },
  mounted() {
    this.$nextTick(() => {
      let that = this
      let content = document.querySelector('#avue-view')
      content.addEventListener('scroll', () => {
        let scrollTop = document.querySelector('#avue-view').scrollTop
        let anchor = document.querySelectorAll('.content-box')
        for (let i = 0; i < anchor.length; i++) {
          if (anchor[i].offsetTop - 50 <= scrollTop) {
            that.count = i + 1
          }
        }
      })
    })
  },
  methods: {
    go(count) {
      this.$nextTick(() => {
        this.count = count
        document.querySelector('#avue-view').scrollTop =
          this.$refs[`item${count}`][0].offsetTop - 50
      })
    },
  },
}
</script>

<style lang="scss" scoped>
#side-nav {
  position: fixed;
  left: 300px;
  top: 100px;
}

#side-nav li {
  width: 60px;
  height: 60px;
  line-height: 60px;
  font-weight: 900;
  text-align: center;
  background-color: #fff;
  border-radius: 10px;
  box-shadow: 2px 1px 3px 0 rgb(26, 25, 25);
  cursor: pointer;
  margin-bottom: 10px;
}

#box {
  margin-left: 300px;
  width: 100%;
  height: 100%;
  overflow: auto;
  div {
    width: 100%;
    height: 1000px;
  }
}

.active {
  color: blue;
}
</style>