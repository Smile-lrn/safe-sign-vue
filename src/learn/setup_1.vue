<script>
import { ref } from 'vue'
export default {
  data(){
    return{
      count:1,//2.0定义数据
    }
  },
  methods:{
    addCount(){
      this.count++ 
    },
    addNum(){
      console.log(this.num) //methods中支持修改setup中的数据
      this.num+=2 
    },
  },
  // 3.0
  setup(){
    // let num = 2; 
    //这种直接定义的不具有响应式性质，方法中更新数据视图也不会更新 需要ref()去定义响应式变量
    let num = ref(2);  
    // const addNumber = ()=>{   
    //   console.log(num)
    //   num+=3 //无效操作
    // }
    // 在setup中定义的函数无法直接通过变量名对其处理，其拿到的是一个对象，需要.value获取或设置其值
    const addNumber = ()=>{   
      console.log(num.value)
      num.value+=3 //无效操作
    }
    return{
      num,
      addNumber
    }
  },
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

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
