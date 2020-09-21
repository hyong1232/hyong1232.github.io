---
title: babel使用介绍
date: 2020-09-21 15:08:19
tags:
- [ES6]
- [babel]
categories:
- [ES6,babel]
---

## 简介
babel+webpack作为es6必用的工具，配置和使用较为麻烦，小节了一下常见的使用和配置。
<!-- more -->

### 配置在项目中使用
> 可使用配置文件.babelrc将常见配置写入文件中（放置在项目的根目录下），再webpack打包的过程中，会自动读取这个文件的配置，常见的配置写法如下:
{% codeblock lang:javascript %}
{
    "presets":['es2015','env','stage-0'],
    "plugins":['transform-runtime']
}
{% endcodeblock %}

+ .babelrc文件整个就是一个对象，在对象{}中配置相应的属性即可
+ 常用的presets规则以及转换插件需要自行下载（npm命令即可）
**babel配置也可以在webpack的配置文件中配置，即在module下的rules数组对象的规则对象的use属性中添加options属性中添加即可**
{% codeblock lang:javascript %}
module:{
    rules:[
        {
            test:/\.js$/,
            exclude:/node_modules/,
            use:{
                loader:'babel-loader',
                options:{
                    presets:['env'],
                    plugins:['transform-runtime']
                }
            }
        }
    ]
}
{% endcodeblock %}
**关于转换规则stage-0/1/2...在新的webpack中不在推荐使用，避免过多使用**

### 命令行中直接转换
> 除了在项目中使用还可以直接在命令行转换es6的代码

1、安装@babel/cli
{% codeblock lang:javascript %}
npm i -D @babel/cli
{% endcodeblock %}
2、基本用法
{% codeblock lang:javascript %}
//转换单个es6语法的文件到指定文件夹
npx babel es6.js --out-file out.js
//简写为
npx babel es6.js -o out.js

//转换文件夹至指定路径输出
npx babel es6dir -out-dir outdir
//简写为
npx babel es6dir -d outdir

//加上 -s参数生产source map文件
npx babel es6dir -d outdir -s
{% endcodeblock %}
+ 转换文件到目标文件/文件夹时，没有会自动创建
+ 文件夹转换是将源文件夹中的文件依次转换到对应的输出，出错则停止转换
+ 关于npx可见
{% blockquote 阮一峰 https://www.ruanyifeng.com/blog/2019/02/npx.html npx使用教程 %}
常见的npx使用方式
{% endblockquote %}
+ 关于sourceMap可见
{% blockquote 阮一峰 http://www.ruanyifeng.com/blog/2013/01/javascript_source_map.html JavaScript Source Map 详解 %}
sourceMap介绍
{% endblockquote %}