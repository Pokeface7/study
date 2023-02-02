# Vue

WEB开发的发展史：

早期：利用原生DOM实现

中期：jQuery

利用代码封装技巧，简化了DOM操作的代码  旧时代的王者

现在：Vue  尤雨溪

自动化：DOM操作全自动--自动查找到元素然后进行操作

Vue目前有3个版本，从2014开始

Vue1：已淘汰

Vue2：目前主流，但是过渡期

Vue3:未来的主流，市场份额逐步深入

Vue以其简单著称：

- jQuery理念：write less ，do more
- Vue理念：不写，也能做

Vue的开发方式：分两种

- 脚本方式：同JQuery，适合入门阶段
- 脚手架方式：工程化   适合实际开发

### 1、插值语法

```
 <!-- Vue为了简化DOM开发, 提供了大量的新语法, 需要背 -->
  <div id="app">
    <!-- DOM操作的难点之一: 如何选中要操作的元素 -->
    <!-- Vue提供了新的语法 {{}} 插值语法, 可以直观的把数据放在页面中 -->
    <div>亲爱的主人: {{name}}</div>
    <!-- {{}} : 相当于 模板字符串的 ${}, 把HTML当成是模板字符串来用就行 -->
    <!-- 可以在HTML中, 随意书写 JS 代码 -->
    <p>9*9 = {{9 * 9}}</p>
    <p>主人的资产: {{money}}</p>
  </div>

  <!-- 脚本分两种: 开发版vue.js 和 压缩版vue.min.js -->
  <!-- 开发版会提供更多的报错, 适合开发阶段使用 -->
  <script src="./vendor/vue.js"></script>
  <script>
    // Vue: 就是 vue.js 脚本中提供的构造函数
    // Vue会自动创建出一个对象, 来自动操作DOM元素 -- 钢铁侠的战甲
    // 固定的一些配置项, 需要设定

    // el : element元素, 值是 id选择器, 代表使用 Vue 管理的元素
    // 此时, 生成的 Vue对象, 就专为 id=app 的元素而服务
    const v = new Vue({
      el: '#app',
      // data: 数据,  给 el 关联的DOM元素使用的各种数据
      // data中的数据随便写

      // data属性中的元素, 会混入到 创建出来的vue对象里
      data: { money: 900000, name: "家乐" }

      // 我把 钱包(400块)交给了 家乐, 最终会混入到 家乐的口袋里
    })

    // 自动化: 数据变化时, 相关的DOM元素会 自动 更新
    // Vue框架核心竞争力: 数据驱动DOM的变化

    console.log(v)
  </script>
```

### 2、属性绑定

```
 <!-- 
    1个标签由: 标签名 + 内容 + 属性 组成
   -->
  <a href="http://www.baidu.com" id="a1" class="danger" title="百度一下">Baidu</a>

  <div id="app">
    <!-- 标签内容, 用 {{}} 来书写JS代码 -->

    <!-- vue1语法: v-bind:属性名="JS代码" -->
    <!-- vue2语法: :属性名="JS代码" -->
    <a v-bind:href="h" :title="c" :id="a" :class="b">{{d}}</a>

    <!-- 属性名不带: 就是HTML的原生语法, 值是字符串 -->
    <button id="8+8">11</button>
    <!-- 属性名带: 是vue的语法, 其中的值作为JS代码运行 -->
    <button :id="8+8">22</button>
  </div>

  <script src="./vendor/vue.js"></script>
  <script>
    new Vue({
      el: '#app', // 管理 id=app 的元素, el是固定的
      data: {
        a: 101,
        b: 'success',
        c: 'Tmooc',
        d: 'Welcome !',
        h: 'http://tmooc.cn'
      }
    })
  </script>
```

### 3、事件

```
 <div id="app">
    <!-- Vue1 语法: v-on:事件名="方法名" -->
    <button v-on:click="a">点我</button>
    <!-- Vue2 语法: @事件名="方法名" -->
    <button @click="a">来呀!</button>
    <button @click="b">再碰下试试!</button>
  </div>

  <script src="./vendor/vue.js"></script>
  <script>
    new Vue({
      el: '#app',
      // data: 专门存放数据的属性
      // methods: 专门存放方法的属性
      methods: {
        a: function () { alert('别碰我!') },
        // 语法糖: 可以省略 : function
        b() { alert('找揍啊你!') }
      }
    })
  </script>
```

### 4、事件的this

```
 <div id="app">
    <button @click="a">打我</button>
  </div>

  <script src="./vendor/vue.js"></script>
  <script>
    const v = new Vue({
      el: '#app',
      // function的this是 运行时所在对象

      // methods中的元素, 最终会混入到 创建的Vue实例对象中
      // 所以 函数中的this 就是 Vue 实例对象
      methods: {
        // 错误答案: this是methods
        // 家乐买了个锤子,  那么 用锤子打人 就一定是家乐吗??  -- 不, 要看使用者
        a() {
          console.log('this:', this)
          console.log(this == v);
        }
      }
    })

    console.log(v);
  </script>
```

### 5、计数器

```
<div id="app">
    <!-- 当 num 是1, 则按钮不可用 disabled 属性 -->
    <!-- disabled: 不可用, 表单元素带有的属性 -->
    <!-- disabled=true 代表不可用状态生效, 即按钮不可用,  num是1  1==1 true -->
    <!-- disabled=false 代表 不不可用  就是可用 -->
    <button @click="num--" :disabled="num==1">-</button>
    <span>{{num}}</span>
    <!-- 当数量是10, num==10 为true, 不可用 -->
    <button @click="num++" :disabled="num==10">+</button>
    <p>单价: {{price}}</p>
    <!-- Vue的核心竞争力: 数据驱动DOM变化, 数据变化后, 凡是相关的DOM元素都自动变 -->
    <p>总价: {{price * num}}</p>
  </div>

  <script src="./vendor/vue.js"></script>
  <script>
    new Vue({ el: '#app', data: { num: 5, price: 2000 } })
  </script>
```

### 6、事件参数

@事件名="方法名"

```
 <div id="app">
    <h2>选择你的英雄: {{hero}}</h2>
    <button @click="c">蔡文姬</button>
    <button @click="c">瑶</button>
    <button @click="c">猪八戒</button>
    <button @click="c">李白</button>
  </div>

  <script src="./vendor/vue.js"></script>
  <script>
    // 凡是页面上变化的东西, 必然和 数据挂钩
    new Vue({
      el: "#app",
      data: { hero: '待定' },
      methods: {
        c(e) {
          // 事件参数: 凡是事件触发的方法, 都会自带事件参数
          // alert("选择英雄!")
          console.log(e)
          // 修改数据项 = 触发事件的元素上的内容, 页面自然会更新
          this.hero = e.target.innerHTML
        }
      }
    })
  </script>
```

### 7、自定义事件参数

@函数名="方法名(值, $event)"

```
<!-- 
    事件传参分两种方式
    - 1. 利用DOM 的 自定义属性实现,  @事件名="方法名" ,方法的默认第一参 就是事件

    - 2. 抛弃DOM,使用函数传参方式  @事件名="方法名(值, 值...)"
          -- 由于指定了实参后, 则默认的事件参数会消失, 必须用关键词 $event 来传递
   -->

  <div id="app">
    <h2>{{price}}</h2>
    <!-- 为不会自定义传参的用户, 提供了 函数传参语法 -->
    <!-- 自定义传参之后, 默认的事件传参会消失 -->
    <!-- 可以利用 $event 关键词, 来显式传递事件参数 -->
    <button @click="choose(4399, $event)">8G+256G</button>
    <button @click="choose(4899, $event)">12G+256G</button>
    <button @click="choose(4499, $event)">8G+512G</button>
    <button @click="choose(5299, $event)">12G+512G</button>
  </div>

  <script src="./vendor/vue.js"></script>
  <script>
    new Vue({
      el: '#app',
      data: { price: 4399 },
      methods: {
        // Vue作者希望打造的效果: 让不会DOM的人也能书写
        // 自定义属性, 事件参数  都属于DOM知识点

        // 会DOM可以有更多做法, 不会DOM 也能实现 -- 灵活
        choose(p, e) {
          this.price = p
          console.log(e);
        }
      }
    })
  </script>
```

### 8、样式

:style="{属性名: 值}"

:class="{类名: 布尔值}"

```
 <!-- 样式分两类:  style  和 class -->
  <div id="app">
    <!-- 需求: 点击文字, 让字体变大 -->
    <!-- 让属性变化, 代码是JS, 必须用 : 改造 -->

    <!-- :style="{属性名: 值}"   值是对象类型 -->
    <!-- CSS的属性名, 常见 - 间隔, 例如 border-color  font-size  padding-top
    在JS的对象类型里, 属性名不允许中划线   { a-b: 1 }
    解决方案: 1.改小驼峰 fontSize   2.用字符串 'font-size'

    -->
    <div style="color:red" :style="{fontSize: size+'px'}" @click="size++">Hello: {{size}}</div>

    <div style="color:red" :style="{'font-size': size+'px'}" @click="size++">Hello: {{size}}</div>

    <hr>
    <!-- 希望: size是偶数, 就让 ok生效,  奇数就让 err 生效 -->

    <!-- :class="{类名: 布尔值}"  如果值是true就生效, false则不生效 -->
    <div :class="{ok: size%2==0, err: size%2==1}">成龙</div>
  </div>

  <script src="./vendor/vue.js"></script>
  <script>
    // Vue特点: 数据驱动, 凡是页面上会变化的 一定会绑定数据
    new Vue({
      el: '#app',
      data: { size: 17 }
    })
  </script>
```

### 脚手架

> 脚手架是一类软件的总称:  用来生成完善的项目包, 类似`一键安装`
>
> 类似于:
>
> - 原始方式: 先安装电脑系统, 然后自己找软件个性化安装
> - 脚手架: 一键安装, 电脑系统 + 一套常见的软件

- 先安装脚手架软件

  - 前提: node版本在 `12 ~ 16 `   查看`node -v`

- npm需要中国镜像 -- `查看jQuery03 的文档`

- 执行全局安装命令: `npm i -g @vue/cli`

  - 安装完毕后, 通过 `vue --version` 或  `vue -V` 来查看版本号

利用脚手架来生成项目包

> 不是一定要自己生成, 可以使用别人生成的包, 例如 百度网盘上的 `vue-pro`

- 在你要生成项目的目录下, 执行命令: `vue create vue-pro`
  - 范式: `vue create 包名` , 即 `vue-pro` 是自定义的包名, 可以随便起

![image-20220518214015216](C:\Users\深海钢琴师\AppData\Roaming\Typora\typora-user-images\image-20220518214015216.png)

个性化选项

![image-20220518214038334](C:\Users\深海钢琴师\AppData\Roaming\Typora\typora-user-images\image-20220518214038334.png)

选择 vue2 版本

![image-20220518214051184](C:\Users\深海钢琴师\AppData\Roaming\Typora\typora-user-images\image-20220518214051184.png)

直接回车

![image-20220518214102447](C:\Users\深海钢琴师\AppData\Roaming\Typora\typora-user-images\image-20220518214102447.png)

直接回车

![image-20220518214117133](C:\Users\深海钢琴师\AppData\Roaming\Typora\typora-user-images\image-20220518214117133.png)

直接回车

![image-20220518214148087](C:\Users\深海钢琴师\AppData\Roaming\Typora\typora-user-images\image-20220518214148087.png)

直接回车

![image-20220518214129033](C:\Users\深海钢琴师\AppData\Roaming\Typora\typora-user-images\image-20220518214129033.png)

成功

![image-20220518214205972](C:\Users\深海钢琴师\AppData\Roaming\Typora\typora-user-images\image-20220518214205972.png)

- 如果安装了 Git 软件, 可能会有额外的提示, 不用管
- 如果生错了, 则到文件夹里 删除掉, 然后重新生

### 编程方式

要求使用 `VSCODE` 软件 直接打开生成的项目包: `vscode 专门为此项目包服务, 会有各种优化`

![image-20220518214255152](C:\Users\深海钢琴师\AppData\Roaming\Typora\typora-user-images\image-20220518214255152.png)

### 自带服务器

> 脚手架生成的项目包中, `自带服务器`

运行项目包中的服务器

- 在项目包目录下运行 cmd
- 命令: `npm run serve`

> 开启时 偶尔会卡住, 在命令行上按 回车 ,大概率能解决

![image-20220518214313433](C:\Users\深海钢琴师\AppData\Roaming\Typora\typora-user-images\image-20220518214313433.png)

端口号如果被占用, 会自动改成别的, 例如 8080  -> 8081  -> 8082...

![image-20220518214328518](C:\Users\深海钢琴师\AppData\Roaming\Typora\typora-user-images\image-20220518214328518.png)

VSCode提供`傻瓜式`开启方式

![image-20220518214339687](C:\Users\深海钢琴师\AppData\Roaming\Typora\typora-user-images\image-20220518214339687.png)

插件：Vetur      /     Vue Vscode Snippets

### 项目包分析

`public`: 静态资源文件夹

favicon.ico : 标签栏上的图标

![image-20220518214443430](C:\Users\深海钢琴师\AppData\Roaming\Typora\typora-user-images\image-20220518214443430.png)

`index.html`: 固定名称的文件, 作为服务器默认的首页

![image-20220518214506595](C:\Users\深海钢琴师\AppData\Roaming\Typora\typora-user-images\image-20220518214506595.png)

`src`: 专门存放代码

- main.js

  ![image-20220518214524919](C:\Users\深海钢琴师\AppData\Roaming\Typora\typora-user-images\image-20220518214524919.png)

![image-20220518214537499](C:\Users\深海钢琴师\AppData\Roaming\Typora\typora-user-images\image-20220518214537499.png)

App.vue

![image-20220518214636260](C:\Users\深海钢琴师\AppData\Roaming\Typora\typora-user-images\image-20220518214636260.png)

key

![image-20220518214701846](C:\Users\深海钢琴师\AppData\Roaming\Typora\typora-user-images\image-20220518214701846.png)

```
<template>
  <div>
    <!-- .vue文件是专为 Vue 而生的 -->
    <!-- 安装插件以后:  使用 v 可以看到各种提示 -->
    <h1 class="box">我的第一个Vue</h1>
    <!-- 脚手架可以精准定位报错, 显示在页面上 -->
    <button @click="num++">{{ num }}</button>
  </div>
</template>

<script>
// 旧语法的导出/暴露模块到外部 module.exports = {}
// 新语法的导出 export default {}

// 之前写法: new Vue({配置项})
// {}: 中用来书写配置项
export default {
  // vdata
  // 在脚手架中, 要求 data 是个函数类型, 返回数据项 -- 以后解释,和复用有关
  data() {
    return {
      num: 10,
    };
  },
};
</script>

<style lang="scss" scoped>
.box {
  border: 2px solid red;
  padding: 10px;
}
</style>
```



```
<template>
  <!-- template下, 只能有一个子元素 -->
  <!-- template 和 div 相同, 是vue提供的标签 虚拟标签，不能添加样式 -->
  <!-- <div></div> -->
  <div>
    <!-- main.js文件, 固定加载名字是 App.vue 的文件 -->
    <!-- 把 App.vue 复制改名, 就属于备份 -->
    <!-- 以后使用时, 可以到 main.js 中, 把第二行 的文件名, 改成你要加载的文件即可 -->
    <div id="pages">
      <!-- 循环数组生成的DOM元素, 最好是添加 唯一标识 key -->
      <!-- 为什么? -->
      <!-- key的用途在于 数组可能会发生变化的场景 -- 增 或 删除数据 -->
      <!-- 发生增删的时候, 相同唯一标识的元素 会直接复用 而不需要进行修改 -- 提高性能 -->

      <!-- key可以不写, 一旦有数组增删, 则性能偏低 -->
      <!-- 不过 vscode 推荐大家写, 所以 不写会爆红 -->
      <span v-for="n in 10" :key="n">{{ n }}</span>
    </div>

    <!-- 数组的shift方法, 删除第一个元素 -->
    <button @click="names.shift()">删除小马</button>
    <ul>
      <!-- 最好不要用序号, 数组内容变化会导致序号变化 -->
      <!-- 重复唯一标识会报错, 如果没有唯一标识可用, 只能勉强用 序号 index -->
      <li v-for="(value, index) in names" :key="value">
        {{ index }}_{{ value }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      names: ["小马", "亮亮", "铭铭", "楠楠", "楠楠"],
    };
  },
};
</script>
```

关于key:

- 有可能重复的 不可以
- 有可能变化的 不可以, 例如 `序号`, 除非实在找不到唯一标识, 可以凑合用
- 例如: `数据库查询出来的元素的 id ` 可以

```
<template>
  <div>
    <div id="page">
      <!-- 动态  :class="{ 类名: true/false }" -->
      <span
        v-for="n in 10"
        :class="{ active: current == n }"
        :key="n"
        :data-n="n"
        @click="current = n"
      >
        {{ n }}
      </span>
    </div>
    <h3>current: {{ current }}</h3>
  </div>
</template>

<script>
export default {
  data() {
    return {
      // vue的核心: 数据驱动 -- 凡是页面上会变的, 都和数据 有关
      current: 1, //当前是哪个页号
    };
  },
};
</script>

<style lang="scss" scoped>
// 如果你的后台报错: 关键词是 sass-loader, 说明你创建项目时没有安装对应模块
// 重新按照笔记创建新的项目包
#page {
  background-color: lightgray;
  padding: 20px;
  user-select: none;

  span {
    width: 50px;
    text-align: center;
    line-height: 50px;
    display: inline-block;
    background-color: white;
    color: #4e6ef2;
    border-radius: 4px;
    margin: 5px;

    // & 读并且, 代表当前所在的父, 即span
    &:hover {
      background-color: #4e6ef2;
      color: white;
    }
    // span.active 即 <span class='active'
    &.active {
      background-color: #4e6ef2;
      color: white;
    }
  }
}
</style>
```



### 9、常见Vue指令

#### 1、v-text: innerText

#### 2、v-html: innerHTML

```
 <div id="app">
    <!-- 原生DOM中
       innerHTML: 标签的内容, 赋值当做HTML进行解析  
       innerText: 标签的内容, 赋值当做普通文本显示 

       会覆盖标签中原有内容
      -->
    <div v-text="msg">Hello</div>
    <div v-html="msg">小马哥</div>
  </div>

  <script src="./vendor/vue.js"></script>
  <script>
    new Vue({
      el: '#app',
      data: { msg: "<h1>Welcome to Vue!</h1>" }
    })
  </script>
```

#### 3、v-show: 利用css的display:none 来隐藏元素

```
<div id="app">
    <button @click="show = true">显示</button>
    <button @click="show = false">隐藏</button>
    <!-- 变量值 = 其反值 -->
    <button @click="show = !show">切换</button>
    <!-- 指令: directive -->
    <!-- 每个元素都拥有很多系统属性, 也可以用 data- 声明自定义属性 -->
    <!-- 而 vue 也提供了一些属性, 都是 v- 开头的, 称为 指令 -->

    <!-- v-show: 值是false 会自动添加 display:none -->
    <div v-show="show" id="box"></div>

    <!-- 之前学过的 v-bind   v-on 都是指令, 因为太常用, 所以有语法糖 -->
    <!--           :         @ -->
  </div>
  <script src="./vendor/vue.js"></script>
  <script>
    new Vue({
      el: '#app',
      // vue核心思想: 数据驱动DOM变化,  凡是变化的DOM必然捆绑一个数据
      data: { show: false }
    })
  </script>
```

#### 4、v-if: 通过删除元素 来隐藏元素

```
<div id="app">
    <button @click="a = true">添加</button>
    <button @click="a = false">移除</button>
    <div>a: {{a}}</div>
    <!-- 指令 v-if   如果条件true 添加元素;  false 移除元素 -->
    <!-- 面试题: v-if 和 v-show 都能让元素隐藏, 区别在哪里?? -->
    <!-- v-show: 利用css display:none -- 消耗资源少, 适合频繁切换 -->
    <!-- v-if : 利用 删除DOM元素实现 -- 消耗资源更多, 适合不频繁的切换 -->
    <!-- 通俗来说: 你希望元素永远消失, 用if;  元素短期内消失 show -->
    <div id="box" v-if="a"></div>
  </div>

  <script src="./vendor/vue.js"></script>
  <script>
    new Vue({ el: '#app', data: { a: false } })
  </script>
```

#### 5、v-else, v-else-if  配合 v-if使用

```
<div id="app">
    <h3>小马哥的月考分数: {{score}}</h3>
    <button @click="getScore">随机获取分数</button>
    <p v-if="score < 60" style="color:red">2203班再见!</p>
    <p v-else-if="score>=60 && score<80">加油! 再接再厉!</p>
    <p v-else-if="score>=80 && score<=99">优秀! 你是最棒的!</p>
    <p v-else>逆天! 作弊了吧??</p>

    <!-- if  elseif else : 复习 亮亮部分 -->
  </div>
  <script src="./vendor/vue.js"></script>
  <script>
    new Vue({
      el: '#app',
      data: { score: null },
      methods: {
        getScore() {
          // floor: 向下取整, 例如 100.9999  也是100
          this.score = Math.floor(Math.random() * 101)
        }
      }
    })
  </script>
```

#### 6、v-for: 遍历

```
 <div id="app">
    <!-- for(let key in obj){} -->
    <!-- for(let value of arr){} -->

    <!-- 作者 把 for 循环和 DOM元素直接合并 -->
    <!-- 直接在DOM元素上循环, 自动生成多个 -->
    <!-- 格式 v-for="变量 of 数组" -->
    <button v-for="value of names">{{value}}</button>
    <!-- of 和 in 都可以作为中间词, 效果相同 -->
    <hr>
    <button v-for="x in names">{{x}}</button>
    <hr>
    <!-- 支持遍历数字 -->
    <button v-for="n in 10">{{n}}</button>
    <!-- 带有序号的遍历 -->
    <ul>
      <!-- v-for="(值, 序号) in 数组" -->
      <li v-for="(value, index) in names">{{index}} . {{value}}</li>
    </ul>
  </div>

  <script src="./vendor/vue.js"></script>
  <script>
    new Vue({
      el: '#app',
      data: {
        // 需求: 把数据放在按钮标签里, 显示到页面;    先map -> 拼接 -> 添加
        names: ['亮亮', '铭铭', '楠楠', '涛涛']
      }
    })
  </script>
```

#### 7、v-on: 事件绑定, `@`

#### 8、v-bind: 属性绑定 `:`

#### 9、v-pre: 原样显示代码, `{{}}`

```
 <div id="app">
    <!-- {{}} 是一个特殊的语法, 其内容是 JS 代码 -->
    <div>{{ 8 + 8 }}</div>
    <!-- pre: 显示代码本身, 内容作为普通字符串展示 -->
    <div v-pre>{{ 8 + 8 }}</div>
  </div>

  <script src="./vendor/vue.js"></script>
  <script>
    new Vue({ el: '#app' })
  </script>
```

#### 10、v-once`: 一次性, 把初始值显示后, 后续不会更新

```
<div id="app">
    <button @click="num++">num+1</button>
    <p>{{num}}</p>
    <!-- 指令 v-once: 一次性渲染, 数据变化时不会随着变化 -->
    <p v-once>初始值: {{num}}</p>
  </div>

  <script src="./vendor/vue.js"></script>
  <script>
    new Vue({ el: '#app', data: { num: 10 } })
  </script>
```

`脚手架`: 一类软件的总称, 可以`一键自动生成项目包`

- 先安装 -> 再生成
- vue项目包: 自带服务器 + 带有很多模块能直接用

`key`:

- 面试总问有什么用
- 给数组遍历生成的DOM元素 加唯一`标识`
- 当`数组`发生增删时, 要生成的新元素 如果 标识和旧元素一样, 会直接复用

#### 练习：制作表格

```
<template>
  <div class="app">
    <table>
      <thead>
        <td>序号</td>
        <td>种类</td>
        <td>单价</td>
        <td>数量</td>
        <td>总价</td>
      </thead>
      <tbody>
        <tr v-for="({ pname, price, count, max }, i) in products" :key="i">
          <td>{{ i + 1 }}</td>
          <td>{{ pname }}</td>
          <td>{{ price }}</td>
          <td>
            <!-- 修改数组中的值：必须通过数组一步步查到里面的值，不能直接用count修改 -->
            <button @click="products[i].count--" :disabled="count == 1">
              -</button
            ><span class="count">{{ count }}</span
            ><button @click="products[i].count++" :disabled="count == max">
              +
            </button>
          </td>
          <td>{{ price * count }}</td>
        </tr>
      </tbody>
      <tfoot>
        <tr>
          <td colspan="6">总价:{{ sum }}</td>
        </tr>
      </tfoot>
    </table>
  </div>
</template>

<script>
export default {
  //计算属性的作用：函数不用()也能触发，适合不带参数的函数
  //固定属性：存放在这里的方法，使用时不用(),会自动触发
  computed:{
    sum() {
      //一般写法
      // let s = 0;
      // this.products.forEach((p) => (s += p.price * p.count));
      // return s;

      //reduce写法（）需要两个return
      // return this.products.reduce((s,p)=>
      //   { return s+p.price*p.count},0)
        //简写
        return this.products.reduce((s,p)=>
          s+p.price*p.count,0)
    },
  },
  methods: {
    total() {
      //遍历product，把每个商品的总价计算在一起
      let s = 0;
      this.products.forEach((p) => (s += p.price * p.count));
      return s;
    },
  },

  data() {
    return {
      products: [
        { pname: "香蕉", price: 9, count: 10, max: 40 },
        { pname: "苹果", price: 15, count: 1, max: 30 },
        { pname: "鸭梨", price: 19, count: 10, max: 20 },
        { pname: "荔枝", price: 29, count: 34, max: 60 },
        { pname: "葡萄", price: 39, count: 12, max: 50 },
      ],
    };
  },
};
</script>

<style lang="scss" scoped>
table {
  border-collapse: collapse;
  user-select: none;
  .count {
    display: inline-block;
    margin: 0 5px;
    min-width: 35px;
    text-align: center;
  }
  thead {
    background-color: #eee;
  }
  td,
  th {
    border: 1px solid gray;
    padding: 3px 30px;
  }
}
</style>
```

### 10、计算属性computed

computed：{  方法    }



计算属性的作用：函数不用()也能触发，适合不带参数的函数

固定属性：存放在这里的方法，使用时不用(),会自动触发

 **注意：**

@click="事件"   这个事件必须是 通过点击才能触发的 ；

  事件不能写在计算属性里, 因为不应该自动触发, 必须是手动触发 要写在methods中；

```
computed:{
    sum() {
      //一般写法
      // let s = 0;
      // this.products.forEach((p) => (s += p.price * p.count));
      // return s;

      //reduce写法
      // return this.products.reduce((s,p)=>
      //   { return s+p.price*p.count},0)
        //简写
        return this.products.reduce((s,p)=>
          s+p.price*p.count,0)
    },
```

运用场景：当需要进行数值计算，并且依赖于其他数据时，应该使用，因为可以利用其缓存特性，避免每次获取值都要重新计算；

computed和methods的区别：

可以将同一个函数定义为一个方法或者一个计算属性。对于最终的结果，两种方式是相同的。

不同点：

- computed：计算属性是基于它们的依赖进行缓存的。只有在它的相关依赖发生改变时，才会重新计算；
- methods调用总会执行该函数

```

```



### 11、双向数据绑定

v-model

数据传递方向1: 从 data 中, 传递到 DOM元素里；

 数据传递方向2: 当用户修改表单元素时, 自动更新绑定的数据项；

 这套操作就叫: 双向数据绑定；

Form表单元素有一个特色: 按钮 单选框 多选框 输入框 等, 都能和用户交互

v-model: 输入框变化会实时更新到 uname 变量,  uname变量就存储的是输入框值

**小技巧：**

 需求: x是0, 显示 girl   x是1 显示 boy  x是2 显示 secret 

    <p>{{ ["girl", "boy", "secret"][x] }}</p>
    <!-- 常见操作: 数据库中 存储选项类型的变量, 用序号 0 1 2 3 ... -->
    <!-- 前端通常搭配 数组, 认为创造巧合 -->

### 12、单选框

```
<template>
  <div>
    <!-- 有几个选项的数据类型, 在数据库中最好用 0 1 2 来代表 -->
    <span>男</span>
    <input type="radio" name="sex" value="1" v-model="x" />
    <br />
    <span>女</span>
    <input type="radio" name="sex" value="0" v-model="x" />

    <br />
    <span>保密</span>
    <input type="radio" name="sex" value="2" v-model="x" />

    <h3>x:{{ x }}</h3>
    <!-- 需求: x是0, 显示 girl   x是1 显示 boy  x是2 显示 secret -->
    <p>{{ ["girl", "boy", "secret"][x] }}</p>

    <!-- 常见操作: 数据库中 存储选项类型的变量, 用序号 0 1 2 3 ... -->
    <!-- 前端通常搭配 数组, 认为创造巧合 -->

    <!-- 数组[序号] -->
    <!-- ["girl", "boy", "secret"][0] -->
  </div>
</template>

<script>
export default {
  data() {
    return {
      x: 0,
    };
  },
};
</script>

<style lang="scss" scoped>
</style>
```



### 13、勾选框

```
<template>
  <div>
    <!-- 勾选 -->
    <input type="checkbox" v-model="agree" />
    <span>雷佳乐先生, 您愿意娶 如花 吗? {{ agree }}</span>

    <div v-show="agree">我愿意!</div>

    <input type="checkbox" @change="chb" />
  </div>
</template>

<script>
export default {
  methods: {
    chb(e) {
      // 勾选框的值 是 checked属性, 是开发HTML的人 设定的
      // 尤雨溪 在写v-model的时候, 自动判断所在的元素是什么类型, 如果是checkbox 就读取 checked 属性,  如果是 input 就读取value属性
      console.log(e.target.checked);
    },
  },

  data() {
    return {
      agree: false,
    };
  },
};
</script>

<style lang="scss" scoped>
</style>
```



### 14、多选框

```
<template>
  <div>
    <!-- 多选框 -->
    <h3>家乐: 选择你的爱好 {{ skills }}</h3>
    <ul>
      <li>
        <!-- 勾选框有两种作用, 单独使用代表是否勾选 -- checked属性就行 -->
        <!-- 勾选框做多选: 则需要设置 value, 代表其对应的值 -->
        <input type="checkbox" value="唱" v-model="skills" />
        <span>唱</span>
      </li>
      <li>
        <!-- 尤雨溪: 自动判断参数类型, 是数组就加入, 是boolean, 就是true/false -->
        <input type="checkbox" value="跳" v-model="skills" />
        <span>跳</span>
      </li>
      <li>
        <input type="checkbox" value="rap" v-model="skills" />
        <span>rap</span>
      </li>
      <li>
        <input type="checkbox" value="篮球" v-model="skills" />
        <span>篮球</span>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      // 多选操作, 值是多个, 要存储在数组里
      skills: [],
    };
  },
};
</script>

<style lang="scss" scoped>
</style>
```



### 15、下拉菜单

```
<template>
  <div>
    <!-- 下拉选框 -->
    <h3>请家乐先生选择您的座驾: {{ car }}</h3>
    <select v-model="car">
      <option value="0">思域</option>
      <option value="1">凯迪拉克</option>
      <option value="2">奥迪</option>
      <option value="3">宝马</option>
      <option value="4">奔驰</option>
      <option value="5">保时捷</option>
      <option value="6">法拉利</option>
    </select>
  </div>
</template>

<script>
export default {
  data() {
    return {
      car: 5,
    };
  },
};
</script>

<style lang="scss" scoped>
</style>
```



### 16、购物车

```
<template>
  <div>
    <table>
      <thead>
        <tr>
          <th>
            <!-- 当 勾选状态变化时, 触发 change 事件 -->
            <!-- 勾选状态属性: checked , 其值是计算属性计算而来的-->
            <input type="checkbox" @change="checkAll" :checked="chb_all" />
            <span>全选</span>
          </th>
          <th>商品名</th>
          <th>单价</th>
          <th>数量</th>
          <th>小计</th>
          <th>操作</th>
        </tr>
      </thead>

      <tbody>
        <tr v-for="({ name, price, num }, i) in products" :key="i">
          <td>
            <!-- v-model: 双向数据绑定, 绑定的一定是 data 中的数据项 -->
            <input type="checkbox" v-model="products[i].checked" />
          </td>
          <td>{{ name }}</td>
          <td>{{ price }}</td>
          <td>
            <button @click="products[i].num--" :disabled="num == 1">-</button>
            <!-- 双向绑定, 必须绑定 data 中的 -->
            <input type="text" v-model="products[i].num" />
            <button @click="products[i].num++">+</button>
          </td>
          <td>{{ price * num }}</td>
          <td>
            <!-- 数组.splice(i, n): 删除序号i开始 的 n个元素 -->
            <!-- ['小马', '小雷', '小蔡'].splice(0, 1) 删除序号0开始的1个元素 -->
            <button @click="products.splice(i, 1)">删除</button>
            <button @click="removeP(i)">删除</button>
          </td>
        </tr>
      </tbody>

      <tfoot>
        <tr>
          <td colspan="6">总价格: {{ sum }}</td>
        </tr>
      </tfoot>
    </table>
  </div>
</template>

<script>
export default {
  methods: {
    //全选
    checkAll(e) {
      // e.target 看 DOM03 事件冒泡部分
      console.log(e.target.checked); // 全选按钮的勾选状态 true/false

      // 遍历数组, 把每个元素的 checked 都变成和 全选一样
      this.products.forEach((p) => (p.checked = e.target.checked));
      // 关于参数p: 必须复习 JS高级的 高阶函数函数部分

      var obj = { num: 4 };
      var b = obj.num;
      b = 10; //不会影响 obj.num,  值传递
      //修改obj的num属性, 必须是 obj.num = 10

      // 类似: 给班级每个同学 发个雪糕
      // 同学们.forEach( 每个同学 => 每个同学.手里 = 雪糕)
    },

    removeP(i) {
      // this代表当前vue对象, 详见 vue01 的 this 部分讲解
      this.products.splice(i, 1);
    },
  },

  // 计算属性
  computed: {
    // 全选状态:  数组中的每一个(every)元素 都是勾选, 则是全选
    chb_all() {
      // every: 检测数组中, 每个元素的 checked 属性, 都是真的 结果才是true
      return this.products.every((p) => p.checked);
      // JS高级 的 高阶函数, 大概在 Day04
    },

    sum() {
      // return this.products.reduce((a, p) => a + p.price * p.num, 0);

      let s = 0;
      // 只累加勾选的, 即 checked 是 true 的;  checked是false , 就不会累加
      // 因为数学运算中, true->1  false->0   任何数字x0 都是0
      this.products.forEach((p) => (s += p.price * p.num * p.checked));
      return s;
    },
  },

  data() {
    return {
      products: [
        { name: "兰蔻小黑瓶", price: 1080, num: 5, checked: true },
        { name: "欧莱雅套装", price: 339, num: 1, checked: false },
        { name: "SK-II", price: 1540, num: 10, checked: true },
        { name: "香奈儿5号", price: 568, num: 3, checked: true },
        { name: "海洋之谜", price: 4080, num: 1, checked: false },
        { name: "six god", price: 12, num: 20, checked: false },
      ],
    };
  },
};
</script>

<style lang="scss" scoped>
table {
  user-select: none;
  border-collapse: collapse;

  thead {
    background-color: #eee;
  }

  td,
  th {
    border: 1px solid gray;
    padding: 5px 30px;
    text-align: center;
  }

  //属性选择器
  [type="text"] {
    width: 50px;
    text-align: center;
  }
}
</style>
```

### 17、自定义属性

在direction属性下添加方法，利用v-方法名调用



```
 <!-- v-xx="JS代码"  指令的值是JS代码 -->
      <li v-color="'purple'">凯凯</li>
      <li v-color="'blue'">小马</li>
      <li v-color="'orange'">小婷</li>

      <!-- 仿写系统的 v-text, 让值原样显示到 标签里 -->
      <li v-textH="'<h1>Hello World</h1>'"></li>

      <!-- 自定义指令 v-green, 作用是让DOM元素变绿 -->
      <!-- v- 是指令的固定前缀 -->
      <li v-green>亮亮</li>
      <li v-red>家乐</li>
 ////////////////////////
 
 directives: {
    textH(sui, bian) {
      sui.innerText = bian.value;
    },

    // v-color="'purple'"
    color(el, bindings) {
      // el: 参数1, 代表当前元素
      // bindings: 参数2, 绑定的值
      console.log("bindings:", bindings);

      el.style.color = bindings.value; //value是什么,详见后台打印
    },
    // v-red
    red(suibian) {
      suibian.style.color = "red";
    },

    // v-green:  v- 固定前缀   green 名称
    green(el) {
      // 参数1: 指令所在的元素
      console.log("el:", el);
      console.dir(el);
      el.style.color = "green";
    },
  },
```

### 18、自定义指令

生命周期:组件创建到销毁的过程

```
<template>
  <div>
    <!-- 指令的生命周期 -->
    <!-- 生命周期: 拟人的说法 丛生到死经历的过程 -->
    <!-- 例如: 备孕->怀孕->待产->出生->学习中..->学习完->快死了->死了 -->
    <!-- 指令: 创建->绑定在DOM元素->寄生在DOM上 -> 销毁 -->
    <input type="text" />
    <br />
    <!-- v-focus: 调用DOM元素的 focus 方法, 让其获得焦点 -->
    <input type="text" v-focus />
    <br />
    <input type="text" />
  </div>
</template>

<script>
export default {
  directives: {
    // DOM元素: 先创建 -> 设置各种属性 -> 添加到页面上显示
    // 详见 : 案例.html
    focus: {
      // 自选生命周期, 来触发函数
      inserted(el) {
        // insert: 插入, 代表 DOM元素 插入到 页面上显示
        el.focus();
        // 指令所在的元素, 添加到页面上的时候, 触发 焦点
      },
    },

    // 下方写法: 是指令的语法糖写法, 其触发时机 是 DOM元素创建和更新时
    // focus(el) {
    //   console.dir(el); // 找 原型 -> 原型 -> 原型 里, 有focus方法,
    //   // 作用: 让DOM元素获取焦点
    //   el.focus();
    // },
  },
};
</script>
<style lang="scss" scoped>
</style>
```

案例；

```
 <div id="box"> </div>

  <script>
    const inp = document.createElement('input')
    inp.id = 'b1';
    inp.type = 'text'
    inp.className = 'danger';
    inp.innerText = "xxx"
    // inp.focus() //位置1

    // 以上的代码, 都是在内存中构建元素 -- 在肚子里

    box.appendChild(inp) // 添加到页面上-- 降世
    inp.focus() //位置2
  </script>
```

### 19、ref

ref: 可以把一个变量 绑定在元素上,使用 ref 属性, 可以把变量绑定在 DOM元素上, 变量存储在 $refs 中;

```
<template>
  <div>
    <input type="text" />
    <br />
    <!-- ref: 可以把一个变量 绑定在元素上 -->
    <input type="text" ref="inp" />
    <br />
    <input type="text" />
    <br />
    <button @click="doFocus">获得焦点</button>
    <p ref="suibian">Hello World!</p>
  </div>
</template>

<script>
export default {
  methods: {
    doFocus() {
      // 让第二个输入框获得焦点, 即 调用其 focus 方法
      // const inp = document.querySelectorAll("input")[1];
      // inp.focus();

      console.log("this:", this);
      console.log("$ref:", this.$refs);
      // 使用 ref 属性, 可以把变量绑定在 DOM元素上, 变量存储在 $refs 中
      this.$refs.inp.focus();

      this.$refs.suibian.style.color = "red";
    },
  },
};
</script>

<style lang="scss" scoped>
</style>
////////////////////////////////
<template>
  <div>
    <button @click="doSome">表达心意</button>

    <!-- 本质上自动完成下方两行: -->
    <!-- const x = document.querySelector('p') -->
    <!-- $refs['map'] = x -->
    <p ref="map">小马666</p>
    <!-- 把变量和元素绑定在一起, 然后存储在 $refs 里 -->
  </div>
</template>

<script>
export default {
  methods: {
    doSome() {
      this.$refs.map.style.color = "green";
    },
  },
};
</script>

<style lang="scss" scoped>
</style>


```

### 20、组件

```
<template>
  <div>
    <!-- 组件: component  -->
    <!-- 含义: 组成页面的零件 -->
    <!-- 作用: 拆分 + 复用, 把一个大型的网页拆分成 零碎的部件 -->
    <!-- 在开发领域的重要程度相当于: 活字印刷术 -->
    <!-- 把大型网页中的内容, 拆分成独立的一个个模块, 最后再组合到一起 -->
    <!-- components: 专门放组件的文件夹 -->
     <!-- 以为组件过于常用,所以VSCode软件提供了人性化的 自动导入操作 -->
    <!-- 先写 <  然后写组件名, 通过代码提示可以自动生成 -->
    <!-- 但是: 小概率会生成失败, 还是需要查看下代码的 -->

    <!-- 使用: 单标签必须闭合  <标签名 /> -->
    <one-com />

    <!-- 作者为了满足不同人的癖好: 提供了各种语法, 挑你喜欢的 -->
    <one-com></one-com>
    <OneCom />
    <OneCom></OneCom>
  </div>
</template>

<script>
// 使用组件分3步:  引入  -> 注册  -> 使用

// 模块导入语法(旧)
// const OneCom = require("./components/OneCom.vue")

// 模块导入语法(新)
import OneCom from "./components/OneCom.vue";

export default {
  // 把 OneCom 组件, 注册到当前 App.vue 里
  components: { OneCom },
};
</script>

<style lang="scss" scoped>
// 使用组件时, 通常需要为 外来的组件 进行定位操作: 调整位置

// 习惯: 给组件最外层div 一个 class, 与组件名相关
// 使用组件时, 就能猜到组件的class名
.one-com {
  border-radius: 3px;
  margin-top: 10px;

  &:last-child {
    position: fixed;
    bottom: 0;
  }
}
</style>
//////////////////////////////
在compons文件夹下创建组件
<template>
  <!-- 组件名要求 大驼峰 格式 -->
  <!-- 习惯给根div, 添加class 名称与文件名相同 -->
  <div class="one-com">
    <h1>你好, 我的第一个组件</h1>
  </div>
</template>

<script>
export default {};
</script>

<style lang="scss" scoped>
.one-com {
  padding: 10px;
  background-color: aqua;
}
</style>

```

### 21、组件传参props

使用props属性声明参数， 通过 props 属性来声明参数, 用于接收外来的传参

```
//组件
<template>
  <div class="three-com">
    <div>我是{{ who }}, 今晚在 {{ where }} 等我!</div>
  </div>
</template>

<script>
export default {
  // props: 用于声明组件接收的参数, 即 形参
  // 参数用字符串类型标识
  props: ["who", "where"],
};
</script>

<style lang="scss" scoped>
.three-com {
  border: 2px solid blue;
  color: blue;
  padding: 10px;
  border-radius: 4px;
  margin-top: 10px;
}
</style>


////////////////////////////////
主文件
<template>
  <div>
    <!-- 希望组件复用时, 能够接收参数, 产生变化 -->
    <!-- 知识点: 组件传参 -- 和函数传参套路相同! -->
    <!-- 函数传参的套路: 形参 实参  -->
    <three-com who="Moon" where="艾欧尼亚" />
    <three-com who="马鑫鑫" where="祖安" />
    <three-com who="文豪" where="白鹿书院" />
  </div>
</template>

<script>
import ThreeCom from "./components/ThreeCom.vue";
export default {
  components: { ThreeCom },
};
</script>

<style lang="scss" scoped>
</style>
```

案例：

```
<template>
  <div class="four-com">
    <p>我是{{ name }}, 来自{{ where }}, 今年{{ age }}, 爱好:{{ hobby }}</p>
  </div>
</template>

<script>
export default {
  props: ["name", "where", "age", "hobby"],
};
</script>

<style lang="scss" scoped>
// 通常: 组件中适合添加组件自身的样式
// App.vue: 给组件加定位
.four-com {
  border: 2px solid blue;
  color: blue;
  padding: 10px;
  margin-top: 10px;
}
</style>
///////////
<template>
  <div>
    <four-com
      name="家乐"
      where="南京雷氏一族"
      :age="age"
      hobby="唱, 跳, rap, 篮球"
    />
    <!-- age=""  是HTML的语法, 值是 字符串 -->
    <!-- :age="" 是vue的语法, 值是JS代码 -->
  </div>
</template>

<script>
import FourCom from "./components/FourCom.vue";
export default {
  components: { FourCom },
  data() {
    return {
      age: 30,
    };
  },
};
</script>

<style lang="scss" scoped>
</style>
```

### 22、data是函数

当组件被复用的时候, 每次调用data函数, 都会返回一个 全新的对象

 所以: 不同组件之间的数据 不会互相影响!

### 23、插槽

组件有两种传参方式 

1. 属性传参: 利用props声明 属性, 来接收参数 

2.  内容传参: 利用slot属性来接收参数 

   slot 插槽: 一个占位符, 在实际使用时, 会被替换成 组件标签的内容 

   默认插槽: 代表 组件标签使用时的内容 

    插槽的作用:
         - 1个组件负责把 布局全写好, 每个空位都是一个插槽
         - 使用时: 只需要向 指定的插槽放东西就可以

```
<!-- 命名插槽: 有 vue1 2 两种语法 -->
      <!-- vue1语法: 把内容显示在指定名称的 slot 中 -->
      <div slot="jiale">
```

命名插槽: 有 vue1 2 两种语法

1、 vue1语法: 把内容显示在指定名称的 slot 中

slot="jiale"

2、vue2 的语法, 必须搭配 vue 提供的 template 标签

template: 一个虚拟的容器, 不参与css样式，不用div，因为会影响样式

```
      <template v-slot:口红>
        Gucci, dior, 纪梵希, 雅诗兰黛, 兰蔻, 香奈儿
      </template>

      <!-- vue2 的 语法糖, 类似 @ : , 此处用 # -->
      <template #首饰> 周大福, 翡翠, DR, 老凤祥 </template>
```

案例：

```
<template>
  <div class="hua-zhuang-he">
    <!-- 放普通物品 -->
    <div>
      <slot />
    </div>

    <div>
      <h3>香水</h3>
      <slot name="香水" />
    </div>

    <div>
      <h3>口红</h3>
      <slot name="口红" />
    </div>

    <div>
      <h3>首饰</h3>
      <slot name="首饰" />
    </div>
  </div>
</template>

<script>
export default {};
</script>

<style lang="scss" scoped>
.hua-zhuang-he {
  > div {
    display: inline-block;
    width: 300px;
    min-height: 300px;
    background-color: aquamarine;
    padding: 10px;
    border-radius: 4px;
    margin: 10px;
  }
}
</style>
///////////
<template>
  <div>
    <hua-zhuang-he>
      <!-- 直接书写在组件标签内容中的, 会出现在 组件的 默认插槽 slot 里 -->
      <div>日霜, 晚霜, 眼影, 润肤露, 水乳, 洗面奶</div>

      <!-- vue1 的语法 -->
      <div slot="香水">香奈儿, dior, 古龙</div>

      <!-- vue2 的语法, 必须搭配 vue 提供的 template 标签 -->
      <!-- template: 一个虚拟的容器, 不参与css样式 -->
      <template v-slot:口红>
        Gucci, dior, 纪梵希, 雅诗兰黛, 兰蔻, 香奈儿
      </template>

      <!-- vue2 的 语法糖, 类似 @ : , 此处用 # -->
      <template #首饰> 周大福, 翡翠, DR, 老凤祥 </template>
    </hua-zhuang-he>
  </div>
</template>

<script>
import HuaZhuangHe from "./components/HuaZhuangHe.vue";
export default {
  components: { HuaZhuangHe },
};
</script>

<style lang="scss" scoped>
</style>
```

### 24、axios网络请求

懒加载机制: DOM元素没用之前,不加载, 可以节省首次页面显示时的DOM数据, 可以加速页面的首次显示

```
<template>
  <div>
    <button @click="suibian">获取数据</button>
    <!-- data的初始值是null, 需要点击按钮后才能请求到实际的值 -->
    <!-- 所以: null.pageCount 会报错, 以为不能对null读取属性-->

    <!-- 用 v-if 判断: true就添加元素  false就删除元素 -->
    <!-- 在 if 判断中, null -> false, 此时 刚开始 这个p标签不会加载 -->
    <!-- 懒加载机制: DOM元素没用之前,不加载, 可以节省首次页面显示时的DOM数据, 可以加速页面的首次显示 -->

    <!-- 整体一起判断, 但是不要用div -- div会影响css布局 -->
    <!-- vue提供了一个虚拟容器, 不影响css布局 -->
    <template v-if="data">
      <p>页数: {{ data.pageCount }}</p>
      <p>当前页: {{ data.pageNum }}</p>
      <p>每页数量: {{ data.pageSize }}</p>
      <p>总数量: {{ data.totalRecord }}</p>
    </template>
  </div>
</template>

<script>
// axios使用时, 分两种方式
// 1. 单独使用 - 在哪个组件中用, 就在哪里引入
import axios from "axios";
// 2. 全局使用
export default {
  data() {
    return {
      // 提前准备一个变量: 用来存储请求得到值
      data: null, // data:数据
    };
  },

  methods: {
    suibian() {
      const url = "http://www.codeboy.com:9999/mfresh/data/news_select.php";
      // 在 Promise 的语法里, then代表成功  catch代表失败
      axios.get(url).then((res) => {
        // 参数res: 是 response的缩写, 代表 服务器响应的数据
        console.log(res);
        // 返回的数据 存储在 res.data 属性里

        // 请求的数据 如何显示到页面上??
        // -- 页面上显示的数据 应该存在哪里?  -- data属性
        this.data = res.data;
        console.log(this);
      });
    },
  },
};
</script>

<style lang="scss" scoped>
</style>
```

网络请求有多实现方式

- 原生的`AJAX`
- jQuery提供的封装: `$.get(地址, data=>{})`
  - jQuery采用 `回调函数` 来实现 异步请求封装 -- 存在`回调地狱`风险
- axios: 另一款网络请求的第三方, 采用 `Promise` 实现了封装操作, 规避了 `回调地狱` 风险

- 安装 npm i axios vue-axios
- 使用
  - 单独使用:  `axios.get(地址).then(响应的数据 => {})`
  - 数据必须存在 data 中, 才能在页面上用
  - HTML中使用时, 要用 v-if 判断,  实现一种懒加载的效果 -- 数据有的时候再显示

#### 1、axios使用方式分两种:  单独引入 和 全局引入

单独引入: 在每个使用网络操作的组件中, 进行import；

import axios from "axios";

全局引入: 在 main.js 中, 把 axios 注入到 Vue的原型上

```

// 把 axios 存放在 Vue 的原型上
import axios from 'axios';

// 做法2：利用 vue-axios 模块, 来优雅的注入 axios 到 Vue里
import VueAxios from 'vue-axios';
// use: `明媒正娶` 的方式来引入第三方
Vue.use(VueAxios, axios)

// 做法1: 直接操作Vue的原型 -- 简单粗暴,但是不合规矩 -- 导致使用时没有提示
// Vue.prototype.axios = axios
```



### 25、过滤器filter

```
<template>
  <div>
    <!-- 过滤器: filter -->
    <!-- 服务器返回的数据 很有可能 与我们想要展示的数据不一样: 采用过滤器处理 -->
    <!-- 服务器返回性别 0 1 2,  我们想要显示: 女 男 保密 -->

    <!-- 语法 {{ 值 | 过滤器 }}   | 是 shift+回车上面的按钮  -->
    <p>{{ 0 | sex }}</p>
    <p>{{ 1 | sex }}</p>
    <p>{{ 2 | sex }}</p>

    <!-- 练习:  显示出 12万   9.9万 这种效果 -->
    <p>{{ 120000 | wan }}</p>
    <p>{{ 99000 | wan }}</p>
    <p>{{ 145555 | wan }}</p>
    <!-- 不过万 就不转 -->
    <p>{{ 5000 | wan }}</p>
  </div>
</template>

<script>
export default {
  // filters: 过滤器们,  用于声明过滤器
  filters: {
    wan(v) {
      return v > 10000 ? (v / 10000).toFixed(1) + "万" : v;
    },

    // {{ 值 | 过滤器}}
    sex(v) {
      // 值 会作为参数, 传递给过滤器
      // 返回值 就是过滤器的结果
      return ["女", "男", "保密"][v]; // v是序号, 下标取值
    },
  },
};
</script>

<style lang="scss" scoped>
</style>
```

### 26、生命周期

生命周期: 组件从 创建 到 出生 .. 销毁整套过程

beforeCreate、created、beforeMount、 mounted、 beforeUpdate、updated、beforeDestroy、destroyed；

```
<template>
  <div>
    <h1>Hello World!</h1>
    <button @click="num++">{{ num }}</button>
  </div>
</template>

<script>
// 组件的生命周期  和  人的一生相同 -- 是一种常识
// 面试几乎必考题 --- 必须背
//
// 如果希望组件在显示时, 自动发送请求 -- mounted 周期

export default {
  data() {
    return {
      num: 1,
    };
  },

  // 钩子(hook)函数: 一种特殊的函数, 会在特殊的事件发生时, 自动触发
  // 1个组件的生命  和 人的生命历程十分相似
  // 备孕->怀孕->待产->出生->开始学习->学习完毕->快死了->死了
  // 准备创建->创建完毕-准备显示到页面->显示完毕->准备更新->更新完毕->准备销毁->销毁完毕

  // 每个重要的时间节点, 都会自动触发一个固定名称的函数 -- 称为 钩子函数
  // before: 在...之前
  beforeCreate() {
    console.log("beforeCreate: 创建前 -- 备孕");
  },
  created() {
    console.log("created: 创建完毕 -- 怀孕");
  },
  beforeMount() {
    console.log("beforeMount: 准备出生 -- 将要添加到页面上");
  },
  mounted() {
    console.log("mounted: 出生 -- 显示到页面");
  },

  beforeUpdate() {
    console.log("beforeUpdate: 将要更新");
  },
  updated() {
    console.log("updated: 更新完毕");
  },

  beforeDestroy() {
    console.log("beforeDestroy: 将要销毁 -- 快死了");
  },
  destroyed() {
    console.log("destroyed: 销毁完毕 -- 死了");
  },
};
</script>

<style lang="scss" scoped>
</style>
```

#### 1、生命周期的应用

mounted: 最常用, 代表组件显示在页面上时，此时直接发送请求，不需要手动请求

```
 methods: {
    getData() {
      const url = "http://api.xin88.top/bilibili/recommend.json";

      axios.get(url).then((res) => {
        this.data = res.data;
        console.log(res);
      });
    },
  },

  // 其他周期使用极少
  // mounted: 最常用, 代表组件显示在页面上时
  mounted() {
    this.getData();
  },
```

### 英雄联盟案例

要点：

1、播放音频

2、利用字符串替换,得到图片地址

' 字符串'.replace('替换目标','替换结果')

```
<template>
  <div>
    <!-- ref: 把1个变量 和 元素绑定在一起, 会存储在 $refs 里 -->
    <audio ref="au" />

    <template v-if="data">
      <div v-for="h in data.hero" :key="h.heroId" class="cell">
        <div>
          <button @click="playBan(h.banAudio)">ban</button>
          <button @click="playSelect(h.selectAudio)">select</button>
        </div>
        <!-- <img
          :src="`https://game.gtimg.cn/images/lol/act/img/champion/${h.alias}.png`"
          alt=""
        /> -->

        <!-- 利用字符串替换,得到图片地址 -->
        <img :src="data.baseURL.replace('{alias}', h.alias)" alt="" />
        <span>{{ h.name }}</span>
      </div>
    </template>
  </div>
</template>

<script>
export default {
  data() {
    return {
      data: null,
    };
  },
  mounted() {
    this.getData();
  },
  methods: {
    playBan(ban_src) {
      // 此处要使用 audio 元素
      const au = this.$refs.au;
      au.src = ban_src; //音频地址
      au.play(); // 开始播放
    },
    playSelect(src) {
      const au = this.$refs.au;
      au.src = src;
      au.play();
    },

    getData() {
      const url = "https://api.xin88.top/game/heros.json";
      this.axios.get(url).then((res) => {
        console.log(res);

        this.data = res.data;
      });
    },
  },
};
</script>

<style lang="scss" scoped>
.cell {
  display: inline-flex;
  flex-direction: column;
  align-items: center;
  margin: 10px;
  user-select: none;
}
</style>
```

### 27、post请求

1、  GET请求: 适合用于从服务器获取数据的接口 -- 服务器决定的；

2、POST请求: 合适向服务器传输数据, 例如图片上传  -- 服务器决定

使用上的差异: 在于参数的传递方式：

  get:   路径?参数=值&参数=值；

```
getData() {
      const url = "https://api.xin88.top/game/heros.json";
      this.axios.get(url).then((res) => {
        console.log(res);

        this.data = res.data;
      });
```

  post:  路径 和 参数 分开传递,  axios没有对参数进行处理, 只能放字符串类型；

```
  login() {
      console.log(this.uname, this.upwd);

      const url = "http://www.codeboy.com:9999/data/user/login.php";

      // 服务器规定的参数名: uname 和 upwd
      const params = `uname=${this.uname}&upwd=${this.upwd}`;

      // post(路径, 参数)
      this.axios.post(url, params).then((res) => {
        console.log(res);
        // 账号:  doudou     123465
      });
    },
    // 全局引入分两种方式:
    // 简单粗暴: 直接操作原型, 但是不受到vue承认, 所以没有代码提示
    // 优雅规矩(推荐): 利用 vue-axios 模块来 按照规矩进行引入
    // 安装命令: npm i axios vue-axios
    // 到main.js
    getData() {
      // this.axios.get().then((res) => {
      //   console.log(res);
      // });
    },
```

### 28、路由系统

#### 1、内容

Vue中提供的制作`多页`网站`效果`的技术

- 原生开发中, 通过切换`html`文件来实现多个页面的效果 -- 整个网页切换

  <img src="C:\WEB\WEB\ThirdState\Vue1\day06\assets\image-20220523092201649.png" alt="image-20220523092201649" style="zoom:25%;" />

- 现代化的开发方式, 流行`局部`切换

  - 原生相当于-- `笔记本电脑`  -- 集成化高, 更换CPU 就必须更换整个电脑
  - 现代化的方式 -- `台式机`  -- 模块化,  更换CPU 就只需要换CPU即可
    - 用最小的消耗 来实现内容的变换
  - 专业称呼: `SPA` -- `S`ingle `P`age `A`pplication  单页应用
    - 整个网站只有一个页面, 然后通过局部的切换来实现 `多页` 效果

#### 2、路由总结

> 作用: `局部`切换组件, 让我们的网页产生一种 多页的效果, 此技术称为 `SPA - 单页应用` 

- `router-view`: 一个占位符, 会根据路径 切换到 对应的组件
- `views`: 路由切换的组件, 存放在这里
- `router/index.js` : 路由配置
  - 配置 什么路径 对应 什么组件
  - 注意组件的加载方式
    - import: 适合使用频率高的组件
    - 箭头: 适合使用频率低的组件
- `router-link`: 类似超链接 a 标签, 用来实现点击切换
  - 自带两个激活样式
  - router-link-active: 模糊
  - router-link-exact-active :精确

- `$router`: 路由对象, 存储在 vue 实例中, 可以操作路由
- 路由传参:
  - 旧: 通过 `?` 来传递   `to="/路径?参数=值&参数=值..."`
    - 组件中如何读取参数的值??  `$route.query`

  - 新: 简化书写
    - 路径配置中, 需要用 `:` 来标识参数   `path: '/路径/:参数/:参数'`
    - 使用时 `to="/路径/值/值"`
    - 组件中如何读取参数的值?
      - 方式1: params  `$route.params`
      - 方式2: 利用 props
        - 注意: 必须在配置文件中开启此功能  `props:true`

#### 3、路由传参

![image-20220523162801557](C:\WEB\WEB\ThirdState\Vue1\day06\assets\image-20220523162801557.png)

#### 4、配置文件

```js
import Vue from 'vue'
import VueRouter from 'vue-router'
import HomeView from '../views/HomeView.vue'

// 目前: 假设网站中有 100 个页面
// 做法1: 网站刚加载, 就把100个页面全加载完毕, 然后等着使用
//  - 优点: 用户进入不同页面, 瞬间切换
//  - 缺点: 首次进入网站, 要进行大量操作, 首次慢;  用户如果没浏览其他页面, 亏了
// 做法2: 网站刚加载, 就加载用户使用的, 其他页面等到用户使用时再加载
//  - 优点: 首次加载速度快
//  - 缺点: 每个新的页面浏览时, 都要临时加载

// 最佳方案: 先加载最常用的几个页面, 把不常用的用懒加载方式进行

// 非懒加载: 网站加载时, 默认自动加载 -- 适合最常用的几个页面
import JiaLe from '../views/JiaLe.vue'
import FeiFan from '../views/FeiFan.vue';

// 假设 yufei 和 yumeng 使用频率低 -- 改造成懒加载
// import YuFei from '../views/YuFei.vue';
// import YuMeng from '../views/YuMeng.vue';

// 总结: 根据页面的使用频率
// -- 频率高: 用 import
// -- 频率低: 懒加载  箭头函数方式

Vue.use(VueRouter)
// 配置文件: 配置 路径 和 组件的对应关系
const routes = [
  // vroute-named
  {
    // 路径声明时, 可以用 : 来指定参数
    path: '/dy/:type/:id',
    name: 'dy',
    // 小马的狂化状态: true
    props: true, // props功能: 开启,  默认是 false, 不开启
    component: () => import('../views/DY.vue'),
  },
  {
    path: '/douyu',
    name: 'douyu',
    component: () => import('../views/DouYu.vue'),
  },

  {
    // 路径必须带 / 开头
    // 区分大小写吗?? 代码非常严谨, 永远区分大小写

    path: '/yumeng',
    // 懒加载语法: 用箭头函数, 在被调用时才会临时引入
    component: () => import("../views/YuMeng.vue")
  },
  {
    meta: { title: "雨飞" },
    path: '/yufei',
    component: () => import("../views/YuFei.vue")
  },
  {
    path: '/feifan',
    component: FeiFan,
    meta: { title: "非凡" },
  },
  {
    // path: 路径, 
    path: "/jiale",
    // component: 组件
    component: JiaLe,
    // name属性:  为这个路由配置项起个名字, 后期调试时 找BUG用, 加不加都行
    name: '家乐',
    // meta: 固定的属性, 称为 元数据:  可以存放各种自定义的内容
    meta: {
      x: '12121',
      y: 433,
      suibian: true,
      title: "家乐"
    }
  },

  {
    path: '/',
    name: 'home',
    component: HomeView,
    meta: { title: "首页" }
  },
  {
    meta: { title: "关于" },
    path: '/about',
    name: 'about',
    // route level code-splitting
    // this generates a separate chunk (about.[hash].js) for this route
    // which is lazy-loaded when the route is visited.
    component: () => import(/* webpackChunkName: "about" */ '../views/AboutView.vue')
  }
]

const router = new VueRouter({
  mode: 'history',
  base: process.env.BASE_URL,
  routes
})

// 必须在 router 赋值后, 书写代码
// 路由守卫: 看大门的 -- 监听路由的各种跳转操作

// beforeEach: 路由前置守卫, 在路由跳转前触发
router.beforeEach((to, from, next) => {
  console.log('to:', to); // 到哪去
  console.log('from:', from); //从哪来

  // DOM中, 如何修改 标签的标题??
  document.title = to.meta.title

  //next: 放行, 允许路由继续运行
  next()
})

export default router
```

#### 5、路由入门

```vue
<template>
  <div>
    <!-- 路由系统: 属于组件的高级应用方式 -->
    <!-- 希望: 能够根据路径 切换 页面上显示的组件 -->
    <!-- views文件夹: 专门存放 路由系统切换的组件 -->

    <!-- router-link: vue对 a 标签进行了封装, 进而得到了更加强大的 router-link-->

    <!-- 虽然最终呈现在页面上的是 a 标签, 但是其在切换路径时, 不会导致重新加载 -->
    <router-link to="/">首页</router-link>
    <router-link to="/about">关于</router-link>
    <router-link to="/jiale">家乐</router-link>
    <!-- 把 yumeng  yufei  也做成链接跳转 -->
    <router-link to="/yumeng">雨萌</router-link>
    <router-link to="/yufei">雨飞</router-link>

    <!-- 不要直接用a标签, 会导致页面重新加载 -->
    <a href="/feifan" target="_blank">非凡</a>

    <div id="box">
      <!-- router:路由 -- 通过路径 可以找到什么 -->
      <!-- router-view: 路由的占位符, 会根据具体的路径 替换成 对应的组件 -->
      <!-- 例如 localhost:8080/   会显示 HomeView 组件 -->
      <!-- localhost:8080/about  会显示 AboutView 组件 -->
      <router-view />
    </div>
  </div>
</template>

<script>
export default {};
</script>

<style lang="scss" scoped>
#box {
  background-color: orange;
  padding: 10px;
}

// router-link 最终表现出来的是 a 标签
// 所以直接给 a 标签添加样式即可
a {
  margin: 10px;
  display: inline-block;
  padding: 10px 20px;
  // 文本-修饰  即  上中下 3个线
  text-decoration: none;
  color: white;
  background-color: #666;
  opacity: 0.8;
  transition: 0.3s;

  &:hover {
    opacity: 1;
    border-radius: 4px;
  }
}

// router-link: 会自动为当前激活项添加class

// router-link-active: 模糊匹配
// 例如 路径是 /a/b/c , 与之模糊匹配的路径有4种  /  /a  /a/b   /a/b/c
// 即: 1个路径的 父级路径 都会匹配成激活状态 -- 一人得道鸡犬升天/株连九族
a.router-link-active {
  background-color: orange;
}
// 因为模糊匹配, 所有  /about 会导致 /  和 /about 都带上橘黄色背景

// router-link-exact-active
// exact: 精确的
a.router-link-exact-active {
  // background-color: orange;
}
// 因为精确匹配, 所以只有 /about 带有背景色
</style>
```

#### 6、编程式跳转

```vue
<template>
  <div>
    <!-- 标签式跳转 -->
    <router-link to="/">Home</router-link>
    <router-link to="/about">About</router-link>
    <!-- 编程式跳转 -->
    <button @click="goMeng">3秒后,切换到雨萌</button>

    <!-- 占位符: 被替换成对应组件 -->
    <router-view />
  </div>
</template>

<script>
export default {
  methods: {
    goMeng() {
      var num = 3;
      console.log(this); // 在后台找到 router

      // 在 vue 对象中, 有很多 $ 开头的属性
      // Vue自带的属性, 都是 $ 开头, 一个标识, 用户看到就知道是系统的
      // $router: 就是 路由对象, 其中包含了路由相关的各种操作

      const a = setInterval(() => {
        num--;
        console.log("num:", num);
        // push: 推入一个新的页面
        if (num == 0) {
          this.$router.push("/yumeng");
          clearInterval(a);
        }
      }, 1000);
    },
  },
};
</script>

<style lang="scss" scoped>
</style>
```

#### 7、当前路由信息

```vue
<template>
  <div>
    <!-- 需求: 在输入框中按回车, 切换到 /about 路径 -->
    <!-- 实际开发时, 往往会跳转到 搜索页面 -->
    <input type="text" placeholder="搜索..." @keyup.enter="goAbout" />

    <router-view />
  </div>
</template>

<script>
export default {
  methods: {
    goAbout() {
      // 编程式跳转: 如果重复跳转, 会报错 -- 避免重复导航到 当前路径

      // 解决方案: 在跳转之前, 添加判断, 当前路径 和 目标路径(要往哪里跳) 不相同再跳转

      // 当前路径信息的读取方式
      // $router.currentRoute

      // 由于 当前路径 信息经常被读取使用, 所以作者好心的提供了 $route 的属性, 用于快速读取路径配置信息
      console.log(this.$route);

      // 注意区分:
      // $router : 路由对象, 包含路由的所有信息 和 操作
      // $route : 当前路由信息, 属于 $router 的一部分

      console.log(this);

      // 如果当前路径的 path 和 要跳转的地址不同, 再跳转
      if (this.$route.path != "/about") {
        this.$router.push("/about");
      }
    },
  },
};
</script>

<style lang="scss" scoped>
</style>
```

#### 8、路由传参

```vue
<template>
  <div>
    <router-link to="/">Home</router-link>
    <!-- ? 传参语法 结构复杂, 实际开发中有更好的方案 -->
    <router-link to="/dy/DNF/33">DNF</router-link>
    <!-- <router-link to="/dy?type=ecy&id=11">二次元</router-link> -->
    <router-link to="/dy/ecy/11">二次元</router-link>
    <router-link to="/dy/hpjy/22">和平精英</router-link>
    <!-- 路由配置 path:"/dy/:type/:id" -->

    <!-- 占位符 -->
    <router-view />
  </div>
</template>

<script>
export default {};
</script>

<style lang="scss" scoped>
a {
  margin: 10px;
  text-decoration: none;

  &.router-link-exact-active {
    color: orange;
  }
}
</style>
```

组件

```vue
<template>
  <div>
    <h2>DY 欢迎您</h2>
    <p>type: {{ $route.params.type }}</p>
    <p>type: {{ type }}</p>
  </div>
</template>

<script>
export default {
  // 作者贴心的帮你 简化了 路由参数的读取方式 :  仅限于新式传参
  // props: 可以用来声明参数接收路由传参
  // 这个用 props 接收路由传参的功能, 必须手动开启 -- 配置文件  router/index.js
  props: ["type"],

  // watch: 监听器, 可以监听 vue的任意属性的变化
  watch: {
    // 通过 ? 传参 : 存储在query里
    // 通过新式传参 : 存储在params里
    $route(to, from) {
      console.log("to:", to);
      this.getData();
    },
  },
  mounted() {
    this.getData();
  },
  methods: {
    // 触发场景分两种:
    // 1. 页面首次展示
    // 2. 路由参数变化时
    getData() {
      // const type = this.$route.params.type;

      // 当使用 props 来接收参数, 只需要 this.type 就可以使用
      const url = "https://douyu.xin88.top/api/room/list?type=" + this.type;

      console.log("url:", url);
    },
  },
};
</script>

<style lang="scss" scoped>
</style>
```

#### 9、meta和路由守卫

```js
{
    path: '/',
    name: 'home',
    component: HomeView,
meta:{title:'首页'}
  },
//必须在router赋值后，书写代码
//路由守卫：看大门的--监听路由的各种跳转操作

//beforEach:路由前置守卫，在路由跳转前触发
router.beforeEach((to,from,next)=>{
//to:到哪去
//from：从哪来，当前路由
document.title=to.meta.tilte
//next:放行，允许路由继续运行
next();
})
```

### 29、外部文件的使用

```vue
<template>
  <div>
    <img src="./assets/logo.png" alt="" />
    <one-com />
    <two-com />

    <div class="danger">DANGER</div>

    <div>
      <p>家乐</p>
      <p>小马</p>
    </div>
  </div>
</template>

<script>
import OneCom from "./components/OneCom.vue";
import TwoCom from "./components/TwoCom.vue";
// 外部文件的使用
// JS CSS 图片
// 图片: 本地图片应该存储在 assets 目录下
// css: 存储在 assets 目录下
// JS: 放哪里都可以, 在 src 目录下即可

import my from "./suibian/my"; // .js 后缀名可以省略

export default {
  components: { OneCom, TwoCom },
  mounted() {
    my.show();
  },
};
</script>

<style lang="scss" scoped>
</style>
```

组件

```vue
<script>
//外部的css有三种引入方式
//1.在js中：特点：全局生效，会引入到index.html里影响所有组件
import "../assets/css/my.css";
export default {};
</script>

<style lang="scss" scoped>
.one-com {
  border: 1px solid blue;
  padding: 10px;
}
</style>
<style>
/*2. 默认的style 是css模式，只对css生效 */
/* @import url('../assets/css/my.css');
@import url('../assets/css/you.scss'); */
</style>
<style lang="sass">
// scss兼容css，但是css不兼容scss
// @import url('../assets/css/my.css')
 @import ('../assets/css/you.scss')
</style>
<style lang="sass" scoped>
// scoped：范围，作用域；会让scss代码只影响当前组件中的内容
// scoped 对引入的 css 文件无效, 依然是全局
//@import url('../assets/css/my.css')
//@import ('../assets/css/you.scss')

// url 和 不带 url 都行 -- 偶尔有兼容性问题
// 具体看效果, url好用就写url, 不好用就去掉url
</style>

<!-- css局部引入: -->
<style scoped src="../assets/css/my.css"></style>
```

### 30、Vuex

Vuex: 全局状态共享

多个页面 或 组件中共享的数据 存储在 共享的对象中: Vuex

- store: 存储共享的数据
  - 使用时: `$store.state.数据`
- 修改分两种方式:
  - 简单粗暴(`不推荐,不安全`): 直接修改 `$store.state`
  - 规矩(`安全`): 
    - 必须在 `mutations` 中声明方法, 来进行允许的修改操作
    - 通过 `commit` 方法提出申请, 触发对应的修改操作

![image-20220525002617930](C:\Users\深海钢琴师\AppData\Roaming\Typora\typora-user-images\image-20220525002617930.png)

#### 1、vuex初步

```vue
<template>
  <div>
    <!-- Vuex: 全局状态管理 -- 组件间的数据共享 -->
    <!-- store文件夹: 仓库, 放共享数据 -->
    <three-com />
    <four-com />
    <hr />
    <button @click="addNum">num+1</button>
    <p>num: {{ $store.state.num }}</p>
    <p>uname: {{ $store.state.uname }}</p>
    <p>isLogin: {{ $store.state.isLogin }}</p>
  </div>
</template>

<script>
import FourCom from "./components/FourCom.vue";
import ThreeCom from "./components/ThreeCom.vue";
export default {
  components: { ThreeCom, FourCom },
  methods: {
    addNum() {
      // commit:提交
      // 向 $store 提交申请, 触发 名字是 numAdd1 的方法
      this.$store.commit("numAdd1");
      // 共享数据的修改, 必须保障安全 -- 必须提供专业渠道来修改
    },
  },
  mounted() {
    console.log(this); //查看其中有没有 store 这个仓库

    // this.$store.state
  },
};
</script>

<style lang="scss" scoped>
</style>
```

store.js

```js
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

// 场景模拟:
// 小马把自己的工资上缴 家库, 全家人都能用
// 小马想给 女主播 刷礼物 -- 500元
// 做法1: 小马直接从 家库 中拿钱
// 如果启动严格模式: 则做法1 依然可以,但是会报错
//
// 做法2: 规矩 -- 要想修改共享的数据, 必须通过 指定的方法

export default new Vuex.Store({
  // 严格模式:
  strict: true,
  // state: 状态 -- 共享数据都存储在这里
  state: {
    num: 1,
    isLogin: true, //当前是否登录
    uname: '小马哥'
  },
  // 计算属性:
  getters: {
    // 通过已有的属性, 计算返回新的值
    status(state) {
      // 参数1: 固定的 state, 代表共享的数据项
      return state.isLogin ? '登录' : '未登录'
    }
  },
  // 变化: 在这个属性中, 书写用于修改 共享数据的方法
  mutations: {
    // 登录分 true 和 false 两种值, 则需要传参
    updateLogin(state, x) {
      state.isLogin = x
    },
    numAdd1(state) {
      // 参数1: 固定传入的,共享数据所在的对象
      state.num++
    }
  },
  actions: {
  },
  modules: {
  }
})

```

#### 2、辅助函数原理

```vue
<template>
  <div>
    <!-- 传统写法 -->
    <div>num: {{ $store.state.num }}</div>
    <div>uname: {{ $store.state.uname }}</div>
    <div>isLogin: {{ $store.state.isLogin }}</div>

    <hr />
    <!-- 利用计算属性简化 -->
    <div>num: {{ num }}</div>
    <div>uname: {{ uname }}</div>
    <div>isLogin: {{ isLogin }}</div>
  </div>
</template>

<script>
// 把传入的数组, 转换成 对象类型
function mapState(arr) {
  var obj = {};
  // name是数组中每个元素的值
  for (let name of arr) {
    // 假设 name 是 num
    // 则下方代码:  obj.num = function (){ return this.$store.state.num }
    // 因为name是变量, 所以必须用中括号语法才能赋值
    obj[name] = function () {
      return this.$store.state[name];
    };
  }
  return obj;
}

console.log(mapState(["num", "uname", "isLogin"]));

export default {
  // 利用计算属性简化
  computed: {
    // 展开符 ...  破掉对象类型 {}
    // mapState: 自动帮你生成所有的函数
    ...mapState(["num", "uname", "isLogin"]),

    // 方法在使用时, 自动触发 不需要()
    // num: function () {
    //   return this.$store.state.num;
    // },
    // uname: function () {
    //   return this.$store.state.uname;
    // },
    // isLogin: function () {
    //   return this.$store.state.isLogin;
    // },
  },
};
</script>

<style lang="scss" scoped>
</style>
```

#### 3、辅助函数

```vue
<template>
  <div>
    <!-- 传统写法 -->
    <div>num: {{ $store.state.num }}</div>
    <div>uname: {{ $store.state.uname }}</div>
    <div>isLogin: {{ $store.state.isLogin }}</div>

    <hr />
    <!-- 利用计算属性简化 -->
    <div>num: {{ num }}</div>
    <div>uname: {{ uname }}</div>
    <div>isLogin: {{ isLogin }}</div>
  </div>
</template>

<script>
// vuex: 提供了辅助函数 mapState, 帮你自动生成计算属性, 简化state的使用
import { mapState } from "vuex";

// 辅助函数的原理, 参考 App.4  : 感兴趣了解下
// 不感兴趣: 直接背语法即可 :  在 computed 中, 书写 ...mapState([名称, 名称])

export default {
  // 利用计算属性简化
  computed: {
    // 展开符 ...  破掉对象类型 {}
    // mapState: 自动帮你生成所有的函数
    ...mapState(["num", "uname", "isLogin"]),

    // 方法在使用时, 自动触发 不需要()
    // num: function () {
    //   return this.$store.state.num;
    // },
    // uname: function () {
    //   return this.$store.state.uname;
    // },
    // isLogin: function () {
    //   return this.$store.state.isLogin;
    // },
  },
};
</script>

<style lang="scss" scoped>
</style>
```



```vue
<template>
  <div>
    <p>登录状态: {{ $store.getters.status }}</p>
    <!-- commit的参数2, 会传递给 方法的参数2 -->
    <button @click="$store.commit('updateLogin', true)">登录</button>
    <!-- 发申请commit, 触发指定的事件 -->
    <button @click="updateLogin(false)">退出</button>
    <hr />
    <button @click="numAdd1">{{ $store.state.num }}</button>
  </div>
</template>

<script>
// 在使用vuex 的内容时, 分3种写法
// 1. 直接用 $store.state.xx   $store.commit(...)
// 2. 手动通过 计算属性 或 methods 来映射
// 3. 使用辅助函数 mapXxxx 来实现映射

// 辅助函数有些人不会
// 团队合作时很麻烦, 不一定你的队友会哪种, 所以你 都要会才能兼容别人!

import { mapMutations } from "vuex";
export default {
  methods: {
    // 作者提供了辅助函数, 帮你自动实现映射代码
    // 在数组中书写 要映射的mutations 中的方法名即可
    ...mapMutations(["numAdd1", "updateLogin"]),
    // numAdd1() {
    //   this.$store.commit("numAdd1");
    // },
    // updateLogin(x) {
    //   this.$store.commit("updateLogin", x);
    // },
  },
  mounted() {
    console.log(this); // 找到 getters.status
  },
};
</script>

<style lang="scss" scoped>
</style>

```

#### 4、vuex总结

```vue
<template>
  <div>
    <div>count:{{ count }}</div>
    <div>num: {{ num }}</div>
    <div>age: {{ age }}</div>
    <button @click="countJian10">更新count</button>
    <button @click="numJia1">更新num</button>
    <button @click="ageJiaN(10)">更新age</button>
    <hr />
    <p>{{ age_db }}</p>
    <p>{{ num_db }}</p>
    <p>{{ count_db }}</p>
    <!-- double 双倍 db -->
  </div>
</template>

<script>
import { mapGetters, mapMutations, mapState } from "vuex";
export default {
  computed: {
    // 辅助函数, 把 state 中的值映射到组件中使用
    ...mapState(["count", "num", "age"]),
    // 自动触发的, 放计算属性
    ...mapGetters(["age_db", "num_db", "count_db"]),
  },
  // mutations: 属于主动触发的方法, 应该放在 methods里
  methods: {
    // 辅助函数: 把 mutations中的方法映射到组件里用
    ...mapMutations(["numJia1", "countJian10", "ageJiaN"]),
  },
};
</script>

<style lang="scss" scoped>
</style>
```



```js
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)


export default new Vuex.Store({
  // 共享的数据存储在state里
  state: {
    count: 100,
    num: 1,
    age: 30
  },
  // 用于存储修改 state 中的值的方法
  mutations: {
    numJia1(state) {
      state.num += 1
    },
    countJian10(state) {
      state.count -= 10
    },
    ageJiaN(state, n) {
      state.age += n
    }
  },
  // 计算属性: 把 state 中的值 ,计算后返回一个新的值
  getters: {
    age_db(state) {
      return state.age * 2
    },
    num_db(state) {
      return state.num * 2
    },
    count_db(state) {
      return state.count * 2
    }
  }
})
```

