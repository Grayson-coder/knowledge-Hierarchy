# Vue响应式原理



## 什么是响应式原理？

- 我们都知道，只要在 Vue 实例中声明过的数据，那么这个数据就是响应式的。

- **意思就是在改变数据的时候，视图会跟着更新**。这意味着你只需要进行数据的管理





- 我们可以问出下面三个问题

    1. Vue 是怎么知道数据改变？

    2. Vue 在数据改变时，怎么知道通知哪些视图更新？

    3. Vue 在数据改变时，视图怎么知道什么时候更新？





- 当一个Vue实例创建时，vue会遍历data选项的属性，用 **Object.defineProperty** 将它们转为 getter/setter并且在内部追踪相关依赖，在属性被访问和修改时通知变化。

- 每个组件实例都有相应的 watcher 程序实例，它会在组件渲染的过程中把属性记录为依赖，之后当依赖项的 setter 被调用时，会通知 watcher 重新计算，从而致使它关联的组件得以更新。









































## Object.defineProperty()

- `Object.defineProperty()`：**定义对象新属性或修改原有的属性值**，并返回此对象

- ```js
    Object.defineProperty(obj, prop, descriptor)
    ```
    - **obj**：目标对象  

    - **prop**：要定义或修改的属性的名称

    - **descriptor**：要定义或修改的**属性描述符**。以对象形式书写

    

- **descriptor**可填配置选项

    - `enumerable:`：如果为false，则该对象的属性不允许遍历，**默认值是false**
    - `configurable`:：**目标属性是否可以被删除或是否可以再次修改特性** true | false  **默认值为false**
    - `value`：设置属性的值 
    - `writable`：属性值是否可以重写。true | false  **默认为false**

    - `get`：
        - `get`函数。当**访问目标属性**时，会调用此函数。该函数的返回值会被用作属性的值。

    - `set`：
        - `set`函数，当**目标属性值被修改**时，会调用此函数。该方法接受一个参数（也就是被赋予的新值)

    - ***set函数会被get函数先被调用***



- ```js
    let obj = {};
    let bValue
    Object.defineProperty(obj, "b", {
        get() {  // 访问b属性时触发，return后的值将作为b属性的值
            console.log('监听正在获取b')
            return bValue
        },
        set(newValue) { // 当b属性值被修改时触发，接收的参数为修改后的值
            console.log('监听正在设置b')
            bValue = newValue
        },
    });
    
    obj.b = 38;  // 触发set函数
    console.log(obj.b);  // 触发了get函数
    
    // 分别打印：监听正在设置b、监听正在获取b、38
    ```

    

- 通过`Object.defineProperty()`实现一个简易版的**Vue双向绑定**

    - ```js
        let input = document.querySelectorAll('input')[0]
        let span = document.querySelectorAll('span')[0]
        let obj = {}
        Object.defineProperty(obj, 'msg', {
            set(newValue) { // 当obj.msg发生改变时将会触发set函数
            		span.innerHTML = newValue
            },
        })
        
        input.addEventListener('input', function(event) {
            // 文本框改变时，改变obj.msg属性
            obj.msg = event.target.value
        })
        ```

        



- Vue通过设定对象属性的 setter/getter 方法来监听数据的变化，通过getter进行依赖收集，而每个setter方法就是一个观察者，在数据变更的时候通知订阅者更新视图。





## 观察者模式

- 什么是观察者模式？它分为**注册环节跟发布环节**。

​        比如我去买芝士蛋糕，但是店家还没有做出来。我就需要隔一段时间来回来问问蛋糕做好没，对于我来说是很麻烦的事情。

​		店家肯定想要做生意，不想流失我这个吃货客户。于是，在蛋糕没有做好的这段时间，有客户来，他们就让客户把自己的电话留下，这就是观察者模式中的**注册环节**。然后蛋糕做好之后，一次性通知所有记录了的客户，这就是观察者的**发布环节**。



- 这里来简单实现一个**观察者模式**的构造函数

    - ```js
        class Observer {
            constructor() {
                this.dep = []
            }
            
            // 订阅环节
            register(fn) {
                this.dep.push(fn)
            }
            
            // 发布环节
            notify() {
                this.dep.forEach(item => item())
            }
        }
        
        const wantCake = new Observer()
        // 订阅者模式
        wantCake.register(() => console.log('call 张三'))
        wantCake.register(() => console.log('call 李四'))
        wantCake.register(() => console.log('call 王五'))
        
        // 蛋糕最好之后，发布者模式
        wantCake.notify()
        ```

        







## 定义属性和观察者模式的结合

- 我们了解了Object.defineProperty和发布订阅者模式后，我们不难可以想到，vue.js是基于以上两者来实现数据监听的。



1. vue.js首先通过`Object.defineProperty`来对要监听的数据进行`get`和`set`劫持，当数据的属性被赋值/取值的时候，vue.js就可以察觉到并做相应的处理。

    

2. 通过观察者模式，我们可以为对象的每个属性都创建一个发布者，当有其他订阅者依赖于这个属性的时候，则将订阅者加入到发布者的队列中。利用Object.defineProperty的数据劫持，在属性的setter调用的时候，该属性的发布者通知所有订阅者更新内容。









# Vue数据代理原理



```js
class Vue {
    constructor(opation) {
        this.$data = opation.data
        Object.keys(this.$data).forEach(items => {
            this._proxy(items)
        })
    }

    _proxy(key) {
        Object.defineProperty(this, key, {
            get() {
                return this.$data[key]
            }
        })
    }
}
let vm = new Vue({
    data: {
        name: '张三',
        age: '18',
        sex: '男'
    }
})
// vm.name 张三 ...
```





































































































































































































































































































































































































































































