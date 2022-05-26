
<script lang='tsx'>
import { defineComponent } from 'vue'

export default defineComponent({
  setup () {
    return {

    }
  },
  props: {
    modelValue: String
  },
  emits: ['update:modelValue'],
  methods: {
    changeValue (e:any) {
      this.$emit('update:modelValue', e.target.value)
    }
  },
  render () {
    return <div>
      <input type={'text'} value={this.modelValue} onInput={(e:any) => { this.changeValue(e) }}/>
    </div>
  }
})
</script>
<style  scoped lang='scss'>

</style>
