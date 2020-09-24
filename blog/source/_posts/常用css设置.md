---
title: 常用css设置
date: 2020-09-24 09:58:33
tags:
categories:
---

## 简介
列举常见的css命令，用于特定的功能。
<!-- more -->

## 文本用超过使用...表示

1、单行显示省略号
{% codeblock lang:javascript %}
selector{
    overflow:hidden;
    text-overflow:ellipsis;//使用省略号代替截断文字
    white-space:nowrap;//不换行
}
{% endcodeblock %}

2、多行显示（适用于chrome内核的浏览器）
{% codeblock lang:javascript %}
selector{
    overflow:hidden;
    text-overflow:ellipsis;
    display:-webkit-box;//显示格式为弹性伸缩盒子
    -webkit-box-orient:vertical;//元素内部排列方式
    -webkit-line-clamp:2;//显示的文本行数（非标准属性，与上面两个属性结合才可使用）
}
{% endcodeblock %}

## 将元素设置为吸顶模式
{% codeblock lang:javascript %}
selector{
    
}
{% endcodeblock %}

## 将元素设置为内敛模式
{% codeblock lang:javascript %}
selector{
    box-sizing:content-box;默认
    box-sizing:border-box;//设置为内敛模式
}
{% endcodeblock %}