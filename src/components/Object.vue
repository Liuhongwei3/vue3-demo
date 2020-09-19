<template>
  <div class="hello">
    <ul>
      <li>name: {{ state.obj.name }}</li>
      <li>age: {{ state.obj.age }}</li>
      <li>job: {{ state.obj.job }}</li>
    </ul>
    <button @click="changeName">changeName</button>
  </div>
</template>

<script>
import { reactive, computed, toRefs, watch } from "vue";

export default {
  name: "Reactive",
  setup() {
    // 只使用 reactive 的问题是，使用组合函数时必须始终保持对这个所返回对象的引用以保持响应性。这个对象不能被解构或展开：
    // toRefs API 用来提供解决此约束的办法——它将响应式对象的每个 property 都转成了相应的 ref。
    const state = reactive({
      obj: {
        name: "tadm",
        age: "20",
        job: "Front-end",
      },
    });

    // Proxy
    watch(state.obj, () => console.log(state.obj));

    function changeName(params) {
      state.obj.name = "Liuhongwei3";
    }

    return {
      state,
      changeName,
    };
    // return toRefs(state)
    // 如果我们将此段逻辑抽离出去进行结构则需要使用 toRefs 使得其依然是响应式
    // let {count, doubleCount} = xxx(export defaul xxx)
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
button {
  margin: 10px;
}
</style>
