
<script lang="tsx">
import { defineComponent, reactive, ref, onMounted, provide, readonly, watchEffect, nextTick, h, resolveComponent, PropType } from 'vue'
import Child from './Child.vue'
import A from './A.vue'
import Test1 from './Test1.vue'
import SetupCom from './SetupCom.vue'
import RenderRef from './RenderRef.vue'
import SlotCom from './SlotCom.vue'
interface GoodObj{
  name:string,
  good:(data:string)=>void
}

interface Book {
  title: string
  year?: number
}

export default defineComponent({
  name: 'HelloWorld',
  methods: {
    hello ():string {
      return '返回字符串'
    }
  },
  components: {
    Child
  },
  directives: {
    cSelect (el, binding, vnode) {
      el.style.color = binding.value
    }
  },
  props: {
    nameFun: {
      type: Function as PropType<(name:string)=>void>,
      default () {
        return (name:string) => { console.log(name) }
      }
    },
    goodObj: {
      type: Object as PropType<Book>,
      default: () => ({
        title: '222'
      })
    }
  },
  setup (prop, { expose }) {
    const modelShow = ref(false)
    const test1Value = ref('1')
    const test2Value = ref('2')
    const childProps = reactive({ foo: 123 })
    const childRef = ref<any>(null)
    const childObj = ref({ count: 123 })
    const stepValue = () => {
      childObj.value.count++
    }
    onMounted(() => {
      console.log('mounted')
      console.log('d', childRef.value) // => <div>This is a root element</div> 在setup中拿不到dom实例，因为dom在setup中，写在模版template中可以出来
    })
    // provide  -> readonly防止儿子直接更改 响应式状态
    provide('childValue', readonly(childObj))
    provide('stepValue', stepValue)

    const FunComSpecial = () => {
      return <div class="red">
          我是func组件
      </div>
    }

    expose({
      childRef
    })
    return () => {
      return (
        <>
          <div>
            <child onGoClick={(e:any) => { console.log(e) }} ref={childRef} childProps={childProps} vCSelect={'orange'}>
              {{
                good: (params:any) => {
                  return <h3>儿子插槽good{params.foo}</h3>
                }
              }}
            </child>
            <A/>
            <Test1 v-model={test1Value.value}/> ---- {test1Value.value}
            <SetupCom setupProps={'单文件组件的props'} v-model={test2Value.value}/> --- {test2Value.value}
            <RenderRef/>
            <FunComSpecial/>
            <SlotCom>
              {{
                header: () => {
                  return <h3> others slots</h3>
                }
              }}
            </SlotCom>
          </div>
        </>
      )
    }
  }
})
</script>

<style lang="scss" scoped>
  .red{
    border:1px solid red
  }
  .yellow{
    color: yellow;
    border:yellow
  }
</style>
