<script>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
// import HelloWorld from './components/HelloWorld.vue'
export default {
  data(){
    return{
      
    }
  },
  beforeCreate(){
    console.log('实例化之前')
    setTimeout(()=>{
      console.log('实例化之前s3')
    },200)
  },
  created(){
    console.log('实例化之后挂载前')
    setTimeout(()=>{
      console.log('实例化之前s1')
    },0)
  },
  beforeMount(){
    console.log('dom挂载到页面之前')
  },
  mounted(){
    console.log('dom挂载到页面完毕')
     setTimeout(()=>{
      console.log('实例化之前s2')
    },100)
  } ,
  beforeUpdate(){
    console.log('更新之前')
  },
  updated(){
    console.log('更新之后')
  },
  beforeUnmount(){
    console.log('组件卸载前')
  },
  unmounted(){
    console.log('组件卸载之后')
  }
}
</script>

<template>
  <img alt="Vue logo" src="./assets/logo.png" />
  <HelloWorld msg="Hello Vue 3 + Vite" />
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
