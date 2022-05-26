
<script setup lang="ts">
import { reactive, defineProps, defineEmits, withDefaults, onMounted, ref } from 'vue'
interface Props{
  setupProps:string,
  modelValue:string
}
// 第一种 声明props
// const props = defineProps({
//   setupProps: {
//     type: String,
//     default () {
//       return '123'
//     }
//   },
//   modelValue: String
// })

// 第二种 ts声明props,并设置默认值
const props = withDefaults(defineProps<Props>(), {
  setupProps: '123'
})
// 声明emits
const emit = defineEmits(['update:modelValue'])
const foo = reactive({ name: 'lancer is good', color: 'blue' })
const cColor = ref('yellow')
onMounted(() => {
  cColor.value = 'red'
  foo.color = 'green'
})
</script>

<template>
    <h3 class="text1">单文件组件</h3>
    <div>
       {{foo.name}}----{{setupProps}}
    </div>
    <input type="text" :value="modelValue" @input="e=>$emit('update:modelValue',e.target.value)">
</template>

<style lang="scss" scoped>
  .text1{
    color:v-bind('cColor')
  }
</style>
