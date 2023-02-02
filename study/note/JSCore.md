#                     JSCore

### 1、声明提升

var声明的变量带有声明提升；

学习js语言必须知道的一个特征：其他编程语言都没有的特征；

为什么其他语言都没有这个特征？因为此特征特别垃圾；

js语言在运行时，实际代码分为两次运行：

第一次：先找到所有的声明操作（var/function/let/const/class），提取到顶部；

第二次：再执行提升后的代码；

js中：眼见不一定为实，底层会隐式，先提升，再执行提升后的代码

var 和 function 都是声明, 谁先谁后?

 JS的作者从来没有明确说明过到底谁先谁后 ；

但是先后顺序不重要 ；

函数提升时 会携带函数体；

 var提升时, 只提升变量声明没有值 ；

不管谁先写谁后写, 提升后的值 都是函数；

```
 <!-- HTML中, 有两个特殊的标签 -->
  <!-- style: 其中用于书写 css 代码 -->
  <!-- script: 其中用于书写 JavaScript 代码 -->
  <script>
    // function: 用于声明函数
    // 函数就是把 一段代码保存起来, 起了个名字
    // 注意: 函数必须调用之后, 才能执行{}中的代码
    // 调用函数的格式:   函数名().  通过()来触发
    
    // JS的反人类设计: 不能按照正常人的阅读顺序来理解代码
    // 你所见到的 并非 JS 实际运行时的模样
    // 因为JS拥有: 声明提升的机制

    // 声明: 制作出来一个变量 就叫声明 -- 变量出生的时候
    // 用于声明变量的关键词: var/function + let/const/class
    a()
    function a(){
      console.log(111)
    }
    var a //声明了变量a
    var b //声明了变量b
    function c(){} //声明了函数c
   </script>
   <script>
    // 在阅读JS代码时, 一定不要当正常人
    // 正常人: 从上向下阅读
    // JS具有声明提升特征:  先隐式调整代码的顺序, 然后再执行
     function b(){
       console.log(111)
     }
     b()
     function b(){
       console.log(222)
     }
     b()
   </script>
```

![Snipaste_2022-04-27_09-47-31](D:\WEBStudyRecord\Notes\typora-images\Snipaste_2022-04-27_09-47-31.png)

![Snipaste_2022-04-27_09-53-01](D:\WEBStudyRecord\Notes\typora-images\Snipaste_2022-04-27_09-53-01.png)

![Snipaste_2022-04-27_10-23-35](D:\WEBStudyRecord\Notes\typora-images\Snipaste_2022-04-27_10-23-35.png)

![Snipaste_2022-04-27_10-48-54](D:\WEBStudyRecord\Notes\typora-images\Snipaste_2022-04-27_10-48-54.png)

### 2、作用域（scope）

断点调试

![Snipaste_2022-04-27_11-57-12](D:\WEBStudyRecord\Notes\typora-images\Snipaste_2022-04-27_11-57-12.png)

作用域是一类有特殊操作的对象类型的称呼

- 全局
- 局部、函数
- 块级
- 脚本

宿主环境：js运行在哪个平台上，这个平台就称为js的宿主环境

- node.js： 操作数据库/网络请求/操作文件系统...
- 浏览器：提供了操作浏览器相关的技能包
- 存储在window对象中，此对象也称为全局作用域
- 因为利用var/function声明的变量，都会自动存储在window里

```
 <script>
    // JS有4种作用域: 全局 函数 脚本 块级
    // 专业名词: 宿主环境 -- 被寄生的就叫宿主
    // JS语言有两种常见的宿主: node.js 和 浏览器
    // JS寄生在宿主上之后, 就可以使用宿主的各种功能
    // JS寄生在浏览器上时, 就拥有了操作浏览器的各种技能
    // 这些技能存储在 浏览器提供的 window 对象属性中
    console.log(window);
    console.log(typeof window); // object:对象类型
    // 作用域 就是 一个特殊的对象类型的值
    // window对象,就是浏览器提供的全局作用域
    // 使用 var 在脚本中声明的变量, 就会存储在全局作用域 window对象里
    var aa = 'AAA'
    function aab() { }
    // 用法1: 读取 全局作用域 window对象中的值
    console.log(window.aa);
    // 用法2: 直接用变量, 默认会从全局作用域获取
    console.log(aa);
  </script>
```

var具有全局变量污染特征：

全局window

var声明的变量会自动存储在window中，导致window原有的结构被污染了

### 3、局部作用域

函数在运行时, 会自动创建一个对象, 用来保存函数中声明的变量 

这个特殊的对象就称为: 函数作用域  也叫 局部作用域 

局部作用域 和 全局作用域 是独立关系, 互相不影响

因为函数运行时创建 作用域对象, 在 函数运行结束后 会自动销毁 

所以, 必须利用 断点调试 功能才能查看到 这个特殊的作用域对象



```
 <script>
    // 2015年之前, 即ES6 -- JS的第六次升级版本 前
    // 只有两种作用域: 全局 , 局部(函数)
    function a() {
      var x = 11
      var y = 22
      var z = 33
      console.log(x, y, z);
    }
    // 注意: 函数需要调用才能触发
    // 调用时, 会触发 {} 中的代码, 并制作一个 局部作用域--对象类型
    // 需要浏览器提供的 断掉调试 软件, 来查看函数运行时的作用域
    a()
  </script>
```

### 4、脚本作用域

```
 <!-- 
    由于 var 在 script 中声明的变量, 自动出现在 window 对象里,
    而 window 对象是浏览器提供的 用于存储 系统方法 的对象

    把自定义的变量存储在 window 中, 会造成全局变量污染
    所在 从 2015年开始 的 第六个JS版本, 称为 ES6 
    提供了新的脚本作用域, 专门存储 自定义的 变量
  -->
  <script>
    // var在 script 声明的变量, 存储在 window 对象里
    // 和系统提供的内容 混合在一起: 全局变量污染
    var aa = 'AAA'

    // let/const : ES6中提供的 声明变量的 关键词
    // 在 script 中声明的变量, 存储在 script 对象里 而非 window
    // 避免的全局变量污染
    let bb = 'BBB'
    // 取舍:
    // 理论上: 推荐用 let/const 代替 var  -- var就特性,被淘汰!
    // 实际上: 为了兼容性的考虑, 对于2015年之前的浏览器--IE8
    //        -- 有些政府项目中, 要考虑适配 旧版本浏览器, 只能用var
    console.log('-----');
  </script>
```

### 5、块级作用域

```
 // 块级: 由 ES6 中提供的作用域, 类似 局部作用域
    // {} 配合 let/const 使用, 就会生成独立的块级作用域对象
    // 但是 var 对块级无效, 依然在全局中
    // 代码中: if  for while switch 都有 {}, 会产生块级
    {
      let a = 5
      const b = 6
      var c = 7
      console.log('....');
    }
    function d() {
      // 函数的{} 不会产生块
      // 依然是 函数作用域
      let a
      {
        // 依然形成块级作用域
        let b
        console.log(b);
      }
      console.log(a);
    }
    d()
  </script>
```

### 6、作用域链

含义：**按照代码的书写位置，函数中使用一个变量时，会先在自身作用域中查找，如果自身没有则向上一级作用域查找--就近原则**

 当使用一个变量时，会按照就近原则，到作用域链中查找并使用

​    //细节：查找时 向上层作用域中查找

​    //找祖宗不找儿子

```
 // JS中, 代码结尾的分号 非必备, 是可选的
    // 由于大家越来越懒.. 现在很多人习惯不写 分号
    // undefined: 声明了但是没赋值
    // undeclare: a is not defined 代表变量不存在, 即没声明
    // 当使用一个变量时, 会按照就近原则, 到作用域链中查找并使用
    // 细节: 查找时 向上层作用有中查找
    // 找祖宗 不找 儿子
    var a = 11
    function b() {
      var a = 22;
      // 函数的自调用  (function(){})()
      // 细节: 自调用写法 和 上一行代码之间 必须有 分号 间隔
      (function () {
        var a = 33
        function c() {
          var a = 44
        }
        c()
        // 如果 a = 33 不写, 会到上层作用域中查找
        // 不会到 c 中查找
        console.log(a) //??
      })()
    }
    b()
  </script>
```



### 7、闭包（closure)

#### 1、含义

**函数在声明时，会保存其所在的词法作用域到自身的scopes属性里，其中如果词法作用域是函数作用域的话，就称为闭包；**

JS的固有设定:当一个函数出生时，会自动保存其所在的`词法作用域`（所在的作用域们）；

词法作用域有四类：全局、脚本、块级、闭包（函数/局部）；

函数作用域的别名:闭包的本质就是局部作用域，只是在当前场景，称为闭包；

闭包的形成：必须是外部函数中声明了内部函数，此时外部函数就是内部函数的闭包；

存储在函数的scopes属性里；

为什么要存？以后函数不管在哪里使用，永远都是曾经的--携带固有属性；

这些固有的作用域中，函数作用域称为闭包；

当你听到闭包这个词：就应该知道这是个函数作用域，被保存在另一个函数的scopes里了。（b函数作用域，被保存在c函数的scopes里，此时就说b是c的闭包）

#### 2、闭包的缺点

**本来函数作用域会自动销毁，由于闭包的保存操作，不再自动销毁，浪费内存。**

函数分为两种状态：静态和动态

- 静态：声明函数--闭包存储在静态的函数中
- 动态：调用函数--执行的时候会使用到闭包里面的值

#### 3、闭包的作用

- 在ES6之前，只用两种作用域：全局、局部
- 通过var声明的变量，存储在全局里，造成全局变量污染
- 闭包：可以把变量声明在函数作用域中，避免全局变量污染
- 制作私有的变量，避免全局变量污染

应用：

```
 <!-- 
    闭包的设计的缺点:
    - 正常 函数执行时 会形成 局部作用域对象, 当函数执行结束时, 这个对象会销毁, 来节省内存
    - 但是: 闭包机制会导致 函数作用域 被保存到另一个函数中, 无法释放. 导致内存的浪费
    所以: 在ES6中, 提供了 块级作用域的写法, 来代替闭包
    由于兼容性 和 习惯: 闭包依然非常常见
   -->
  <script>
    // 闭包作用: 为函数提供私有变量, 避免全局污染 -- ES6之前
    // 例如: 记录一个函数的调用次数
    // var声明的变量, 存储在 window 全局中: 污染全局变量
    // 如何避免全局污染??  let/const -- ES6  2015年出现
    // 2015年之前 靠什么?  需要闭包 -- 提供一个函数作用域来存储变量
    console.log(window);
    // 习惯使用匿名函数自调用, 来提供一个函数作用域
    // 声明变量, 保存函数的返回值; 此时就可以在外部使用b
    var b = (function () {
      // 在匿名函数作用域中, 声明变量: 不在全局区 就没有全局污染
      var count = 0
      function b() {
        // var count = 0
        count++
        console.log('调用了第' + count + '次');
      }
      // 通过return 把b暴露到外部  -- return 大腰子
      return b
    })()
    // 目的是:让count变成私有的, 避免全局污染
    console.dir(b) // 查看 count 是不是存在 scopes 里
    b()
    b()
    b()
    b()
  </script>
```



### 8、总结

1、 对闭包的理解

**闭包是指有权访问另一个函数作用域中变量的函数**，创建闭包的最常见的方式就是在一个函数内创建另一个函数，创建的函数可以访问到当前函数的局部变量。

2、闭包有两个常用的用途；

\- 闭包的第一个用途是使我们在函数外部能够访问到函数内部的变量。通过使用闭包，可以通过在外部调用闭包函数，从而在外部访问到函数内部的变量，可以使用这种方法来创建私有变量。

\- 闭包的另一个用途是使已经运行结束的函数上下文中的变量对象继续留在内存中，因为闭包函数保留了这个变量对象的引用，所以这个变量对象不会被回收

3、 浏览器的垃圾回收机制

 （1）垃圾回收的概念

**垃圾回收**：JavaScript代码运行时，需要分配内存空间来储存变量和值。当变量不在参与运行时，就需要系统收回被占用的内存空间，这就是垃圾回收。

**回收机制**：

\- Javascript 具有自动垃圾回收机制，会定期对那些不再使用的变量、对象所占用的内存进行释放，原理就是找到不再使用的变量，然后释放掉其占用的内存。

\- JavaScript中存在两种变量：局部变量和全局变量。全局变量的生命周期会持续要页面卸载；而局部变量声明在函数中，它的生命周期从函数执行开始，直到函数执行结束，在这个过程中，局部变量会在堆或栈中存储它们的值，当函数执行结束后，这些局部变量不再被使用，它们所占有的空间就会被释放。

\- 不过，当局部变量被外部函数使用时，其中一种情况就是闭包，在函数执行结束后，函数外部的变量依然指向函数内部的局部变量，此时局部变量依然在被使用，所以不会回收。

（2）垃圾回收的方式

浏览器通常使用的垃圾回收方法有两种：标记清除，引用计数。

 （1）标记清除

\- 标记清除是浏览器常见的垃圾回收方式，当变量进入执行环境时，就标记这个变量“进入环境”，被标记为“进入环境”的变量是不能被回收的，因为他们正在被使用。当变量离开环境时，就会被标记为“离开环境”，被标记为“离开环境”的变量会被内存释放。

\- 垃圾收集器在运行的时候会给存储在内存中的所有变量都加上标记。然后，它会去掉环境中的变量以及被环境中的变量引用的标记。而在此之后再被加上标记的变量将被视为准备删除的变量，原因是环境中的变量已经无法访问到这些变量了。最后。垃圾收集器完成内存清除工作，销毁那些带标记的值，并回收他们所占用的内存空间。

4、 对作用域、作用域链的理解

（1）全局作用域和函数作用域

（1）全局作用域

\- 最外层函数和最外层函数外面定义的变量拥有全局作用域

\- 所有未定义直接赋值的变量自动声明为全局作用域

\- 所有window对象的属性拥有全局作用域

\- 全局作用域有很大的弊端，过多的全局作用域变量会污染全局命名空间，容易引起命名冲突。

（2）函数作用域

\- 函数作用域声明在函数内部的变量，一般只有固定的代码片段可以访问到

\- 作用域是分层的，内层作用域可以访问外层作用域，反之不行

（3）块级作用域

\- 使用ES6中新增的let和const指令可以声明块级作用域，块级作用域可以在函数中创建也可以在一个代码块中的创建（由`{ }`包裹的代码片段）

**\- let和const声明的变量不会有变量提升，也不可以重复声明**

\- 在循环中比较适合绑定块级作用域，这样就可以把声明的计数器变量限制在循环内部。

**作用域链：** 在当前作用域中查找所需变量，但是该作用域没有这个变量，那这个变量就是自由变量。如果在自己作用域找不到该变量就去父级作用域查找，依次向上级作用域查找，直到访问到window对象就被终止，这一层层的关系就是作用域链。

作用域链的作用是**保证对执行环境有权访问的所有变量和函数的有序访问，通过作用域链，可以访问到外层环境的变量和函数。**

作用域链的本质上是一个指向变量对象的指针列表。变量对象是一个包含了执行环境中所有变量和函数的对象。作用域链的前端始终都是当前执行上下文的变量对象。全局执行上下文的变量对象（也就是全局对象）始终是作用域链的最后一个对象。

当查找一个变量时，如果当前执行环境中没有找到，可以沿着作用域链向后查找。

### 9、函数的arguments

函数隐式带有一个arguments属性，其中存储了函数收到的所有参数；

  arguments是个对象类型，只是这种属性名是0 1 2 3...跟数组很相似而已，这样的对象称为伪数组，像数组但是没有数组的各种方法

### 10、函数的重载

概念：通过判断参数的数量或类型来执行不同的逻辑代码；

优点：让一个函数具有多种作用，功能更加强大

依赖函数自带的 arguments 属性:  存储函数接收的所有参数 

利用 arguments 来判断 函数接受的参数数量 ；

或者 从arguments 中读取参数, 判断其类型；

判断是否为数组：Array.isArray(参数)  输出结果ture flase；

```
function getSum() {
            if (arguments.length == 1 ) {
                var sum = 0
                for (var i = 0; i <= arguments[0]; i++) {
                    sum += i
                }
                console.log(sum)
            } 
            if(arguments.length==2) {
                var sum = 0
                for (var i = arguments[0]; i < arguments[1]; i++) {
                    sum += i
                }
                 console.log(sum)
            }
            if(arguments.length==3) {
                var sum = 0
                for (var i = arguments[0]; i < arguments[1]; i+=arguments[2]) {
                    console.log(i)
                    sum += i
                }
                 console.log(sum)
            }
        }
        getSum(100)
        getSum(50, 100)
        getSum(50,200,2)
```

### 11、对象的访问器语法

对象.属性名：在点语法中，就是个属性名，不会变化

对象[ ]：方括号中是JS代码，其中的变量会换算成值

### 12、对象是引用类型

内存分两种：

把内存想象成是一本字典/书：分为两个部分 目录和详情页

为什么？：目录记录简单的标题，其中存储详情的页数，通过页数找到存放详细内容的页（目录的内容少，查询速度快）

栈内存：相当于目录，存储少量数据，查询速度快

堆内存：相当于详情页，存储大量数据，拥有一个固定的页数

在js中，基础数据类型属于少量数据的范畴

- number
- Boolean
- null
- undefined
- string
- symbol
- bigInt

#### 1、栈内存

**基本数据类型**，赋值时，值传递

#### 2、堆内存

对象类型：属于存很多数据的类型，{}中可以存储任意数量的数据

在内存中存储在堆内存中，相当于书本中的详情页，带有一个页号；

对象是引用（内存地址）类型

#### 3、js数据类型

JS的数据类型有哪些? 

 基本数据类型: string boolean number null undefined + symbol bigInt 

 在 ES6 2015年 新增了 symbol(唯一,做属性名用)  bigInt(大整型) 

  引用/对象类型: object 

### 13、拷贝、克隆（clone）

![Snipaste_2022-04-28_20-09-28](D:\WEBStudyRecord\Notes\typora-images\Snipaste_2022-04-28_20-09-28.png)

```
 var x = { num: 10, ename: 'mike', age: 18 }
    // 克隆 x 对象: 分两步
    // 1. 创建1个空对象
    var y = {}
    // 2. 遍历x对象, 把其中的属性挨个存入空对象里
    // for..in.. 用于遍历对象
    for (var key in x) {
      // key: 是 x 对象中的属性
      console.log('key:', key);
      var value = x[key] // 对象 方括号取值
      // 把值存储在 y 这个空对象里
      y[key] = value
    }
    console.log('x:', x);
    console.log('y:', y);
    // 对比是否是同一个
    console.log('x == y:', x == y) //false: 不是同一个
    // 因为 x 和y 非同一个, 所以x的修改 不会影响 y
    x.age = 99
    console.log(y.age) // 18
```

### 14、函数的this

代表函数运行时所在的对象

```
// 全局中声明, 存储在window里
    function show() {
      // this: 这个
      console.log('我是:', this);
    }
    show() // 猜猜this

    var emp1 = { ename: '亮亮' }
    emp1.show = show // show函数存储到 emp1 里
    emp1.show()
    var emp2 = { ename: '娅楠', show: show }
    emp2.show()
    var a = 10
    var b = 20
    function c() { console.log(this) }
    // 属性名: 值(JS代码)
    // 简化语法: 属性名和值一样, 可以简化成一个 {b:b} -> {b}
    var obj = { num: 10, count: a, b, c: c }
    // 相当于
    obj.b = b
    obj.c() // 打印的this是什么
    console.log(obj)
    // 粗暴理解: 
    // 对象.方法()  : 方法中的this 就是前面的对象
    // 我.打亮亮() : 主语是   我
    // 涛哥.打亮亮() : 主语是 涛哥
    // 楠姐.打亮亮() : 主语是 楠姐
    // emp2.打亮亮() : this 就是 emp2
    // emp3.打亮亮() : this 就是 emp3
    var e1 = {
      name: '楠姐',
      打亮亮: function () {
        console.log(this, "在打亮亮");
      }
    }
    e1.打亮亮()
    // 函数中的this: 代表谁在使用
    var e2 = { name: '涛哥', 打亮亮: e1.打亮亮 }
    e2.打亮亮()
    // 面试的考点: 存储在window中的属性, 在使用时可以省略前缀
    var 打亮亮 = e1.打亮亮
    // window.打亮亮()
    打亮亮() //没有前缀 触发的方法, 都是window里的
```

#### 1、对象的创建方式

语法糖: 作者提供的简化语法, 使用起来非常方便, 让人感觉幸福, 所以像吃糖一样甜蜜! 

 创建一个对象, 通常分两种方式

1. 字面量: 一种语法糖,简化创建 

2. 构造方式 

```
 // 数组的语法糖: 字面量
    var names = ['mike', 'lucy', 'lily']
    console.log(names);
    // 构造方式
    var names = new Array('tom', 'jerry', 'shirley')
    console.log(names);
    // 对象类型
    var emp = { name: '亚楠', age: 18, phone: '18332434344' }
    console.log(emp);
    // 构造方式
    var emp = new Object()
    emp.name = '凯凯'
    emp.age = 32
    emp['phone'] = '15534343444'
    console.log(emp);
    // 函数
    function aa(a, b) { console.log(a + b) }
    // 函数的构造写法:  前几个参数 是形参, 最后一个是函数体
    var bb = new Function('a', 'b', 'console.log(a + b)')
    console.log(bb);
    bb(20, 40)
```

#### 2、this的作用

在对象中复用函数，省内存

```
 // 矩形
    // 1个矩形, 长10  宽5   拥有方法area 来计算面积
    var r1 = {
      length: 10,
      width: 5,
      area: function () {
        // 长 x 宽
        return this.width * this.length
      }
    }
    console.log(r1);
    console.log(r1.area());
    // 创建r2对象, 长 20, 宽 30   area方法 算面积
    var r2 = {
      length: 20,
      width: 30,
      area: function () {
        return this.width * this.length
      }
    }
    console.log(r2.area());
    // 创建r3对象, 长 120, 宽 35   area方法 算面积
    var r3 = {
      length: 120,
      width: 35,
      area: function () {
        return this.width * this.length
      }
    }
    console.log(r3.area());
    // 思考1: r1 r2 r3 中都有area函数, 函数体一模一样
    // 他们是同一个函数吗??
    console.log(r1.area == r2.area) //不是同一个
    // area在不同的对象中声明的, 所以并非同一个函数
    // 思考2: 有必要吗?  同样功能的函数 声明3个 在不同对象里
    // 没必要, 浪费内存, 一个足够了
    // 怎么办?  提取area函数放在外面 共享即可
    function area() { return this.width * this.length }
    var r4 = {
      width: 100,
      length: 200,
      // area: area  语法糖: 属性名和变量名相同, 可以合写
      area
    }
    console.log(r4.area());
    // r5:  宽300, 长100  area方法
    var r5 = { width: 300, length: 100, area }
    console.log(r5.area()); // 函数()  ()是调用函数, 让函数运行
    // 思考1: r4的area 和 r5的area 是否相同?   是
    // 因为都引用的同一个函数
    console.log(r4.area == r5.area) // true
    // 思考2: 为什么函数书写在外部, 引入到不同的对象里, 就能为所在的对象服务??
    // 因为 灵活的 this 关键词: 函数在哪个对象里执行, 就代表哪个对象
    // this是特别好用的特性: 实现节省内存, 在不同对象里复用函数
```

#### 3、构造函数

构造函数的两件事

this关键词：把对象中共同的方法，提取到外部存储

构造函数：自动化思想，把制作对象的步骤，封装成函数，调用函数即可自动完成对象的创建

```
 function salary_year() {
      return this.salary * 12
    }
    // 变量名: 见名知意
    function Employee(ename, age, salary) {
      // 1.制作一个空对象
      var obj = {}
      // 2.把传入的参数存储在对象里
      obj.ename = ename
      obj.age = age
      obj.salary = salary
      obj.salary_year = salary_year
      // 3.返回制作完毕的对象
      return obj
    }
    // e2   凯凯  32  15000
    var e2 = Employee('凯凯', 32, 15000)
    console.log(e2.salary_year());
```

### 15、原型链

![live-parent_2821465_16511988275576](D:\WEBStudyRecord\Notes\typora-images\live-parent_2821465_16511988275576.jpeg)

- 对象的`__proto__`的特性：对象.属性时，自己没有，则到`__proto__`中查找
- 构造函数共享的方法，存储在 函数.prototype 对象里---避免全局污染
- 神奇： `对象.__proto__=函数.prototype`

![image-20220429110240767](D:\WEBStudyRecord\ThirdState\jscore1\Day03\JSCORE03.assets\image-20220429110240767.png)

![image-20220429102032793](D:\WEBStudyRecord\ThirdState\jscore1\Day03\JSCORE03.assets\image-20220429102032793.png)

![image-20220429114533825](D:\WEBStudyRecord\ThirdState\jscore1\Day03\JSCORE03.assets\image-20220429114533825.png)

![image-20220429113952207](D:\WEBStudyRecord\ThirdState\jscore1\Day03\JSCORE03.assets\image-20220429113952207.png)

### 16、new运算符

```
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>new运算符</title>
</head>

<body>
  <script>
    // new运算符: 作者提供的用来简化 构造函数 的运算符

    // 矩形: 长 和 宽; 面积 和 周长 方法;
    // 对象中存储的内容分两类: 函数(共享-prototype) 和 非函数(值)
    function Rectangle(length, width) {
      // new运算符的作用: 自动隐式完成一些固定的代码
      // 1. 创建空对象  var this = {} -- 固定的变量名叫 this
      // 2. 设置this的父: this.__proto__ = 函数.prototype
      // 3. return this

      // 纠结的点: this关键词
      // 作者偏爱 this 这个单词, 所以在不同的场景 赋予其 不同的能力
      // 函数触发时, this代表其所在的对象
      // 楠姐.打亮亮() : 打亮亮方法中的this 就是 楠姐
      // 
      // new 函数(): this是创造的那个对象

      this.length = length
      this.width = width
    }

    // 共享的方法存 prototype 对象
    Rectangle.prototype.area = function () {
      return this.width * this.length //面积
    }

    Rectangle.prototype.perimeter = function () {
      return (this.width + this.length) * 2
    }

    // 使用:  new运算符 来触发构造函数
    var r1 = new Rectangle(10, 5)
    console.log(r1);

    console.log(r1.area());
    console.log(r1.perimeter());

  </script>
</body>

</html>
```

### 经典面试题

```
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>面试题</title>
</head>

<body>
  <script>
    var a = 10

    function test() {
      // new隐式做了什么?
      // 作用域链: 自己有的变量用自己的, 自己没有才用别人的
      // var this = {}
      // 此处的this.a 赋值给 构造出来的空对象 而不是 window
      this.a = 20
      // test(): this是window, window.a = 20
    }

    new test()
    console.log(a)  // 10 - window.a

    // 楠姐.打亮亮() :  this是楠姐
    // 打亮亮() : 隐藏的前缀是 window
    test() // this就是window
    // window.test()
    console.log(a) // 20

  </script>

  <script>
    var aaa = 1

    function Demo() {
      console.log(this);
      console.log(this == window) // true
      this.aaa = 999 // window.aaa = 999
    }

    // window.aa = 20 // 对象的属性赋值

    Demo() //看this是什么
    console.log(aaa) // 999

    // 理解1:
    // var a = 1
    // window.a = 999
    // a?    是9999

    // 理解2:
    // var a = 1
    // function demo(){ window.a = 999 }
    // demo() //触发函数完成赋值
    // a?   是999
  </script>

  <script>
    // var obj = {}
    // window.b = 10
    // obj.b = 100
    // 问: window的b是几? 10

    var a = 10 // window.a = 10
    // {}.a = 50
    // 问 window.a 是几? 10

    function Test() {
      // new隐式 var this = {}
      console.log(this);
      this.a = 100
      // 对 空对象 添加a属性,  对window不产生任何影响
    }

    new Test()
    console.log(window.a) //?? 10
  </script>

</body>

</html>
```

原型的面试题:

- 描述下什么是原型?
  - 构造函数的一种设计, 把共享的方法存储在原型里. 给创建出来的对象使用
  - 最终目的: 省内存
- `__proto__` 和 `prototype` 的关系
  - 指向同一个内存地址, 即 存储共享的方法的对象
  - `prototype原型` 是 构造函数的属性 -- 爸爸
  - `__proto__(原型链)` 是 对象的 -- 儿子 
    - 用来 `链接` 到 prototype 的

### 17、严格模式

ES5版本中推出的特性, 来自`2009`年

让一些存在风险的操作, 报错!   把风险 显示的提醒, 修改后 让代码更健壮安全

> 在后期使用的各大框架中, 都会默认开启严格模式

学习严格模式有什么用?  `面试用`

- 面试题: 说说什么是严格模式, 你知道严格模式下哪些特点
  - 全局中, 只有声明的变量才能用  -- 怕写错单词导致全局污染
  - 函数中的this, 如果是window 转为 undefined  -- 避免全局污染
  - 取消静默失败：以前失败但不报错，现在报错

```
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>严格模式</title>
</head>

<body>
  <!-- 在 ES5 版本中:  JS的第五个版本 2009年, 推出了很多新的特性, 其中推出了  严格模式 特性 -->
  <!-- 严格模式下: JS会提供更多的报错提示, 保证代码更加安全健壮 -->
  <script>
    // 场景: 不小心写错变量名, 导致全局window对象中出现了一个新的属性, 造成了全局变量污染
    // 在 ES5 之前没办法避免, 后台没有报错
    // ES5 提供了 严格模式, 开启后就可以避免这种情况

    // use:使用  strict:严格    在字符串书写 放在JS开头
    // 后续的JS代码 会进入严格模式
    'use strict'

    // 严格模式下, 未声明的变量不允许使用, 会报错
    // 避免了 写错变量名 导致的全局变量污染

    var servername = 'localhost'

    // 修改成 www.baidu.com

    // 常见问题: 写错变量名 -- 后台不报错
    // 如果没有前缀, 默认使用window下的
    // window.servrname = ....  //会存储在全局对象里
    servrname = 'www.baidu.com'

    console.log(servername);
  </script>

</body>

</html>
```

```
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>严格模式</title>
</head>

<body>
  <!-- 以后写代码: 都是要开启严格模式的. 以后大多数时间都会使用框架来编写项目, 框架会自动开启严格 -->
  <script>
    // 开启严格模式
    // 严格模式下, 如果直接触发函数, 其中的this 不再是window 而是undefined.  有效避免全局变量污染
    'use strict'

    // 构造函数
    function Student(sname, age, phone) {
      // new隐式完成:  var this = {}
      console.log('this:', this);
      this.sname = sname
      this.age = age
      this.phone = phone
    }

    // 构造函数要搭配 new 运算符使用
    var s1 = new Student('凯凯', 28, '18877374444')
    console.log(s1);

    // 正常人用构造函数 -- 配合new使用
    // 但是 - 梓豪 不知道要new,  直接调用了,  会怎样?
    // 直接触发函数, 则函数中的this指向window, 导致在 window对象中新增了 3个属性 -- 全局污染
    var s2 = Student('梓豪', 24, '18744434343')
    console.log('s2:', s2);
  </script>
</body>

</html>
```

```
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>严格模式</title>
</head>

<body>
  <script>
    // 严格模式下 取消了 静默失败
    // 本来 失败的操作 不报错, 现在会报错
    'use strict'

    var emp = { ename: "凯凯", age: 19 }

    // freeze: 冻结  -- 冻结一个对象, 让其 无法增删改 属性
    Object.freeze(emp)

    emp.age = 40 // 由于对象被冻结, 修改属性会失败 -- 静默失败
    console.log(emp);

  </script>
</body>

</html>
```

### 18、精确配置对象

Object.defineProperty

```
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>精确的配置对象</title>
</head>

<body>
  <script>
    // 开启严格模式, 阻止静默失败 -- 有错大声说出来
    'use strict'

    // 精确配置对象的属性
    var emp = { ename: "凯凯", age: 28 }

    // 希望 ename 属性不可修改
    // define 定义  Property 属性

    // 参数1: 要操作的对象    参数2: 要修改的属性名   参数3: 具体的配置项
    Object.defineProperty(emp, 'ename', {
      // 快捷键: ctrl + i  可以弹出提示
      writable: false, //可写: 假
    })

    emp.ename = '孙凯'
    console.log(emp);
  </script>

  <script>
    'use strict'
    // 练习:
    var p = { name: "家乐", age: 24, wife: null }

    // 把 wife 属性改为不可写
    Object.defineProperty(p, 'wife', { writable: false })

    p.wife = '迪丽热巴' // 报错: 拒绝妻子设置为 热巴..
    // freeze: 冻结所有属性 -- 范围太大

    console.log(p);
  </script>
</body>

</html>
```

```
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>精确的配置对象</title>
</head>

<body>
  <script>
    'use strict'

    // 观察: 属性名 有的是 深色, 有的浅色
    console.log([11, 22, 33, 44]);
    // 浅色的属性是 不可遍历的 
    for (var key in [11, 22, 33, 44]) {
      console.log('key:', key);
    }

    var emp = {
      ename: "凯哥",
      age: 32,
      wife: null,
      salary: 23000
    }

    // 让 emp 的 salary 属性, 不可遍历
    Object.defineProperty(emp, 'salary', {
      enumerable: false //可遍历 可枚举
    })

    // 让 emp 的 wife 属性, 不可遍历, 不可修改
    Object.defineProperty(emp, 'wife', {
      enumerable: false, //不可遍历
      writable: false, // 不可修改
      // 不可删
      configurable: false, //不可重新配置, 配置锁死 后期无法修改
    })

    // delete: 删除某个属性
    delete emp.wife // 无法删除, 因为不可重新配置
    // 最后给凯哥一句话: yyds 永远单身!
    emp.wife = '娜扎'


    console.log(emp);

    for (var key in emp) {
      console.log('key:', key);
    }
  </script>
</body>

</html>
```

#### 1、新增属性

```
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>新增属性</title>
</head>

<body>
  <script>
    // 为一个对象类型 新增属性, 有两种做法
    var emp = {}

    //做法1: 此方式增加的属性, 所有权限都是开放的:  可写 可删 可遍历
    emp.ename = '凯凯'

    emp.ename = '孙凯' //可写
    delete emp.ename // 可删

    // 做法2: 新增的属性 所有权限都不开放: 不可遍历 不可修改 不可删除
    // value: 用于赋 初始值
    Object.defineProperty(emp, 'age', { value: 28 })

    emp.age = 40 //不可改
    delete emp.age // 不可删

    console.log(emp);
  </script>
</body>

</html>
```

#### 2、配置多个属性

```
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>配置多个属性</title>
</head>

<body>
  <script>
    var emp = {
      ename: "凯凯",
      age: 29,
      wife: null
    }
    // 需求:
    // 1. 让 age 不可修改
    // 2. 让 wife 不可遍历 + 不可删除
    // 3. 新增 salary 属性, 初始值 20000

    // defineProperties: 带有es 表示复数, 即多个
    // 参数1: 要配置的对象   参数2: 要配置的所有属性
    Object.defineProperties(emp, {
      // 属性名: 配置项
      age: { writable: false },
      wife: { enumerable: false, configurable: false },
      salary: { value: 20000 }
    })

    console.log(emp);
  </script>
</body>

</html>
```

#### 3、计算属性get

```
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>计算属性</title>
</head>

<body>
  <script>
    var r1 = {
      width: 10,
      length: 20,
      // 语法糖: 在对象中书写的函数, 可以省略 : function 部分
      // area: function () {

      // get: 称为计算属性
      // 前提: 函数没有参数, 添加 get 关键词以后, 使用时就不用写()
      get area() {
        return this.width * this.length
      },
      // perimeter 方法, 返回 (长+宽)*2
      get perimeter() {
        return (this.width + this.length) * 2
      }
    }

    console.log(r1);
    // 调用函数要用(), ()目的是为了传递实参使用的
    // 作者:那如果不用传递实参, 还写() 干啥??
    // 利用get关键词, 把函数改为 计算属性, 使用时不需要() 
    console.log(r1.area);
    console.log(r1.area);
    console.log(r1.area);
    console.log(r1.perimeter);
  </script>

  <script>
    // 利用 define 方式在对象中新增 计算属性
    var r2 = { width: 10, length: 4 }

    Object.defineProperty(r2, 'area', {
      // get: 用于添加计算属性, 调用时不用()
      // get: function () {
      get() {
        return this.length * this.width
      },
      // value: 用于添加普通的值, 调用时需要()
      // value: function () { }
    }) 

    console.log(r2.area);
  </script>
</body>

</html>
```

#### 4、set

```
 <script>
    var emp = {
      ename: '亚楠',
      _age: null, // 用于存储 检查站 age 检查出来的值
    }

    // 为 age 属性, 添加检查站: 监听器 set(设置)
    Object.defineProperty(emp, 'age', {
      // 计算属性get: 特点 值是函数,但使用时不用()
      // get: function () { },
      get() {
        // emp._age
        return this._age;
      },
      // set: 检查站属性, 值是函数
      // set: function (value) { }
      // 语法糖: 省略 function 
      // 参数value: 就是设置给 age 属性的值, 
      // 例如 emp.age = 200, 就是这个200
      set(value) {
        console.log('age赋值为:', value);
        // 检查标准: age 1~100
        if (value >= 1 && value <= 100) {
          // 如果正确, 则赋值给 _age
          // age是监听器/检查站, 只负责检查, 不负责存值
          // _age 是配合 age检查站使用的属性, 用来存储值
          this._age = value
        } else {
          // 抛出错误, 提醒用户
          throw Error('age合法范围1~100, 您的赋值:' + value)
        }
      }
    })


    // 修改age 年龄
    // 问题: 娅楠的年龄不可能是200, 明显的错误
    // 期望: 监听这个赋值操作, 如果值明显不对, 则报错, 给出提示
    // emp.age = 200

    // 用户看到: 把100 存储到 age 属性里
    // 本质age是检查站不存值, 但是用户不知道, 用户只看表面
    emp.age = 100
    // 外观上: 就应该从 age 读取值
    console.log(emp.age);
    // emp.age: 实际上age是个函数,但是因为是get计算属性, 不要()
    // 从外观上看起来: 好像是在读属性

    // 楠姐.打亮亮() : this就是楠姐
    // emp.age() : this就是 emp

    console.log(emp);
    // 读取年龄: 从_age读取完全没问题
    // 但是: 从用户角度来看
    console.log(emp._age);
  </script>
```

##### 1、属性的 set配置

把一个属性转换成 `监听器/检测站`: 实现赋值检测

搭配 另一个属性, 来存储实际的值

通过 get 计算属性, 欺骗用户, 提供一个友好的读值写法

#####  2、  对象属性的精确配置

- writable: 是否可写
- enumerable: 是否可遍历
  - 在 谷歌浏览器中, 不可遍历的属性是 `浅色` 的
- configurable: 是否可重新配置 -- 属性能否删除
- value: 默认值
- get: 计算属性,  值是`函数`, 但是使用时不用`()` 就能触发
- set: 监听器, 把一个属性转换成监听器, 监听赋值

#### 5、函数的三个触发方式（修改this指向）

##### 1、call: 

立刻触发函数; 临时把函数放在对象中执行 -- 修改this指向;

参数部分, 1个1个传递

```
<script>
    // 函数的call方法: 用于指定函数使用时的this关键词指向

    // 函数的this: 指向运行时所在的对象
    // 例如  楠姐.打亮亮() -- this就是楠姐

    // 函数分两种状态：声明时 和 运行时

    // 声明:   问: this是什么?  不可能知道--运行时决定
    // 举例: 马路边停了一辆车, 问: 司机是谁? -- 开起来才知道
    function 打亮亮() {
      console.log(this.uname, '使劲打亮亮');
    }

    var emp = { uname: "娅楠" }
    // 把 打亮亮 这个函数, 存储到 emp 里
    emp.hit = 打亮亮
    emp.hit()

    var emp1 = { uname: '凯哥' }
    emp1.hit = 打亮亮
    emp1.hit()
    delete emp1.hit //删除 hit 属性, 毁灭证据

    // 又把 公用的锤子
    // 1. 把锤子拿到手里  2.用锤子打亮亮  3.把锤子扔掉
    console.log(emp1);

    // 打亮亮方法在使用时分两步: 
    // 1. 先把此方法存储到 对象里
    // 2. 再通过对象来调用
    // 3. 删除打亮亮方法, 因为是临时使用

    // 官方为了用户使用方便, 封装了一个call方法, 能够自动把函数放在对象里, 进行调用, 随后进行删除
    // 函数的构造方式:  new Function()
    // 所以 函数.__proto__ == Function.prototype
    console.dir(打亮亮);
    // 函数具有一个call
    // 函数.call(obj):  隐式 把函数存储在obj里, 然后通过obj调用
    打亮亮.call(emp1)

    var emp2 = { uname: '涛涛' }
    // 两种做法:
    // 做法1: 手动模式
    // - 把 打亮亮 存储在 emp2 中, 属性名叫 hit, 可以随便起名
    emp2.x = 打亮亮
    // - 调用 hit 方法
    emp2.x()  // 打亮亮的 this 就是 emp2
    // - 删除 hit 属性, 毁灭证据
    delete emp2.x
    console.log(emp2);

    // 做法2: 系统提供的快速隐式完成以上操作 -- call
    打亮亮.call(emp2)
  </script>
```

call带有参数

```
  // 使用系统提供的 call 方式
    // 函数.call(对象, 参数): 自动隐式完成 - 把函数放对象里,调用后,删除
    // call() 从参数2开始, 就是传递给函数本身的参数
    打亮亮.call(emp1, 10) // emp1.打亮亮(10)

    // 范式:  fn.call(A, B) ->实际执行 -> A.fn(B)

    // 计算 n个月 支付的薪资
    function pay(n) {
      console.log(this.salary * n);
    }

    var emp2 = { ename: "凯凯", salary: 14000 }
    var emp3 = { ename: "涛涛", salary: 24000 }

    // 计算 emp2 10个月的薪资
    pay.call(emp2, 10)
    // 计算 emp3 4个月的薪资
    pay.call(emp3, 4)
```



##### 2、apply

立刻触发函数; 临时把函数放在对象中执行 -- 修改this指向; 

特殊: 参数部分用 数组进行传递

```
<script>
    // apply: 与 call 作用十分相似
    // 都是临时把函数放在对象里执行
    function pay(n, off) {
      // off: 折扣
      console.log(this.salary * n * off);
    }

    var emp = { ename: "凯凯", salary: 14000 }
    // 用call 算出10个月工资: 把pay临时放到 emp 中执行
    pay.call(emp, 10, 0.7)
    // apply: 临时把函数放在对象里执行, 差异: 参数放数组中传递
    pay.apply(emp, [10, 0.7])

    // apply的用途: 把 1个1个 传递的参数, 改为用数组传递

    // 求最大值: Math.max()
    var m = Math.max(12, 43, 2154, 657, 67, 21)
    console.log(m);

    // 找出数组中的最大值
    var nums = [123, 345, 546, 657, 67]
    // max: 只能接收 1个1个传递的参数
    // apply: 把数组作为函数的参数, 数组->1个1个传递的
    // Math.max.apply(A, B) -> A.Math.max(B)
    // Math.max 不需要存储在任何对象中, 独立就能运行, 所以参数1 随便写, 没有任何影响
    var m = Math.max.apply(0, nums)

    // ES6之前, 只能用 apply 来转换数组 为参数
    // ES6之后, 有扩展符  ... 更方便, 后续讲解
    console.log(m);
  </script>
```



##### 3、bind

不会触发函数; 把 参数和this指向 都保存在函数自身, 返回绑定好的函数; 以后随时都能触发 -- `延时执行`

```
<script>
    // bind: 与call相似
    // call: 临时 把函数放在对象中, 立即执行
    // bind: 永久 把函数放在对象中, 不会立即执行, 返回处理后的函数

    function pay(n) {
      console.log(this.salary * n);
    }

    var emp = { ename: "凯凯", salary: 14000 }
    // 用call实现 10个月工资
    pay.call(emp, 10)

    // bind(): 不会触发pay函数, 而是返回一个值
    // 返回值是一个函数, 其中的 BoundThis 属性存储了this指向
    // 其中的 BoundArgs : 存储了相关参数

    // 打比方: 一把手枪
    // call: 填充弹药 -> 立刻激发
    // bind: 填充弹药 -> 返回这把带有弹药的手枪
    var pay_b = pay.bind(emp, 10)
    console.dir(pay_b);

    // 在后续, 用()来触发
    pay_b()

    // 实际工作用途:
    // 1. 配合定时器使用: 延时执行
    // 2. 在 React 框架中常用: 2个月后的 5阶段会用到
  </script>
```



#### 6、箭头函数

- 从`格式`上提供了更简单的匿名函数写法:  `() =>{}`
- 两种语法糖:
  - 参数只有一个, () 可是省略:  ` x => { return x * 2 } `
  - 函数体只有一行, `{return }` 省略:   `x => x * 2`
- this关键词的指向
  - function的this: `运行时`所在的对象   `楠姐.打亮亮()`
  - 箭头的this: `声明时`所在的对象 -- 固定的,永远不变
  - 构造函数的this(`new`):  构造出来的那个对象
    - new隐式3件事: 
      - `var this = {};  `
      - `this.__proto__ =函数.prototype`
      - `return this`
  - 严格模式下, 函数的this
    - 如果直接在全局调用, 则this指向 undefined

#### 7、数组的高阶函数

- `高阶函数`: 函数中使用了其它的函数

- every: 每一个元素都满足条件则为真,  类似于 逻辑与 &&

- ```
  // every: 每一个. 用于遍历数组, 检查每一个元素是否符合条件
      // every的参数: 要求是函数类型, 函数固定接收3个参数
      // every会遍历 nums 中的每一个元素, 传递给函数
       // 判断是否都是正数 > 0
      var a = nums.every((value, index, array) => {
        return value > 0
      })
  
      // 没用到的参数, 可以不用声明
      var a = nums.every((value) => {
        return value > 0
      })
  
      // 箭头函数: 单参数省略()   函数体只有1行 {return }
      var a = nums.every(value => value > 0)
      // 参数名随便起, 但是原则: 见名知意
      var a = nums.every(x => x > 0)
  ```

  

- some: 至少有一个元素满足条件则为真, 类似于 逻辑或 ||

- filter: 把满足条件的元素过滤出来, 组合成新的数组

- map: 映射. 遍历每个元素, 处理后把返回值组成新的数组;
  - 使用场景: 把数据转换成HTML字符串
  
  - ```
    var girls = ['迪丽热巴', '古力娜扎', '马尔扎哈', '努尔哈赤']
        // 把每个元素, 放在按钮标签里  <button>xx</button>
        var a = girls.map(value => {
          // ES6提供了 模板字符串, 转为拼接HTML而生
          // 符号 `` 反引号, 特殊标识 ${} 代表JS代码
          return `<button>${value}</button>`
        })
        
        var webs = [
          { name: "百度一下", href: "http://www.baidu.com" },
          { name: "Tmooc", href: "http://www.tmooc.cn" },
          { name: "斗鱼", href: "http://www.douyu.com" },
          { name: "哔哩哔哩", href: "http://www.bilibili.com" },
        ]
    
        // 要求: 映射成 超链接 字符串组成的数组
        // 例如  <a href="http://www.baidu.com">百度一下</a>
        var a = webs.map(value => `<a href="${value.href}">${value.name}</a>`)
    ```
  
    

### 19、ES6新特性

#### 1、forEach

遍历数组，没有返回值

```
nums.forEach(value => a += value)
```

#### 2、reduce

合并数组数据，遍历数组的元素，把处理后的返回值累加在一起

参数a:每一次遍历都会把结果，交给下一次的参数a

参数：0  是a的初始值，即第一次循环时的初始值

```
var s = products.reduce((a, value) => {
      return a + value.price * value.count
    }, 0)
```

#### 3、let/const

都是ES6中推出的新特性，用来声明变量

特征1：没有全局变量污染，存储在script作用域中

特征2：没有声明提升（不准确）---作者设定了暂存死区的概念

准确解释：let提升了，但是在声明代码执行之前，一直处于暂存死区状态--无法使用

const：声明时必须赋值，之后就无法重新赋值，注意：如果常量的值是对象类型，可以修改，因为对象存储在堆内存，传递的是地址，地址不变

### 20、保护对象的方式

#### 1、preventExtensions

阻止增加属性

#### 2、seal

不可增删

#### 3、freeze

不可增删改

### 21、数组、对象的展开语法

...运算符 去掉数组的[   ]

```
<script>
    // 来自 ES6 的新增语法糖: 展开语法
    var a = [11, 22, 33, 767, 77, 88, 88]
    // ... 运算符: 去掉 数组的 []
    var b = [44, 55, ...a]
    console.log(b);
    // max: 的参数只能是 1个1个的, 不接数组类型
    // ES6之前:  Math.max.apply(0, a)
    // ES6之后: ... 来去掉[], 把数组里面的东西拿出来
    var m = Math.max(...a)
    console.log(m);
  </script>
```

去掉对象的{    }

```
<script>
    var a = { x: 10, y: 20 }
    var b = { y: 30, z: 40 }
    // ... : 去掉对象/数组的 外层括号
    // 同名的属性, 后写的覆盖先写的
    var c = { w: 100, ...a, ...b }
    // 相当于: { w:100, x: 10, y: 20, y: 30, z: 40 }
    console.log(c);
  </script>
```

### 22、剩余参数

ES6之前使用arguments   来使用函数的不固定数量的参数

缺点：隐藏的变量；类型是伪数组，不具备数组的各种方法

 ES6之后用...表示接受剩余参数

```
<script>
    // ...: 固定运算符
    // nums: 自定义变量, 名字无所谓
    // ... 就代表把收到的所有参数, 保存到后方的变量里(数组类型)
    function show(x, ...nums) {
      console.log('nums:', nums);
      // nums = [2, 3, 4]
      // nums[0]: 数组的下标取值, 获取数据
    }
    function show(x, y, ...nums) {
      console.log('x:', x);
      console.log('nums:', nums);
    }
    show(1, 2, 3, 4)
  </script>
```

### 23、参数的默认值

```
 <script>
    // ES6的 函数参数增强特征: 可以为函数的参数设置默认值
    function show(name = '家乐') {
      // 相当于: var name = '家乐'
      // 如果传参了:  name = '思琦'
      console.log(name);
    }

    show() // 没有传递参数, 则 采用默认值
    show('思奇') // 如果传递参数, 则 使用传递的值
  </script>
```

### 24、解构

可以快速从数组、对象中抓取元素，保存到变量里

#### 1、数组的解构语法

```
var r1 = [10, 20, 50] // 分别存储到变量  x, y, z 中

    var [x, y, z] = r1
    console.log(x, y, z);

    // 可选解构
    var names = ['凯凯', '楠楠', '亮亮', '铭铭']
    //    n1     n2     n3
    var [n1, n2, , n3] = names  //不想解构的, 可以省略不写
    console.log(n1, n2, n3);

    // 灵活用法: 互换变量的值
    var yy = 100
    var rr = 200;

    // [yy, rr] = [200, 100]

    // 先组合出一个数组 [rr, yy] == [200, 100]
    // 然后解构
    [yy, rr] = [rr, yy] // = [200, 100]
    console.log(yy, rr);
```

#### 2、对象的解构语法

```
<script>
    // 
    var emp = {
      ename: "家乐",
      age: 18
    }

    // 传统写法
    var ename = emp.ename
    var age = emp.age

    // 解构语法
    var { ename, age } = emp
    console.log(ename, age);

    // 练习
    var p1 = { pname: "iPhone", price: 9999, count: 5 }
    // 把属性读取出来, 保存在变量里
    var { count, pname } = p1
    // 对象类型:无序的
    console.log(count, pname);

    // 起别名
    var p2 = { pname: "mike", count: 10 }

    // count -> c2
    var { count: c2 } = p2
    console.log(c2);
  </script>
```

#### 3、复杂解构

```
<script>
    var emp = {
      ename: '家乐',
      age: 23,
      skills: ['唱', '跳', 'rap', '篮球'],
      love: ['杨洋', '王一博', '胡歌']
    }

    // 把内容解构出来
    var { ename, age: eage, skills: [q, w, e, r], love } = emp

    console.log(ename, eage, q, w, e, r, love);

    var iPhone = {
      maker: "Apple",
      price: 9999,
      tags: ['高刷', 'iOS', '最佳cpu'],
    }

    // 
    var { maker, price: p_price, tags: [tag1, tag2, tag3] } = iPhone

    console.log(maker, p_price, tag1, tag2, tag3);
  </script>
```

#### 4、函数的参数解构

```
 // map: 把数组映射成 HTML 代码
    var a = emps.map(value => {
      return `<a class='${value.married ? 'ok' : 'err'}'>${value.ename}-${value.age}-${value.salary}</a>`
    })

    // 利用解构简化:
    var a = emps.map(value => {
      const { ename, age, salary, married } = value

      return `<a class='${married ? 'ok' : 'err'}'>${ename}-${age}-${salary}</a>`
    })

    // 参数解构: 参数解构, 需要用() 包围, 防止歧义
    var a = emps.map(({ ename, age, salary, married }) => {
      return `<a class='${married ? 'ok' : 'err'}'>${ename}-${age}-${salary}</a>`
    })

```

### 25、class语法



### 26、面向对象的3大特征

- 封装: 用`{}`把代码封装在一起, 后续随时触发

  - 具体表现: 函数

- 继承: 原型链指向其他的对象.  自己没有的 到原型中查找

  ![image-20220614193118556](C:\Users\深海钢琴师\AppData\Roaming\Typora\typora-user-images\image-20220614193118556.png)

- 多态: 子中可以重写一个 与 父相同的方法, 使用时优先使用子中带有的

### 27、回调地狱

在JS中进行一些异步操作时(网络操作), 层层嵌套, 会导致代码阅读困难

解决方案：promise

#### promise

```
new Promise((resolve, reject) => { }).then(res => { }).catch(err => { })

 new Promise((resolve, reject) => {
      // 当调用 resolve 时, 会触发 then 中的箭头函数
      // resolve的参数, 会传递给 then 中的箭头函数
      // resolve('调用resolve') // 这代表成功

      // reject 会触发 catch, 其参数传递到 catch 中
      reject('调用reject') // 这代表失败

      // resolve和 reject 互斥, 同一时间只能触发一种
    })
      .then(res => console.log('res:', res))
      .catch(err => console.log('err:', err))
```

> pPromise有3种状态
>
> - 刚new出来: new Promise -- pending
> - 触发 resolve 之后 -- fulfilled
> - 触发 reject 之后 -- rejected

### 28、正则表达式

官网: https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions

```
 // 构造方式创建正则
    // JS的 \ 是转义符, \d 转义成 d
    // 需要用 \\d 来转义成 普通的 \d
    var r = new RegExp('\\d\\d', 'g')
    var a = words.match(r)
    console.log(a)

    var a = words.match(/\d\d/g)
    console.log(a);
```



#           DOM

 DOM: `D`ocument `O`bject `M`odel

> - Document: 文档 -- 就是HTML代码
> - Object: 对象 -- HTML代码转换而来的对象
> - Model: 模型 -- HTML 转换成 Object 这种方式

`HTML`: 就是一种 `语法糖` 写法, 可以快速的创建出DOM元素

- 浏览器在阅读HTML后, 会转换成`document`对象, 最后显示到页面上
- 浏览器真正展示到页面上的, 是 `document`对象
- 学习DOM的目的: 直接操作`document` 对象, 不再使用普通的HTML 
- HTML只能提供简单的操作操作
- 可以粗暴理解: `DOM`犹如玩游戏 `开挂`, 操作底层代码, 突破限制

## 1、查找元素

DOM的重要核心操作: `先查找到元素` -> `然后修改元素的属性`

#### 1、固定元素的查找: 

- `document.head`
- `document.body`
- `document.documentElement`: 整个html

#### 2、按照关系查找

- 第一个子元素:`firstElementChild`
- 所有子元素: `children`
  - 数组类型, 利用 下标取值来读取某个元素
  - 常见`利用数组解构`语法, 快速获取多个元素
- 下一个兄弟元素: `nextElementSibling`
- 上一个兄弟元素: `previousElementSibling`
- 找元素的父元素  ：parentElement
- 找元素父的父： parentElement.parentElement

- 按照id查找:
  - `document.getElementById()`
  - 特殊: 浏览器会自动把 id 的元素找到并保存在同名变量中, 可以直接用

#### 3、按照特征查找(除了id 其他很少用)

- id       `document.getElementById()`
- class    `getElementsByClassName( )`
- 标签名 `getElementsByTagName( )`
- name     `getElementsByName( )`

#### 4、利用 css选择器 查找

- `querySelector`: 查`单个`元素, 返回值是 元素本身
- `querySelectorAll`: 查`多个`元素, 返回值是 类数组, 有forEach可以用

#### 5、class

- className: 就是 class 属性本身
- `classList`: 一个`工具箱`, 存放了很多操作class的方法, 更加易用!
  - add: 添加样式
  - remove: 移除样式
  - toggle: 切换样式   (有就删，没有就加，设置点击选中，再次点击取消效果)
  - contains: 是否有某个样式

案例：保证唯一性

```
 <script>
    const spans = document.querySelectorAll('#pages span')
    spans.forEach(span => span.onclick = function () {
      // 保障唯一性:  新的添加前, 要移除旧的

      // 参数是 css选择器  .cur 代表 class=cur,查找带有该属性的元素
      const cur = document.querySelector('.cur')
      // 参数是 class名
      cur.classList.remove('cur')
      // 区别: 当前练习 默认第一项就是 class='cur', 不存在搜索不到的情况, 所以不需要判断 cur 是否存在
      //如果不存在默认项，则需要判断
      //cur && cur.classList.remove('cur')

      this.classList.add('cur')
    })
  </script>
```

#### 6、大小图切换

```
 const imgs = document.querySelectorAll('#box>div>img')
    const big_img = document.querySelector('#box>img')
    console.dir(big_img) // 查看其 src 属性

    imgs.forEach(img => img.onmouseenter = function () {
      const active = document.querySelector('#box .active')
      active.classList.remove('active')

      // 当前项.工具箱.添加工具()
      this.classList.add('active')

      // 读取当前项中, 存储的自定义属性 big, 即大图的名字
      // 图片使用时, 需要有路径, 不能光有名字, 所以要拼接
      big_img.src = './imgs/' + this.dataset.big
    })
  </script>
```

#### 7、自定义属性

可以让不同元素联系起来

data-自定义mign="  "

dataset:专门存储利用data-声明的自定义属性



#### 8、标签栏

```
  <script>
    const tabs = document.querySelectorAll('#tabs>div:first-child>span')

    tabs.forEach(tab => tab.onclick = function () {
      const s = '#tabs>div:first-child>span.active'
      document.querySelector(s).classList.remove('active')

      this.classList.add('active')

      // 把之前带有 .active 的详情, 移除激活态
      document.querySelector('#tabs div.active').classList.remove('active')

      // 读取当前点击项中存储的 自定义属性 id
      const id = this.dataset.id
      // 通过id 找到对应的详情元素
      // id是变量, 需要用模板字符串拼接
      const detail = document.querySelector(`#tabs #${id}`)
      detail.classList.add('active')
    })
  </script>

```

#### 9、输入框

```
<script>
    const inp = document.querySelector('#box input')

    // 获得焦点: 让 .info 显示 
    inp.onfocus = function () {
      // bug修复: 如果手机号已经对了, 则不做处理
      if (/^1[3-9]\d{9}$/.test(this.value)) return

      const active = document.querySelector('#box .active')
      // active:不一定存在, 使用前先判断为真
      active && active.classList.remove('active')

      const info = document.querySelector('#box .info')
      info.classList.add('active')
    }

    // 失去焦点
    inp.onblur = function () {
      // 删除之前激活的
      document.querySelector('#box .active').classList.remove('active')

      // 判断:如果输入框是空的
      if (this.value == '') {
        const empty = document.querySelector('#box .err:nth-child(2)')
        empty.classList.add('active')
        return //停止函数的执行, 后续代码不生效
      }

      // 正则验证手机号格式 /^1[3-9]\d{9}$/
      if (/^1[3-9]\d{9}$/.test(this.value)) {
        const ok = document.querySelector('#box .ok')
        ok.classList.add('active')
      } else {
        const err = document.querySelector('#box .err:first-child')
        err.classList.add('active')
      }
    }
  </script>

```

#### 10、轮播图

获取到的自定义属性是变量。括号里面需要（模板字符串拼接）

根据id 名关联起来，但是id命名要符合规则

const img = document.querySelector(`#box #${id}`)

利用伪类选择器，直接用数字，关联到第几个子元素

 const img=document.querySelector(`#banner img:nth-child(${index})`)

```
<div id="banner">
        <div>
            <img class="active" src="./imgs/banner1.png" alt="">
            <img src="./imgs/banner2.png" alt="">
            <img src="./imgs/banner3.png" alt="">
            <img src="./imgs/banner4.png" alt="">
        </div>
        <div>
            <span data-index="1" class="active"></span>
            <span data-index="2"></span>
            <span data-index="3"></span>
            <span data-index="4"></span>
        </div>
    </div>
    <script>
        const dian=document.querySelectorAll('#banner span')
        dian.forEach(dian=>dian.onmouseenter=function(){
   document.querySelector('#banner span.active').classList.remove('active')
       this.classList.add('active')
   //获取dataset里面存储的自定义属性
          const index=this.dataset.index
   //index存储的第几个 ，利用自定义属性获取与当前对象要关联的img元素
 const img=document.querySelector(`#banner img:nth-child(${index})`)
 document.querySelector('#banner img.active').classList.remove('active')
            img.classList.add('active')
        })
    </script>
```

自动滚动轮播图

```
<script>
    const dians = document.querySelectorAll('#banner span')
    dians.forEach(dian => dian.onmouseenter = function () {
      document.querySelector('#banner span.active').classList.remove('active')

      this.classList.add('active')

      const index = this.dataset.index
      const img = document.querySelector('#banner img:first-child')
      img.style.marginLeft = -400 * index + 'px'
    })

    // 定时器实现自动滚动
    setInterval(() => {
      // 获取当前的项目, 然后触发其下一项
      const active = document.querySelector('#banner span.active')
      // 下一个小圆点
      let next_dian = active.nextElementSibling
      console.log(next_dian);
      // 如果 next_dian 是null, 说明已经是最后一个, 则回到第一个
      // if (next_dian == null) {
      // 激活的元素.父元素.第一个子元素
      // next_dian = active.parentElement.firstElementChild
      // }

      // 进阶语法: 逻辑短路,  在逻辑或中, 前面是假的, 则会执行后续代码;
      next_dian || (next_dian = active.parentElement.firstElementChild)

      // 直接触发小圆点的 mouseenter 
      next_dian.onmouseenter()
    }, 2000);

    // 下一个 和 上一个 按钮的逻辑, 与自动滚动几乎一样, 仅是利用点击触发
    // 更加细节的轮播图: 后续采用 第三方 swiper 实现
  </script>
```



#### 11、change事件

效果：不勾选选框，按钮灰色，不响应



```
 <style>
    .btn {
      display: inline-block;
      width: 300px;
      text-align: center;
      background-color: #72b134;
      border-radius: 3px;
      line-height: 30px;
      color: white;
      user-select: none;
    }

    .btn:active {
      opacity: 0.7;
    }

    /* 联合在一起写: 代表同时具备 */
    .btn.disabled {
      background-color: #aaa;
      /* 指针-事件们: 一个都不留;    去掉所有鼠标响应 */
      pointer-events: none;
    }
  </style>
</head>

<body>
  <div id="box">
    <!-- label被点击时, 会触发其子元素的点击事件 -->
    <label>
      <input type="checkbox">
      <span>我已阅读并同意用户注册协议</span>
    </label>
    <br>
    <div class="btn disabled">提交注册</div>
  </div>
<script>
    // 检测: 勾选按钮的 状态变化
    const btn = document.querySelector('.btn')
    const chb = document.querySelector('#box input')

    // change: 值发生变化
    chb.onchange = function () {
      console.dir(this); // 检查 : checked 属性的值
      console.log('checked:', this.checked);
      // if (this.checked) {  //勾选状态, 删除disabled
      //   btn.classList.remove('disabled')
      // } else {
      //   btn.classList.add('disabled')
      // }

      this.checked ? btn.classList.remove('disabled') : btn.classList.add('disabled')

      // []: 其中书写JS代码
      // btn.classList[this.checked ? 'remove' : 'add']('disabled')

      // 下方3行代码同含义
      // btn.classList.add('xxx')
      // btn.classList['add']('xxx')

      // var x = 'add'
      // btn.classList[x]('xxx')
    }
  </script>
</body>

```

小知识

1、[   ]中间写js代码

 下方3行代码同含义
      // btn.classList.add('xxx')
      // btn.classList`['add']('xxx')`

2、ES6提供的语法:  变量?.    如果变量是真的, 才会继续执行

 document.querySelector('#box .active')?.classList.remove('active')

等同于下面代码

const active = document.querySelector('#box .active')
      // active:不一定存在, 使用前先判断为真
      active && active.classList.remove('active')

### 2、标签内容操作

#### 1、innerHTML区别

```
 box.innerHTML = '<h1>Hello</h1>' // 值作为HTML代码解析
 app.innerText = '<h1>Hello</h1>' // 值作为普通文本显示
```

#### 2、数组转HTML

```
 <script>
    const data = ['vue', 'react', 'angular', 'uniapp']
    // 要求: 把数据放到按钮里, 显示在 div#box 中

    // 高阶函数: map 映射. 把数组中的元素 映射成 HTML代码
    const els = data.map(v => `<button>${v}</button>`)
         console.log(els);

    // 如何把数组的元素, 拼接成字符串: join
          console.log(els.join('')) //默认是逗号间隔, 主动传递 ''

    box.innerHTML = els.join('') // 参数代表用什么间隔

    // 套路: 先用 map 把数组中的元素转换成 HTML 代码
    // 然后利用 join 拼接到一起, 设置给 innerHTML
  </script>
```

利用解构获取变量

```
<script>
    const data = [
      { title: '新闻', href: 'http://news.baidu.com/' },
      { title: 'hao123', href: 'https://www.hao123.com/' },
      { title: '地图', href: 'https://map.baidu.com/' },
      { title: '贴吧', href: 'https://tieba.baidu.com/' },
      { title: '视频', href: 'https://haokan.baidu.com/' },
    ]
    // 示例: <a href="http://news.baidu.com/">新闻</a>

    // 参数解构: ES6  -- JS高级的第五天
    const a = data.map(({ title, href }) => `<a href="${href}">${title}</a>`)
    box.innerHTML = a.join('')

    const b = data.map(v => {
      return `<a href='${v.href}'>${v.title}</a>`
    })
    box.innerHTML = b.join('')
  </script>
```

#### 3、冒泡机制

概念：当子元素上触发事件, 会自动通知父元素, 触发其相同的事件，事件参数e: 其中的target属性存储了 事件触发的当事人

  利用 stopPropagation() 可以停止冒泡

```
<script>
    // 事件冒泡机制: 当子元素上发生某个事件, 会传递给父元素 
    // 通俗: 找家长  找老师... -- 家乐被人打了, 家乐找爸爸告状

    const red = document.querySelector('.red')
    // 凡是事件触发时,都会自动带有事件参数: 包含了事件触发时的各种信息
    red.onclick = function (e) {
      // 红色触发的点击事件, 不一定是自己触发的, 有可能是子元素传递
      console.log(e) // 找到target属性

      // e.target: 代表触发事件的 当事人

      console.log('red被点击');
    }

    const blue = document.querySelector('.blue')
    blue.onclick = function () {
      console.log('blue被点击');
    }

    const green = document.querySelector('.green')
    green.onclick = function (e) {
      // stop:停止  propagation: 传播
      e.stopPropagation()
      // 事件的冒泡机制被终止, 不会通知父元素

      console.log('green被点击');
    }
  </script>
```

#### 4、事件委托

 事件委托: 元素的事件 交由 父元素来管理, 委托给父元素 

 适用场景: 动态新增的子元素 

```
 <script>
    const items = document.querySelectorAll('#box span')
    items.forEach(item => item.onclick = function () {
      this.remove()
    })

    const inp = document.querySelector('input')
    inp.onkeyup = function (e) {
      // 键盘事件的 keyCode 属性, 13代表回车
      if (e.keyCode == 13) {
        // 累加
        box.innerHTML += `<span>${this.value}</span>`
        this.value = ''
      }
    }

    // 问题: 新增每个元素 都需要重新为其添加 点击事件, 过于繁琐
    // 做法: 给父元素添加
    box.onclick = function (e) {
      // target: 事件触发的当事人
      console.log('box被点击:', e.target);
      // 查看其属性, 哪个能分辨出span还是div
      console.dir(e.target)
      if (e.target.tagName == 'SPAN') {
        e.target.remove()
      }
    }
  </script>
```

#### 5、手动创建dom元素

创建元素：createElement

把元素添加到子元素的末尾：appendChild 

插入到某元素之前：insertbefore

替换某个子元素：replaceChild

删除：removeChild

```
const btn = document.createElement('button')
btn.innerHTML = '点我'
    btn.id = 'b1'
    btn.className = 'danger'
    
    
    
    const box = document.getElementById('box')
    // 添加到 box 的子元素
    // append:新增/添加   child:子元素
    box.appendChild(btn) // 向box元素中,添加子元素

    //常规：字符串 -> 被浏览器解析成DOM元素 -> 再展示到页面上
    // box.innerHTML = '<button>啦啦啦</button>'
```

#### 6、文档片段

const frag = document.createDocumentFragment()

 一个虚拟的容器, 用来放多个DOM元素；之前: 制作一个放一次, 制作一个放一次...；现在: 把制作好的DOM元素, 先放在一个虚拟容器里, 再用appendChild一起放到页面

```
 const data = ['铭铭', '亮亮', '楠楠', '小新', '涛涛']
    // 之前: 制作一个放一次, 制作一个放一次...
    // 现在: 把制作好的DOM元素, 先放在一个虚拟容器里, 一起放到页面

    // create创建 Document文档 Fragment片段
    // 一个虚拟的容器, 用来放多个DOM元素
    const frag = document.createDocumentFragment()

    data.forEach(v => {
      const btn = document.createElement('button')
      btn.innerHTML = v
      // 把生成的DOM 先放在 虚拟的 文档片段里
      frag.appendChild(btn) // 类似 雪糕放到塑料袋里
    })
    // box: 相当于冰箱, 把所有东西 一起放进去
    box.appendChild(frag)
```

#### 7、阻止默认事件

preventDefault

```
 // 用途: 主要是团队合作
    // 例如 家乐(JS) 和 马(HTML) 组队
    // 家乐开发JS, 需要给 a 标签添加个性化的 onclick 事件
    // 佩奇-不知道不应该写 href: <a href="">xxx</a>
    // 防御: 在JS中阻止默认事件, 防止 href 产生的刷新效果

    const a = document.querySelector('a')
    a.onclick = function (e) {
      // prevent阻止 Default默认
      e.preventDefault()

      // 超链接 带有 href: 点击后默认会进行跳转操作
      alert('a被点击了')
    }
```

#### 8、事件监听器：为一个事件添加多个方法

通常一个事件只能一个方法，同时只能赋1个值，后面会覆盖前面的值

addEventListener

```
const btn = document.querySelector('button')
    // 问题: onclick 是个属性, 同时只能赋1个值，后面会覆盖前面的值
    btn.onclick = function () {
      alert("家乐是最棒的!")
    }

    btn.onclick = function () {
      alert("佩奇才是最棒的!")
    }

    // 事件监听器: 可以为1个事件 添加多个方法
    // add添加 Event事件 Listener监听器
    // 参数1: 事件名 -- 系统规定, 注意没有 on 开头
    btn.addEventListener('click', function () {
      alert('111111')
    })

    btn.addEventListener('click', function () {
      alert(22222)
    })
```

#### 9、鼠标事件

1.点击时, 创建一个元素 添加到页面上

2.通过事件参数, 获取 点击的坐标

3.设置给创建的元素, 显示在对应位置



```
<script>
    let num = 1

    box.onclick = function (e) {
      // 仅限 事件触发的当事人 target, 是box 的场景 才添加
      if (e.target !== this) return

      console.log(e) //展开查看, 猜一猜哪个是坐标
      // x,y: 点击位置距离 浏览器内容的左上角
      // offsetX, offsetY: 点击位置距离当前元素的左上角
      // screenX, screenY: 距离屏幕的左上角
      const span = document.createElement('span')
      span.innerHTML = num++ // 先赋值, 再+1
      const { offsetX, offsetY } = e
      // 默认是左上角, 需要移动到中间, 所以-13  1半的宽
      span.style.top = offsetY - 13 + 'px'
      span.style.left = offsetX - 13 + 'px'

      this.appendChild(span)
    }
  </script>
```

#### 10、滚动监听

onscroll

```
 <!-- 监听页面的滚动距离, 切换内容的显示与否 -->
  <div id="box"></div>
  <!-- diplay:'' -->
  <div id="xx" style="display: none"></div>

  <script>
    for (let i = 0; i < 1000; i++) {
      const div = document.createElement('div')
      div.innerHTML = i
      box.appendChild(div)
    }

    // window提供的, 监听窗口的滚动
    window.onscroll = function () {
      // console.log('onscroll');
      // 获取滚动的距离: 由于兼容性问题, 提供两种读取方式, 在不同浏览器上不一定哪个好用.  y的值就是其中 正常读取的值

      // document.documentElement.scrollTop: 获取滚动的距离
      // document.body.scrollTop: 获取滚动的距离

      const y = document.documentElement.scrollTop || document.body.scrollTop

      // 设定: 至少有一个人会答应, 不一定是谁
      // 例如: 家乐的媳妇 = 迪丽热巴答应不 || 马尔扎哈答应不
      // 所以: 家乐的媳妇是 后方表达式中 首个 为真的


      console.log('y:', y);

      // 如果 y > 4000 像素  就显示 div#xx; 否则就隐藏
      // display="none" 代表隐藏
      // display="" 代表不隐藏
      xx.style.display = y > 4000 ? '' : 'none'
      // if (y > 4000) {
      //   xx.classList.remove('hide')
      // } else {
      //   xx.classList.add('hide')
      // }
    }

    // 逻辑或 表达式的值: 是从左到右 第一个真值, 如果没有则是最后一个
    var a = null || 0 || '' || 11
    console.log(a);

    var b = null || 0 || '' || false || undefined
    console.log(b)
  </script>
```

#### 11、属性读取

读取属性：getAttribute

设置属性：setAttribute

判断属性是否存在：hasAttribute

移除属性：removeAttribute

为元素自定义属性:data-

读取自定义属性函数方式：getAttribute('data-')

读值方式：dataset.

```
<script>
    // DOM元素的属性分: 系统 和 自定义 data-
    const a1 = document.getElementById('a1')
    console.dir(a1)

    // 读取属性的 旧写法
    // get获取 Attribute属性
    console.log(a1.getAttribute('id'))
    console.log(a1.getAttribute('href'))
    // 修改:  set设置
    a1.setAttribute('href', 'http://www.baidu.com')
    // 判断元素是否设置了 某个属性
    // has: 有
    console.log(a1.hasAttribute('id')) //true
    console.log(a1.hasAttribute('target')) //false

    // 自定义属性
    console.log(a1.getAttribute('data-xx'))


    //读取系统属性
    console.log(a1.id)
    console.log(a1.className)
    // 自定义属性 dataset
    console.log(a1.dataset.xx)
    console.log(a1.dataset.yy)
  </script>
```

#### 12、地址栏

```
<!-- replace: 替换 -->
  <button onclick="location.replace(`http://www.baidu.com`)">切换到百度</button>
  <button id="b3">3秒后跳转</button>

  <script>
    // 手动为当前路径结尾添加  ?name=家乐&age=19
    // URLSearchParams: 专门转化 URL的传参
    const params = new URLSearchParams(location.search)
    console.log(params.get('name')) // 读取 name 属性的值

    b3.onclick = function () {
      setTimeout(() => {
        location.replace('http://www.tmooc.cn')
      }, 3000);
    }

    console.log(location);

    // 需求1: 每隔2s 刷新一次页面
    setInterval(() => {
      // location.reload()
    }, 2000);
  </script>
```

#### 13、open

```
<!-- 编程方式开启新的网页:open -->
  <a href="http://www.baidu.com" target="_blank">百度一下</a>

  <!-- 常见于 广告 -->
  <button id="b1">3秒后开启新页面</button>

  <script>
    b1.onclick = function () {
      setTimeout(() => {
        open('http://www.tmooc.cn')
        // JS高级第一天: 在全局中直接用的属性, 存储在 window 里
      }, 3000);
    }
  </script>
```

#### 14、浏览器信息

读取到 浏览器所在的系统信息, 浏览器的插件信息等...

console.log(navigator);

#### 15、历史信息

```
 <!-- 利用 history 的 go 方法 -->
  <!-- go(n): n<0代表后退  n>0代表前进   n=0 代表刷新 -->
  <!-- 如下: n是几,就是几页-->
  <button onclick="history.go(-1)">上一页</button>
  <button onclick="history.go(1)">下一页</button>
  <button onclick="history.go(0)">刷新</button>
  <hr>
  <a href="./04.浏览器信息.html">浏览器信息</a>

  <script>
    console.log(history);
  </script>
```

#### 16、输入框事件

获得焦点：focus 

失去焦点：blur

内容变化：change

实时监听：input

键盘事件：keyup

获取勾选框的勾选状态通过：checked属性
