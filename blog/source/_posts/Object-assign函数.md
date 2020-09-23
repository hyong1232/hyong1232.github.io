---
title: Object.assign函数
date: 2020-09-23 17:05:02
tags:
categories:
---

## 简介
**Object.assign()**方法使用target的setter方法和origin对象的getter方法，复制对象可枚举的属性值，适用于很多的object操作。
<!-- more -->

## 常用方法
1、复制对象值，并返回新创建新对象
{% codeblock lang:javascript %}
Objec
t.assign({},{a:'a'},{b:'b'})
{% endcodeblock %}

2、为对象添加新属性
{% codeblock lang:javascript %}
Object.assign(orgin,{add:'add'})
{% endcodeblock %}

3、为对象添加新方法
{% codeblock lang:javascript %}
const obj = {
    val:'val',
}
Object.assign(obj.prototype,{
    getName(){
        ....
    }
})
{% endcodeblock %}

### 特性：
1、由于Object.assign采用的是浅拷贝，因此源对象的属性值是对象时，只是复制了引用，再后面的复制中出现此对象的修改，则直接替换他的引用
{% codeblock lang:javascript %}
const obj1 = {a: {b: 1}};
const obj2 = Object.assign({}, obj1);

obj1.a.b = 2;
obj2.a.b // 2
{% endcodeblock %}

2、不能复制origin源对象的继承属性，只能同通过Object.getPrototypeOf(origin)+Object.create()+origin方法，将其继承的方法单独调出来，然后合并

{% codeblock lang:javascript %}
let originProto = Object.getPrototypeOf(origin);
return Object.assign(Object.create(originProto), origin);
{% endcodeblock %}


3、target/orgin对象为非对象
+  target为非对象，转换成对象，如果是null/undefined不可转换成对象的属性时，报错
+ origin为非对象时，自动转换，如果是null/undefined不可转换成对象的属性时，直接跳过

4、数组处理
> 将数组当成对象处理，键值为index下标
{% codeblock lang:javascript %}
Object.assign([1,2,3],[4,5])=>[4,5,3]
{% endcodeblock %}

5、取值函数处理（关键字get开头）
> 直接取值，不会获取取值函数合并
{% codeblock lang:javascript %}
const obj = {
    get name (){
        return 'jack'
    }
}
Object.assign({},obj)=>{name:'jack'}
{% endcodeblock %}