#                                AJAX

AJAX知识组件

1、HTTP协议

2、DOM常用操作

3、AJAX核心对象

4、服务器对应程序（接口）

### 一、HTTP协议

### 1、HTTP概述

- HTTP就是超文本传输协议，也就是HyperTextTransferProtocol

  #HTTP是互联网的基石，

  #主要功能：传输网页资源（图片、文字、音频、视频）真正互联网快递系统

- HTTPS协议是有HTTP和SSL协议构建的可进行加密传输和身份认证的网络协议，比HTTP协议的安全性更高；

- HTTP基本工作方式

基本工作流程就是：**请求—>响应**；一发一收的模式;

在这个过程中参与请求和应答的是服务器端、客户端、HTTP本身。

### 2、URL

URL 统一资源定位符 Uniform Resource Locator ，我们俗称网址

协议名：即放文该资源应当使用的协议、HTTP和HTTPS和ftp等

s ：安全（对所有发送和接收数据进行加密处理）

主机名：即互联网上主机的标记，可以使域名或IP地址；

端口号：代表服务器上的资源或者特定的服务的门牌号；

80：HTTP  协议的标准端口号；

443： HTTPS；

21 ：ftp  文件传输协议；

22 ：ssh 安全登录、文件传送和端口重定向；

3306： mysql ；

1024-65535： 用来给用户程序自定义端口；

资源路径：即资源在主机的位置，使用/分隔多级目录

参数：是提供给服务器的额外参数

4、HTTP协议内部报文

HTTP协议的核心



请求起始行（浏览器发送请求）/请求头/请求主体

GET     /	 HTTP/1.1

请求行由三部分构成

1、请求的方式：GET/POST 

2、请求的目标：通常是个URL，标记了请求方法要操作的资源；

3、版本号：表示报文使用的HTTP协议邦本

(1)浏览器请求方法

**GET:**  浏览器向服务器**获取**数据(要服务器上东西)，这个资源既可以是静态的文本、页面、图片、视频；

**POST:**  浏览器向服务器**发送**数据，相当于上传数据；

**PUT:**  类似POST，**修改**服务器数据而PUT则是“  ”的含义；

**DELETE: ** **删除**服务器数据；

CONNECT（测试用）:建立特殊的连接隧道;

OPTIONS（测试用）:备用;

TRACE(测试用）:追踪请求;

HEAD(测试用）:是GET方法的“简化版”，也是请求从服务器获取资源，服务器的处理机制也是一样的，但服务器不会返回请求的实体数据，只会传回响应头，也就是资源的“元信息”。比如，想要检查一个文件是否存在，只要发个HEAD请求。

get请求和post不同：

①语义不同，get要数据，post发数据；

②数据发送方式，get通过地址栏url发送数据，post请求主体；

③数据发送大小，get发送数据大小1k~2K（字母几百个），post发送数据大小默认是没有限制的；

④保存，get可以收藏，post不能；

⑤安全，get不安全，post也不太安全（不加密）；

### 二、DOM树

#### 1、js操作HTML内容

将div中的9改为10

```
 <h2 id="msg">9</h2>
    <script>
        document.getElementById('h2');
        var num=Number(msg.innerHTML);//字符串转数值，声明的变量名不能和HTML中变量重复
        num=num+1;
       msg.innerHTML=num;
    </script>
```



#### 2、通过JS创建新标签

在div标签里面添加新元素

```
<!-- 通过js创建新标签 在div中加h1; -->
    <div id="msg"></div>
    <script>
        //发送ajax获取服务器所有商品数量
        //创建字符串中间保存一个或者多个标签
        //将字符串赋值 innerHTML
        var str="<h1>创建</h1>";
        console.log(str);
        msg.innerHTML=str;
    </script>
```

#### 3、动态创建字符串创建商品列表

方案一:添加一行

```
 //创建字符串
var str="<tr><td>3</td><td>黑鲨</td><td>3888</td></tr>";
 //赋值
msg.innerHTML=str;
```

方案二：通过数组动态穿件商品多行；

```
var rows = [
            { id: 1, name: "小米", price: 4999 },
            { id: 2, name: "华为", price: 3999 },
            { id: 3, name: "黑鲨", price: 5999 },
            { id: 4, name: "一加", price: 6999 }
        ];
        //固定写法
        //1、创建变量保存空字符串；
        var str = "";
        //2、创建循环遍历数组每个元素
        for (var i = 0; i < rows.length; i++) {
             //2.1创建变量保存当前对象 
            var obj = rows[i];
            console.log(rows[i]);
           //2.2拼接字符串；模板字符串，str要+=不然只出来一行；
            str += `<tr><td>${obj.id}</td><td>${obj.name}</td><td>${obj.price}</td></tr>`
        }
        //3、循环外为msg赋值
        msg.innerHTML = str;
```

### 三、ajax

#### 1、概念

ajax全称为Asynchronous Java Script and XML 即异步的JavaScript和XML；

##### 1、ajax极大特点：

**ajax是一种发送异步请求并且局部更新网页的技术**（背下来）

##### 2、异步：同步

异步与同步是网络中程序工作的两种方式

异步：工作方式特点：高效，无序

同步：工作方式特点：效率较底，有序

浏览器中提供一个对象XMLHTTPRequest所有ajax功能都是依靠此对象完成ajax

#### 2、作用

主要功能向服务器**发送不同请求**并且**接受服务器返回数据**

#### 3、流程

![image-20220402142853630](D:\WEBStudyRecord\Notes\typora-images\image-20220402142853630.png)

五种状态xhr.readyState

![image-20220402143052046](D:\WEBStudyRecord\Notes\typora-images\image-20220402143052046.png)

##### 1、创建对象；

负责去要数据和拿回来

所有浏览器内置一个对象XMLHttpRequest

**var xhr=new XMLHttpRequest();**

##### 2、打开网络连接；

有一个方法用于指定服务器地址，并且还可以指定请求方式，同步请求或者异步请求；

**xhr.open("请求方式"，"请求服务器地址"，是否异步请求)；**

发送请求

**xhr.send();**

如果发送GET DELETE请求，不需要加参数

如果发送POST PUT 请求要加参数 xhr.send("name=tom");

xhr.open("get","http://127.0.0.1:3000/get2",true)

##### 3、服务器返回的数据放在哪；

**xhr.responseText;**

创建四行代码发送请求并且接收服务器数据

```
创建对象
var xhr= new XMLHttpRequest();
指定服务器地址，与服务器端建立连接
xhr.open("get","http://127.0.0.1:3000/get",trye)
发送
xhr.send();
接受服务器返回数据
xhr.responseText;
```

运行：要在服务器打开，不能直接打开

##### 4、get请求传参

在地址后？参数名=参数值&参数名=参数值

```
创建对象
var xhr=new XMLHttpRequest();
指定服务器地址，与服务器端建立连接
var url="http://127.0.0.1:3000/get3?name=cxxl";
xhr.open("get",url,true);
发送
xhr.send();
接收服务器返回的结果
setTimeout(function(){ console.log(xhr.responseText);
},1000);
服务器
app.get("/get3,(req,res)=>{
res.send(req.query.name+"get3 ok");
});
```

验证用户是否存在

```
 <form action="">
        用户名<input id="input" type="text" placeholder="请输入用户名">
        <input id="btn" type="button" value="验证"><br>
        <span id="msg" style="color: aquamarine;"></span>
    </form>
    <script>
        //1:获取按钮，给按钮加id属性 不能用name
        //2:为按钮绑定事件点击
        btn.onclick = function () {
            //1、创建对象
            var xhr=new XMLHttpRequest();//构造函数，这是个函数
            //2、指定服务器地址
            var url="http://127.0.0.1:3000/exists?name="+input.value;
            console.log(url);
            xhr.open("get",url,true);
            //3、发送
            xhr.send();
            //4、接受数据
            //4.1创建定时器
            setTimeout(function(){
            //4.2在定时器获取服务器返回的结果
                var res=xhr.responseText;
                console.log(res);
            //4.3显示结果
                msg.innerHTML = res; 
            },1000);  
        }
    </script>
```

##### 5、post传参

```
创建对象  
var xhr= new XMLHttpRequest();
指定服务器地址 建立连接 xhr.open("post","http://127.0.0.1:3000/post2",trye)
指定发送数据类型；   在open下方写，注意顺序
                           
发送数据；   send函数内就是请求主体
xhr.send("属性值=属性名&...");
接收
console.log(xhr.responseText);
服务器
app.post("/post3",(req,res)=>{
res.send(req.body.name+"post3 ok");
});
```

显示注册成功

```
 btn.onclick = function () {
            //1、新建对象
            var xhr = new XMLHttpRequest();
            //2、指定服务器地址
            var url = "http://127.0.0.1:3000/login";
            //与服务器端建立连接
            xhr.open("post", url, true);
            xhr.setRequestHeader("Content-type", "application/x-www-form-urlencoded");
            //3、发送数据
            xhr.send("name=input.value");
            //4、设置定时器接收服务器返回的结果
            setTimeout(function () {
                var res = xhr.responseText;
                msg.innerHTML = res;
            },1000);
        }
```

验证用户登录

```
btn.onclick = function () {
            //创建正则表达式
            var reg = /^[a-zA-Z0-9]{3,11}$/
            //验证如果出错提示，如果参数错误，停止函数return
            if (!reg.test(uname.value)) {
                msg1.innerHTML = "用户名格式错误";
                return;
            }
            if (!reg.test(pwd.value)) {
                msg2.innerHTML = "密码格式错误";
                return;
            }
            //创建对象 指定服务器地址建立连接，发送 接收
            //输出用户输入参数
            console.log(uname.value, pwd.value);
            //创建对象
            var xhr = new XMLHttpRequest();
            //指定服务器地址建立连接
            var url = "http://127.0.0.1:3000/login";
            xhr.open("post", url, true);
            //修改数据类型
            xhr.setRequestHeader("Content-type", "application/x-www-form-urlencoded");
            //发送
            var data = `name=${uname.value}&pwd=${pwd.value}`
            console.log(data)
            xhr.send(data);
            //接收
            setTimeout(function () {
                console.log(xhr.responseText);
            }, 1000);
        }    
```



##### 6、错误

hbuilder   启动网页 8804

vscode     启动网页   5505

ajax不能在默认浏览器运行，要在服务器运行；

![image-20220402103824999](D:\WEBStudyRecord\Notes\typora-images\image-20220402103824999.png)

#### 4、json字符串

##### 1、服务器自动会将js对象转json格式的字符串，

‘{"name":"tom","id":"3"}’    JSON格式对象

'[{id:1},{id:2}]'            JSON格式数组

##### 2、前端代码将json字符串转js对象方便操作

**JSON.stringify(obj);** //转换对象为json字符串，服务器自动进行

 **JSON.parse(str);**//转换json字符串为对象

```
1、一个js对象转换json字符串
var obj={id:3,name:"tom"}
var jsonstr=JSON.stringify(obj); #转换为json字符串对象
2、一个JSON字符串转换js对象
var str='{”name":"tom"}'
var obj= JSON.parse(str);#转换为js对象
```

![image-20220402110006405](D:\WEBStudyRecord\Notes\typora-images\image-20220402110006405.png)

#### 5、xhr.readyState

![image-20220402142853630](D:\WEBStudyRecord\Notes\typora-images\image-20220402142853630.png)

五种状态xhr.readyState

![image-20220402143052046](D:\WEBStudyRecord\Notes\typora-images\image-20220402143052046.png)

xhr对象事件 xhr.onreadystatechange=function（）{}

#当xhr.readyState   **状态值发生改变时则触发事件**（接收太快，服务器传的值还没来，添加事件，就不需要定时器协助了）

#### 6、xhr.status

该属性保存着服务器响应状态码

案例：查询服务器内的数据

```
//1:创建对象
 var xhr = new XMLHttpRequest();
//2:打开网络连接 
var url = "http://127.0.0.1:3000/find";
xhr.open("GET", url, true);
//3:发送请求
xhr.send();
//4:为xhr绑定事件 onreadystatechange
xhr.onreadystatechange = function () {
 //4.1；输出xhr状态数据 readyState
 //服务器数据是否完全返回  4
 //服务器发送正确数  2000
   if (xhr.readyState === 4 && xhr.status === 200)
 //将服务器发送的数据转为js对象
   var obj = JSON.parse(xhr.responseText);
 //将data.id显示在h1标签
   msg1.innerHTML =obj.data.id
}
```

##### 案例：管理员登录功能

```
//完成管理员登录功能
        //添加点击事件
        btn.onclick = function () {
            //创建正则表达式
            var reg = /^[a-zA-Z0-9]{3,11}$/;
            //检验用户名格式
            if (!reg.test(aname.value)) {
                tip.innerHTML = '用户名格式错误';
                //停止函数执行
                return;
            }
            //检验密码格式
            if (!reg.test(apwd.value)) {
                tip.innerHTML = '密码格式错误'
                //停止函数执行
                return;
            }
            //创建xhr对象
            var xhr = new XMLHttpRequest();
            //打开网络连接
            var url = "http://127.0.0.1:3000/admin/login"
            xhr.open("post", url, true);
            //修改请求主体数据格式
            xhr.setRequestHeader("Content-type", "application/x-www-form-urlencoded");
            //发送数据
            xhr.send(`aname=${aname.value}&apwd=${apwd.value}`);
            //为xhr绑定事件 xhr.onreadystatechange
            xhr.onreadystatechange = function () {
                //判断  xhr.readyState
                //console.log(xhr.readyState);
                if (xhr.readyState === 4 && xhr.status === 200) {
                    //将获取的服务器返回数据转换为对象
                    var obj = JSON.parse(xhr.responseText);
                    console.log(obj);
                    //判断，如果code:1 跳转 main.html
                    if (obj.code === 1) {
                        location.href = "main.html";
                    }else{
                        tip.innerHTML = '用户名或者密码有误';
                    }
                    //判断如果code:0  tip=innerHTML='用户名或者密码有误';
                }
            }
        }
```

#### 7、跨域常见错误：

![image-20220406093618452](C:\Users\web\AppData\Roaming\Typora\typora-user-images\image-20220406093618452.png)

如果浏览器程序访问其他域名或者端口不同程序，则报错；

通常解决方法是在服务器下载安装cors配置；

![image-20220406094022051](D:\WEBStudyRecord\Notes\typora-images\image-20220406094022051.png)

（2）url地址错误:http://要写全

（3)参数名:传数据时，参数名称是服务器决定的，要与其保持一致；

（4）设置修改数据类型：

（5）常见错误后台服务器错误（没有响应 ）

解决问题：查看服务器工作控制台（Node.js，命令窗口查看）

##### 案例：查询用户列表（管理员登录成功后）

```
//创建xhr对象
        var xhr = new XMLHttpRequest();
        //打开网络连接
        var url = "http://127.0.0.1:3000/admin/list";
        xhr.open("GET", url, true);
        //发送请求
        xhr.send();
        //接收服务器返回数据
        //为xhr绑定事件
        xhr.onreadystatechange = function () {
            //判断状态码
            if (xhr.readyState === 4 & xhr.status === 200) {
                //接收数据
                var obj = JSON.parse(xhr.responseText);
                console.log(obj);
                //创建变量保存空字符串
                var str=""
                //创建循环遍历js对象
                for(var i=0;i<obj.data.length;i++){
                    //拼接
                  str+=`
                  <tr>
                    <td>${obj.data[i].u_id}</td>
                    <td>${obj.data[i].u_names}</td>
                    <td>${obj.data[i].u_phone}</td>
                    <td>${obj.data[i].u_member==1?"会员":"未加入"}</td>
                    <td>操作</td>
                    </tr>
                                                         `;
                 }
                msg.innerHTML=str;
            }
        } 
    </script>
```

易错点：获取的服务器数据obj里面有多种数据，找到data数组

#### 8、案例：删除指定用户

##### 1、选择 删除的网页标签

```
<button></button>   慎选，它也会发送请求，并且刷新网页
<input type="button">  可选，
<a href="#"></a>       可选，会跳转
<a href="javascript:;"></a>  #阻止a自动跳转
```

注意事项：删除数据有一定损坏性操作，对其特殊处理；

口诀：删除之前要提示“是否要删除此数据”

防止用户误删除；

浏览器提供确认框：var rs=confirm（“是否要删除指定数据”）

rs=true 表示用户点击确认；false表示取消

##### 2、注意：地址写法

```
var url = "http://127.0.0.1:3000/admin/del/"+id//`http://127.0.0.1:3000/admin/del/${id}`
```

**id是形参有自己的数值，不能直接写在引号里面，写在里面获取的只是字符串id,需要拼接才能获得id的数值；**

##### 3、自动刷新网页：刷新整个网页所有内容

①location.reload(true);强制刷新网页不允许使用缓存

②location.href="main.html";跳转（自动刷新）

自动刷新网页（`<tbody id="msg"></tbody>`）

删除后，重新发送请求GET http://127.0.0.1:3000/admin/list id="msg"

**解决方法：**添加函数init();将获取服务器数据的过程封装在init内；开始时调用init（）；，在删除用户函数内，显示删除成功后再次调用init（）；

```
<script>
        init();
        //初始化第一次赋值
        function init() {
            //创建xhr对象
            var xhr = new XMLHttpRequest();
            //打开无网络连接
            var url = "http://127.0.0.1:3000/admin/list";
            xhr.open("GET", url, true);
            //发送请求
            xhr.send();
            //接收服务器返回数据
            //为xhr绑定事件
            xhr.onreadystatechange = function () {
                //判断状态码
                if (xhr.readyState === 4 & xhr.status === 200) {
                    //接收数据
                    var obj = JSON.parse(xhr.responseText);
                    console.log(obj);
                    //创建变量保存空字符串
                    var str = ""
                    //创建循环遍历js对象
                    for (var i = 0; i < obj.data.length; i++) {
                        //拼接
                        str += `
                  <tr>
                    <td>${obj.data[i].u_id}</td>
                    <td>${obj.data[i].u_names}</td>
                    <td>${obj.data[i].u_phone}</td>
                    <td>${obj.data[i].u_member == 1 ? "会员" : "未加入"}</td>
                    <td><a onclick="delItem(${obj.data[i].u_id})" href="javascript:;">删除</a></td>
                    </tr>
                     `;//在a标签添加点击事件，调用函数
                    }
                    msg.innerHTML = str;
                }
            } //事件结束
        }//init end

        //完成删除用户函数   id用户编号
        function delItem(id) {
            //显示用户确认的提示框；
            var rs = confirm("是否删除指定数据！" + id);
            //如果用户点击取消则不做任何操作；
            if (!rs) {
                return;
            }
            //创建对象xhr
            var xhr = new XMLHttpRequest();
            //打开链接delete http://127.0.0.1:3000/admin/del/3
            var url = "http://127.0.0.1:3000/admin/del/" + id//`http://127.0.0.1:3000/admin/del/${id}`
            console.log(url);
            xhr.open("DELETE", url, true)
            //发送请求
            xhr.send();
            //为xhr绑定事件 onreadystatechange
            xhr.onreadystatechange = function () {
                //判断xhr.readyState==4 xhr.status==200;
                if (xhr.readyState == 4 && xhr.status == 200) {
                    //接收返回数据
                    var obj = JSON.parse(xhr.responseText);
                    if (obj.code == 1) {
                        //提示删除成功或者删除失败
                        alert(obj.msg);
                        //局部刷新
                        init();
                    } else {
                        alert(obj.msg);
                    }
                }
            }
        }
    </script>
```

#### 9、案例：注册用户

失去焦点事件：.onblur

禁用按钮属性：.disabled=true；

```
  //创建点击事件
        btn.onclick = function () {
            if (u_names.value == "") {
                alert("用户名不能为空");
                return;
            }
            if (u_phone.value == "") {
                alert("用户电话不能为空");
                return;
            }
            if (u_member.value == "") {
                alert("会员不能为空");
                return;
            }
            //新建对象
            var xhr = new XMLHttpRequest();
            //打开连接
            var url = "http://127.0.0.1:3000/user/reg";
            xhr.open("POST", url, true);
            //修改数据类型
            xhr.setRequestHeader("Content-type", "application/x-www-form-urlencoded");
            var str = `u_names=${u_names.value}&u_phone=${u_phone.value}&u_member=${u_member.value}`;
            console.log(str);
            //发送
            xhr.send(str);
            //创建事件
            xhr.onreadystatechange = function () {
                //判断状态码
                if (xhr.readyState == 4 && xhr.status == 200) {
                    //转换数据类型
                    var obj = JSON.parse(xhr.responseText);
                    if (obj.code == 1) {
                        alert(obj.msg);
                        //跳转到修改页面，注意拼接字符串时，等于号不写，会获取不到数值
                         var url="edit.html";
                        url+="?uphone="+u_phone.value;
                        url+="&umember="+u_member.value;
                        url+="&unames="+u_names.value;
                        console.log(100)
                        //2.自动跳转
                        location.href=url;
                    } else {
                        alert(obj.msg);
                    }
                }
            }
        }
```

添加禁用按钮功能

```
 //1.禁用按钮,当用户打开网页时禁用
        btn.disabled = true;
        //2为手机输入框加失去焦点事件
        u_phone.onblur = function () {
            //2.1验证手机号不能为空
            if (u_phone.value == "") {
                alert('手机号不能为空');
                return;
            }
            //2.2创建对象
            var xhr = new XMLHttpRequest();
            //2.3打开网络连接
            var url = `http://127.0.0.1:3000/user/exists?u_phone=${u_phone.value}`;
            xhr.open("get", url, true);
            //2.4发送请求
            xhr.send();
            //2.5接收服务器返回结果
            //创建事件
            xhr.onreadystatechange = function () {
                //判断状态码
                if (xhr.readyState == 4 && xhr.status == 200) {
                    //转为js对象
                    var obj = JSON.parse(xhr.responseText);
                console.log(1);
                    //2.6如果手机号可用；启用按钮
                    if (obj.code == 1) {
                        msg.innerHTML=obj.msg;
                        btn.disabled =false;
                    }else{
                        msg.innerHTML=obj.msg;
                        btn.disabled = true;
                    }
                }
            }
        }
```

错误分析：转js对象要在if里面写

#### 10、案例：修改用户

如何获取地址栏中用户数据；

var str=location.search;//获取跳转网页的地址

var str="uphone=111&uname=tom&umember=1";

var obj=new URLSearchParams(str);#将字符串转为对象

var rs=obj.get('uname')#获取uname的值

易错点：拼接字符串时，观察结果，注意等于号，修改失败时，在后端接口打印获取的数据，观察数据；

```
<script>
        //1.获取查询字符串 location.search;
        var str = location.search;
        console.log(1)
        console.log(str)
        //2.转为对象后放在新建对象中
        var obj = new URLSearchParams(str);
        //3.获取输出
        var unames=obj.get('unames');
        var uphone = obj.get('uphone');
        var umember = obj.get('umember');
        u_phone.value = uphone;
        u_names.value = unames;
        u_member.value = umember;
        console.log(unames,uphone,umember)
        //获取btn按钮绑定点击事件
btn.onclick=function(){
        //新建对象
        var xhr = new XMLHttpRequest();
        //打开网络连接
        var url = "http://127.0.0.1:3000/user/edit";
        xhr.open("PUT", url, true);
        //修改数据类型
        xhr.setRequestHeader("Content-type", "application/x-www-form-urlencoded");
        //发送请求
        //新数据从表单获取，旧数据从上一个网页获取
        var str=`uname=${u_names.value}&uphone=${u_phone.value}&umember=${u_member.value}&oldphone=${uphone}`;//注意要写等于号
        console.log(str)
        xhr.send(str);
        //获取返回结果
        xhr.onreadystatechange=function(){
            if(xhr.readyState==4&&xhr.status==200){
var obj=JSON.parse(xhr.responseText);
if(obj.code==1){
    alert(obj.msg)
}else{
    alert(obj.msg)
}
            }
        }
    }
    </script>
```

