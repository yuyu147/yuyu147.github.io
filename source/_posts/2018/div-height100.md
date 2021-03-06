---
layout:     post
title:      "DIV的Height为什么不能100%"
subtitle:   "width:100%;"
date:       2018-05-30
author:     "BoomXu"
tags:
    - CSS
---

> 跟着百度IFE的基础做做，确实是遇到不少问题，在**[《三种简历》](http://ife.baidu.com/course/detail/id/40)**这一章，侧边导航就遇到了高度无法铺满的问题。

# 那为什么 height:100%; 不起作用

> 在html布局中body内第一个div盒子对象设置100%高度height样式，是无法成功显示100%高度的。这个是因为body高度默认值为自适应的，所以及时设置body第一个布局div高度为百分比也是无效的，因为div解析上级高度为0，自然div height 100%实际高度也为0。

> 浏览器根本就不计算内容的高度，除非内容超出了视窗范围(导致滚动条出现)。或者你给整个页面设置一个绝对高度。否则，浏览器就会简单的让内容往下堆砌，页面的高度根本就无需考虑。

> 因为页面并没有缺省的高度值，所以，当你让一个元素的高度设定为百分比高度时，无法根据获取父元素的高度，也就无法计算自己的高度。换句话说，父元素的高度只是一个缺省值：height: auto;。当你要求浏览器根据这样一个缺省值来计算百分比高度时，只能得到undefined的结果。也就是一个null值，浏览器不会对这个值有任何的反应。

> 如果想让一个元素的百分比css高度height: 100%;起作用，你需要给这个元素的   **所有父元素**   的高度设定一个有效值。

~~这里的  **所有父元素**  我发现其实是错误的，只要根元素 < html > 的高度设置好，其他子元素都是自动继承的。。而父元素块HTML本身是没有高度的~~

以上当我没说，还是必须要所有的父元素都要设置。
```
html,body{
  height:100%;
}
```

# 解决方法

## 方法一

为 根元素 < html  > 设置高度

```
html{
  height:100%;
}
```

## 方法二

方法二就是使用绝对定位，使div脱离标准流，也就是脱离了他的根元素 html
``` CSS
.title{
  float: left;
  position:absolute;
  width: 20%;
  height: 100%;
  background-color: dodgerblue;
  font-size: 28px;
  font-weight: bold;
}
```

# 结果

Height:100%的方法，缺点缺非常显著，你在div内定义 padding 或者是 margin 就会把页面撑开，也就是说超过了 100%，就会出现一个非常不完美的滚动条。。 当然你可以用 `overflow: hidden;` 溢出隐藏，但是这样只是掩耳盗铃，滚动条是没了，页面的滚动却不受控制了。

神奇的CSS 。。 