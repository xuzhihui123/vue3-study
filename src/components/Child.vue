<template>
<div>
  <button @click="stepValue">儿子的button</button>
   儿子{{childValue.count}}
   <button @click="goClick">儿子的click</button>
   <slot name="good" v-bind="childProps"></slot>
</div>
</template>

<script lang='ts'>
import { defineComponent, inject, toRefs } from 'vue'

export default defineComponent({
  props: {
    childProps: {
      type: Object
    }
  },
  setup (props, { emit }) {
    const { childProps } = toRefs(props)
    console.log(childProps.value, '22')
    const childValue = inject('childValue')
    const stepValue = inject('stepValue')
    const goClick = () => {
      emit('goClick', 44)
    }
    return {
      childValue,
      stepValue,
      goClick
    }
  }
})
</script>
<style  scoped lang='scss'>

</style>
