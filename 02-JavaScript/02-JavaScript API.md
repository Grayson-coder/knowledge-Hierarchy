#  一、DOM

## 一、DOM简介

### 1.1 什么是DOM？

- 文档对象模型（***Document Object Model，简称 DOM***）

  - W3C 已经定义了一系列的 DOM 接口，通过这些 DOM 接口可以改变网页的内容、结构和样式 
  
      

### 1.2 DOM树

<img src="./images/javaScript.assets/image-20200528145536082.png" alt="image-20200528145536082" style="zoom: 67%;" />

- 文档：一个页面就是一个文档，DOM 中使用 document 表示 

- 元素：页面中的所有标签都是元素，DOM 中使用 element 表示 

- 节点：网页中的所有内容都是节点（标签、属性、文本、注释等），DOM 中使用 node 表示 节点

- **DOM 把以上内容都看做是对象 **

  


## 二、获取元素对象

### 2.1 根据 id 获取

- `getElementById('id') `

  - 可以返回一个匹配到 ID 的 DOM 元素对象，如果没有匹配的， 则返回null

      

- 语法格式如下

  ```js
  var element = document.getElementById('id')
  ```
  
  

### 2.2 根据 标签名 获取

- `getElementsByTagName() `

  - 可以返回**所有匹配到** 标签名的 DOM 元素对象 

  - 返回的是一个**伪数组**，所以需要进行遍历 

- 语法格式如下

  ```js
  document.getElementsByTagName('标签名')
  ```

  

- 还可以获取**父元素内部所有指定标签名的子元素对象**
  - ```js
      element.getElementsByTagName('标签名'); 
      ```
  
      

 


### 2.3 根据 类名 获取

-  `document.getElementsByClassName('类名')`

   - 返回一个或多个匹配到 的类名 DOM元素

   - 返回的是一个伪数组，需要进行遍历
   
       

### 2.4 根据 选择器 获取（重点）

- `document.querySelector('CSS选择器')`

  - 根据匹配到的 选择器 ***返回第一个元素对象*** 

      

- `document.querySelectorAll('CSS选择器')`

  - 根据匹配到的 选择器 ***返回 多个匹配到的对象***

  - **返回的是一个伪数组**

      

- 注意:querySelector 和 querySelectorAll里面的选择器需要加符号

  ```js
  document.querySelector('#nav>li'); 
  ```



### 2.5 细节补充

- 使用 ***console.dir()*** 可以打印获取的元素对象，更好的***查看对象里面的属性和方法***

- 获取 body 和 html 元素 可以使用简写

  ```js
  doucumnet.body  // 返回body元素对象 
  document.documentElement  // 返回html元素对象 
  ```

  

## 三、事件

### 3.1 事件概述

- 事件可以理解为***响应机制***

- 网页中的***每个元素都可以触发 JavaScript 的事件***

- 事件三要素

  1. 事件源 （哪个元素触发了事件） 

  2. 事件类型 （触发了什么事件） 

  3. 事件处理程序 （触发事件后，做了什么）

       

### 3.2 执行事件的三步骤

- ① 获取事件源

  ```js
  var div = document.querySelector('#one')
  ```

- ② 注册事件（绑定事件）

- ③ 添加事件处理程序（***采取注册事件监听方式***）  ，当事件被触发时  其对应的函数就会被调用

  ```js
  div.addEventListener('click', function() {
      alert(1)
  })
  ```

  


### 3.3 注册（绑定）事件

- 方式一：

  ```js
  domElement.onclick = function() {
  	alert(1)
  }
  ```

  - 这是传统的注册方式，现在***已经很少用了***

  - ***同一个元素同一个事件只能设置一个处理函数***，最后注册的处理函数将会覆盖前面注册的处理函数 

    

- 方式二：通过事件监听方法

  ```js
  domElement.addEventListener('click', function() {  // addEventListener(添加事件监听)
  	alert(1)
  })
  ```

  - ***W3C 标准推荐方式***

  - ***同一个元素同一个事件可以注册多个监听器***，按注册顺序依次执行 处理函数

    

- `domElement.addEventListener(type, listener[, useCapture])`

  - type：***事件类型字符串***，比如 click 、mouseover ，注意这里不要带 on 

  - listener：***事件处理函数***，事件发生时，会调用该监听函数 

  - useCapture：可选参数，是一个布尔值，默认是 false。***false：冒泡阶段      true：捕获阶段***

    

>注：给整个**页面添加事件**：` document.addEventListener('事件名', fn)`
>



### 3.4 删除(解绑)事件

- 解绑**传统注册**的事件(通过on赋值函数绑定的事件)

  - ```js
    domElement.onclick = null
    ```

- 解绑**监听方式**注册的事件

  - ```js
    domElement.addEventListener('click', foo)
    
    function foo() {
        alert(1)
        domElement.removeEventListener('click', foo) // 移除事件以及要回调的函数
    }
    ```

    

>注：如果真的需要**解绑事件**，那么**建议通过传统方式注册事件**，因为监听方式解绑必须传入函数
>



### 3.5 事件流

```js
<div>
　　<p>元素</p>
</div>
```

- 思考:如果上图两个元素都绑定了鼠标点击事件，那么优先执行谁呢？

- ***事件流***描述的是***从页面中接收事件的顺序*** 

- DOM 事件流分为3个阶段：  
  1. 捕获阶段 

  2. 当前阶段
  
  3. **冒泡阶段 (最主要的)**

<img src="./images/javaScript.assets/image-20200531175854448.png" alt="image-20200531175854448" style="zoom: 67%;" />



  

- ***冒泡阶段指的是事件的向上传导***，当**后代元素**上的事件被触发后，**祖先元素**上的**相同事件**再被触发

- ***捕获阶段指的是事件的向下传导***，当后代元素上的事件被触发后，**优先**触发祖先元素上的**相同事件**

- 注：

  - ***onclick 只能得到冒泡阶段***

  - addEventListener()第三个参数如果是 true，表示在事件捕获阶段调用事件处理程序；如果是 false（***默认false***），表示在事件冒泡阶段调用事件处理 程序

  - **有些事件是没有冒泡的，比如 onblur、onfocus、onmouseenter、onmouseleave**

    

- 思考：如果后代元素和祖先元素的事件不一致，那么优先执行谁？

  ```js
  li.addEventListener('click', function(e) {
  	console.log('我是li')
  	e.stopPropagation()  // 因为事件后代元素和祖先元素的事件不一样，所以不会产生冒泡
  })
  
  ul.addEventListener('mousedown', function() {
  	console.log('我是ul') // 优先执行
  })
  ```

  - **优先执行祖先元素上的事件**，如果后代元素和祖先元素的事件**不一致**，**那么不会产生冒泡**，此时后代元素阻止事件冒泡**不影响**祖先元素上所触发的事件

    
    
    

- 补充：冒泡机制里，一个元素下面的***所有后代元素都会触发祖先元素的事件***

  - ```js
    ul.addEventListener('click', function() {
    		console.log('我是ul')  // 点击ul下的后代元素 都会触发ul这个祖先元素的事件
    })
    ```

    

- 如何**阻止事件冒泡**？

  - **利用事件对象里面的 stopPropagation()方法** 

    
    
    

### 3.6 事件委托

- 事件委托也称为事件代理
- 事件委托的原理：
  - ***将监听的事件绑定给祖先元素***，***利用事件冒泡机制***，***每个后代元素都会触发祖先元素的事件***

- 好处：减少事件绑定的次数，提高程序性能



### 3.7 事件对象

#### 0. 事件对象的概述

- 事件对象：***存储了触发事件时一系列相关的数据***，比如鼠标移动的坐标，***事件对象有很多属性和方法***	

- 事件对象只存在事件监听的**回调函数**中

- 每个监听事件的回调函数里面都有一个形参，该形参就是事件对象，是系统自动创建的，里面有内置的属性和方法

  - ```js
    div.addEventListener('click', function(e) { // 这个e就是事件对象
    	console.log(e);
    })
    ```

  


####  1. 常见的属性和方法

- <img src="./images/javaScript.assets/image-20200601102305026.png" alt="image-20200601102305026" style="zoom: 67%;" />

  

#### 2. e.target和this指向的对象不同

- ```js
  ul.addEventListener('click', function(e) {
      console.log(this);  // this永远指向注册事件的元素
      console.log(e.target);   // e.target指向的触发事件的元素（后代元素或者是自身元素）
  })
  ```



#### 3. 事件对象的鼠标相关属性

- <img src="./images/javaScript.assets/image-20200601120654835.png" alt="image-20200601120654835" style="zoom:67%;" />

  

  - 注意：鼠标事件对象的属性**返回的都是不带单位(px)的值**

    

- 案例：跟随鼠标移动的天使图

  - ```js
    var img = document.querySelector('img')
    document.addEventListener('mousemove', function(e) {
        var x = e.clientX
        var y = e.clientY
    
        img.style.left = x - 50 + 'px'
        img.style.top = y - 40 + 'px'
    })
    ```

    

#### 4. 事件对象的键盘相关属性

<img src="./images/javaScript.assets/image-20200601132157953.png" alt="image-20200601132157953" style="zoom:67%;" />



- 通过键盘上的ASCII值，我们可以判断按下了哪个键

- 案例：按下s键之后，自动聚焦到表单

  - ```js
    document.addEventListener('keyup', function(e) {
        if(e.keyCode === 83) {
        	input.focus()
        }
    })
    ```



### 3.8 常见的事件名

- 鼠标事件

  <img src="./images/javaScript.assets/image-20200528153540083.png" alt="image-20200528153540083" style="zoom: 67%;" />

  

- mouseenter 和mouseover的区别 

  - 当***鼠标移动到元素上时就会触发*** **mouseenter** 和 **mouseover** 事件 

  - ***mouseover事件具有冒泡机制***：给父元素绑定的mouseover事件会**传递到后代元素**上

  - ***mouseenter事件没有冒泡机制***：只对绑定mouseenter事件的元素有效果

    

- mouseleave 和mouseout的区别 

  - 不论鼠标指针离开**被选元素**还是**任何子元素**，都会触发 **mouseout** 事件。

  - 只有在鼠标指针离开被选元素时，才会触发 **mouseleave 事件**

    

- 键盘事件
  
  - <img src="./images/javaScript.assets/image-20200601132029892.png" alt="image-20200601132029892" style="zoom:67%;" />
  
      
  
    - **keyup事件使用的最多**
  
    - onkeypress 和前面2个的区别是，它不识别功能键，比如左右箭头，shift 等
  
  
  
- 案例：快递单号物流案例

  - ```js
        var input = document.querySelector('input')
        var p = document.querySelector('p')
      
        input.addEventListener('keyup', function() {
            if (this.value.length > 0) {
                p.style.display = 'block'
                p.innerHTML = this.value
                p.style.fontSize = '20px'
            } else {
                p.style.display = 'none'
            }
        })
      
        input.addEventListener('blur', function() {
            p.style.display = 'none'
        })
    ```

    

### 3.9 自动触发事件

- ```js
  let span = document.querySelector('span')
  span.addEventListener('click', () => {
    console.log(123);
  })

  setInterval(() => {
    span.click() 
  }, 1000);
  ```
  
- **click** 方法可以用来模拟鼠标左键单击一个元素，***不需要用户手动去点击按钮，而是自动触发事件对应的回调函数***，如果希望多***次触发，则需要配合定时器来完成***







## 四、操作元素

### 4.1 操作元素的内容

- element.innerText （***获取元素的文本内容***）

  - 无法解析HTML标签，非标准

      

- 获取元素内容
  
    - `element.innerHTML `
- 设置元素内容
  
    - `element.innerHTML  = '要设置的内容'`

  

### 4.2 操作元素的属性

- **获取**元素的属性值
    - `element.getAttribute('元素的属性名')`

    

- **修改**元素的属性值

    - `element.setAttribute('属性名', '属性值')`

        

- **删除**元素的属性
  
    - `element.removeAttribute('属性名')`



- 操作元素的src属性

    - `ele.src = xxx`（可读写）

    - 以上方法可以直接修改图片src属性为**本地图片路径**

>坑：通过**js修改src属性时**，**相对路径要相对js所在的html页面**，否则图片无法加载成功
>



### 4.3 操作表单元素的属性

- 表单元素对象中有以下属性

  - type、value、checked、selected、disabled

    ```js
    var input = document.querySelector('input')
    input.type = 'password'
    input.disabled = false
    ```

  - 以上***属性都是可读写的***

      

- 京东显示隐藏密码案例

  ```js
  a.onclick = function() {
  
      if (flag === true) {
          img.src = './img/open.png'
          input.type = 'text'
          flag = !flag // 每次点击之后flag都需要进行取反，以便于下次执行不同的流程
      } else {
          img.src = './img/close.png'
          input.type = 'password'
          flag = !flag
      }
  }
  ```

  

### 4.4 操作元素的样式

#### 4.4.1 css

- 我们**可以通过 JS 修改元素的大小、颜色、位置等样式**

- `element.style.css样式名`   

  - ```js
      div.style.backgroundColor = 'pink'
      ```

  - 注意： 

    - ***JS 里面的样式名采取驼峰命名法*** 比如 fontSize、 backgroundColor 

    - JS 修改 style 样式操作，**产生的是行内样式**，权重比较高，如果CSS样式有!improtant ，那么js修改的样式不起效果

    - 如果不想产生行内样式，那么可以设置为空`ele.style.xxx = ''`
    
      

#### 4.4.2 className

- **`element.className`   类名样式操作**

  - ```js
      div.className = 'one'
      ```

  - 如果样式修改较多，***可以采取给元素添加类名来更改元素样式***（**在style标签中提前定义好类的样式**）

  - ***className 会直接更改元素的类名，会覆盖原先的类名***，如果不想覆盖原先的类名，可以追加一个空格隔开多个类

  - ```js
    div.className += ' ' + 'one'
    ```

    
    
    

#### 4.4.3 classList

- **`element.classList `  类名样式操作**

  - 该属性会***返回一个元素的所有类名，以伪数组的形式存储***

  - **添加**类名

    - ```js
        element.classList.add（’类名’）； 
        ```

    - 该方法不会覆盖掉先前的类名，而是在末尾追加一个类名

  - **删除**指定的类名

    - ```js
      element.classList.remove（’类名’）; 
      ```

  - **切换**类名

      - ```
        element.classList.toggle（’类名’）
        ```

      - 例子：通过点击事件不断的切换类名
  



### 4.5 操作元素总结

<img src="./images/javaScript.assets/image-20200529124458548.png" alt="image-20200529124458548" style="zoom: 50%;" />



## 五、节点操作

### 5.1 节点的概述

- 什么是节点？

  - ***网页中的所有内容都可以看成是节点（标签、属性、文本、注释等）***，在DOM 中，节点使用 node 来表示

  - 节点分为三类：***元素节点、属性节点、文本节点***

  - **DOM元素对象也可以看做是一个节点**

    

- 节点有什么作用？

  - 节点可以帮助我们通过父子、兄弟关系来**获取DOM元素对象**

  - 节点操作可以对元素进行**增删改查**

      

  


### 5.2 获取父节点和子节点

- `node.parentNode  ` 

  - ***parentNode 属性可返回某节点的父节点*** 

  - 如果指定的节点没有父节点则返回 null 

    

- `parentNode.children`

  - 返回所有的***子元素节点***。它***只返回子元素节点，其余节点不返回*** 

      

- `parentNode.firstElementChild` ，  `parentNode.lastElementChild `

  - 返回 ***第一个或者最后一个 子元素节点***，找不到则返回null

    

### 5.3 获取兄弟节点

- `node.nextElementSibling`

  - ***返回当前元素下一个兄弟元素节点***，找不到则返回null

      

- `node.previousElementSibling`     

  - ***返回当前元素上一个兄弟元素节点***，找不到则返回null

    

### 5.4 创建元素节点

- `document.createElement('tagName') `

  - 动态创建元素节点，但是不会再页面中展示 ，**需要添加到特定节点里面，创建的节点才会生效**

  - ```js
    // 创建了一个li元素节点，但是在页面中不会生效
    var li = document.createElement('li') 
    ```

    

### 5.5 添加元素节点

- `node.appendChild(childNode)` 

  - ***将一个节点添加到指定父节点的列表末尾***。

  - ```js
    var ul = document.querySelector('ul')
    var li = document.createElement('li')
    ul.appendChild(li) // 将创建的元素节点添加到指定的节点里面
    ```
    
    

- `node.insertBefore(childNode, 指定节点)`

  - ***将一个节点添加到父节点的指定子节点前面***。

  - ```js
    var li = document.createElement('li')
    var ul = document.querySelector('ul')
    ul.insertBefore(li, ul.children[0])  // 将创建的节点插入到指定的节点前面
    ```

    

-  `node.insertAdjacentHTML(追加的位置,‘要追加的字符串元素’)  ` 

  - ```js
    ul.insertAdjacentHTML('beforeend', '<li>测试后1231</li>');
    ```
    
    



### 5.6 删除元素节点

- `node.removeChild(childNode) `

  - 从 DOM 中***删除一个指定的子节点***，返回删除的节点

  - ```js
    var ul = document.querySelector('ul')
    var li = ul.removeChild(ul.children[0]) // 删除ul节点下的第一个子元素节点
    ```

    

- `ChildNode.remove()`

  - **删除指定的节点**

  - ```js
    li.remove()  // 删除了一个li子元素节点
    ```

    



### 5.7 拷贝节点

- `node.cloneNode() `

  - 返回调用该方法的节点的一个副本。 **也称为克隆节点/拷贝节点** 

  - **如果括号参数为空或者为 false ，则是浅拷贝，即只克隆复制节点本身，不克隆里面的子节点**

  - ***如果括号参数为 true ，则是深度拷贝，会复制节点本身以及里面所有的子节点*** 

  - ```js
    var btn = document.querySelector('button') 
    var clone = btn.cloneNode(true) // 深拷贝节点，包括节点里面的所有子节点(文本节点)
    console.log(clone);
    ```

    
    
    

### 5.8 动态生成表格案例(重点)

<img src="./images/javaScript.assets/image-20200531113344747.png" alt="image-20200531113344747" style="zoom: 67%;" />

- ① 因为里面的学生数据都是动态的，我们需要js 动态生成。 ***数据我们采取对象形式存储***

  - ```js
    var datas = [
           {name: '魏璎珞',subject: 'JavaScript',score: 100}, 
           {name: '魏璎珞',subject: 'JavaScript',score: 100}, 
           {name: '魏璎珞',subject: 'JavaScript',score: 100}, 
           {name: '魏璎珞',subject: 'JavaScript',score: 100}, 
           {name: '魏璎珞',subject: 'JavaScript',score: 100}, 
       ]
    ```

    

- ②根据数组的长度，来创建tr

  - ```js
    var table = document.querySelector('table')
    
    for(var i = 0; i < datas.length; i++) { // 遍历数组
    	// 创建表格的行
    	var tr = document.createElement('tr')
    	table.appendChild(tr)
    }
    ```

    

- ③ 每个行里面又有很多单元格（对应里面的数据），循环遍历每个数组中的对象(双重for循环)

  - ```js
    for(var i = 0; i < datas.length; i++) {  // 遍历数组
        .....
        
        var msg = datas[i] // 获取数组中的对象
    
        for(var k in msg) {  // 遍历数组中的对象
            // 创建单元格
            var td = document.createElement('td')
            td.innerHTML = msg[k] // 给每个单元格赋值数据
            tr.appendChild(td)
        }
    }
    
    ```

    

- ⑤ 最后一列单元格是删除，需要单独创建单元格

  - ```js
    for(var i = 0; i < datas.length; i++) {  // 遍历数组
        .....
        var msg = datas[i] // 获取数组中的对象
        for(var k in msg) {  // 遍历数组中的对象
            .....
        }
        
        // 创建删除的单元格
        var td = document.createElement('td')
        td.innerHTML = '<a href="#">删除</a>'
        tr.appendChild(td)   
    }
    ```

    

- ⑥ 最后添加删除操作，单击删除，可以删除当前行

  - ```js
    for(var x = 0; x <  a.length; x++) { // 遍历每个a的点击事件
        a[x].onclick = function() {
            table.removeChild(this.parentNode.parentNode)
        }
    }
    ```

    

## 六、offset系列属性

### 6.1 offset概述

- offset(偏移量)， 使用 offset 系列**相关属性**可以动态的得到该**元素的位置、大小**等

- **偏移量**：***元素距离某个原点的位置，我们称之为''偏移量''***

  

### 6.2 offset系列属性

<img src="./images/javaScript.assets/image-20200602191358887.png" alt="image-20200602191358887" style="zoom:67%;" />

- `offsetParent`返回当前元素**最邻近**的且开启了**非static定位的祖先元素**，如果没有这样的祖先元素，参照对象是**body元素**

- `offsetTop、offsetLeft `的参照对象是`offsetParent`元素

- offsetWidth、offsetHeight 获取到的是元素的宽度和高度，**但是这些宽度和高度包括了 内边距 和边框**

- **注意：offset系列属性返回的数值都不带单位** 

  
  
  

### 6.3 offset 与 style 区别

- ![image-20200602192735011]( ./images/javaScript.assets/image-20200602192735011.png)

  
  
  

### 6.4 案例

#### 1. 鼠标在盒子内的坐标

```js
var div = document.querySelector('div')
div.addEventListener('mousemove', function(e) {
    var x = e.clientX
    var y = e.clientY
    
    x = x - div.offsetLeft
    y = y - div.offsetTop
    console.log(x,y);
})
```



#### 2. 拖动模态框

<img src="images/02-JavaScript API.assets/image-20210107162309420.png" alt="image-20210107162309420" style="zoom:50%;" />

1. 鼠标按下时，获取鼠标相对于拖拽元素的坐标点(起点坐标)

2. 鼠标移动时，获取鼠标相对于页面的坐标点 - 起点坐标 = 拖拽元素的偏移量

    >注：**鼠标移动、移出事件**，需要给`document`对象绑定
    >



```js
drag(login)
// 封装了一个使元素可以拖拽的函数,传入一个参数，该参数就是需要拖拽的元素对象
function drag(ele) {
    title.onmousedown = function (e) {
        // 当鼠标点下时，获取鼠标相对于盒子的坐标(起始坐标)
        var boxX = e.clientX - ele.offsetLeft;
        var boxY = e.clientY - ele.offsetTop;
        document.onmousemove = function (e) {
            // 当鼠标移动时，获取鼠标相对于页面的偏移量 - 起点坐标，就是拖拽元素的偏移量
            ele.style.left = e.clientX - boxX + 'px';
            ele.style.top = e.clientY - boxY + 'px';
        }
    };
    document.onmouseup = function () {
        //清除盒子的移动事件;
        document.onmousemove = null;
    };
};
```



#### 3. 放大镜效果

- 通过`jQuery之家`中的放大镜插件实现









## 七、scroll 系列 属性

### 7.1 scroll概述

- 使用 scroll 系列的相关属性可以得到该元素的大小、**滚动距离**等 

- <img src="./images/javaScript.assets/image-20200604113543119.png" alt="image-20200604113543119" style="zoom:50%;" /><img src="./images/javaScript.assets/image-20200604113618819.png" alt="image-20200604113618819" style="zoom:50%;" />

- 如果浏览器的高（或宽）度不足以显示整个页面时，会自动出现滚动条。当滚动条向下滚动时，页面**上面被隐藏 掉的高度**，我们就称为**页面被卷去的头部**

    

- 滚动条在滚动时会触发 **onscroll 事件**

    - scroll系列属性一般给**documen(页面)使用**

        

- 注意：***元素被卷去的头部是 `element.scrollTop`***  , ***如果是页面被卷去的头部 则是 `window.pageYOffset`*** 

- `window.scroll(x, y)  `

  - ***页面的滚动条滚动到指定的位置***

  - 注意，里面的x和y 不跟单位，如果都为0则表示回到顶部

    

### 7.2 案例

- 仿考拉海购固定右侧边栏

  - ```Js
    ① 需要用到页面滚动事件 scroll  因为是页面滚动，所以事件源是 document 
    ② 滚动到某个位置，就是判断页面被卷去的上部值。 
    ③ 页面被卷去的头部：可以通过window.pageYOffset 获得  如果是被卷去的左侧 window.pageXOffset 
    	 
    var rightSide = document.querySelector('.right-side')
    
    // 给页面绑定一个滚动事件，必须是给页面绑定
    document.addEventListener('scroll', function() {
    	// 判断页面滚动的位置，然后固定定位
    	if (window.pageYOffset >= 400) {
    		rightSide.style.position = 'fixed'
    		rightSide.style.top = '100px'
    	} else {
    		rightSide.style.position = 'absolute'
    		rightSide.style.top = '500px'
    	}
    })
    ```
    
    

- 平滑的回到页面顶部

  - ```js
    // 封装了一个动画的回到页面顶部的函数
    function backTop() {
        var timer
        timer = setInterval(() => {
            if (window.pageYOffset === 0) {
            	clearInterval(timer) // 如果页面滚动条的Y坐标为0，就停止定时器
            } else {
                // 每执行一次定时器，页面的滚动条位置就会变化
                var step = window.pageYOffset - 50
                window.scroll(0, step)
        	}
        }, 15);
    }
    ```

    

###7.3 三大系列总结

- ***offset系列 经常用于获得元素位置***    offsetLeft  offsetTop 
  
  - 参照对象是最邻近**的且**开启**了定位的祖先元素**，如果没有则参照对象是**body元素**
  
  ​    
  
- ***client 经常用于获取元素大小***  clientWidth  clientHeight 
  
  - 返回一个**不包括边框的元素大小**，包括内边距和内容区
  
  ​    
  
- ***scroll 经常用于获取页面滚动距离***  scrollTop  scrollLeft 
  -    一般给`document`使用scroll事件和属性
  -    注意**页面的Y轴滚动距离**通过 **window.pageXOffset**  获得 





- `ele.getBoundingClientRect()` 方法返回元素的大小及其**相对于视口的位置**

    - 返回的width、height***包括元素的border、padding***

        <img src="images/02-JavaScript API.assets/image-20210108173729674.png" alt="image-20210108173729674" style="zoom:50%;" />











## 八、client 系列属性（了解）

- 通过 client 系列 的相关属性可以***动态的得到该元素的边框大小、元素大小等*** 

    <img src="./images/javaScript.assets/image-20200604090903333.png" alt="image-20200604090903333" style="zoom:50%;" />





- document.body.clientWidth ==> BODY元素的宽度
- document.body.clientHeight ==> BODY元素的高度
- `document.documentElement.clientWidth` ==> 视口的宽度（**不包括**border、滚动条尺寸）
- `document.documentElement.clientHeight` ==> 视口的高度 （不包括border、滚动条尺寸）
- `window.innerWidth` ==> 视口的宽度（**包括**滚动条尺寸）





# 二、BOM

## 一、BOM概述

### 1.1 什么是BOM?

- BOM（Browser Object Model）即**浏览器对象模型**，其核心 对象是 ***window***

    


### 1.2 BOM和DOM的区别

- <img  src=" ./images/javaScript.assets/image-20200601143821205.png" alt="image-20200601143821205" style="zoom: 50%;" />

    

    

### 1.3 BOM的构成

<img  src=" ./images/javaScript.assets/image-20200601144327670.png" alt="image-20200601144327670" style="zoom:50%;" />



- BOM比DOM**更大**，他包含了DOM

- `window` 对象是浏览器的顶级对象，它具有双重角色

  - ***它是 JS 访问浏览器窗口的一个接口*** 

  - ***它是一个全局对象。通过var定义在全局作用域中的变量、函数都会变成 window 对象的属性和方法***

  - ```js
    var a = 1
    console.log(window.a) // 1
    
    // window.alert() == alert(1)
    //在调用window对象下的方法的时候可以省略 window
    ```

    
    



## 二、window对象的事件

### 2.1 窗口加载事件  

- ```Js
  window.addEventListener('load', function() {})
  ```

  - 当文档内容**完全加载完成后**会触发该事件(包括图像、脚本文件、CSS 文件等), 然后调用处理函数

  - 有了 **window.onload** 就可以把 JS 代码写到页面元素的上方，因为 **load事件** 是等页面内容全部加载完毕， 再去执行处理函数

  - 下面三种情况都会刷新页面都会触发 **load 事件**

    1. a标签的超链接 
    2. F5或者刷新按钮（强制刷新） 
    3. 前进后退按钮 

    

- ```js
  document.addEventListener('DOMContentLoaded',function(){}) 
  ```

  - **仅当DOM加载完成**就会触发该事件，**性能效率更高**

    

- ```js
  window.addEventListener('pageshow', function() {})
  ```

  - pageshow事件在强制刷新页面后触发。在重新加载页 面中，**pageshow事件会在load事件触发后触发**



### 2.2 调整窗口大小事件

- ```js
  window.addEventListener("resize",function(){});  // resize 调整大小
  ```

  - 只要浏览器的窗口大小发生变化，就会触发'resize'事件
  - **innerWidth** 可以获取当前窗口的宽度



## 三、定时器

### 3.1 创建定时器

- ```js
  var id = window.setTimeout(回调函数, [延迟的毫秒数]); 
  ```

- setTimeout() 方法用于设置一个定时器，该定时器在延迟的毫秒数到期后执行回调函数 ，**只会调用一次**

  - window 可以省略

  - 延迟的毫秒数不需要跟单位，默认为0

  - **该方法会返回一个定时器所对应的标识符**，页面中有不同的定时器，需要用该标识符来区分它们

    

- ```js
  var id = setInterval(回调函数, [间隔的毫秒数]); 
  ```

- setInterval() 方法**重复调用回调函数**，**每隔这个时间，就去调用一次回调函数** 

  - window 可以省略

  - 延迟的毫秒数不需要跟单位，默认为0

  - **该方法会返回一个定时器所对应的标识符**，页面中有不同的定时器，需要用该标识符来区分它们

    

- 案例：实现京东页面的倒计时效果

  - ```js
        setInterval(() => {
            countDown('2020/6/1 18:30:0')
        }, 1000)
    ```

    


### 3.2 停止定时器

- ```js
  clearTimeout(timeoutID)
  ```

  - clearTimeout()方法可以取消了通过 **setTimeout()** 建立的定时器
  - 传入的参数就是定时器的标识符 

  

- ```js
  clearInterval(intervalID); 
  ```

  - clearInterval()方法可以取消通过 **setInterval()** 建立的定时器

  - 传入的参数就是定时器的标识符 

    

## 四、 location 对象

### 4.1 location 对象的属性

- ![image-20200602165513436](./images/javaScript.assets/image-20200602165513436.png)

    

- 案例1：5秒之后自动跳转百度页面

- 案例2：获取表单跳转携带过来的参数

  

### 4.2 location 对象的方法

- ![image-20200602180920798](./images/javaScript.assets/image-20200602180920798.png)

    

- ***强制刷新：清除当前页面缓存并且刷新***



## 五、 navigator 对象(了解)

- ***navigator 对象包含有关浏览器的信息***，***我们最常用的是 userAgent属性***，该属性可以返回 当前用户访问浏览器的设备

- 下面**前端代码**可以判断用户是用哪个终端打开页面，然后实现跳转 

  - ```js
    if ((navigator.userAgent.match(/(phone|pad|pod|iPhone|iPod|ios|iPad|Android|Mobile|BlackBerry|IEMobile|MQQBrowser|JUC|Fennec|wOSBrowser|BrowserNG|WebOS|Symbian|Windows Phone)/i))) {
                window.location.href = "../H5/index.html";  //手机
            }
    ```

    

## 六、 history 对象(了解)

- ***该对象包含用户（在浏览器窗口中） 访问过的 URL（浏览历史）***

    ![image-20200602182459481](./images/javaScript.assets/image-20200602182459481.png)

    

- history 对象一般在实际开发中比较少用，但是会在一些 OA 办公系统中见到

  - <img  src=" ./images/javaScript.assets/image-20200602182538914.png" alt="image-20200602182538914" style="zoom:50%;" />

    

  

## 七、本地存储

### 7.1 本地存储的概述

- **数据存储在用户浏览器中** 

- 设置、读取方便、甚至页面**刷新不丢失数据** 

- **容量较大，sessionStorage约5M、localStorage约20M** 

- **只能存储JSON格式的数据**，可以将对象数据结构以***JSON.stringify()方法*** ***编码后存储*** 

    

- 在浏览器中可以查看存储的数据

  <img  src=" ./images/javaScript.assets/image-20200608162340210.png" alt="image-20200608162340210" style="zoom:50%;" />

  

  

### 7.2 sessionStorage 对象

- 该对象可以用于存储用户的数据， 比如用户名、密码

- 存储在 `sessionStorage` 里面的数据**在页面会话结束时会被清除**。刷新当前页面不会被清除，关闭当前页面则会清除

- sessionStorage对象，以**键值对形式操作**用户数据

  

- 存储数据

  - ```js
    sessionStorage.setItem(key, value) 
    ```

- 获取数据

  - ```js
    sessionStorage.getItem(key) 
    ```

- 删除指定数据：

  - ```js
    sessionStorage.removeItem(key) 
    ```

- 删除所有数据***（慎用）***

  - ```js
    sessionStorage.clear() 
    ```

    

### 7.2 localStorage 对象

- **生命周期永久生效**，除非手动删除 ***否则关闭页面也会存在*** 

- 以键值对的形式存储使用 

- 存储数据

  - ```js
    localStorage.setItem(key, value) 
    ```

- 获取数据

  - ```js
    localStorage.getItem(key) 
    ```

- 删除指定数据：

  - ```js
    localStorage.removeItem(key) 
    ```

- 删除所有数据（慎用）

  - ```js
    localStorage.clear() 
    ```

    

### 7.3 记住用户名

```js
var username = localStorage.getItem('username') // 获取浏览器中的用户名数据
var input = document.querySelectorAll('input')[0] // 用户名文本框
var remember = document.querySelectorAll('input')[1]

remember.addEventListener('click', function() {
    var value = input.value
    // 将用户名文本框的值永久的存储到浏览器数据中
    localStorage.setItem('username', value)
})

input.value = username
```





#  三、PC端网页特效

## 1. 封装一个动画函数

- ***该函数只能用来实现左右平移的动画***

- ```Js
  /**
   * 封装动画的函数，使用该函数需要传入三个参数
   *  第一个参数：要使用动画的元素对象
      第二个参数：元素对象移动到的目标位置(数值)
      第三个参数：动画执行完成后的回调函数
   */
   function animation(obj, target, callback) {
          // 每调用一次动画函数，就把上一次的定时器关闭，防止定时器累加
          clearInterval(obj.id)
  
          obj.id = setInterval(() => {
              var step = (target - obj.offsetLeft) / 10
              step = step > 0 ? Math.ceil(step) : Math.floor(step);
              
              // 判断传入的对象移动的距离
              if (obj.offsetLeft == target) {
                  clearInterval(obj.id) // 结束定时器
                  if(callback) { 
                      callback() // 动画执行结束后，调用用户传递进来的函数
                  }
  
              } else { 
                  // 定时器每执行一次，box1.offsetLeft就会发生变化
                  obj.style.left = obj.offsetLeft + step + 'px'
              }
          }, 15)
  
          // 匀速动画 就是 盒子是当前的位置 +  固定的值 10 
          // 缓动动画就是  盒子当前的位置 + 变化的值(目标值 - 现在的位置) / 10）
  }
  ```

  

## 2. 网页轮播图

- 功能需求

  1. 鼠标经过轮播图模块，左右按钮显示，离开隐藏左右按钮

  2. ***点击右侧按钮一次，图片往左播放一张***，以此类推， 左侧按钮同理。 
  3. 图片播放的同时，下***面小圆圈模块跟随一起变化***。 
  4. ***点击小圆圈***，可以播放相应图片 
  5. 鼠标不经过轮播图， 轮播图也会自动播放图片
  6. 鼠标经过，轮播图模块， 自动播放停止

- 核心要点

  1. 小圆圈的索引号乘以图片的宽度做为 banner的 移动距离 

  2. 声明一个全局变量num， 点击一次，自增1， 让这个变量乘以图片宽度，就是 banner 的滚动距离

  3. 小圆点的索引值需要跟num相等 

- 基本布局

  - ```html
    <!-- HTML -->
    <body>
        <div class="swiper">
            <!-- 轮播图中左右两个图标 -->
            <div class="icon">
                <a href="#" class="left"><</a>
                <a href="#" class="right">></a>
            </div>
    
            <!-- 轮播图滚动的内容 -->
            <ul class="banner">
                <li>
                    <a href="#"><img src="./img/focus.jpg" alt=""></a>
                </li>
                <li>
                    <a href="#"><img src="./img/focus1.jpg" alt=""></a>
                </li>
                <li>
                    <a href="#"><img src="./img/focus2.jpg" alt=""></a>
                </li>
                <li>
                    <a href="#"><img src="./img/focus3.jpg" alt=""></a>
                </li>
            </ul>
    
            <!-- 轮播图下方的小圆点,在js中动态的生成 -->
            <ul class="dot"></ul>
        </div>
    </body>
    ```

  - ```js
    window.addEventListener('load', function() {
        
        var swiper = document.querySelector('.swiper') // 轮播图
        var dot = document.querySelector('.dot')  // 小圆点的ul
        var banner = document.querySelector('.banner') // 轮播图的图
        var dots = dot.children // 小圆点
        var icon = document.querySelector('.icon')  // 左右按钮的div
    
        // 需求1：动态的生成小圆点 根据图片的长度
        for(var i = 0; i<banner.children.length; i++) { // 遍历图片个数
            var li = document.createElement('li')
            dot.append(li)
        }
    
        // 第一个小圆点类名设置为current
        dot.children[0].className = 'current'
    
        // 需求2：点击当前的小圆点，小圆点就变色 (排他思想)
        for(let i = 0; i < dots.length; i++) { // 遍历每个dots
    
            dots[i].addEventListener('click', function() { // 点击每个小圆点
                // 让所有的小圆点没有背景颜色
                for(let i = 0; i < dots.length; i++) {
                    dots[i].className = ' '
                }
                // 让当前点击的小圆点有颜色
                this.className = 'current'
                
                // 需求3：点击小圆点，图片移动到相应位置
                // 核心：小圆圈的索引号乘以图片的宽度做为banner移动距离 
                animation(banner, - (i * 721))
    			
                // 让全局变量的num等于当前点击到的小圆点的索引是为了图片的索引和小圆点对应
                num = i
            })
        }
    
        // 需求4：点击左右侧图标，让轮播图滚动
        // 核心：定义一个全局变量，该变量用于记录当前图片的索引
        // 让这个变量乘以图片宽度，就是 banner 的滚动距离
    
        var left = icon.children[0]
        var right = icon.children[1]
        var num = 0
        right.addEventListener('click', function() {
            num++ 
            if (num === banner.children.length) { // 如果num等于图片的长度
                num = 0
            }
            // 让这个变量乘以图片宽度，就是 banner 的滚动距离
            animation(banner, - (721 * num )) 
    
            // 遍历所有的小圆点，让小圆点和图片对应
            for(let i = 0; i < dots.length; i++) {
                // 让所有的小圆点没有背景颜色
                for(let i = 0; i < dots.length; i++) {
                    dots[i].className = ' '
                }
                
                dots[num].className = 'current'
            }
        })
    
        left.addEventListener('click', function() {
            num--
            if (num < 0) { // 如果num是负数
                num = banner.children.length - 1 
            }
    
            animation(banner, - (721 * num )) 
    
            // 遍历所有的小圆点，让小圆点和图片对应
            for(let i = 0; i < dots.length; i++) {
                // 让所有的小圆点没有背景颜色
                for(let i = 0; i < dots.length; i++) {
                    dots[i].className = ' '
                }
                dots[num].className = 'current'
            }  
        })
    
        // 需求5：鼠标经过时停止自动播放，离开时自动播放轮播图
        var timer
        swiper.addEventListener('mouseout', function() {
            timer = setInterval(() => {
                    num++
                    if(num === banner.children.length) {
                        num = 0
                		}
                    animation(banner, - (721 * num))
                    // 遍历所有的小圆点，让小圆点和图片对应
                    for(let i = 0; i < dots.length; i++) {
                        // 让所有的小圆点没有背景颜色
                        for(let i = 0; i < dots.length; i++) {
                            dots[i].className = ' '
                        }
                        dots[num].className = 'current'
                    }  
            }, 4000);
        })
    
        swiper.addEventListener('mouseover', function() {
            clearInterval(timer)
        })
    })
    ```

    

## 3. 筋斗云特效



```js
var cloud = document.querySelector('.cloud')
var li = document.querySelectorAll('li')
var ul = document.querySelector('ul')

for(let i = 0; i < li.length; i++) {
    // 给每个小li绑定一个鼠标进入的监听事件
    li[i].addEventListener('mouseenter', function() {
        // 筋斗云移动的距离，就是当前索引i乘以图片的宽度
        // cloud.style.left = i * 83 + 'px'
        animation(cloud, i * 83) 
    })
}
ul.addEventListener('mouseleave', function() {
    animation(cloud, 0)
})
```





# 四、移动端网页特效

## 一、触屏事件



### 1.1 触屏事件概述

- ***触屏事件只对移动端生效***
- touch 对象代表一个触摸点。触摸点可能是一根手指，也可能是一根触摸笔。
- 触屏事件可响应用户手指（或触控 笔）对屏幕的操作 



### 1.2 常见的触屏事件

- <img src="./images/javaScript.assets/image-20200605155426715.png" alt="image-20200605155426715"  />

  

  

### 1.3 触摸事件对象（touchEvent）

- **触屏事件对象**可以为我们提供用户触屏时的**手指的坐标**

- 触屏事件对象有以下三个重要的属性

  - ![image-20200605160422391](./images/javaScript.assets/image-20200605160422391.png)

    

  - touches：返回一个数组，该数组里面存放了所有**正在触摸屏幕的手指**

  - targetTouches：返回一个数组，该数组中存放了**所有正在触摸当前DOM元素的手指**

  - **重点记住 targetTocuhes[0]**

    

- 每个触摸屏幕的手指列表 都有坐标值，`clientX`坐标参照于**视口左上角的原点**

  <img src="./images/javaScript.assets/image-20200606095213328.png" alt="image-20200606095213328" style="zoom: 67%;" />





## 二、移动端案例

### 2.1 拖拽移动端元素

- 移动端拖动的原理：手指移动中，***计算出手指移动的距离***。***然后用盒子原来的位置 + 手指移动的距离*** 
- 手指移动的距离：手指滑动中的位置 减去  手指刚开始触摸的位置 

```js
				// 用于存储手指刚开始触摸时的坐标以及盒子原来的坐标
        var startX = 0, startY = 0, x = 0, y = 0   

        div.addEventListener('touchstart', function(e) {
            // 当手指触摸时，获取当前触摸手指的坐标以及盒子原来的位置
            startX = e.targetTouches[0].pageX
            startY = e.targetTouches[0].pageY
            x = this.offsetLeft
            y = this.offsetTop
        })
        div.addEventListener('touchmove', function(e) {
            // 当手指触摸并且移动元素时，计算出手指移动的距离
            var moveX = e.targetTouches[0].pageX - startX
            var moveY = e.targetTouches[0].pageY - startY
            // 拖拽后盒子的坐标 = 盒子原来的坐标 + 手指移动的坐标
            this.style.left = moveX + x + 'px'
            this.style.top = moveY + y + 'px'
            // 手指移动也会触发滚动屏幕所以要阻止默认的屏幕滚动 e.preventDefault(); 
            e.preventDefault()
        })
```



### 2.2 移动端的轮播图

- ```js
     var main = document.querySelector('.main') // 图片的ul
     var dots = document.querySelectorAll('.dots') // 小圆点
     var back = document.querySelector('.backTop') // 回到顶部
     var img = main.children
     
     var w = img[0].clientWidth // 轮播图图片的宽度
      
     var index = 0
     var timer, distance
      
     // 通过定时器来自动播放轮播图
     timer = setInterval(() => {
         index++
      
         if(index === img.length) {
             index = 0
         }
      
         distance = index * w
         main.style.transform = 'translate(' + -distance + 'px)'
      
         // 小圆点跟随图片发生变化
         for(var i = 0; i < dots.length; i++) {
             dots[i].classList.remove('current')
         }
         dots[index].classList.add('current')
     }, 2000);
      
     back.addEventListener('click', function() {
         backTop()
     })
  ```
  
  

## 三、移动端的click延迟

- ***移动端的click 事件会有 300ms 的延时***，原因是移动端屏幕双击会缩放(double tap to zoom) 页面

- 解决方法一：

  - ```html
    <meta name="viewport" content="user-scalable=no"> 
    ```

  - 禁用缩放。 浏览器禁用默认的双击缩放行为并且去掉 300ms 的点击延迟

    


### 3.1 fastclick插件解决延迟（最优）

- fastclick插件地址： https://github.com/ftlabs/fastclick 

- fastclick插件的功能：**用于解决移动端300ms延迟的问题**

  - 将fastlick插件引入到页面中	

    - ```js
      <script src="./js/fastclick.js"></script>
      ```

  - 按照插件的**语法规范**来解决300ms延迟

    - ```js
      if ('addEventListener' in document) {
      	document.addEventListener('DOMContentLoaded', function() {
      		FastClick.attach(document.body);
      	}, false);
      }
      ```

      

## 四、移动端开发插件

### 4.1 插件的概述

- **JS 插件**是 **js 文件**
- 特点：它一般是为了解决某个问题而专门存在，**其功能单一，并且比较小**

- 插件的使用
  - 使用插件之前***必须了解该插件的功能***
  
  - ***引入 js 插件文件***

  - **在官网文档中查看使用说明**
  
      
  
- 所有的插件使用步骤都可以***参考swiper插件***



### 4.2 swiper插件的使用

- 中文官网地址： https://www.swiper.com.cn/  

- swiper插件的功能：**可以快速的帮助开发者搭建一个轮播图的效果**

  

- swiper使用步骤：

  1. 在官网中下载swiper压缩包，然后解压该文件

  2. 查看文件的目录结构

     <img src="./images/javaScript.assets/image-20200608100521334.png" alt="image-20200608100521334" style="zoom: 67%;" />

     

     - demo文件夹下存放的是**轮播图效果的演示页面**， package文件夹下放的是一些**css、js的初始化文件**

         

  3. 查看演示页面源代码中需要引入的相关文件

     - ```html
     <link rel="stylesheet" href="./css/swiper.min.css">
       <script src="./js/swiper.min.js"></script>
       ```

       

  5. 在效果页面的**源代码**中**复制HTML内容和CSS内容**

     - ```HTML
       <!-- Swiper -->
       <div class="swiper-container">
         <div class="swiper-wrapper">
               <div class="swiper-slide">Slide 1</div>
               <div class="swiper-slide">Slide 2</div>
               <div class="swiper-slide">Slide 3</div>
         </div>
         <!-- Add Pagination -->
         <div class="swiper-pagination"></div>
         <!-- Add Arrows -->
         <div class="swiper-button-next"></div>
         <div class="swiper-button-prev"></div>
     </div>
       ```

  6. 给Swiper定义一个大小，当然不要也行

     - ```css
       .swiper-container {
           width: 600px;
           height: 300px;
     }  
       ```

       

  7. 在效果页面的**源代码中复制JS内容**，如果不能写在HTML内容的后面，则需要在**页面加载完成后再初始化**

     - ```js
       var swiper = new Swiper('.swiper-container', {
           spaceBetween: 30,
           centeredSlides: true,
           autoplay: { // 自动播放相关配置
               delay: 5000, // 设置轮播图的切换时间
               disableOnInteraction: true,   // 点击轮播图之后停止轮播图的自动切换  默认为false
           },
           pagination: { // 分页器相关配置（小圆点）
               el: '.swiper-pagination',
               clickable: false, // 点击分页器时是否切换轮播图，默认为true
           },
           navigation: {
               nextEl: '.swiper-button-next',
               prevEl: '.swiper-button-prev',
           },
     });
       ```

  

8. 如果想要修改细节相关样式，需要到浏览器中查看类名，然后进行更改，**注意权重问题(!important)**

  

### 4.3 其他插件

- superslide： http://www.superslide2.com/ 
  
  - 功能：新闻的轮播图
- iscroll： https://github.com/cubiq/iscroll
  
- 功能：设置滚动条
  
- zy.media：
  
- 功能：解决HTML5中的video标签在各个浏览器中控制栏不一的问题
  
  ​    
  
- **这些插件的用法和swiper插件用法大同小异**





## 五、移动端开发框架

### 5.1 框架的概述

- 什么是框架？

  - 框架会基于自身的特点向用户提供**一套较为完整的解决方案**。使用者要按照框架所规定的**某种规范进行开发**

- 框架和插件的区别？

  - 框架： **功能多，拥有一整套解决方案**

  - 插件： **功能单一，实现某个功能的解决方案** 

    

- 常见的框架

  - 前端常用的框架有 **Bootstrap、Vue、Angular、React** 等。既能开发PC端，也能开发移动端 

  - 前端常用的移动端插件有 **swiper、superslide、iscroll**等 

    

### 5.2   Bootstrap的初体验

- Bootstrap 是一个简洁、直观、强悍的前端开发框架，它让 web 开发更迅速、简单

  - 它能开发PC端，也能开发移动端

  - Bootstrap官方地址：https://www.bootcss.com/

    

- Bootstrap 开发一个轮播图效果

  - 轮播图使用说明：https://v3.bootcss.com/javascript/#carousel

  - 引入相关的css、js文件

    - ```HTML
      <script src="./bootstrap/js/jquery.min.js"></script>
      <script src="./bootstrap/js/bootstrap.min.js"></script>
      <link rel="stylesheet" href="./bootstrap/css/bootstrap.min.css">
      ```

  - 复制轮播图的HTML结构

    - ```HTML
      <div id="carousel-example-generic" class="carousel slide" data-ride="carousel">
          <!-- Indicators 小圆点区域 -->
          <ol class="carousel-indicators">
              <li data-target="#carousel-example-generic" data-slide-to="0" class="active"></li>
              <li data-target="#carousel-example-generic" data-slide-to="1"></li>
              <li data-target="#carousel-example-generic" data-slide-to="2"></li>
          </ol>
      
          <!-- Wrapper for slides 轮播图片区域-->
          <div class="carousel-inner" role="listbox">
      
              <div class="item active">
                  <img src="./Img/banner1.dpg" alt="...">
              </div>
      
              <div class="item">
                  <img src="./Img/banner2.dpg" alt="...">
              </div>
      
              <div class="item">
                  <img src="./Img/banner3.dpg" alt="...">
              </div>
      
          </div>
      
          <!-- Controls 左右箭头区域-->
          <a class="left carousel-control" href="#carousel-example-generic" role="button" data-slide="prev">
              <span class="glyphicon glyphicon-chevron-left" aria-hidden="true"></span>
              <span class="sr-only">Previous</span>
          </a>
          <a class="right carousel-control" href="#carousel-example-generic" role="button" data-slide="next">
              <span class="glyphicon glyphicon-chevron-right" aria-hidden="true"></span>
              <span class="sr-only">Next</span>
          </a>
      </div>
      ```

  - 修改对应样式

    - ```css
      .carousel-inner img {
      	width: 100%;
      }
      ```

  - 修改轮播图相关的JS配置

    - ```js
      $('.carousel').carousel({
          interval: 1000 // 配置轮播图的轮播时间
      })
      ```

      

  

  





# 细节补充

### 1. this的指向

- ***全局作用域或者普通函数中this***指向**全局对象window**

  - 定时器里面的回调函数的this指向window对象

  - ```js
    function bar() { 
    	console.log(this) // window对象
    }
    ```

- 方法中的this指向的是**该方法的调用者**

  - ```js
    var obj = {
        methods:function() {
            console.log(this) // 打印是obj对象
        }
    }
    obj.methods()
    ```

- 构造函数中this指向的是**构造函数的实例对象**

  - ```js
    function Foo() {
    	console.log(this) // 这里的this指向的是people这个实例对象
    }
    var people = new Foo()
    ```

- 绑定事件中的回调函数的this永远指向**绑定事件的元素对象**

  - ```js
    btn.addEventListener('click', function() {
    	console.log(this) // 永远指向绑定事件的元素对象 也就是btn
    })
    ```

    

### 2. 排他思想(算法)

- 如果有同一组元素，我们想要某一个元素实现某种样式， 需要用到循环的排他思想算法： 

  1. ***所有元素全部清除样式（干掉其他人）*** 
  2. ***给当前元素设置样式 （留下我自己）*** 

  3. 注意顺序不能颠倒，首先干掉其他人，再设置自己 

```js
var btn = document.querySelectorAll('button')
for(var i = 0; i < btn.length; i++) { 

    btn[i].onclick = function() { 
        
        for(var j = 0; j < btn.length; j++) {
            btn[j].style.backgroundColor = '' // 当点击按钮时，给所有的元素清除样式
        }

        this.style.backgroundColor = 'pink' // 给当前触发事件的对象添加样式
    }
}
```







### 3. 创建元素的三种方式

- `document.write()`

  - ```js
    document.write('<div>123</div>')
    ```

  - 直接将内容写入页面的内容流，但是文档流执行完毕，则它会导致页面全部重绘 ,**性能较低很少使用**

- `element.innerHTML `

  - ```js
    var div = document.querySelector('div')
    div.innerHTML = '<a href="#">123</a>'
    ```

  - 是将内容写入某个 DOM 节点，不会导致页面全部重绘 ，**性能较高**

      

- `document.createElement() `

  - ```js
    var div = document.querySelector('div')
    var a = document.createElement('a')
    a.innerHTML = 123
    div.appendChild(a)
    ```

  - **写法比较麻烦**

    

### 4. 阻止a标签的链接跳转

- 阻止a标签自动跳转，需要将a标签的href属性设置为 `javascript:void(0)`或者 ` javascript:; `

  - ```html
    <a href="javascript:void(0)">123</a>
    
    <a href=" javascript:; ">123</a>
    ```

    

- 方式二：**禁止全局的默认行为**

    - ```js
        document.addEventListener('click', (e) => {
               e.preventDefault()
        })
        ```

        



### 5. 回调函数

- 什么是回调函数？

  - 你定义的函数，但是这个函数是匿名函数
  - 你没有去调用它
  - 但是最终这个函数会被执行

- **绑定事件所触发的函数**和**定时器**，都是**回调函数**，都不需要我们手动的去调用它

    

- 回调函数**原理**

  - **函数可以作为一个参数**。**将这个函数作为参数传到另一个函数里面**，当另一个函数执行完之后 ，再调用传进去的这个函数，这个过程就叫做回调。 

  - ```js
    bar(function() {})
    function bar(callback) {
        callback()  // 内部调用传递过来的函数
    }
    ```

    

### 6.  阻止元素默认行为

- 比如阻止表单提交按钮的默认跳转行为

  - ```js
    submit.addEventListener('click', (e) => {
      e.preventDefault()
    })
    ```

    

- `return false`和`e.preventDefault()`区别：
    - 用**addEventListener()**绑定事件就要用**e.preventDefault()**方法
    - 通过`on`绑定事件，就要用`return false`方式

<img src="images/02-JavaScript API.assets/image-20210203111649402.png" alt="image-20210203111649402" style="zoom:50%;" />









