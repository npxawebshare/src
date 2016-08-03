---
title: 实习总结-JavaScript hy-001篇
date: 2016-04-26 18:45:55
tags:

- JavaScript
- ajax
- 实习学习总结

---

### JavaScript原生ajax原理，发送一个异步请求的主要步骤是：

1. 创建XMLHttpRequest或ActionXObject(IE浏览器)实例xhr；
2. 设置xhr的属性onreadystatechange触发的函数，一般要在函数内部判断xhr的readyState属性值，在等于4的时候表示请求正常返回，可以接收和处理xhr的返回值responseText或responseXML；
3. 创建主函数，用包装发送请求，调用步骤2的触发函数，做出响应。

### 字符串的使用：

1. 两种不同初始化字符串的区别，`String(s)`, `new String(s)`，前者创建变量类型是string，后者是object；
2. 基本字符获取类的函数：`charAt(index)` 返回字符串string的第n个字符、`charCodeAt(index)` 返回第n个字符的Unicode编码、`ndexOf(substring[,start])`在string中的start位置之后存在substring返回出现的第一个substring 的位置、以及`lastIndexOf()`的使用方法；
3. 字符抽取类的几个函数演示：`substring(from[, to = end])` --返回一个新字符串，包含的字符是从string中的from处到to-1处复制的、`substr(from, to) `、`slice(start, end) `返回包括字符串从start开始(包括start)到end为止(不包 括end)的所有字符、`split("?")` 返回截取字符串段的数组、`concat(s) `连接字符串 一般使用 “+”
4. `replace(regexp, replacement)` 替换匹配的第一个、`match(reg) `返回匹配结果的数组

### 数组

1. 学习，大部分函数类似string的函数，分清其`pop push shift unshift`；`splice`会改变原数组元素，`slice`不会改变原数组；借助`sort`函数自定义排序
2. 函数对象Function的了解，主要是apply和call的使用，他们可以重新定义函数的上下文，了解argument的基本用法;
3. Json的基本格式 会遍历`json`，`eval("(" + jsonstr +")")`可以把json字符串转换为json对象eval加括号将括号内的表达式（expression）转化为对象，而不是作为语句来执行。