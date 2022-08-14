<!--
 * @Description: 
 * @Author: hbj
 * @Date: 2022-08-14 22:14:48
 * @LastEditTime: 2022-08-14 23:14:15
 * @LastEditor: 
-->
<template>
  <div>{{ demo }} :{{ state.count }}</div>
  <button @click="addCount(2)">+2</button>
  <button @click="addCount">+1</button>
  <br />
  {{ obj }}
  <button @click="changeObj">changeObj</button>
  <br />
  {{ publishedBooksMessage }}
  {{full}}
</template>

// <script  lang="ts">
// import { reactive, ref } from "vue";

// export default {
//   name: "setUpDemo",
//   setup() {
//     const state = reactive({
//       count: 1,
//     });
//     const demo = ref("demo");

//     function addCount(val?) {
//       //   console.log(val);
//       //   if (val) state.count += val;
//       //   else {
//       //     state.count++;
//       //   }
//       state.count++;
//     }
//     return { state, demo, addCount };
//   },
// };
//
</script>

<script setup lang="ts">
import { log } from "console";
import { reactive, ref, computed, onMounted } from "vue";
const state = reactive({
  count: 1,
});
function addCount(val?) {
  //   console.log(val);
  //   if (val) state.count += val;
  //   else {
  //     state.count++;
  //   }
  console.log(count);
  state.count++;
}
// count 也和 state.count 失去了响应性连接
let { count } = state;
// 不会影响原始的 state
count++;
console.log("count", count);

const demo = ref("demo");
console.log(demo.value);

const obj = reactive({
  demo1: 1,
  demo2: "demo2",
});
/**
 * @description: 深层响应
 * @return {*}
 */
function changeObj() {
  obj.demo1++;
  obj.demo2 = "demo2+1";
}
const cloneRef = ref({ count: 0 });
// 这是响应式的替换
cloneRef.value = { count: 1 };
console.log("cloneRef", cloneRef);

const cloneObj = {
  foo: ref(1),
  bar: ref(2),
};

// 该函数接收一个 ref
// 需要通过 .value 取值
// 但它会保持响应性
//  callSomeFunction(cloneObj.foo)

// 仍然是响应式的
const { foo, bar } = cloneObj;
foo.value += 1;
console.log(cloneObj);

const author = reactive({
  name: "John Doe",
  books: [
    "Vue 2 - Advanced Guide",
    "Vue 3 - Basic Guide",
    "Vue 4 - The Mystery",
  ],
});

// 一个计算属性 ref
const publishedBooksMessage = computed(() => {
  return author.books.length > 3;
});

const jk = ref('1');
const mn = ref('2');
const full = computed({
  get() {
    return jk.value + " " + mn.value;
  },
  set(val) {
    console.log(val)
    // 注意：我们这里使用的是解构赋值语法
    [jk.value, mn.value] = (val as any).split(' ')
  },
});

onMounted(()=>{
    full
})

</script>


<style scoped>
</style>