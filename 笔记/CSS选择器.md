# CSS选择器

## 伪类选择器

### 简介

很像类但是不是一个类是对元素的特殊状态的一种描述

**简单例子：**

```html
<style>
    /* 这个访问或者没访问是根据超链接来判断的 */
    /* 没访问过的 */
    a:link {
      color: orange;
    }

    /* 访问过的 */
    a:visited {
      color: red;
    }
  </style>
</head>

<body>
  <a href="https://baidu.com">百度</a>
  <a href="https://youtube.com">天猫</a>
</body>
```

### 动态伪类

![image-20240407103043419](C:\Users\DC\AppData\Roaming\Typora\typora-user-images\image-20240407103043419.png)

```css
   /* 这个访问或者没访问是根据超链接来判断的 */
    /* 没访问过的 */
    a:link {
      color: orange;
    }

    /* 访问过的 */
    a:visited {
      color: red;
    }

    /* 悬浮 */
    a:hover {
      color: black;
    }

    /* 选中但是未发生跳转 */
    a:active {
      color: skyblue;
    }

    /* 注意需要按照上面的顺序书写动态伪类不然可能会导致样式没有奏效 */
```

### 结构伪类（重点）

**常用的结构伪类选择器：**

```html
<style>
    /* 选中第一个儿子选择器 */
    /* 注意这个选择器拿到的是div下面的第一个p标签 如果p标签前面还有其他的元素将不会出现任何效果 */
    /* 他是按照下面所有的子元素计算的 */
    /* div>p:first-child {
      background-color: rebeccapurple;
    } */

    /* 选中最后一个元素 */
    /* div p:last-child {
      background-color: skyblue;
    } */


    /* 选中指定第n个元素 注意这里是按照1开头不是按照0 */
    /* 在这个括号里面可以写公式 比如： 2n 就能选中全部的偶数 写even就是偶数 */

    /* 选中偶数 */
    /* div p:nth-child(even) {
      background-color: pink;
    } */

    /* 选中全部基数 */
    /* div p:nth-child(odd) {
      background-color: red;
    } */

    /* 选中前三个 注意这个括号里面都必须是 an + b 的形式 */
    /* n 是 从0 开始 那么 -n + 3 也就是 3 2 1 -1 其中-1 明显选不到任何元素 */
    /* div p:nth-child(-n+3) {
      background-color: skyblue;
    } */


    /* first-of-type */
    /* 选中div下 第一个类型为p的元素 */
    /* div>p:first-of-type {
      background-color: red;
    } */

    /* nth-of-type */
    /* 选中div下 第n个类型为p的元素 */
    /* 选中全部偶数 */
    /* 其他和child一样使用 */
    /* div p:nth-of-type(even) {
      background-color: skyblue;
    } */
  </style>
  
  
  <div>
    <p>第一名</p>
    <p>第二名</p>
    <p>第三名</p>
    <p>第四名</p>
    <p>第五名</p>
  </div>
```

总结：结构伪类常用的就是 first-child 、last-child 、 nth-child() 、 以及类型选择 first-of-type 和 nth-of-type

注意使用的时候注意是在哪个父亲元素下，以及常用的nth-child() 括号里面可以使用公式，an+b的形式其中n是从1开始计数和js稍微不同，在使用的时候常见三种情况，第一是数字代表第n个元素，第二是公式，第三是even和odd分别代表偶数和基数。

**不常用的结构伪类选择器：**

```html
<style>
    /* 拿到第5个p元素  使用nth写 */
    /* div p:nth-of-type(5) {
      background-color: skyblue;
    } */

    /* 从下向上数 同样是拿到第五名 这个时候括号里面是从下向上数的number */
    /* 同样的nth-last-of-type 使用方法也是同理上 */
    div p:nth-last-child(3) {
      background-color: slategray;
    }

    /* 选中唯一子元素 */
    /* 这个时候应该只有测试3变化 测试1和测试2是不发生变化的 */
    /* 同样的 nth-of-type也是一样使用 */
    div span:only-child {
      background-color: blue;
    }

    /* :root 以html为根标签 选中的是全部的网页 */
    :root {
      background-color: coral;
    }

    /* :empty 选中没有子元素的 */
    div:empty {
      width: 100px;
      height: 200px;
      background-color: bisque;
    }
  </style>
  
<body>
  <div></div>
  <div>
    <span>测试3</span>
  </div>
  <div>
    <span>测试1</span>
    <p>第一个</p>
    <p>第二个</p>
    <p>第三个</p>
    <p>第四个</p>
    <p>第五个</p>
    <p>第六个</p>
    <span>测试2</span>
  </div>
</body>
```

### 否定伪类

![image-20240407111959092](C:\Users\DC\AppData\Roaming\Typora\typora-user-images\image-20240407111959092.png)

### UI伪类

```html
 <style>
    /* check复选框 选中后变化 */
    div input:checked {
      width: 100px;
      height: 100px;
    }

    /* 选中被禁用的输入框 */

    div input:disabled {
      background-color: antiquewhite;
    }

    /* 选中可以使用的输入框 */
    div input:enabled {
      background-color: gray;
    }
  </style>
  
  <div>
    <input type="checkbox">
    <input type="radio">
    <input type="text">
    <input type="text" disabled>
  </div>
```

### 伪元素

并不是选中的元素，只是元素的一种特殊位置  注意伪元素俩个冒号

```html
 <style>
    /* 选中第一个单词变换 */
    div p::first-letter {
      color: rebeccapurple;
      font-size: 50px;
    }

    /* 第一行 不论窗口怎么变换都不会改变第一行的样式 */
    div p::first-line {
      background-color: slategray;
    }

    /* 选中的文字 */
    div p::selection {
      color: orange;
      background-color: blue;
    }

    /* 选中文本框中的提示文字 */
    div input::placeholder {
      color: bisque;
    }

    /* 在元素前面添加内容 注意这样添加是鼠标无法选中我们添加的内容的 */
    div span::before {
      content: '$';
    }

    /* 在元素后面添加内容 注意这样添加是鼠标无法选中我们添加的内容的 */
    div span::after {
      content: '.00';
    }

    
  </style>
  
  
  <div>
    <p>bdchsvdcsd sbchsdcusd csbcsb </p>
    <input type="text" placeholder="请输入密码">
    <br>
    <span>199</span>
    <br>
    <span>299</span>
    <br>
    <span>399</span>
    <br>
    <span>499</span>
  </div>
```

### 优先级（重点）

​		！import  》 行内 》 ID  》 类 》 元素 》 继承/通配符*

权重：     无穷大 》 1000 》 0100 》 0010 》 0001 》 0000 

注意在css优先级中根据权重计算的，而不是根据前后顺序，只有当俩个css权重相同的时候才考虑前后顺序的问题。这上面的权重是一个量级的问题，也就是说在css中 行内永远大于ID，无论写多少ID也不能超过一个行内样式。存在同一个量级的时候才需要去可考虑一共权重相加是谁大谁小的问题

### 三大特性

