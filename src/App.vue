<script>
import { onBeforeMount, onErrorCaptured, onMounted, ref } from 'vue'
export default {
  data(){
    console.log('data函数')
    return{
      count:1,//2.0定义数据
    }
  },
  methods:{
    addCount(){
      this.count++ 
    },
  },
  setup(){
    console.log('setup函数开始执行')
    //这种直接定义的不具有响应式性质，方法中更新数据视图也不会更新 需要ref()去定义响应式变量
    let num = ref(2);  
    // 在setup中定义的函数无法直接通过变量名对其处理，其拿到的是一个对象，需要.value获取或设置其值
    const addNumber = ()=>{   
      num.value+=3 //无效操作
    }
    onBeforeMount(()=>{
      console.log('dom挂载前onBeforeMount')
      console.log(num.value)
      
    })
    onMounted(()=>{
      console.log('dom已成功挂载')
    })
    onErrorCaptured((err,vm,info)=>{
      console.log(err,vm,info)
    })
    return {
      num,
      addNumber
    }

  },
  beforeMount(){
    console.log('dom挂载到页面之前beforeMount')
  },
  mounted(){
    console.log('dom挂载到页面完毕mounted')
  } ,

}
</script>

<template>
  <span>count：{{count}}</span>  
  <button @click="count++">count++</button>
  <br>
  <span>num：{{num}}</span>  
  <button @click="addNum">num+2</button>
  <button @click="addNumber">num+3</button>
</template>

<style lang="scss">
#app{
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: $u-type-primary;
  background: $u-type-warning;
  margin-top: 60px;
}
</style>
