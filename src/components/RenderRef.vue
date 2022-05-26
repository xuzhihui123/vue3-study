
<script lang='tsx'>
import { defineComponent, reactive, ref } from 'vue'

export default defineComponent({
  setup () {
    const foo = reactive({ name: '我是renderref字符串' })
    const gg = ref('')
    return {
      foo,
      gg
    }
  },
  mounted () {
    // console.log('renderref', this.gg)  // 第一种ref
    console.log('renderref', this.$refs.gg) // 第二种$refs
  },
  render () {
    return <div ref="gg">
      {this.foo.name}
    </div>
  }
})
</script>
<style  scoped lang='scss'>

</style>
