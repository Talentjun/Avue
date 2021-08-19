<template>
  <div class="father">
    <h3>这里是父组件</h3>
    <!--第一次使用：用flex展示数据-->
    <child>
      <template slot-scope="scope">
        <div class="tmpl">
          <span v-for="item in scope.lists" :key="item.id">{{item}}</span>
        </div>
      </template>

    </child>

    <!--第二次使用：用列表展示数据-->
    <child>
      <template slot-scope="scope">
        <ul>
          <li v-for="item in scope.lists" :key="item.id">{{item}}</li>
        </ul>
      </template>

    </child>

    <!--第三次使用：直接显示数据-->
    <child>
      <template slot-scope="scope">
       {{scope.lists}}
      </template>

    </child>

    <!--第四次使用：不使用其提供的数据, 作用域插槽退变成匿名插槽-->
    <child>
      我就是模板
    </child>
  </div>
</template>
<script>
import child from '@/views/yj/child'
export default {
  components: {
    child,
  },
}
</script>
