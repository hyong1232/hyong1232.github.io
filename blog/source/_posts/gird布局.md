---
title: gird布局
date: 2020-05-14 17:21:53
tags: 
- [css布局]
- [css]
categories:
- [css,css布局]
- [前端开发]
---
## 简介

**感谢阮一峰先生的分享[grid-layout-tutorial](http://www.ruanyifeng.com/blog/2019/03/grid-layout-tutorial.html) 仅供个人学习。**

网格布局（Grid）是最强大的 CSS 布局方案。

它将网页划分成一个个网格，可以任意组合不同的网格，做出各种各样的布局。以前，只能通过复杂的 CSS 框架达到的效果，现在浏览器内置了。
<!-- more -->

{% img https://www.wangbase.com/blogimg/asset/201903/1_bg2019032501.png 802 366 "grid布局演示图片" %}

如上图所示，grid布局是一种类二维布局的css布局方式，与flex布局一样，极大的方便了网页布局。

## 浏览器支持
![browser-spport](/images/browserSupport.PNG)
<p class="image-caption">支持的浏览器及其版本</p>

## grid属性

### display
>可选参数 gird/inline-grid
 当参数为：gird时为块级元素、inline-grid则为行内元素

### grid-template-columns
> 规定grid的列宽
example:
{% codeblock lang:css3 %}
grid-template-columns:100px 100px 100px;
{% endcodeblock %}

### grid-template-rows
> 规定grid的行宽
example:
{% codeblock lang:css3 %}
grid-template-rows:100px 100px 100px;
grid-template-rows:33% 33% 33%;
grid-template-rows:repeat(3,33%);
{% endcodeblock %}

{% blockquote %}
**grid函数设置宽高的函数**
>这些函数都可以与百分比、px、fr特数字组合定义宽高

固定100px的结果如下图所示
{% img https://www.wangbase.com/blogimg/asset/201903/bg2019032506.png 220 320 "固定px的grid示例" %}

平分宽度|高度的可以设置== 百分比 ==，或者设置1fr-类似flex，结合repeat函数则为
#### repeat(循环次数，循环体)
     参数：循环体可以为特殊关键字n+fr，与flex类似。
        >循环次数可为特殊关键字auto-fill，表示使用循环体格式自动填充满整个grid布局 。

        {% codeblock lang:css3 repeat函数示例 %}
        grid-template-rows:repeat(3,1fr);
        grid-template-rows:repeat(3,33%);
        {% endcodeblock %}
        >特殊的循环体
        {% codeblock lang:css3 repeat函数特殊循环体示例 %}
        grid-template-columns: repeat(2, 100px 20px 80px);
        {% endcodeblock %}
        
        {% img https://www.wangbase.com/blogimg/asset/201903/bg2019032507.png  "特殊循环体的repeat示例" %}

#### minmax(min,max)函数
    #### 参数：最大最小值，可以为px，fr，百分比
    #### 定义一个范围值，让宽高在这之中自适应
    {% codeblock lang:css3 minmax函数示例 %}
    grid-template-rows:minmax(100px,1fr);
    grid-template-rows:minmax(100px,33%);
    {% endcodeblock %}

#### auto关键字
>可在宽高定义时，与百分比，px，fr混用
{% codeblock lang:css3 %}
grid-template-columns: 100px auto 100px;
{% endcodeblock %}
>表示grid布局中，左右为100px，中间为自适应宽度

#### auto-fill关键字
>可以与百分比，fr，px混用，还可以代替repeat函数的循环次数，让他自适应，并换行，类似flex布局的
{% codeblock lang:css3 %}
flex-wrap:wrap;
{% endcodeblock %}
>自动换行：
{% codeblock lang:css3 %}
display: grid;
grid-template-columns: repeat(auto-fill, 100px);
{% endcodeblock %}
{% img https://www.wangbase.com/blogimg/asset/201903/bg2019032508.png  "auto-fill关键字+repeat函数自动换行示例" %}

#### 布局实用示例
    ### 3:7两栏式布局
    {% codeblock lang:css3 %}
    display: grid;
    grid-template-columns: 70% 30%;
    {% endcodeblock %}
    ### 十二网格布局
    {% codeblock lang:css3 %}
    display: grid;
    grid-template-columns: repeat(12,1fr);
    {% endcodeblock %}

{% endblockquote %}

### grid-row-gap&&grid-column-gap
> 两者可以结合写成```css3 gird-gap:<grid-row-gap> <grid-column-gap>
> 简写成gird-gap时，可以只写一个值，表示行间距与列间距相同
{% codeblock lang:css3 example %}
grid-gap: 20px
{% endcodeblock %}
>新标准省略grid-字符，简写为
{% codeblock lang:css3 example %}
gap: 20px
{% endcodeblock %}
 
{% img https://www.wangbase.com/blogimg/asset/201903/bg2019032511.png 280  "gap间距为20px示例" %}

### grid-auto-flow
>规定grid布局的排列顺序，可选参数：row/column，默认为row，即优先从左到右的依次排列
>可选参数row dense/column dense规定除了指定行列的布局外，其他grid单元的布局顺序
{% codeblock lang:css3 container的css %}
display:grid;
grid-template-rows:repeat(3,100px);
grid-template-columns:repeat(3,100px);
grid-auto-flow:row dense;
{% endcodeblock %}

>指定grid-cell的列宽，左闭右开原则
{% codeblock lang:css3 指定列宽的grid-cell的css %}
grid-column-start:1;
grid-column-end:3;
{% endcodeblock %}

>grid-column-start/end设置的数字单位为grid-cell面积，左闭右开
>结果如下
{% img https://www.wangbase.com/blogimg/asset/201903/bg2019032514.png 280 "指定单元格，其余row
布局示例" %}

>如果单独设置grid的大小要注意不要超过grid定义的gird-cell个数，否则自适应
![over-grid-number](/images/overgridnumber.PNG)
<p class="image-caption">自定义grid-cell范围超过初始化定义图</p>

上图中7、8、9因为超过了初始设置的grid-cell范围，而自适应 **解决办法**：补足不足grid个数或调整布局 **增加初始设置的行列即可**

### align-items&&justliy-items&&place-items
>规定grid-cell的位置，align表示高（上、中、下）、justlify表示宽（左、中、右）
可选属性：start|center|end|stretch——靠左|居中|靠右|自动填满
place-items是简写形式
{% codeblock lang:css3 %}
place-items:<align-items> <justify-items>
{% endcodeblock %}
>如果不写第二个参数则默认两个属性值相同
{% codeblock lang:css3 %}
align-items:center;
justify-items:strech;
{% endcodeblock %}
>可简写为
{% codeblock lang:css3 %}
place-items:<align-items> <justify-items>
place-items:stretch center;
{% endcodeblock %}
>如下图所示
![place-items](/images/center-stretch.PNG)
<p class="image-caption">place-items结果图</p>

### align-self&&justify-self&&place-self
>与align|justify|place-items用法完全一致，但只作用于单个grid-cell
{% codeblock lang:css3 %}
.item-1 {
  place-self:stretch center;
  background-color: #ef342a;
} 
{% endcodeblock %}
 
![place-self](/images/place-self.PNG)
<p class="image-caption">place-self单个grid-cell作用域</p>

### align-content&&justify-content&&place-content
>规定整个项目在grid-container中的位置
可选属性：start|center|space-between|space-evenly|space-around——between间隔在项目之间
    <div style="display:grid;grid-template-columns:repeat(3,1fr);grid-template-rows:160px;grid-auto-rows:0;gap:10px">
        <div style="grid-column-start:1;grid-row-start:1;">{% img https://www.wangbase.com/blogimg/asset/201903/bg2019032522.png  "space-around" %}</div>
        <div style="grid-column-start:2;grid-row-start:1;">{% img https://www.wangbase.com/blogimg/asset/201903/bg2019032523.png  "space-between" %}</div>
        <div style="grid-column-start:3;grid-row-start:1;">{% img https://www.wangbase.com/blogimg/asset/201903/bg2019032524.png  "space-evenly" %}</div>
    </div>

### grid-auto-row&&grid-auto-column
>规定如果定义的grid-cell不在初始定义的grid-cell数量之内，扩展的grid-cell的列宽、行高
{% codeblock %}
  display: grid;
  grid-template-columns: 100px 100px 100px;
  grid-template-rows: 100px 100px 100px;
  grid-auto-rows: 50px;
{% endcodeblock %}

{% img https://www.wangbase.com/blogimg/asset/201903/bg2019032525.png 280 "grid-auto-row为50px" %}

### grid-template&&grid
>+ grid-template属性是grid-template-columns、grid-template-rows和grid-template-areas这三个属性的合并简写形式。
{% codeblock lang:css3 %}
grid-template:<grid-template-rows> <grid-template-area> / <grid-template-columns>
example
grid-template: [header-left] "head head" 30px [header-right]
                [main-left]   "nav  main" 1fr  [main-right]
                [footer-left] "nav  foot" 30px [footer-right]
                / 120px 1fr;
{% endcodeblock %}                
>等同于
{% codeblock lang:css3 %}
grid-template-rows: [header-left] 30px [header-right main-left] 1fr [main-right footer-left] 30px [footer-right];
grid-template-columns: 120px 1fr;
grid-template-areas: "head head" "nav main" "nav foot";
{% endcodeblock %}
>结果图
![grid-template](/images/grid-template.PNG)
<p class="image-caption">grid-template简写结果图</p>

>+ grid属性是grid-template-rows、grid-template-columns、grid-template-areas、 grid-auto-rows、grid-auto-columns、grid-auto-flow这六个属性的合并简写形式。
从易读易写的角度考虑，还是建议不要合并属性，所以这里就不详细介绍这个属性了。

## grid-cell属性

### grid-column-start|end&&grid-row-start|end
>+ 属性值可为数字，与grid-auto-flow属性结合可以实现特定布局
{% codeblock%}
  grid-column-start: 1;
  grid-column-end: 3;
  grid-row-start: 2;
  grid-row-end: 4;
{% endcodeblock%}
 
{% img https://www.wangbase.com/blogimg/asset/201903/bg2019032527.png 280 "数字方式定义grid-cell起始位置" %}
>+ span参数结合使用，表示跨过多少个grid-cell，即可用在start，也可用在end
{% codeblock%}
 grid-column-end: span 2;
{% endcodeblock%}
 
{% img https://www.wangbase.com/blogimg/asset/201903/bg2019032528.png 280 "数字方式定义grid-cell起始位置" %}
>+ 如果因为设置属性产生了重叠，可通过设置z-index调整

### grid-column&&grid-row
>+ 是grid-row-start|end和grid-column-start|end的简写
{% codeblock%}
 grid-row:<grid-row-start> <grid-row-end>;
 grid-columns:<grid-columns-start> <grid-columns-end>;
{% endcodeblock%}

>+ 可以与span（宽行）联合使用
{% codeblock%}
  background: #b03532;
  grid-column: 1 / 3;
  grid-row: 1 / 3;
/* 等同于 */
  background: #b03532;
  grid-column: 1 / span 2;
  grid-row: 1 / span 2;
{% endcodeblock%}
>+ 可以不写/end，默认是跨了一行
{% codeblock%}
  grid-column: 1;
  grid-row: 1;
{% endcodeblock%}
>上面代码表示第一个grid
**简写时不可直接写span+n而不规定起/始位置**

### grid-template-areas
>+ 给grid命名并划分区域
{% codeblock%}
  display: grid;
  grid-template-columns: 100px 100px 100px;
  grid-template-rows: 100px 100px 100px;
  grid-template-areas: 'a b c'
                       'd e f'
                       'g h i';
{% endcodeblock%}
>上面代码表示将grid划分为a~i的九个区域，相同命名就是同一个区域，结合grid-area可指定grid-cell大小

>+ 不用利用的区域用'.'代替命名
{% codeblock%}
    display: grid;
    grid-template-columns: 100px 100px 100px;
    grid-template-rows: 100px 100px 100px;
    grid-template-areas: 'a . c'
                        'd . f'
                        'g . i';
{% endcodeblock%}
>上面代码表示中间区域不使用,不属于任何区域

>+ 区域的命名会影响到网格线。每个区域的起始网格线，会自动命名为 **区域名-start**，终止网格线自动命名为 **区域名-end**。如上面的a区域的起始网格线为a-start&a-end

### grid-area
>+ 与grid-template-area结合使用，指定grid-cell位置
{% codeblock%}
.container{
  display: grid;
  grid-template-columns: 100px 100px 100px;
  grid-template-rows: 100px 100px 100px;
  grid-template-areas: 'a b c'
                     'd e f'
                     'g h i';
}
.item-1 {
  background-color: #ef342a;
  grid-area: e;
}       
{% endcodeblock%}
>如下图
{% img https://www.wangbase.com/blogimg/asset/201903/bg2019032530.png 280 "grid-area指定grid-cell位置" %}

>+ 是grid-row|column-start|end的简写
{% codeblock%}
    grid-area: <row-start> / <column-start> / <row-end> / <column-end>;
    example
    gird:1/1/3/3
{% endcodeblock%}
>如下图所示，简写结果 **不支持span结合使用**
![grid-area简写](/images/grid-area.PNG)
<p class="image-caption">gird-area简写</p>