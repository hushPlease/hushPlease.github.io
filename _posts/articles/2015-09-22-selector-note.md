---
layout: post
title: "CSS3 Selector Note"
excerpt: "A note when I finished studying CSS3 selector."
categories: articles
tags: [CSS, Markdown]
author: hush_please
comments: true
share: true
modified: 2016-07-12T14:18:57-04:00
image:
  feature: so-simple-sample-image-7.jpg
  credit: WeGraphics
  creditlink: http://wegraphics.net/downloads/free-ultimate-blurred-background-pack/

---

选择器指明了{}中“样式”的作用对象，也就是样式作用于网页中的哪些元素

## 属性选择器：声明属性与属性值
声明方法：[att = val]（att代表属性，val代表属性值）
[id = inst] {background-color: #66ccff;}

* [att *= val]属性选择器
如果元素用att表示的属性的属性值中包含使用val指定的字符，则该元素使用此样式
`[id *= inst] {background-attachment: fixed;}`
* [att ^= val]属性选择器
如果元素用att表示的属性的属性值的开头字符为用val所指定的字符，则该元素使用此样式
`[id ^= inst] {background-image: url();}`
* [att $= val]属性选择器
如果元素用att表示的属性的属性值的结尾字符为用val所指定的字符，则该元素使用此样式
`[id $= inst] {background-repeat: repeat;}`

## 结构性伪类选择器

首先了解两个概念：*伪类选择器* 与 *伪元素选择器*

### 伪类选择器：CSS中已经定义好的选择器，不能随便取名
常用4种锚元素(a)的选择器分别为：

        a:link {color: red; text-decoration: underline;}
        a:visted {color: red; text-decoration: underline;} 
        a:hover {color: red; text-decoration: underline;}
        a:active {color: red; text-decoration: underline;}

### 伪元素选择器

并不是针对真正的元素使用的选择器，而是针对CSS中已经定义好的伪元素使用的选择器
主要有如下*四种*伪元素选择器：

* first-line伪元素选择器：用于向某个元素中的第一行文字使用指定样式
`p:first-line {font-style: italic;}`
* first-letter伪元素选择器：用于向某个元素中的文字的首字母或第一个字使用指定样式
`p:first-letter {text-transform: uppercase;}`
* before伪元素选择器：用于在某个元素之前插入一些内容
`p:before {content: url(Sunflower.png);}`
* after伪元素选择器：用于在某个元素之后插入一些内容
`p:after {content: "(我爱你中国)";}`
  
### 四个最基本的结构性伪类选择器：root, not, empty, target

* root选择器：将样式绑定到页面的根元素中
`:root {background-color: forestgreen;} body {background-color: pink;}`
* not选择器：对某个结构元素使用样式，但是想排除这个结构元素下面的子结构元素让其不使用该样式时选用
`body *:not(p) {background-image:url(yurisa.jpeg);}`
* empty选择器：指定当元素中内容为空白时使用的样式
`:empty {background-color: limegreen;}`
* target选择器：对页面中某target元素指定样式，该样式在用户点击超链接并跳转后起作用
`:target {background-color: red;}`
  
### 选择器：first-child, last-child, nth-child, nth-last-child

单独指定*第一个子元素*、*最后一个子元素*的样式

* first-child: 对一个父元素中的第一个子元素指定样式
`li:first-child {background-color: red;}`
* last-child: 对一个父元素中的最后一个子元素指定样式
`li:last-child {background-color: red;}`

对*指定序号*的子元素使用样式

* nth-child: 对指定序号的子元素设置样式(正数)
`li:nth-child(2) {background-color: red;} -- 第2个li元素的样式`
* nth-last-child: 对指定序号的子元素设置样式(倒数)
`li:nth-last-child(2) {background-color: red;} -- 倒数第2个li元素的样式`

对所有*第奇数个子元素*或*第偶数个子元素*指定样式

* nth-child(odd): 所有正数下来第偶数个子元素
* nth-child(even): 所有正数下来第奇数个子元素
* nth-last-child(odd): 所有倒数上去第偶数个子元素
* nth-last-child(even): 所有倒数上去第奇数个子元素

> 注意，nth-child选择器在计算子元素是第奇数个元素还是第偶数个元素时，是连同父元素中的所有子元素一起计算的

### 选择器：nth-of-type, nth-last-of-type

使用这两个选择器时，CSS3在计算子元素是第奇数个子元素还是第偶数个元素时，就会*只计算同类型元素*

        td:nth-of-type(odd) {background-color: yellow;}
        td: nth-of-type(even) {background-color: blue;}
  
循环使用样式
nth-child(n)，把参数n改成可循环的an+b的形式，a表示每次循环中共包括几种样式；b表示指定的样式在循环中所在的位置
如下所示：
  
        li:nth-child(4n+1) {background-color: yellow;}   // 第一个li背景色为 黄色，依次循环 
        li:nth-child(4n+2) {background-color: bule;}     // 第二个li背景色为 蓝色……  
        li:nth-child(4n+3) {background-color: red;}      // 第三个li背景色为 红色……  
        li:nth-child(4n+4) {background-color: green;}    // 第四个li背景色为 绿色……            
                                                         // 4n+4可缩写为4n 
前面所讲的nth-child(odd)&nth-child(even)可以用如下代码替代：

        nth-child(2n+1) {样式}         // 所有正数下来的第奇数个子元素
        nth-child(2n+2) {样式}         // ……第偶数个子元素
        nth-last-child(2n+1) {样式}    // 所有倒数上去的第奇数个子元素
        nth-last-child(2n+2) {样式}    // ……第偶数个子元素

### only-child选择器：当某个父元素中只有一个子元素时使用的样式
`li:only-child {background-color: red;}`
  
## UI元素状态伪类选择器
在CSS3中共有17种UI元素状态伪类选择器，它们的共同特征是：**指定的样式只有当元素处于某种状态下才起作用，在默认状态下不起作用**

### hover, active, focus选择器
* Element:hover选择器被用来指定当鼠标指针移动到元素上时元素所使用的样式
* Element:active选择器被用来指定元素被激活（鼠标在元素上按下还没有松开）时使用的样式
* Element:focus选择器被用来指定元素获得光标焦点时使用的样式，主要在文本框控件获得焦点并进行文字输入时使用

### enabled, disabled伪类选择器
* Element:enabled伪类选择器用来指定当元素处于可用状态时的样式
* Element:disabled伪类选择器用来指定当元素处于不可用状态时的样式

### read-only, read-write伪类选择器
* Element:read-only伪类选择器用来指定当元素处于只读状态时的样式
* Element:read-write伪类选择器用来指定当元素处于非只读状态时的样式

> 在Firefox浏览器中，需写为"-moz-read-only"或"-moz-read-write"的形式

### checked, default, indeterminate伪类选择器
* Element:checked伪类选择器用来指定当表单中的radio单选框或checkbox复选框处于选取状态时的样式 
* Element:default选择器用来指定当页面打开时默认处于选取状态的单选框或复选框空间的样式

> 注意，即使将该单选框或复选框控件的选取状态设定为“不选取”，Element: default选择器指定的样式仍然有效

> 目前只有Firefox与Opera浏览器支持这一选择器

### Element:indeterminate伪类选择器
* 用来指定当页面打开时，一组单选框中没有任何一个单选框被设定为选取状态时整组单选框的样式，如果用户选取了其中任何一个单选框，则该样式取消指定

> 目前只有Opera与Chrome浏览器支持这一选择器

### Element::selection伪类选择器
* 用来指定当元素处于选中状态时的样式

> 在Firefox浏览器中，需写为"-moz-selection"的形式

### invalid, valid伪类选择器
* Element:invalid伪类选择器用来指定，当元素内容不能通过HTML5通过使用元素的诸如required，pattern等属性所指定的检查或元素内容不符合元素的规定格式时的样式
* Element:valid伪类选择器用来指定，当元素内容通过HTML5通过使用元素的诸如required，pattern等属性所指定的检查或元素内容符合元素的规定格式时的样式

### required, optional伪类选择器
* Element:required伪类选择器用来指定允许使用required属性，且已经指定了required属性的input元素、select元素以及textarea元素的样式
* Element:optional伪类选择器用来指定允许使用required属性，且未指定required属性的input元素、select元素以及textarea元素的样式

### in-range, out-of-range伪类选择器
* Element:in-range伪类选择器用来指定当元素的有效值被限定在一段范围之内，且实际输入值在该范围内时使用的样式
* Element:out-of-range伪类选择器用来指定当元素的有效值被限定在一段范围之内，但实际输入值在该范围之外时使用的样式

## 通用兄弟元素选择器
用来指定位于同一个父元素之中的某个元素之后的所有其他某个种类的兄弟元素所使用的样式

使用方法如下：

    <子元素> ~<子元素之后的同级兄弟元素> {
        //指定样式
    }

示例代码如下：

    <!DOCTYPE html>
    <html lang="en">
    
    <head>
        <meta charset="UTF-8">
        <title>通用兄弟元素选择器E~F</title>
        <style type="text/css">
            div ~ p {
                background-color: #00FF00;
            }
        </style>
    </head>
    
    <body>
        <div style="width:733px;border:1px solid #666;padding:5px;">
            <div>
                <p>p元素为div元素的子元素</p>
                <p>p元素为div元素的子元素</p>
            </div>
            <hr>
            <p>p元素为div元素的兄弟元素</p>
            <p>p元素为div元素的兄弟元素</p>
            <hr>
            <p>p元素为div元素的兄弟元素</p>
            <hr>
            <div>p元素为div元素的子元素</div>
            <hr>
            <p>p元素为div元素的兄弟元素</p>
        </div>
    </body>
    
    </html>