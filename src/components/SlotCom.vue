
<script lang='tsx'>
import { defineComponent, h, ref } from 'vue'

export default defineComponent({
  setup () {
    const title = ref('我是slotcom')
    const dateValue = ref('')
    return {
      title,
      dateValue
    }
  },
  render () {
    return (<div class="margin">
      <span>{this.title}</span>
      {
        this.$slots.header!()
      }
      <el-date-picker
        v-model={this.dateValue}
        type="date"
        placeholder="Pick a day"
      />
    </div>)
    // 第二种 return h('div', this.$slots.header())
  }
})
</script>
<style  scoped lang='scss'>
.margin{
  margin-top: 30px;
}
</style>
