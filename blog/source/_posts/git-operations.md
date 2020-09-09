---
title: git-operations
date: 2020-09-08 13:57:23
tags: 
- [git]
categories:
- [git,git常用操作]
---
## 简介

**感谢阮一峰先生的分享[常用git命令清单](http://www.ruanyifeng.com/blog/2015/12/git-cheat-sheet.html) 仅供个人学习。**
关于git的常见操作命令，和对版本，分支的处理还有git的工作流程的解释说明。
<!-- more -->
常用的6个git命令可以用下面的一张图表示：

{% img /images/git.png '常用git命令图' %}

|名称|释义|
|---|---|
|workspace|工作区，即自己写代码的文件夹|
|Index|暂存区，可以撤销保存，适用于大型项目文件的提交修改|
|Remote|可以是自己的服务器或者是github或者gitee这样的第三方工作仓库。|
|Repository|指的是自己的本地仓库，就是在以.git结尾的文件夹中的文件|

## 新建代码库
 初始化一个代码库 
> 本地初始化
{% codeblock lang:shell  %}
git init [project-name]
{% endcodeblock %}
+ 本地新建一个代码库会新建一个.git隐藏文件

> clone仓库中已有的代码到本地
{% codeblock lang:shell  %}
git clone url [project-name] [--depth=num] 
{% endcodeblock %}
+ 其中num为想要拷取的代码仓库深度，为1则表示最近一次的更新的最新代码

## 暂存区操作
1、添加文件到暂存区
{% codeblock lang:shell %}
git add [file1] [file2] ...
git add [dir]
git add .
{% endcodeblock %}
+ 其中 . 代表所有修改了的文件，最常用

2、将文件删除/从暂存区删除
{% codeblock lang:shell %}
git rm [file1] [file2] ...
git rm --cached [filename]
{% endcodeblock %}
+ 其中--cached代表不删除工作区文件，只是从暂存区中删除
+ 只有在暂存区中的文件对其执行删除操作才有效

3、修改文件名称，并将修改信息存入暂存区
{% codeblock lang:shell %}
git mv [file-origin-name] [file-new-name] 
{% endcodeblock %}
+ 文件要先在暂存区中

## 提交文件到本地仓库
>提交操作都是需要写注释的，便于协作

1、直接提交文件到仓库
{% codeblock lang:shell %}
#提交所有有修改记录的文件到仓库
git commit -m "message"

#指定要提交的提交文件
git commit [file1] [file2]... -m "message" 
{% endcodeblock %}

2、用本次提交覆盖上次的提交
{% codeblock lang:shell %}
#覆盖上次提交到仓库的内容，仓库中的文件修改一本次为准
git commit --amend -m "message"

#指定要覆盖的仓库文件
git commit --amend [file1] [file2]... -m "message" 
{% endcodeblock %}

3、其他提交
{% codeblock lang:shell %}
#提交工作区自上次commit之后的变化，直接到仓库区(不包括新增文件/文件夹)
git commit -a

#提交时显示所有diff信息
git commit -v
{% endcodeblock %}