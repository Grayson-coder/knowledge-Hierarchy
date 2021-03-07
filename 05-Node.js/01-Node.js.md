# 一、Node.js的概述

## 1.1 Node.js是什么？

- Node.js（软件）**一种javascript的运行环境**，能够使得javascript代码脱离浏览器运行

  

- 什么是**代码运行环境**？

  - 浏览器（软件）能够运行JavaScript代码，**浏览器就是**JavaScript代码的**运行环境**

  - Node.js（软件）能够运行JavaScript代码，**Node.js就是**JavaScript代码的**运行环境**

    

## 1.2 为什么要学习Node.js？

- 通过学习Node.js，我们可以学习到**开发服务端的基础**
- **学习Node.js能够和后端程序员更加紧密的配合**
- 通过Node.js技术，我们可以**对数据库进行增删改查操作**



## 1.3 Node.js运行环境安装

- Node.js官网：https://nodejs.org/en/

    <img src="./images/Node.js.assets/image-20200705100145093.png" alt="image-20200705100145093" style="zoom: 67%;" />






- 一键傻瓜式安装，一直点击next下一步
- 安装完成之后，**Node会自动配置系统环境变量**，打开命令行窗口，输入`node -v`查看当前node版本

  <img src="./images/Node.js.assets/image-20200705100842417.png" alt="image-20200705100842417" style="zoom:50%;" />



- 弹出版本则表示安装成功





## 1.4 Node.js的组成

- **浏览器**中的JavaScript 由三部分组成，**ECMAScript**，**DOM**，**BOM。**
- **Node.js**中的JavaScript是由 **ECMAScript**及**Node 环境**提供的一些**附加API**组成的，包括文件、网络、路径等等一些更加强大的 API。



<img src="./images/Node.js.assets/image-20200705101448440.png" alt="image-20200705101448440" style="zoom:50%;" />





- **ECMAScript**：JavaScript的**基础语法**
- 在Node环境下编写的JS代码，并**不具备BOM、DOM提供的API**





## 1.5 Node.js的初体验

- 在之前学习阶段中，我们都是通过在**HTML文件中引入JS文件**，让浏览器加载HTML页面时，顺带加载JS文件

- 通过Node.js的学习，我们可以完全脱离浏览器，可以**让独立的JS文件在Node.js环境下运行**

- 以下为**Vscode**编辑器为例

  <img src="./images/Node.js.assets/image-20200705102645588.png" alt="image-20200705102645588" style="zoom: 50%;" />

  

  - 前提是安装好：`Code Runner`插件和`Node.js`运行环境，才能右键执行JS文件





## 1.6 Node.js下的全局对象

- 在**浏览器**中全局对象是**window**，在**Node**中全局对象是**global**
- Node中全局对象下有以下方法，可以在任何地方使用，**global可以省略**
  - console.log()   在控制台中输出
  - setTimeout()   设置超时定时器
  - clearTimeout() 清除超时时定时器
  - setInterval()   设置间歇定时器
  - clearInterval()  清除间歇定时器



>可以将**global对象**看做是一个**单例模式**，**一个Node运行环境只有一个global**，其**作用与Vuex类似**
>







# 二、Node.js模块化开发

## 2.1 Node.js的模块化规范

### 2.1.1 CommonJS模块规范

- 在`Node.js环境下`JS代码遵循的是`CommonJS`模块规范（**规范即规定如何导入导出**）

  

- Node.js规定一个**JavaScript**文件**就是一个模块，模块**内部定义的变量和函数**默认情况下在**外部无法得到

  - `CommonJS`模块规范下，***导入和导出的永远都是`exports`对象***

    

- 注意：`Node环境下`不支持ES6的模块化语法规范，支持`CommonJS`语法规范

    <img src="./images/Node.js.assets/image-20200903155421341.png" alt="image-20200903155421341" style="zoom:50%;" />







### 2.1.2 CommonJS的导出

- 方式一：`exports.xxx = 要导出的内容`

  - ```js
    // 导出数据
    exports.obj = {name: '张三'}
    ```
    
    
  
- 方式二：`module.exports = 要导出的内容`

  - ```js
    module.exports = {name: '王五'}
    ```

    

- 在`CommonJS`模块规范下，默认导出的是一个`exports`对象

    

- 如果以上两种方式**同时导出**，**导出对象最终以`module.exports`为准**



### 2.1.3 CommonJS的导入

- 语法：

  - ```js
    let a = require(xxx)
    ```
    
  - `require`方法有返回值，返回值是导入的模块中的`exports`对象
  
  - 引入**自定义模块**时，xxx是路径位置，引入**第三方模块**时，xxx是模块名
  
    
  
- 导入模块时文件**后缀名可以省略**，默认寻找`以JS`为后缀名的文件
  
- 注意：用`require(xxx)`导入模块时，**会执行导入模块中的代码**







## 2.2 系统模块

### 2.2.1 什么是系统模块？

- ***系统模块就是Node运行环境提供的API***
- **系统模块无需下载**，引入的时候不需要跟路径，只需要跟模块的名字



### 2.2.2 文件模块

- 操作文件模块时，**文件路径都采用绝对路径方式**

    

- 引入文件 **fs模块**
  - ```js
    let fs = require('fs')
    ```
  
    
  
- 简单的**文件读取**：

  - ```js
    fs.reaFile('文件路径', callback(err,data));
    ```

  - 第二参数为回调函数，当文件读取成功或失败时，会自动调用该函数

  - ```js
    // 拼接成一个绝对路径
    let filePath = path.join(__dirname, 'test.txt')
    
    fs.readFile(filePath, (err, data) => {
        !err ? console.log(data.toString()) : console.log(err);
    })
    ```

  

- 简单的**文件写入**：

  - ```js
    fs.writeFile('文件路径', '要写入的内容', callback(err));
    ```

  - 回调函数中只有一个参数，该参数为**当文件写入失败时的报错信息**

  - ```js
    // 拼接成一个绝对路径
    let filePath = path.join(__dirname, 'test.txt')
    
    fs.writeFile(filePath, '加油复习完Node123', err => {
        !err ? console.log('文件写入成功') : console.log(err);
    })
    ```

  

  


### 2.2.3 路径模块

- 引入路径模块(path)

  - ```js
    let path = require('path')
    ```

- 路径拼接操作：

  - ```js
    let filePath = path.join('public', 'uploads', 'test')
    // 拼接成的路径：public\uploads\test
    ```

  - 注意：**路径拼接一般配合绝对路径使用**

  - ```js
    let filePath = path.join(__dirname, '文件路径')
    ```



- 注：**运行在Node环境下的JS代码**，一旦需要操作一些路径相关，则必须要采用**绝对路径**



- 在Node环境下拥有`__dirname`全局变量，该变量用于存储**当前文件所在的绝对路径**



## 2.3 Node中模块的分类

- **系统模块**

  - 又称为核心模块，是Node中自带的模块

  - 无需下载，引入的时候不需要跟路径，只需要跟***模块的名字***

  - 比如`require('fs')`

    

- **自定义模块**

  - 自己写的JS文件，通过` CommonJS`模块规范向外导出内容

  - 通过`require`引入时，必须跟上***模块文件相对路径***

  - 比如`require('./a.js')`

    

- **第三方模块**

  - 通过npm 下载的模块，称为第三方模块
  
  - 通过`require`引入时，必须跟上***模块的名字***
  
  - 比如`require('express')`
  
      
  
- 在现阶段，引入第三方模块只能通过`CommonJS规范`引入，在后续学习的Vue中，通过`vue-cli`搭建的项目可以使用`ES6模块规范`引入

  
  
  

## 2.4 第三方模块的加载机制

- 模块查找规则：**当引入的模块拥有路径但没有后缀时**

  - ```js
    require('./b')
    ```

  - 优先级100：查找**当前文件夹**下的**同名JS文件**
  - 优先级90：查找当**前文件夹下的同名文件夹**下的`index.js`文件
  - 优先级80：查找**文件夹根目录**中的`package.json`文件中的**主入口文件**

  - 如果都没有找到则报错

    

- 模块查找规则：**当引入的模块只有模块名时**

  - ```js
    require('vue')
    ```

  - 优先级100：去**Node系统模块下查找**是否有该名字的模块 （系统模块）
  
  - 优先级90：去`node_modules`文件夹下**查找同名的JS文件**

  - 优先级80：去`node_modules`文件夹下**查找同名的文件文件夹**下的`index.js`文件
  
  - 优先级80：去`node_modules`文件夹下**查找同名的文件文件夹**下的`package.json`文件中的**入口文件**
  
  - 如果都没有找到则报错
  
      

>注：以上模块的**查找机制**也适用于ES6语法的`import`的查找
>











#三、第三方模块

## 3.1 什么是第三方模块？

- **别人写好的、具有特定功能的、我们能直接使用的模块就是第三方模块**，第三方模块有时有称为**包**。

  

- 第三方模块有两种存在形式：

  - 以**js文件**的形式存在，**提供具体功能的API接口**
  
  - 以**命令行工具**形式存在，**辅助项目开发**
  
    

- 通过`npm` 指令，我们可以下载第三方模块



## 3.2 什么是npm？

- `npm`：是'Node package manager'的简写，俗称**Node的包管理者**，这里的包也称为第三方模块

- 安装Node后会自动安装npm

- `npm`是用于管理第三方模块的，**他是通过命令行窗口的指令来对第三方模块进行操作**

  

- `npm`官网：www.npmjs.com  可以查找有哪些第三方模块，以及包的使用说明

  

- `  npm ls xxxx` ：查看我们所安装的xxxx包的版本



 

## 3.3 package.json文件

- 在下载第三方模块之前，我们**需要对使用第三方模块的文件夹进行一个初始化**

  - `npm init -y` 指令可以对当前文件夹进行初始化，并且生成一个`package.json`文件，前提是当前文件夹的`名字只能是英文`

  

- `package.json`文件的作用：

  - 该文件记录了项目名称、版本、作者、当前项目依赖了哪些第三方模块等项目信息
  - 当下载好第三方模块后，当前文件夹下会自动创建`node_modules`文件夹，**所有第三方模块都在存放在该文件夹下**。

  - 当我们在传递项目时，无需复制`node_modules`文件夹给别人，只需要在当前项目下执行`npm i `命令，则`npm`会自动查找到该项目根目录下的`package.json`文件中**所有依赖的第三方模块**，**并且自动下载他们**

  

- `package.json`文件解析

  <img src="./images/Node.js.assets/image-20200706140344602.png" alt="image-20200706140344602"  />



## 3.4 package-lock.json文件

- 安装完第三方模块会自动产生一个`package-lock.json`文件
  - 该文件里面记**录的是每个下载过的模块的下载地址**， 可以加快下载速度



## 3.5 项目依赖和开发依赖

- 什么是项目依赖？

  - 项目部署到服务器上，必须要依赖的第三方模块，就是项目依赖 -----   例如：jquery、vue

  - `npm i 包名`命令下载的文件会被自动添加到 `package.json `文件的`dependencies`  （***项目依赖中***）

    

- 什么是开发依赖？

  - ***在项目的开发阶段需要依赖，线上运营阶段不需要依赖的第三方包，称为开发依赖。***
  - 例如：语法检查库、压缩代码、扩展css前缀的库

  - `npm i 包名 -D` 命令下载的模块会被添加到`package.json `文件的`devDependencies`(***开发依赖中***) 

  

- 为什么要区分项目依赖和开发依赖？
  - 在开发项目时，许多第三方模块都只是辅助开发人员开发使用，比如语法检查
  - 当把项目直接给客户时，已经不需要开发依赖中的模块了，此时应该直接删除开发依赖中所有的模块
  - **区分项目依赖和开发依赖，是为了让项目的结构更清晰，项目体积更小**





##3.6 安装第三方模块

- 安装第三方模块：（安装之前必须保证**文件夹已被初始化**）

  - 安装第三方模块的指令为：`npm i 模块名称`
  
    
  
- 安装后会在当前文件夹下自动创建一个`node_modules`文件夹，所有第三方模块都在存放在该文件夹下

  

- **安装多个第三方模块**，只需要在模块名称之间加个空格
  
  - `npm i 模块名称 模块名称`

      
  
- 指定模块的版本下载：`npm i 模块名称@版本号`



##3.7 全局安装和局部安装

- 全局安装的第三方模块**在任何项目(文件夹)**下都能够使用，指令为:`npm i 模块名称 -g `

  - 一般都是**命令行工具**才需要**全局安装**

  - 查看全局安装的**位置**：`npm root -g`

  - 查看全局安装的包的**版本**：`npm ls 包名 -g`或者`包名 --version`

  - **全局安装时无需初始化项目**

    
    
    

- 局部安装的第三方模块只能**在当前项目(文件夹)**下能够使用

  - 默认安装的都是局部安装，**JS文件一般都是局部安装**





##3.8 第三方模块——nrm

- nrm模块功能：**可以切换npm下载地址**

- npm默认的下载地址在国外，国内下载速度慢，因此我们要切换npm的下载地址

  

- 步骤一：**全局安装** nrm 模块

  - `npm i nrm -g`

- 步骤二：查询可用下载地址列表 
  - `nrm ls`
  
    <img src="./images/Node.js.assets/image-20200705171831129.png" alt="image-20200705171831129" style="zoom: 50%;" />
  
- 步骤三：切换 npm下载地址 
  - `nrm use 下载地址名称`
  
      <img src="./images/Node.js.assets/image-20200705171934210.png" alt="image-20200705171934210" style="zoom:50%;" />



- 查看当前npm远程仓库地址：``` npm config get registry ```





## 3.9 第三方模块  nodemon

- ***nodemon是一个命令行工具，用以辅助项目开发。***

  - 当运行在Node环境下的JS代码发生了变化时，我们需要手动的重新运行该JS文件，非常的繁琐，使用`nodemon`可以监听JS代码的变化，并**自动帮助我们重新运行修改后的JS文件**

    

1. 使用***npm install nodemon –g*** 下载它

    

2. 在命令行工具中用***nodemon命令替代node命令执行文件***，**执行一次后，就会开始监听该文件是否发生变化**

    <img src="images/01-Node.js.assets/image-20201022101041799.png" alt="image-20201022101041799" style="zoom:50%;" />









# 四、Node原生服务器

## 4.1 Node原生服务器

### 4.1.1 基本搭建

- 搭建`原生的Node服务器`步骤

  - ```js
    const http = require('http')
    const server = http.createServer()
    server.on('request', (request, response) => { // 当浏览器有请求时，自动调用该函数
      //设置响应报文中返回给客户端的的内容类型
      response.setHeader('content-type','text/html;charset=utf-8')
      response.end('我是你人生中的第一个服务器')  // 给客户端(浏览器响应)
    })
    
    server.listen(80, err => {
      console.log('服务器启动成功, 可以通过localhost来进行访问')
    })
    ```
    
    

### 4.1.2 请求和响应对象的方法

- 获取请求的`路由+参数`、`请求方式`、`设置响应报文`

  - ```js
    server.on('request', (request, response) => {
      request.url  // 获取到请求的URL地址的 /路由+参数
      request.method  // 获取请求的方式
      response.setHeader('content-type','text/html;charset=utf-8') // 设置响应报文
    })
    ```

    

- 所有**请求报文**信息都在`request`上，所有**响应报文**数据都在`response`上





### 4.1.3 获取GET请求参数

- 获取`GET请求`的参数

  - `GET请求`的参数会放在URL地址栏上进行传递，`localhost:3000/index?name=kobe&age=18`

  - 需要想办法将**路由和传递的参数**进行分离

  - ```js
    const url = require('url') // 引入 url 系统模块  该模块用于处理url地址
    server.on('request', (request, response) => {
      	let { query, pathname } = url.parse(request.url, true)
        console.log(query);  // 传递的参数：{ username: 'zhanmusi', pwd: '999' }
        console.log(pathname);  // 路由：/index
    })
    ```





### 4.1.3 获取POST请求参数

- 获取`POST请求`的参数

  - `POST`请求的参数是`存放在请求体中`的，所以无法通过地址栏获取参数

  - ```js
    const querystring = require('querystring');
    server.on('request', (request, response) => {
        let postData = '';
        // 监听参数传输事件
        request.on('data', (postParam) => postData += postParam);
    
        // 监听参数传输完毕事件
        request.on('end', () => { 
            console.log(postData); // POST请求的参数：username=lbl&pwd=999  
            console.log(querystring.parse(postData));// 将POST请求参数解析成对象形式
        });  
    })
    ```

    
    
    

### 4.1.5 给浏览器发送文件

- 服务器给客户端`发送文件`

  - ```js
    server.on('request', (request, response) => {
      		let filePath = path.join(__dirname, 'public', 'index.html')
          fs.readFile(filePath, (err, data) => response.end(data))
    })
    ```

    

### 4.1.6 页面重定向

- 服务器响应给浏览器新的链接(`重定向`)

  - ```js
    server.on('request', (request, response) => {
      response.writeHead(301, {'Location': 'https://www.baidu.com'})
      response.end()
    })
    ```

    
    
    

## 4.2 第三方模块 —— router

### 4.2.1 router模块的功能

- 在Node原生服务器中，我们需要在`监听浏览器请求的回调函数`中来判断`请求的方式`以及请求地址中的`路由`

  - ```js
    server.on('request', (request, response) => {
      	if (request.method === 'GET'){
    				if (路由 === '/index')		
    		}
    })
    ```

  - 多个`if语句嵌套`，必然维护起来也十分困难，代码也不够优雅

    

- 使用`router模块`，就是帮助我们***实现请求方式和路由的分离***，不再让他们嵌套在`同一个回调函数中`

  

### 4.2.2 router的基本使用

1. 获取路由对象
2. 拦截路由以及请求方式
3. 在`Node原生服务器`监听浏览器请求的回调函数中  ***启用路由，使路由生效***

- ```js
  const getRouter = require('router')  // 引入路由模块
  const router = getRouter();   // 获取路由对象
  // 拦击请求方式以及路由
  router.get('/index', (request, response) => {
      response.end('你好啊')
  })
  
  server.on('request', (request, response) => {
      router(request, response, () => {})  // 启动路由拦截
  })
  ```
  
  





## 4.3 第三方模块 —— serve-static

### 4.3.1 HTML加载时引发的问题

- 当服务器返回给浏览器一个`html页面`，在浏览器加载html页面时，html页面中会有***引入js和css样式的标签和一些图片***，在加载到这些标签时，`会向服务器再次发送请求`，**如果浏览器没有返回给服务器对应的文件**，则`html页面`得不到`css样式和js`的渲染

    

    <img src="./images/Node.js.assets/image-20200712213548568.png" alt="image-20200712213548568"  />

    

    - 上图代码中，服务器返回给浏览器一个`html页面`，在浏览器加载html页面时，会遇到引入的`CSS样式标签`，在加载`CSS样式标签时`，`会向服务器再次发送请求`

    - 如果服务器不给浏览器返回对应的`CSS文件`，则`HTML页面`将会得不到渲染

      

      

- 如何解决上图代码中`html页面加载不到css文件`的问题？

  - 在加载`CSS样式标签时`，浏览器`会向服务器再次发送请求`，其请求地址是：`http://localhost/css/index.css`   

  - 截取路由中`.`后面的后缀名，用来判断请求的文件类型，根据文件类型，返回给浏览器对应的文件

    - ```js
      let { pathname } = url.parse(request.url) // 获取请求路由
      // 截取路由中'.'后面的所有字符串
      let type = pathname.substr(pathname.lastIndexOf('.') + 1) 
      if (type === 'css') { // 如果请求类型为CSS文件
          let static = path.join(__dirname, 'public', pathname)
          // 响应给浏览器请求的CSS文件
          fs.readFile(static, (err, data) => response.end(data)) 
      }
      ```

      

### 4.3.2 静态资源访问的概述

- 在浏览器加载html页面时，html页面中会有其他引入的文件，这些文件我们称为`静态资源`

- 当加载html页面`静态资源`时，服务器需要通过判断`静态资源`的文件类型，来返回不同的文件给浏览器

- 如果要加载的`静态资源`过多，则在服务器中要写的`判断条件响应文件数据`的代码也就越来越多，这样势必会影响开发效率。

    

- 那么有没有当加载`静态资源`时，服务器会`自动返回静态资源给浏览器`的方法呢？
  
  - 答案是有的，就是使用第三方模块`serve-static`





### 4.3.2  serve-static的使用

1. 引入`serve-static模块`
2. 调用`serveStatic`方法创建静态资源服务并指定静态资源服务目录
3. 在`Node原生服务器`监听浏览器请求的回调函数中 ***启动静态资源访问服务***

- ```js
  const serveStatic = require('serve-static')  // 引入静态资源访问模块
  let staticPath = path.join(__dirname, 'public')
  const static = serveStatic(staticPath) // 配置静态资源文件夹目录
  server.on('request', (request, response) => {
      let  { pathname } = url.parse(req.url)
      if (pathname === '/') {
          let html = template('index.art', {})
          res.end(html) // 发送模板文件和数据拼接好的HTML文件
      }
      static(req, res, () => {})  // 启动静态资源访问服务
  })
  ```

- 当返回给浏览器HTML页面时，该HTML页面加载了CSS文件(`静态资源文件`)，则浏览器会再次向服务器发送请求
  
- 开启了静态资源访问服务后，他会判断当前的浏览器请求是否是请求`静态资源文件`，如果是请求`静态资源文件`，则会`根据请求的地址`返回给浏览器其对应的`静态资源文件`

    

    






## 4.4 学生档案管理案例

- 涉及到的知识点：http请求响应、数据库、模板引擎、静态资源访问。
  - <img src="./images/Node.js.assets/image-20200713145517493.png" alt="image-20200713145517493" style="zoom:50%;" />

- 制作流程：

  1. 建立项目文件夹并生成项目描述文件（`npm init -y`）

  2. 创建服务器实现客户端和服务器端通信

  3. 连接数据库并创建集合规则创建学生`集合对象`

  4. 创建路由对象，拦截路由，返回浏览器一个初始化的页面（`添加页面`和`学生档案列表页面`）
     - `学生档案列表页面`中的数据需要在数据库中拿取然后渲染

  5. 实现`静态资源访问`

  6. 实现学生信息添加功能
     1. 为每个表单添加`name`属性，并且指定表单的`提交方式以及提交路由`
     2. 服务器接收浏览器传递过来的`POST请求参数`，将该参数以对象形式添加到数据库中
     3. 将页面`重定向`到学生信息列表页面

  7. 实现学生信息展示功能

     1. 从数据库中将所有的学生信息查询出来

     2. 通过`模板引擎`将学生信息和HTML模板进行拼接

     3. 将拼接好的HTML模板响应给浏览器













# 五、模板引擎

## 5.1 模板引擎的概述

- 什么是**模板引擎**？
  
- 模板引擎是为了使用户界面与业务数据（内容）分离而产生的，它可以生成特定格式的文档，通过模板引擎生成一个标准的文档，**就是将模板文件和数据通过模板引擎生成一个HTML代码**
  
  <img src="./images/Node.js.assets/image-20200712093849727.png" alt="image-20200712093849727" style="zoom:50%;" />
  





## 5.2 模板引擎的安装

- 模板引擎是**第三方模块**，因此需要通过npm下载：`npm i art-template `

- 引入模板引擎模块：`const template = require('art-template')`

- 告诉模板引擎要**拼接的数据**和**模板文件**在哪 

  - ```
    const html = template(‘模板文件路径’, {数据})
    ```

  - 注意：模板文件是以`art`为后缀名，模板文件路径要用`绝对路径`
  - `template`会返回一个拼接好的`HTML文件`

- 使用`模板文件语法`告诉模板引擎，`模板文件`与`数据`应该如何进行拼接 



## 5.3 模板引擎的初体验

- JS代码

  - ```js
    const template = require('art-template')  // 导入模板引擎
    const path = require('path')
    
    // 获取模板文件所在的绝对路径
    const views = path.join(__dirname, 'view', 'index.art')
    
    // 1. 模板文件所在的绝对路径
    // 2. 模板文件中显示的数据
    const html = template(views, { // 将特定模板文件与特定数据进行拼接返回一个HTML文件
        data: {
            name: '张三',
            age: 18,
            sex: '男'
        }
    })
    ```

  - 返回的html变量就是一个`HTML文件`，可以通过服务器发送给浏览器

  

- `.art`文件代码：

  - ```js
    // 先生成HTML骨架
    <div>
        {{data.name}}
        {{data.age}}
        {{data.sex}}
    </div>
    ```

    

## 5.4 模板文件的语法

- 在模板文件中`输出数据`

  - ```html
    <h2>{{ 数据 }}</h2>
    <a href="http://localhost:3000/index?name={{ data.name }}"></a>
    ```

  - 输出数据语法可以嵌套在`引号`中

    

- 解析HTML标签`输出数据`

  - ```html
     <h2>{{@ value }}</h2>
    ```

- 条件判断

  - ```
    {{if 条件}} ... {{/if}}
    {{if v1}} ... {{else if v2}} ... {{/if}}
    ```

- 循环

  - ```
     {{each 循环的数据}}
         {{$index}} {{$value}} 
     {{/each}}
    ```

  - `$value` 是当前遍历的每一项，循环体内的`HTML标签`也会被循环

- 原始语法循环

  - ```
      <!-- 原始语法 -->
     <% for(var i = 0; i < target.length; i++){ %>
         {{ i }}
     <% } %>
    ```

    

 

## 5.5 子模板和继承

- **子模板**

  - 使用子模板可以将模板文件中`公共部分`抽离到单独的文件中。再用其语法引入到子模板中

  - ```
     {{include './header.art'}}
    ```

    

- **模板继承**

  - 使用模板继承可以将网站***HTML骨架抽离到单独的文件中***，其他页面模板可以`继承骨架文件`
  
    <img src="./images/Node.js.assets/image-20200716170806103.png" alt="image-20200716170806103" style="zoom:50%;" />
  
    <img src="./images/Node.js.assets/image-20200716171201966.png" alt="image-20200716171201966" style="zoom:50%;" />
  - ```
    <!--index.art 首页模板-->
    {{extend './framework.art'}}  // 继承骨架模板
        {{block 'head'}} // 填充骨架中名为'head'的坑
            <link rel="stylesheet" href="custom.css"> 
        {{/block}}
        {{block 'content'}} // 填充骨架中名为'content'的坑
            <p>This is just an awesome page.</p> 
        {{/block}}
    ```

    





## 5.6 模板文件的配置

- 向`模板文件`中**导入变量**

  - 例子：当我们想要在模板文件中输出`当前时间数据`时，所输出的格式不是我们想要的，因此需要借助`dateformat`模块下的方法，将该模块下格式化时间的方法导入到模板文件中，模板文件就能够直接使用该方法

  - ```js
    // 向模板文件中导入变量，导入之后就可以在模板文件中使用该方法格式化时间
    template.defaults.imports.dateFormat = dateFormat
    ```

    

- 设置模板文件的`根目录` 

  - 设置完模板文件的根目录之后，***模板文件会在指定的根目录下查找***

  - ```js
    template.defaults.root = path.join(__dirname, 'view')
    // 模板文件会在指定的根目录下查找
    const html = template('index.art', {})
    ```

    

- 设置模板文件的默认`后缀名`

  - 设置完默认后缀名之后，模板文件不需要在加后缀名

  - ```js
    template.defaults.extname = '.art'
    const html = template('index', {})
    ```

    

- 注：以上配置均在**JS文件下编写**





# 六、Express框架（一）



## 6.1 邂逅Express框架

- 什么是Express框架？

    - Express是一个**基于Node平台**的`服务器开发框架`，同时也是一个`第三方模块`，通过`npm i express`下载
    - `Express`官方文档：http://expressjs.jser.us/3x_zh-cn/api.html#app.use

      

- Express框架搭建的服务器***特性***：

  - 对获取HTTP`请求参数`进行了简化处理

  - 提供了简洁的`拦截请求方式以及路由定义`写法

  - 提供了`中间件机制`有效控制HTTP请求

    
    
    

- 总结：

  - 使用Node原生的服务器，需要引入`router`和`serve-static`模块，来进行代码的分离，而使用`express`框架开发的服务器，自带以上两个模块的功能

  - `express`框架开发的服务器，**语法更加简写**

    
    
    

- Node原生服务器和Express框架对比

  <img src="./images/Node.js.assets/image-20200714111651901.png" alt="image-20200714111651901" style="zoom:50%;" />

  <img src="./images/Node.js.assets/image-20200714111740950.png" alt="image-20200714111740950" style="zoom:50%;" />





## 6.2 Express的基本使用

1. 安装express包：`npm i express`

2. 通过express框架快速搭建服务器

    - ```js
        const express = require('express')  // 引入express框架
        const server = express()  // 创建服务器对象
        // 客户端以get方式访问/路由时
        server.get('/', (req, res) => {
            res.send('我不会再乱码了')  // 对浏览器做出响应 send方法会根据内容的类型自动设置请求头
        })
        // 监听3000端口号
        server.listen(3000, () => console.log('服务器启动成功，端口为3000'))
        ```

        





## 6.3 中间件

### 6.3.1 什么是中间件？

- 服务器接收浏览器发来的请求、对该请求做出响应，这一系列的过程可以看成是`中间件处理`的过程

  <img src="./images/Node.js.assets/image-20200714112451881.png" alt="image-20200714112451881" style="zoom:50%;" />



- ```js
  server.get('请求路由', calback)  // 接收并处理get请求
  ```

  - 上述的代码就可以看做是一个`中间件`，其包含了接收请求，并处理请求的过程
  
  
  
  

### 6.3.2 next()用法

- 可以针对**同一个请求**设置`多个中间件`，对同一个请求进行多次处理

  - 默认情况下，请求从**上到下依次匹配中间件**，**一旦匹配成功，终止匹配**。

  - 可以调用`next方法`将请求的控制权交给**下一个中间件**，直到遇到结束请求的中间件。

      

- ```js
  let obj = {}
  server.get('/index', (req, res, next) => {
      obj.name = '张三'
      next()  // 匹配下一个中间件
  })
  server.get('/index', (req, res, next) => {
      res.send(obj) // 结束请求
  })
  ```

  

### 6.3.3 全局中间件用法

- `server.use()`中间件用于匹配`所有的请求方式和所有的请求路由`
    - ```js
      server.use((req, res, next) => {
           console.log('请求走了server.use中间件');
           next(); 
       });
      ```

      

- `server.use()`第一个参数也可以传入请求地址，拦截所有以该**请求地址开头的路由**

  - ```js
    server.use('/index', (req, res, next) => {
         console.log('请求走了server.use /index 中间件');
         next();
     });
    ```

  - 注意：上述匹配的是以`/index开头`的路由

  

- 在全局中间件的**next()**中，**只能传入一个参数**，该参数可以作为下一个匹配到的**中间件的处理函数的形参**

    - ```js
        server.use((req, res, next) => {
            next({name: 'zhang3'},)
        })
        
        server.use('/home', (msg, req, res) => {
            console.log(msg); // home
            res.send('ok')
        })
        ```

        





### 6.3.4 全局中间件的应用

1. 网站维护公告，使用`全局中间件`拦截网站内`所有的请求`，并且响应给浏览器当前网站正在维护

2. 自定义404页面，在中间件的末尾添加`全局中间件`，当请求地址无效时，响应给浏览器`当前页面不存在`并且设置`状态码`

   - ```js
     server.use((req, res, next) => {
         res.status(404).send('你访问的页面不存在')
     })
     ```
     
     

3. ***捕获错误***的全局中间件

   - ```js
     server.get('/index', (req, res, next) => {
         fs.readFile('./main.js', (err, data) => {
             err ? next(err) : res.send(data)
         })
     })
     server.use((err, req, res, next) => {
         res.status(500).send(err.message)
     })
     ```

   - 当程序出现错误时，**调用next()方法**，并且将错误信息通过参数的形式传递给next()方法，即可触发错误处理中间件

     

     

     

     

# 七、Express框架（二）

## 7.1 构建模块化路由

- ```js
  let home = express.Router()  // 创建路由对象
  server.use('/index', home)  // 设置路由对象的一级路由
  home.get('/home', (req,res) => {  // 设置路由对象的二级路由
      // 访问二级路由： /index/home
      res.send('欢迎来到博客首页')
  })
  ```

  ![image-20200714163617368](./images/Node.js.assets/image-20200714163617368.png)
  
  
  



## 7.2 请求参数的获取

- `GET请求参数`的获取

  - ```js
    server.get('/', (req,res) => {
        res.send(req.query)  // 获取地址栏参数，以对象形式进行存储
    })
    ```
    
    

- `POST请求参数`的获取

  - Express中接收post请求参数需要借助第三方包 `body-parser`

  - ```js
    // 引入body-parser模块
    const bodyParser = require('body-parser');
    // 配置body-parser模块 解析urlencoded格式的请求参数
    server.use(bodyParser.urlencoded({ extended: false }));
    // 接收请求
    server.post('/', (req, res) => {
      console.log(req.body);// 获取POST请求参数，以对象形式进行存储
    }) 
    ```
    
    

- `路由参数`的获取

  - ```js
    server.get('/find/:id', (req,res) => {
        res.send(req.params.id)  // 获取路由参数，以对象形式进行存储 { id: 123 }
    })
    访问地址：http://localhost:3000/find/123
    ```



## 7.3 静态资源访问

- 通过Express内置的**express.static**方法可以方便地`托管静态文件`，例如img、CSS、JavaScript 文件等

  - ```js
    server.use(express.static(path.join(__dirname, 'public')));
    ```

  - 注意：设置了`静态资源访问`后，访问根路由默认访问`静态资源文件夹`下的`index.html`文件

  

- 当浏览器解析的HTML文件需要加载静态资源文件时，会向服务器发送请求，通过静态资源访问，可以自动接收静态资源文件请求，并且响应给浏览器其请求的静态资源文件



## 7.4 模板引擎

- 为了使art-template模板引擎能够更好的和Express框架配合，模板引擎官方在原art-template模板引擎的基础上封装了`express-art-template`

- 使用`npm i art-template express-art-template`命令进行安装

  

- express框架中模板引擎的基本使用：

  - ```js 
    // 当渲染后缀为art的模板时 使用express-art-template
    app.engine('art', require('express-art-template'));
    app.set('views', path.join(__dirname, 'views'));  // 设置模板文件的存放目录
    app.set('view engine', 'art');  // 渲染模板时不写后缀 默认拼接art后缀
    
    app.get('/', (req, res) => {
      // 将模板文件渲染成HTML文件并且返回给浏览器
      res.render('index.art', { 数据 });
    }); 
    ```

  

- app.locals 对象

  - 将变量设置到`server.locals`对象下面，这个数据在所有的模板文件中都可以获取到

  - ```js
    server.locals = {name: 'public'}
    {{ name }}  // public
    ```

  - 当多个模板中需要**抽取公共的数据时**，可以使用以上方法









## 7.5 请求对象和响应对象上的方法

- `request`对象上的方法：

  - ```
    request.query	获取get请求的参数，拿到的是一个对象
    request.params	获取get请求的路由的参数，拿到的是一个对象
    request.body	获取post请求的参数，拿到的是一个对象（要借助第三方模块）
    request.url  获取请求的路由
    ```
    
    

- `response`对象上的方法：

  - ```
    response.send()	给浏览器做出一个响应
    response.download()	告诉浏览器下载一个文件
    response.sendFile()	给浏览器发送一个文件
    response.redirect()	重定向到一个新的地址
    res.status(code)	设置响应状态码
    ```

    

- 注：
  
    - 使用`send`方法，服务器会默认返回给浏览器`200状态码`
    - 如果只是单纯的用**Node写接口**，**响应状态码一般都是设置为200**， 只不过响应的数据不一样

<img src="images/01-Node.js.assets/image-20201228182618802.png" alt="image-20201228182618802" style="zoom:50%;" />









# 八、cookie与session

## 8.1 会话控制

- HTTP协议规定了**一次请求对应一次响应的规则**，在完成了一次请求和一次响应后，浏览器就与服务器断开了，不再有任何关系
- 但是在实际开发中，服务器往往需要向浏览器发送一些数据，***且该数据在多个页面中都能够使用***，这种技术称为`会话控制`
- 通常浏览器与服务器之间互相传递的数据 称为`cookie`和`session`





## 8.2 cookie

### 8.2.1 cookie的理解

- 什么是cookie？

  - **cookie**里面包含着**浏览器和服务器沟通**的数据（交互时产生的信息）

  - **cookie以**：key-value的形式存储。***存储在浏览器的请求头中的***

  - **cookie**中的数据是有过期时间的，超过时间数据会被浏览器自动删除

      ![image-20200719140214124](./images/Node.js.assets/image-20200719140214124.png)

      

      

- cookie工作原理：

  - 当浏览器第一次请求服务器的时候，**服务器可能返回一个或多个cookie给浏览器**
  - cookie中的数据会随着请求被自动发送到服务器端。
  
      <img src="./images/Node.js.assets/image-20200719140337485.png" alt="image-20200719140337485" style="zoom:50%;" />



### 8.2.2 操作cookie

```
npm i cookie-parser
const cookieParser = require('cookie-parser')
app.use(cookieParser())

返回给浏览器一个cookie：
       * res.cookie('username','peiqi',{maxAge:1000*60*60})

       备注：1.cookie是以：key-value的形式存在的，前两个参数分别为：key、value。
            2.maxAge用于配置cookie有效期(单位毫秒)。
            3.如果不传入maxAge配置对象，则为会话cookie，随着浏览器的关闭cookie自动会消失。
            4.如果传入maxAge，且maxAge不为0，则cookie为持久化cookie，即使用户关闭浏览器，
              cookie也不会消失，直到过了它的有效期。

接收浏览器传递过来的cookie：
        * req.cookies.xxx ：获取cookie上xxx属性对应的值
        
删除指定的cookie：
				* res.clearCookie('demo') //删除一个名为demo的cookie
```







## 8.3 session

### 8.3.1 session的理解

- 关于***session***：

  - **存储在服务器中**，存储的是**浏览器与服务器之间沟通的一些数据**

  - ***session***存储在服务器的内存中，每当一个浏览器发来新的请求，服务器都会新开辟出一块空间用于存储***session***，***当服务器关闭或重启时session就会丢失***

    

- **session工作流程**：

  1. 第一次浏览器请求服务器的时候，服务器会开闭出一块**内存空间**，用于存储***session***

  2. 返回响应的时候，会自动给浏览器种下一个***cookie***，**cookie**里面包含着***session***对象中的***编号***

  3. 浏览器再次请求的时候，会携带着该***cookie***给服务器

  4. 服务器根据该**cookie中的session中的编号**，去服务器匹配相关的数据

  5. 服务器根据匹配信息，决定响应给浏览器什么

      

- 注意：

  - ***cookie一定要配合着session使用***
  - 服务器一般会做***session的持久化***，**防止由于服务器重启，导致session的丢失**





### 9.3.2 操作session

```js
1. npm i express-session --save 
2. npm i connect-mongo --save 用于将session写入数据库（session持久化)
3.const session = require('express-session');
4.const MongoStore = require('connect-mongo')(session);

5.编写全局配置对象：
    app.use(session({
      name: 'userid',   //设置cookie的key，默认值是：connect.sid
      secret: 'atguigu', 
      store: new MongoStore({
      	// 将session存储到数据库中，这样服务器重启也不会丢失
        url: 'mongodb://localhost/cookies_container', 
      }),
      cookie: {
        maxAge: 1000*30 // 设置cookie的过期时间
      },
      resave: true,
      saveUninitialized: true,
}));
```

- 编写session全局配置对象时，做了以下事情

  1. 服务器拦截浏览器的所有请求，服务器开闭出一块**内存空间**，用于存储***session***

  2. 返回响应的时候，会自动给浏览器种下一个***cookie***，**cookie**里面包含着***session***对象中的***编号***

      

- 向***session***中`添加`一个属性，：req.session.xxxx = yyy
- `获取`***session***上的xxx属性：const {xxx} = req.session









# 细节补充

## 1. Node.js中路径的相关问题

- 在Node环境下，最好使用***绝对路径***，因为相对路径有时候相对的是命令行工具的当前工作目录，**用相对路径容易造成许多麻烦**

- 在Node中，提供了`__dirname`这个变量，***该变量可以获取当前文件夹的绝对路径***

- 注意：`require()`中的相对路径永远**相对的是当前文件所在的路径**，因此可以不用绝对路径

    


- 绝对路径一般配合和路径模块中的`join`方法配合使用

  - ```js
    const path = require('path')
    let filePaht = path.join(__diranem, '文件路径')
    ```

  - **以上方法得到的文件的路径是一个绝对路径**



## 2. 静态资源访问服务的补充

- 开启了`静态资源访问服务`后，其引入的相关文件必须采用如下格式

  - ```
    ./静态资源所在的文件夹/文件名
    ```

  - 在浏览器解析HTML页面时，会**根据静态资源文件夹和文件名**向服务器发送请求
  
  - 如上写法，相当于加载静态资源时，服务器会返回给浏览器`public文件夹 => 静态资源所在文件夹 => 文件名`下的文件
  
      
  
      

## 3. 第三方模块 ----- dateformat

- 该模块可以帮助我们获取当前的时间，以及处理时间的格式

  - ```js
    let  dateFormat  = require (' dateformat ') ; 
    // 获取当前时间 格式为'年-月份-日期'
    let now = dateFormat (new Date, 'yyyy-mm-dd ') 
    ```

    







## 4. 接收request payload参数

- post请求常见的参数格式：`request payload`、`Form Data`

- 在`express`中解析以上**两种格式参数**需要进行如下配置

    - ```js
        // 配置body-parser模块 解析urlencoded格式的请求参数
        app.use(bodyParser.urlencoded());  // Form Data
        // 解决json格式的请求参数
        app.use(bodyParser.json())  // request payload
        ```

        

    

    

## 5. cookie、session失效



>当**Node.js**中使用了**cors解决跨域**后，就会导致**cookie、session失效**
>



- 解决方案：
    - 方案一：通过**前端**来解决**跨域问题**
    - 方案二：在`Node.js`后端中，通过`global.xxx`**全局对象属性**来**模拟cookie、session**







## 6. 模块化导入json数据

>注：不论是**CommonJS**规范，还是**ES6规范**，都**不需要在json中向外导出**，**直接引入json文件即可**
>

- `CommonJS`语法

    - ```js
        // 该data为导入的json文件下的最外层对象
        const data = require('mock/data.json')
        ```

        

- `ES6模块化`语法

    - ```js
        // 该data为导入的json文件下的最外层对象
        import data from 'mock/data.json'
        ```

        







