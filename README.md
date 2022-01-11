## 安全签PC端 Vue 3 + Vite
> 简单组件建议使用vue2.0的形式去书写较好
### 目录分析
- public 该文件夹下放一些静态文件可以在index.html中直接引入
- src 开发的源码
    ```
        --assets  // 静态文件目录：包含字体、图标、图片、样式等静态资源
        --common
        --layouts  // 存放整个项目的布局我呢见
        --middlewares // 中间件 可以防止关于路由跳转的判断文件
        --modules // 应用的业务逻辑部分 & Vuex 数据
        --router //Router 文件夹放置你的路由文件
        --services // https://tuaran.github.io/views/2021/vueclassapi.html#%E5%89%8D%E8%A8%80Services 该文件夹是放请求库和 API 的地方，也包括对 localStorage 的管理等。
        --static 一般用不到
        --store //Store 文件夹放置你的 Vuex 相关文件。在这个目录下主要是一些全局的持久数据及方法：state 、 actions 、 mutations 、 getters，同时也和 modules 文件夹下的 Vuex 进行关联。
        --views //业务组件
    ```






### 动态指令

### 声明式渲染
### 命令式渲染

### watch
### computed

### 生命周期
    ```
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
    ```

### 组合api
> 在vue2.0中，在template中用到一个字段show控制，此时需要在data中定义该字段，
然后在methods中定义控制该字段更改的方法，类似的字段多了或导致整段代码比较凌乱，
不利于开发人员的阅读以及维护，而组合式api就解决了这个问题。
#### setup
##### 注意
    - setup中避免使用this，因为setup是在实例创建之前执行的，此时的data，computed以及
    methods都还未被解析。
    - setup函数接收两个参数props和context。
    - setup函数返回的内容可用于组件中以及计算属性，方法，生命周期等钩子函数中均可用。
##### 定义响应式变量
    - 通过ref()可创建一个响应式变量。ref接收一个参数作为value属性值然后返回一个对象，可使用.value获取或更改该变量值，目的就 是保持不同类型值的行为统一
    ```javascript
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
    ```
##### 在setup内注册生命周期

    > 首先我们观察生命周期函数以及setup函数的打印顺序可知，setup在数据初始化之前就已经执行，所以这里可以认为只要在beforeCreate和created需要进行的逻辑都可以迁移至setup函数中。

    ```html
        [vite] connecting...
        App.vue:16 setup函数开始执行
        App.vue:31 实例化之前beforeCreate
        App.vue:5 data函数
        App.vue:34 实例化之后挂载前created
        App.vue:37 dom挂载到页面之前beforeMount
        App.vue:40 dom挂载到页面完毕mounted
    ```
    > 在setup函数注册生命周期 只需要在原先的生命周期钩子函数前加上on即可访问（调用）。如果在setup访问了同一个生命周期函数那么该生命周期钩子函数执行两次，且setup函数中访问的先执行。
    ```javascript
          setup(){
            console.log('setup函数开始执行')
            //这种直接定义的不具有响应式性质，方法中更新数据视图也不会更新 需要ref()去定义响应式变量
            let num = ref(2);  
            // 在setup中定义的函数无法直接通过变量名对其处理，其拿到的是一个对象，需要.value获取或设置其值
            const addNumber = ()=>{   
            console.log(num.value)
            num.value+=3 //无效操作
            }
            onBeforeMount(()=>{
            console.log('dom挂载前onBeforeMount')
            })
            onMounted(()=>{
            console.log('dom已成功挂载')
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
    // 执行结果如下
        [vite] connecting...
        App.vue:16 setup函数开始执行
        App.vue:5 data函数
        App.vue:25 dom挂载前onBeforeMount
        App.vue:37 dom挂载到页面之前beforeMount
        App.vue:28 dom已成功挂载
        App.vue:40 dom挂载到页面完毕mounted
    ```
    > 新增的生命周期有
    