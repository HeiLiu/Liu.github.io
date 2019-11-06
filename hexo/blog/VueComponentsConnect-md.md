---
title: Vue组件通信
date: 2018-07-15 09:47:21
tags: 'Vue'
categories: 
  - 前端
  - Vue
---
 

# 组件  
   > (Component) 是 Vue.js最强大的功能之一。组件可以扩展，封装可重用的代码。在较高层面上，组件是自定义元素，Vue.js的编译器为它添加特殊功能。在有些情况下，组件也可以是原生 HTML 元素的形式，以 is 特性扩展。

# 通信类型  
## 父组件与子组件通信  

- 父组件给子组件传递数据  
    
    `props`: 使用props，父组件可以使用props向子组件传递数据  
      
```js
        // 父组件 
        <template>
            <child :msg="message"></child>
        </template>
         
        <script>
    
        import child from './child.vue';
         
        export default {
            components: {
                child
            },
            data () {
                return {
                    message: 'father message';
                }
            }
        }
        </script>
```

```js
// 子组件
  <template>
      <div>{{msg}}</div>
  </template>
    
  <script>
  export default {
  // props 另一种写法, 不声明类型与默认值
  // props: ['msg']
      props: {
          msg: {
              type: String,
              required: true
          }
      }
  }
  </script>
```  

- 子组件向父组件通信  

> 在Vue 中子组件一般不具有操作数据和处理事件的权利，所有的数据和事件的处理都要交给父组件进行操作  

**方法一 :** 在子组件中通过$emit()将组件内部的时间传递给父组件的事件进行   

```js  
// 父组件
<template>
<child @msgFunc="func"></child>
</template>

<script>

import child from './child.vue';

export default {
components: {
    child
},
methods: {
    func (msg) {
        console.log(msg);
    }
}
}
</script>

// 子组件  
<template>
<button @click="handleClick">点我</button>
</template>

<script>
export default {
props: {
    msg: {
        type: String,
        required: true
    }
},
methods () {
    handleClick () {
        // 提交出去的处理方法的名称与父组件接收的需一致
        this.$emit('msgFunc');
    }
}
}
</script>  
```  

**方法二:** 通过修改父组件传递的props来修改父组件数据  
> 这种方法只能在父组件传递一个引用变量时可以使用，字面变量无法达到相应效果。因为饮用变量最终无论是父组件中的数据还是子组件得到的props中的数据都是指向同一块内存地址，所以修改了子组件中props的数据即修改了父组件的数据。

> 但是并不推荐这么做，并不建议直接修改props的值，如果数据是用于显示修改的，在实际开发中我经常会将其放入data中，在需要回传给父组件的时候再用事件回传数据。这样做保持了组件独立以及解耦，不会因为使用同一份数据而导致数据流异常混乱，只通过特定的接口传递数据来达到修改数据的目的，而内部数据状态由专门的data负责管理  

---  

## 兄弟组件进行通信  

> 刚开始学习使用Vue时, 在Vue项目中的两个兄弟组件之间如果要进行通信， 通常会通过一个父组件进行数据请求再给子组件传递数据。    


- Vuex 是官方推荐的状态管理方案, 不过如果只是中小型项目，状态管理也没有很复杂的话，使用 Vuex 有种杀鸡用牛刀的感觉    

- Vue 官方推荐使用一个 Vue 实例作为中央事件总线, 即 `EventBus`  ,在需要使用的地方import该Bus   

  > EventBus 解决了兄弟组件之间的事件传递问题，它的本质是订阅发布者模式，同一个事件发布组件发布了，订阅组件就能获得事件的改变摆脱了兄弟组件之间传值需要父组件转达，Vue事件实例，作为中间者不在页面上显示且具有vue的API 如 emit on   

```js  
    // bus.js => new 一个 Vue 实例
    import Vue from 'vue'
    export default new Vue()  

    // clickComponent.vue 相当于发布者, 在需要的组件中订阅就能进行通信
    <template>
      <div>
        <a href="#"class="click" :data-index="index" @click.prevent="doClick($event)">点我</a>
      </div>
    </template>

    <script>
    import Bus from '@/common/bus.js'
    export default {
      props: {
        index: Number
      },
      methods: {
        doClick (event) {
           // console.log(event.target.dataset.index)
           Bus.$emit('getTarget', event.target.dataset.index)
          //  this.$emit('global: getTarget', event.target.dataset.index)
        }
      }
    }
    </script>

    // showComponents.vue 另一个兄弟组件 进行订阅

    <template>
      <div>
        {{html}}
      </div>
    </template>

    <script>
    import Bus from '@/common/bus.js'
    export default {
      data () {
        return {
          html: '还没有点击'
        }
      },
      created () {
         Bus.$on('getTarget', index => {
           this.html = `第${index}个元素`
         })
        //this.$on('global: getTarget', index => {
       //   this.html = `第${index}个元素`
       // })
      }
    }
    </script>
```  
  在node中有一个 `vue-event-proxy` npm包能够实现与EventBus同样的功能，需要安装该npm包, 并且在main.js中进行`引入 `  


```js
  import EventProxy from 'vue-event-proxy'
  Vue.use(EventProxy)   // 激活使用
  // 完成后即可以使用上面组件中js注释部分的代码代替Bus代码
```







