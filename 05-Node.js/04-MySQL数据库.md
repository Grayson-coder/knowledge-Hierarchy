# 一、数据库介绍



## 1.1 数据库概述

- 什么是**数据库**？

    - **数据库(DataBase)**  是按照一定的数据结构来组织、存储和管理数据的**仓库**。

      ​    

- 什么是**数据库管理系统**？

    - **数据库管理系统（Database Management System，简称DBMS）**是为管理数据库而**设计的电脑软件系统**，一般具有存储、截取、安全保障、备份等基础功能。

      ​    

- **数据库管理系统**主要分为以下两类：

    - **关系型数据库**和**非关系型数据库**

      ​    

    

## 1.2 关系型数据库

- 什么是**关系型数据库**？

    - **关系型数据库：**结构化数据集，由**行和列**组合而成的**二维表**结构的数据。

        

- 主流的**关系型数据库**：

    - Oracle：运行稳定、功能齐全、性能超群，适用于大型企业。
    - DB2：速度快、可靠性好、处理海量数据急速高效，适用于大中型企业。
    - **MySQL**：开源、体积小、速度快，适用于中小型企业。
    - SQL server：适用于中小型企业，它的特点是全面高效、界面友好易操作，但是不跨平台。







## 1.3 非关系型数据库

- **非关系型数据库：**键值对形式的非结构化数据**集合**

- 常用的**非关系型数据库**：NOSQL、**mongoDB**等。

  ​    



## 1.4 DB、DBMS、SQL三者之间的关系

- **数据库**是长期存储在计算机内、有组织的、统一管理的相关数据的集合。

- **数据库管理系统**（DBMS）是用于管理数据库的**软件**，它对数据库进行统一的管理和控制，以保证数据库的安全性和完整性。

- **SQL**是一种结构化**查询语言**，与**数据库通讯的语言**



<img src="images/05-MongoDB 数据库.assets/image-20201025153440728.png" alt="image-20201025153440728" style="zoom:50%;" />









## 1.5 数据库与后端语言的关系

- **后端语言可以操作数据库的数据**，对其数据进行**增删改查**的操作

    <img src="images/05-MongoDB 数据库.assets/image-20201025155315477.png" alt="image-20201025155315477" style="zoom:50%;" />





- 前端、后端、数据库 三者之间的**交互流程图**

    <img src="images/05-MongoDB 数据库.assets/image-20201025160003967.png" alt="image-20201025160003967" style="zoom:50%;" />



- 现在**遵循前后端分离原则**，前端需要向后端发送请求，**后端需要在数据库中拿数据响应给前端**，然后前端根据数据对页面进行渲染





# 二、邂逅MySQL

## 2.1 MySQL 简介

- 什么是`MySQL`?
    - `MySQL` 是最流行的关系型数据库管理系统，在 WEB 应用方面 MySQL 是**最好的关系数据库管理系统应用软件**之一。

- `MySQL` 支持多种语言。这些编程语言包括 C、C++、Python、Java、Node 和 PHP 等。



## 2.2 RDBMS 相关概念

- 关系型数据库管理系统 = **RDBMS**



- **数据库：**数据库是一些**关联表的集合**。
- **数据表：**数据库中的表看起来像一个简单的**电子表格**。
- **列：** 一列(数据元素) **包含了相同的数据**
- **行：**一行（或**记录**）是**一组相关的数据**
- **冗余**：存储两倍数据，冗余降低了性能，但提高了数据的安全性。
- **主键**：主键是唯一的。**一个数据表中只能包含一个主键**。你可以使用主键来查询数据。
- **外键：**外键用于关联两个表。
- **复合键**：复合键（组合键）将多个列作为一个索引键，一般用于复合索引。
- **索引：**使用索引可快速访问数据库表中的特定信息。索引是对数据库表中一列或多列的值进行排序的一种结构。类似于书籍的目录。
- **参照完整性:** 参照的完整性要求关系中不允许引用不存在的实体。与实体完整性是关系模型必须满足的完整性约束条件，目的是保证数据的一致性。



<img src="images/04-MySql数据库.assets/image-20201010112002132.png" alt="image-20201010112002132" style="zoom:50%;" />

- 表头(header): 每一列的名称;
- 列(col): 具有相同数据类型的数据的集合;
- 行(row): 每一行用来描述某条记录的具体信息;
- 值(value): 行的具体信息, 每个值必须与该列的数据类型相同;
- **键(key)**: 键的值在当前列中具有**唯一性**。







## 2.3 MySQL 安装

- MySQL安装参考教程：https://zhuanlan.zhihu.com/p/37152572

1. 进入MySQL官方网站（https://dev.mysql.com/downloads/installer/）

    <img src="images/04-MySql数据库.assets/image-20201010112930113.png" alt="image-20201010112930113" style="zoom:50%;" />

    <img src="images/04-MySql数据库.assets/image-20201010113120416.png" alt="image-20201010113120416" style="zoom:50%;" />

    <img src="images/04-MySql数据库.assets/image-20201010113348054.png" alt="image-20201010113348054" style="zoom:50%;" />



2. 第一步也可以替换为直接在`前端学习资料\软件安装包\MySql\数据库mysql`下安装5.7版本的MySQL

    <img src="images/04-MySql数据库.assets/image-20201010113446546.png" alt="image-20201010113446546" style="zoom:50%;" />



3. 双击打开MySQL的安装包，开始安装

4. 按下图勾选同意协议，然后下一步

    <img src="images/04-MySql数据库.assets/image-20201010113602233.png" alt="image-20201010113602233" style="zoom:50%;" />



5. 左边界面是安装到了哪一步，下图是选择安装类型，选Server only（只安装mysql），然后点击“next”。

    <img src="images/04-MySql数据库.assets/image-20201010113721428.png" alt="image-20201010113721428" style="zoom:50%;" />

6. 点击Execute开始安装，安装完成后点击next

    <img src="images/04-MySql数据库.assets/image-20201010113806213.png" alt="image-20201010113806213" style="zoom:50%;" />

7. 点击next

    <img src="images/04-MySql数据库.assets/image-20201010113903515.png" alt="image-20201010113903515" style="zoom:50%;" />

8. 默认选第一个，点击“next”继续

    <img src="images/04-MySql数据库.assets/image-20201010113928036.png" alt="image-20201010113928036" style="zoom:50%;" />



9. 默认，继续点击next

    <img src="images/04-MySql数据库.assets/image-20201010114001771.png" alt="image-20201010114001771" style="zoom:50%;" />



10. 设置密码，需要牢记，最好将登陆用户名（是root）和密码（下图的地方设置）记录到其他地方，因为后面要用这个密码连接数据库。**这里我将密码设置为了 123456**，然后点击next

    <img src="images/04-MySql数据库.assets/image-20201010121905251.png" alt="image-20201010121905251" style="zoom:50%;" />



11. 默认点击next继续，如果出现下图红框的警告，表示**要启动的服务名称重复**了，换个其他名称

    <img src="images/04-MySql数据库.assets/image-20201010121954850.png" alt="image-20201010121954850" style="zoom:50%;" />

12. 按下图红框的地方勾选，点击next继续

<img src="images/04-MySql数据库.assets/image-20201010122050679.png" alt="image-20201010122050679" style="zoom:50%;" />



13. 点击执行（Execute）安装

    <img src="images/04-MySql数据库.assets/image-20201010122130337.png" alt="image-20201010122130337" style="zoom:67%;" />



14. 当出现如下界面后，直接点击"Finish"。

    <img src="images/04-MySql数据库.assets/image-20201010122623996.png" alt="image-20201010122623996" style="zoom:50%;" />

    

15. 当出现如下界面后，直接点击"Next"

    <img src="images/04-MySql数据库.assets/image-20201010122704223.png" alt="image-20201010122704223" style="zoom:50%;" />

16. 当出现如下界面后，直接点击"Finish"。完成安装

    <img src="images/04-MySql数据库.assets/image-20201010122746442.png" alt="image-20201010122746442" style="zoom:50%;" />







- 检查MySQL**是否安装成功**

    <img src="images/04-MySql数据库.assets/image-20201010123150608.png" alt="image-20201010123150608" style="zoom:50%;" />

    <img src="images/04-MySql数据库.assets/image-20201010123335471.png" alt="image-20201010123335471" style="zoom:50%;" />

​	

- MySQL**安装目录详解**：

    - `C:\Program Files\MySQL\MySQL Server 5.7`：MySQL数据库这个软件的**安装路径**

        <img src="images/04-MySql数据库.assets/image-20201010124831950.png" alt="image-20201010124831950" style="zoom:50%;" />

        

    - `C:\ProgramData\MySQL\MySQL Server 5.7`：在数据库中创建库、创建表的**数据保存位置**。该文件夹默认是一个**隐藏项目**

        <img src="images/04-MySql数据库.assets/image-20201010125043723.png" alt="image-20201010125043723" style="zoom:50%;" />
    
        





## 2.4 MySQL配置环境变量

- 找到MySQL的**安装目录**：`C\Program Files\MySQL\MySQL Server 5.7`，在该文件夹下的**bin文件夹**中，存储了大量的可执行的**MySQL相关命令**
- 如果我们每次想要执行**MySQL相关命令**，就必须每次切换到其安装目录的bin文件夹下，这样必然麻烦，因此我们可以为其**配置环境变量**，这样就可以直接在CMD窗口中输入MySQL相关命令，并且正常执行





1. 在系统变量中添加**MYSQL_HOME变量**，并写入**MySQL安装目录下的bin文件夹路径**

    <img src="images/04-MySql数据库.assets/image-20201010130103482.png" alt="image-20201010130103482" style="zoom:50%;" />

2. 将**MYSQL_HOME变量**，添加到path系统变量中

    <img src="images/04-MySql数据库.assets/image-20201010130151850.png" alt="image-20201010130151850" style="zoom:50%;" />



3. 打开命令行窗口，执行`mysql -u root -p`命令，该命令用于**连接MySQL数据库**，并且输入MySQL密码

    <img src="images/04-MySql数据库.assets/image-20201010130501099.png" alt="image-20201010130501099" style="zoom:50%;" />

    



## 2.5 MySQL卸载

1. 打开控制面板，将`MySQL`相关的应用全部都卸载掉

2. 打开c盘，将mysql的数据全部清除

    - 删除MySQL文件夹：`C:\ProgramData\MySQL`(隐藏项目)

    - 删除MySQL文件夹：`C:\Program Files\MySQL`
    - 以上两个文件夹都要删除

3. 删除和`MySQL`相关的**系统环境变量**

    <img src="images/04-MySql数据库.assets/image-20201010131035903.png" alt="image-20201010131035903" style="zoom:50%;" />

    

4. windows+R运行“regedit”，打开注册表，删除注册表中MySQL相关目录（**ctrl+f 搜索mysql**）

5. 打开服务，看表中是否有**mysql服务**，没有则说明卸载干净了

6. 如果mysql服务还存在，那么执行以下cmd窗口命令，删除mysql服务

    - ```js
        sc delete mysql
        ```

        



## 2.6 MySQL GUI工具

### 1. 认识navicat

- 什么是`navicat`

    - `MySQL`数据库用于存放数据，客户端`navicat`是为了`方便操作数据库`而设计的一种`图形化软件`。

    - 只要电脑上安装了`navicat`，在任何地方打开电脑，都可以**使用`navicat`方便的连接**到`MySQL`数据库。

    <img src="images/04-MySql数据库.assets/image-20201010132610427.png" alt="image-20201010132610427" style="zoom:50%;" />

    

    

### 2. navicat的安装

- `navicat`官网地址：http://www.navicat.com.cn/products，选择操作MySQL数据的版本进行下载

    ![image-20201115143656993](images/04-MySQL数据库.assets/image-20201115143656993.png)

    - 一键**傻瓜式进行安装**，一直`next`

    

- **破解**navicat步骤：

    1. 安装完成后不要打开，先打开Keygen注册机

        <img src="images/04-MySQL数据库.assets/image-20201115162812117.png" alt="image-20201115162812117" style="zoom:50%;" />

    2. 点击Patch

        <img src="images/04-MySQL数据库.assets/image-20201115162849858.png" alt="image-20201115162849858" style="zoom:50%;" />

3. 点击确定。

    <img src="images/04-MySQL数据库.assets/image-20201115162930421.png" alt="image-20201115162930421" style="zoom:50%;" />

4. 点击Generate，自动生成序列号到软件窗口

    <img src="images/04-MySQL数据库.assets/image-20201115162954200.png" alt="image-20201115162954200" style="zoom:50%;" />



5. 打开**Navicat Premium 15**，点击帮助 --> 注册 ，将注册机获取到的序列号复制到激活码中

    <img src="images/04-MySQL数据库.assets/image-20201115163148471.png" alt="image-20201115163148471" style="zoom:50%;" />

6. 点击手动激活

    <img src="images/04-MySQL数据库.assets/image-20201115163213390.png" alt="image-20201115163213390" style="zoom:50%;" />



7. 复制软件窗口中的请求码

    <img src="images/04-MySQL数据库.assets/image-20201115163234667.png" alt="image-20201115163234667" style="zoom:50%;" />



8. 点击Paste粘贴，然后点击Generate自动生成激活码到软件窗口

    <img src="images/04-MySQL数据库.assets/image-20201115163303966.png" alt="image-20201115163303966" style="zoom:50%;" />



9. 点击激活

    <img src="images/04-MySQL数据库.assets/image-20201115163325448.png" alt="image-20201115163325448" style="zoom:50%;" />





- 注：
    - 如果出现`rsa public key not find`报错信息，可以尝试断网或重装`navicat15`，然后重复以上步骤
    - 安装完成后不要打开，先点击Navicat Keygen进行patch，patch完后再打开软件进行激活操作！





### 3. navicat的使用



#### 连接数据库

- 使用客户端`navicat`连接`MySQL`数据库

    <img src="images/04-MySql数据库.assets/image-20201010132915075.png" alt="image-20201010132915075" style="zoom:50%;" />

    

#### 查看数据库

- 使用客户端`navicat`查看数据库
  
    - <img src="images/04-MySql数据库.assets/image-20201010133104017.png" alt="image-20201010133104017" style="zoom:50%;" />



<img src="images/04-MySQL数据库.assets/image-20201101174223067.png" alt="image-20201101174223067" style="zoom:50%;" />



- **查看数据表**
    - <img src="images/04-MySQL数据库.assets/image-20201101174701488.png" alt="image-20201101174701488" style="zoom:50%;" />











#### 创建数据表

1. 点击**数据库 --> 表 --> 新建表**

    <img src="images/04-MySQL数据库.assets/image-20201101175051918.png" alt="image-20201101175051918" style="zoom:50%;" />





2. 点击保存后输入表名，就创建成功了一个表

    <img src="images/04-MySQL数据库.assets/image-20201101175137083.png" alt="image-20201101175137083" style="zoom:67%;" />







#### 导入数据表

- 使用客户端`navicat`导入**SQL文件**

    - **SQL文件中可以有大量的SQL语句**，可以用于新建多个表

    <img src="images/04-MySql数据库.assets/image-20201010133835877.png" alt="image-20201010133835877" style="zoom:50%;" />



#### 导出单个数据表

- 选择要导出的**数据表然后右键**，点击转储**SQL文件**

    <img src="images/04-MySQL数据库.assets/image-20201102172454909.png" alt="image-20201102172454909" style="zoom:50%;" />





#### 导出多个数据表

- 可以将**数据库中的所有表导出到一个SQL文件上**

    ​	① 选择数据库 ② 右键转储SQL文件 ③ 选择结构和数据

    <img src="images/04-MySQL数据库.assets/image-20201115164035405.png" alt="image-20201115164035405" style="zoom:50%;" />



<img src="images/04-MySQL数据库.assets/image-20201115164118074.png" alt="image-20201115164118074" style="zoom:50%;" />





#### 修改表格列的宽度

- 右键表格列，显示--> 修改表格列宽

    <img src="images/04-MySQL数据库.assets/image-20201116112048966.png" alt="image-20201116112048966" style="zoom:50%;" />







# 三、Node.js操作MySQL

## 3.1 连接MySQL数据库

1. **安装**MySQL第三方包：`npm install mysql --save`

2. **引入**MySQL包 

    - ```js
        const mysql = require('mysql')
        ```

3. **创建数据库连接对象**

    - ```js
        const db = mysql.createConnection({
                    host   : 'localhost', // 主机ip地址
                    user   : 'root',  // MySQL用户名
                    password : '123456', // MySQL密码
                    database : 'test',  // 要连接的数据库名
          			 prot: 3306,  // 数据库端口号
                  });
        ```

4. 调用连接对象的`connect方法`开始**连接MySQL数据库**

    - ```js
        db.connect(err => {.....});
        ```

        

- 注：只有与数据库**建立连接**之后，才能对数据库进行**增删改查**的操作





## 3.2 SQL语句

- 与**MongoDB**不同的是：
    - 在Node下对**MongoDB**数据库进行增删改查操作都是**基于现有的API操作**
    - 而在Node下对**MySQL**数据库进行增删改查操作都是通过**SQL语句**



- 在连接**MySQL**数据库后，可以通过**连接对象**的`query`方法，对数据库进行**增删该查**的操作

    - ```js
        // db为连接MySQL数据库连接对象
        db.query('sql语句', (err, res) => {
          if (err) ....
          console.log(res)
        })
        ```

        

- `query`方法接收两个参数，**第一个参数**为字符串类型的**SQL语句**，**常见的SQL语句**如下
    - 新增表中数据：`insert into 表名(字段,字段) values(值,值)`

    - 删除表中数据：`delete from 表名 where 条件`

    - 修改表中数据：`update 表名 set 字段=值 where 条件    `
    - 查询表中数据：`select 字段,字段/* from 表名 where 条件`



- `query`方法接收两个参数，**第二个参数**为**回调函数**，该回调函数会在SQL语句执行完成后调用，并且**接收二个参数**
    - 第一个参数：**错误信息**，如果SQL语句执行失败，会会有相应的错误提示
    - 第二个参数：SQL语句执行成功时，**返回的对应数据**，根据**不同的操作会有不同的返回数据**







## 3.3 创建数据表

- **创建数据表**的SQL语句：`CREATE TABLE 数据表名(字段 字段类型,...PRIMARY KEY(指定主键字段))`

    - ```js
        // 创建数据表的SQL语句
        const sql = 'CREATE TABLE user(id int AUTO_INCREMENT,title VARCHAR(255),body VARCHAR(255),PRIMARY KEY(id))'
        
        // 执行创建数据表操作
        db.query(sql, (err, res) => {
            if (err) return console.log(err); 
            console.log(res);
        })
        ```

        

- 如果没有错误信息，则说明数据表已经创建完成了，此时打开**navicat**工具，可以看到**新建的数据表**

    <img src="images/04-MySQL数据库.assets/image-20201101190554979.png" alt="image-20201101190554979" style="zoom:67%;" />

<img src="images/04-MySQL数据库.assets/image-20201101190920478.png" alt="image-20201101190920478" style="zoom:50%;" />





- 数据表名最好以**全部小写来命名**





## 3.4 查询数据

- **查询数据表数据**的SQL语句：`select * from 表名 where 条件`

    - ```js
        const sql = 'select * from studentInfo' // 查询数据表中所有数据
        
        db.query(sql, (err, res) => {
            if (err) return console.log(err); 
            console.log(res);
        })
        ```

        

- 执行以上代码输出的结果为：

    <img src="images/04-MySQL数据库.assets/image-20201101191540129.png" alt="image-20201101191540129" style="zoom:50%;" />





## 3.5 添加行数据

- **添加行数据**的SQL语句：`insert into 表名(字段,字段) values(值,值)`

    - ```js
        const sql = "insert into studentinfo(name, age, sex) value('隔壁老王', 18, '男')"
        
        db.query(sql, (err, res) => {
            if (err) return console.log(err); 
            console.log(res);
        })
        ```

        

- 打开**navicat**工具，**查看**添加的行数据是否有添加到数据表中

    <img src="images/04-MySQL数据库.assets/image-20201101192202010.png" alt="image-20201101192202010" style="zoom:50%;" />



- 如果添加的数据其字段类型是`datetime`时间格式类型，那么在js文件中，需要将**当前时间格式进行转换**，然后再**执行SQL语句**，才能**添加时间数据**

    - ```js
        // 时间格式转换方法
        function timeFommater(value) {
            var dateee = new Date(value).toJSON();
            var date = new Date(+new Date(dateee) + 8 * 3600 * 1000).toISOString().replace(/T/g, ' ').replace(/\.[\d]{3}Z/, '')
            return date;
        }
        
        let date = timeFommater(Date.now())
        let sql = `insert into wish( time) value('${date}')`
        ```

        













## 3.6 删除行数据

- **删除行数据**的SQL语句：`delete from 表名 where 条件`

    - ```js
        // 删除studentinfo表中 name字段为‘隔壁老王’的数据
        const sql = "delete from studentinfo where name='隔壁老王'"
        
        db.query(sql, (err, res) => {
            if (err) return console.log(err); 
            console.log(res);
        })
        ```

        

- 打开**navicat**工具，**查看**删除的行数据是否还存在数据表中





## 3.7 修改行数据

- **修改行数据中单个字段**的SQL语句：`update 表名 set 字段 = 值 where 条件`

    - ```js
        // 将 studentinfo表 中name字段为‘张三’行数据，将该行数据的age字段值修改为了88
        const sql = "update studentinfo set age = 88 where name = '张三' "
        
        db.query(sql, (err, res) => {
            if (err) return console.log(err); 
            console.log(res);
        })
        ```

        

- **修改行数据中多个字段**的SQL语法：`update 表名 set 字段 = 值, 字段 = 值 where 条件`

    - ```js
        // 将name为张三的行数据中的age字段改为了88， name字段改为了王五
        const sql = "update studentinfo set age = 88, name=‘王五‘ where name = '张三' "
        ```

        



- 打开**navicat**工具，**查看**修改的行数据是否生效

    <img src="images/04-MySQL数据库.assets/image-20201101193621732.png" alt="image-20201101193621732" style="zoom:50%;" />







## 3.8 查询字段包含某个字符数据

- SQL语句：`select * from users where tags like '%ios%'`
    - 上面语句表示查询**users数据表**中，**tags字段**中 所有**包含ios的行记录**



<img src="images/04-MySQL数据库.assets/image-20201229173519956.png" alt="image-20201229173519956" style="zoom:50%;" />







































































































































