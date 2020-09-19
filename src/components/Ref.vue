<template>
  <div class="hello">
    <div>count: {{ count }}</div>
    <div>double-count: {{ doubleCount }}</div>
    <button @click="add">click</button>
  </div>
</template>

<script>
import {
  ref,
  watchEffect,
  onBeforeMount,
  onMounted,
  onUpdated,
  watch,
} from "vue";

export default {
  name: "Ref",
  setup() {
    // useState(initValue) ?
    let count = ref(0);
    let doubleCount = ref(0);

    function add(params) {
      count.value++;
    }

    //  watchEffect 应该接收一个应用预期副作用 (这里即设置 double) 的函数。
    // 它会立即执行该函数，并将该执行过程中用到的所有响应式状态的 property 作为依赖进行追踪。
    watchEffect(() => (doubleCount.value = count.value * 2));

    watch(() => {
      console.log("count change: " + count.value);
      console.log("doubleCount change: " + doubleCount.value);
    });

    watch(count, () => console.log("dep-count change: " + count.value));

    // 对应的生命周期函数
    onBeforeMount(() => {
      console.log("onBeforeMount ---- ", count.value, doubleCount.value);
    });
    onMounted(() => {
      console.log("onMounted ---- ", count.value, doubleCount.value);
    });
    onUpdated(() => {
      console.log("onUpdated ---- ", count.value, doubleCount.value);
    });

    return {
      count,
      doubleCount,
      add,
    };
  },

  /*
    Ref.vue?1d90:35 count change: 0
    Ref.vue?1d90:36 doubleCount change: 0
    Ref.vue?1d90:43 onBeforeMount ----  0 0
    Ref.vue?1d90:46 onMounted ----  0 0
    Ref.vue?1d90:35 count change: 1
    Ref.vue?1d90:36 doubleCount change: 2
    Ref.vue?1d90:39 dep-count change: 1
    Ref.vue?1d90:49 onUpdated ----  1 2
  */
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
