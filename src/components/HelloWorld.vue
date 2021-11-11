

<template>
  <h1>Hello</h1>
  <button @click="color = 'red'">变色</button>

  <button type="button" @click="count++">count is: {{ count }} double :{{ double }}</button>
  <p>
    <child :msg="msg" data="qqqqq" @click="handle" @show="showw" />
  </p>
  <h3>姓名:{{ user.name }}</h3>
  <h3>年龄:{{ user.age }}</h3>
  <h3>wife:{{ user.wife }}</h3>
  <h3>computedcomputed: {{ fullName2 }}</h3>
  <h3>watchwatchwatch: {{ fullName3 }}</h3>
  <button @click="updateUser">更新</button>
</template>
<script setup  lang="ts">
import { ref, computed, defineComponent, reactive, watch, watchEffect, toRefs, } from 'vue'
import Child from './child.vue'
// const count = ref(0)
// let double =computed(()=>count.value*3)
defineProps<{ msg: string }>()

const msg = ref<String>('hello,vue33333333333333333');
const count = ref(0)
const fullName3 = ref('');
const color = ref('pink');
let double = computed(() => count.value * 3)
const handle = (value: any) => {
  console.log(value)
}
const showw = () => {
  console.log('name:', 'hzw');
};
const user = ref({
  name: 'hzw',
  age: 18,
  wife: {
    name: 'xioaohong',
    age: 18,
    books: ['红宝书', '设计模式', '算法与数据结构'],
  },
});
// const state = toRefs(user)
const updateUser = () => {
  user.value.name = '小红';
  user.value.age += 2;
  user.value.wife.books[0] = 'JavaScript从入门到入土';
  console.log(user.value)
};
const fullName2 = computed({
  get() {
    return user.value.name + '_' + user.value.age;
  },
  set(val: string) {
    const names = val.split('_');
    user.value.name = "computed";
    user.value.age = 999;
  },
});
interface listProps {
  name?: String,
  age: Number
}
watch(
  user,
  ({ name, age }: listProps) => {
    console.log(777777)
    fullName3.value = name + '_========' + age;
  },
  { immediate: true, deep: true }
);
watchEffect(() => {
  const names = fullName2.value.split('_');
  console.log(names)
  user.value.wife.name = names[0];
  user.value.wife.age = Number(names[1]);
});


</script>
<style scoped>
a {
  color: #42b983;
}
h1 {
  color: v-bind(color);
  font-size: 18px;
}
label {
  margin: 0 0.5em;
  font-weight: bold;
}

code {
  background-color: #eee;
  padding: 2px 4px;
  border-radius: 4px;
  color: #304455;
}
</style>
