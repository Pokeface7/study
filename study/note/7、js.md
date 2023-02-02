# js

### 1、Web APIs 和 JS 基础关联性

#### 1、JS 基础阶段以及WebAPIs阶段

JS基础学习ECMASCRIPT基础语法为后面做铺垫，web APIs 是JS的应用，大量使用js基础语法做交互效果

#### 2、API和webAPI

API是给程序员提供的一种工具，以便能更轻松的实现想要完成的功能。

webAPI：是浏览器提供的一套操作浏览器功能和页面元素的API（BOM /DOM)。

比如想要一个警示框，直接用alert；

### 2、DOM

文档对象模型（document object model）简称DOM，是W3C组织推荐的处理可扩展标记语言的标准编程接口。

#### 1、DOM树

![微信截图_20220419191128](D:\WEBStudyRecord\Notes\typora-images\微信截图_20220419191128.png)

文档：一个页面就是一个文档，DOM中使用document表示；

元素：页面中的所有标签都是元素，DOM 中使用element表示；

节点：网页中的所有内容（标签，属性，文本，注释等）都是节点，DOM中使用node表示；

DOM把以上内容都看作对象；

#### 2、获取元素

如何获取页面元素

##### 1、根据ID获取

使用getElementById()方法可以获取带有ID的元素对象，返回的是一个元素对象。

```
var timer=document.getElementById(id名)
```

console.dir();打印我们返回的元素对象，更好地车看里面的属性和方法。

##### 2、根据标签名获取：

1、使用getElementsByTagName()方法可以返回带有指定标签名的对象集合。

想要打印里面的元素对象可以遍历数组。

如果该标签只有一个，返回的还是伪数组形式。

如果页面中没有这个标签，返回空的伪数组。

2、可以获取某个元素内部指定标签的子元素；

element.getElementsByTagName(‘标签名’)；

注意：父元素必须是单个对象（必须指明是哪一个元素对象），获取的时候不包括父元素自己；

```
先给ol加个id=ol;
var ol=document.getElementById('ol');
console.log(ol.getElementsByTagName('li'))
```

##### 3、通过HTML新增的方法获取;

1、document.getElementsByClassName('类名')//根据类名返回要还俗对象集合；

2、document.querySelector('选择器')；//根据指定选择器返回第一个元素对象；

选择器要写完整（.nav/#nav）

3、document.querySelectorAll('选择器')；//返回全部元素对象

##### 4、特殊元素获取（body、HTML）

1.获取body

document.body//返回body元素对象

2.获取HTML

document.documentElement;//返回HTML元素对象

#### 3、事件

触发---响应机制

事件由三部分组成：

事件源：事件被触发的对象；

事件类型：什么事件（点击、经过）；

事件处理程序： 通过函数赋值的方式；

点击事件：btn.onclick=function(){}

##### 1、执行步骤

创建点击div控制台输出‘我被选中了’

1.获取事件源

var div=document.querySelector('div');

2.绑定事件

div.onclick

3.添加事件处理程序

div.onclick=function({})

| 鼠标事件    | 触发条件         |
| ----------- | ---------------- |
| onclick     | 鼠标左键点击     |
| onmouseover | 鼠标经过触发     |
| onmouseout  | 鼠标离开触发     |
| onfocus     | 获取鼠标焦点触发 |
| onblur      | 失去鼠标焦点触发 |
| onmousemove | 鼠标移动触发     |
| onmouseup   | 鼠标弹起触发     |
| onmousedown | 鼠标按下触发     |

#### 4、操作元素

##### 1、改变元素内容

element.innerText

从起始位置到终止位置的内容，但它去除HTML标签，同时空格和换行也会去掉。

element.innerHTML

起始位置到终止位置的全部内容，包括HTML标签，同时保留空格和换行。

##### 2、常用元素的属性操作

src/href/id/alt/title

```html
创建点击事件切换图片
<button id="ldh">刘德华</button>
<button id="zxy">张学友</button>
<img src="images/ldh.jpg">
    <script>
        //修改元素属性  src
        //获取元素
        var ldh=document.getElementById('ldh');
        var zxy=document.getElementById('zxy');
        var img=document.getElementById('img');
        //注册事件
        zuy.onclick=function(){
           img.src='images/zxy.jpg' ;
        }
        ldh.onclick=function(){
            img.src='images/ldh.jpg'
        }
</script>
```

