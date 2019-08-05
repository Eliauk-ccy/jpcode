# CSS

[TOC]
## 概述

### 一、什么是css

1. css（Cascading Style Sheets）

   层叠样式表  级联样式表  简称  样式表

2. css作用

   ​	写样式

   * 实现了内容与表现的分离
   * 提高了代码的可重用性和可维护性

3. 文件后缀

   ==.css==

4. css由浏览器解析执行，由上往下，由左往右

5. css语法

   * css键值对组成
   * 属性:属性值;

   ==注意：==

   * HTML的属性  属性="属性值"

6. css的特点

   * 继承性

     父元素设置了样式子元素可以继承

   * 层叠性

     一个元素可以同时设置多个样式

   * 优先级

     优先级高的样式生效；优先级相同，后写的样式生效

### 二、CSS引入方式

1. 内联样式  行内样式   —— 只对当前元素生效

   * 用HTML的style属性引入（除了br，都有style属性）

   例子：

```html
<div style="width:200px;height: 200px;background-color: red;color: green; ">盒子</div>
```

2. 内部样式  ——   只对当前页面生效

```html
<head>
    <style>
        选择器{
            属性:属性值;
            属性:属性值;
            属性:属性值;
            属性:属性值;
        }
    </style>
</head>
```
3. 外部方式 —— 实现了内容与表现的完全分离，提高了代码的可重用性和可维护性
```html
<head>
    <link rel="stylesheet" href=".css"/>
</head>
```
* 一个HTML文件可以引入多个css文件

* 同一个css文件可以被多个HTML文件引入

4. 导入式

```html
<head>
    <style>
        @import ".css"|url(".css");
    </style>
</head>
```

==@import 和 link的区别：==

* @import先加载HTML文件，再加载css文件，link是同时加载HTML和css文件
* @import有兼容性（IE5以上支持），link没有兼容性
* @import只能引入css文件，link还可以引入其他内容

		`<link rel="icon" href=""/>`

* JavaScript操作DOM时，只能操作link引入的css样式
* @import会增加页面的http请求

==优先级：行内样式>内部样式(外部样式)==

## 选择器

### 一、基础选择器

1. 全局选择器
   * ` *{}`  ==选中页面所有的元素==

2. 元素选择器
   * ` 标签名{}`==选中页面所有指定的元素==

3. 类选择器
   * ` ."类名"{}`

     * ```html
       <div class="box"></div>
       ```
       ```css
       .box{
           wigth:500px;
       }
       ```

     * 类名 命名规则：

     1. 可以包含数字、字母、下划线；
     2. 不能以数字开头；
     3. 起有意义的名字。
       * class的名字可以重复，一个clas可以起多个名字，用空格隔开

4. ID选择器

   * ` #"id名称"{}`
     * 代码格式以及ID类似于class，如类选择器，但是==ID唯一==

       **选择器优先级**

   		==行内样式>ID选择器>类选择器>元素选择器>全局选择器==
   权重：1000       100              10                1 （数越大，优先级越高）

5. 合并选择器

   ` 选择器一，选择器二，.......{}`

### 二、关系选择器

1. 后代选择器 `选择器1 选择器2{}`  （空格隔开）
   * 选中所有后代（包含子代）
2. 子代选择器 ` 选择器1>选择器2{}`
   * 选中所有直接子代
3. 相邻兄弟选择器` 选择器1+选择器2{}`
   * 平级紧挨着的一个兄弟（后面）
4. 通用兄弟选择器` 选择器1~选择器2{}`
   * 平级后面的所有兄弟

### 三、伪类选择器

1. :link		点击之前（a）
2. :visit  	点击之后	（a）
3. :hover     鼠标悬停
4. :after       鼠标按下



* css3新增
  1. :first-child
  2. :last-child
  3. :nth-child（number|even|odd）
  4. :only-child
  5. :empty
  6. :not(基础选择器)==不包含==
  7. :chencked   被选中时的样式
  8. :focus    获取焦点时的样式

## 属性

### 一、HTML的四大标准属性

==除了`<br>`没有，其他元素都有的属性==

1. title 鼠标悬停给予提示
2. style 行内样式
3. class 类选择器
4. ID ID选择器

### 二、列表属性

1. 设置项目符号
   * `list-style-type:none;`
2. 设置项目符号为图片
   * `list-style-type:url("");`
3. 设置项目符号的位置
   * `list-style-position:outside|inside;`
4. 简写：==list-style:none==

### 三、表格的属性

1. 宽高：
   * `width:x px;`
   * `height:y px;`
2. 表格的边框：
   * `1px solid #xxxxxx;`
3. 内容水平对齐方式：
   * `text-align:left|center|right;`
4. 单元格内容垂直对齐方式：
   * `vertical-align:top|middle|bottom;`
5. 表格水平居中：
   * `margin:0 auto;`==（块级元素）==
6. 边框折叠：
   * `border-collapse;`（折叠）

### 四、背景属性

1. 背景颜色
   * `background-color:transparent(透明);`
     * 颜色的取值：
       * 关键字  red
       * 十六进制   #000   #fff
       * rgb(255,255,255)
       * rgba(0,0,0,.5)
2. 背景图片
   * `background-image:url(""):`

3. 设置背景图片是否平铺（默认平铺）

   * `background-repeat:repeat|no-repeat|repeat-x|repeat-y;`

4. 设置背景图片的大小

   * `background-size:x y;`
     * 取值 %  px  cover  contain
     * cover  完全覆盖背景区域，但是背景图片可能显示不完全
     * contain   图片扩展值足够大，但是背景区域可能覆盖不完全
     * 当只取一个值，第二个默认等比例缩放

5. 设置背景图片定位

   * `background-position:x y;`
     * 默认在0 0（左上角）
     * 当只取一个值，第二个值默认居中
     * 取值 px  %  left right  center top bottom
     * 左上角为0% 0%   右下角为100%  100%
     * 取正值 往右下走  ；  取负值  往左上

6. 设置背景图片固定

   * `background-attachment:fixed|scroll;`

7. ==简写==

   * background:背景颜色 背景图片 是否平铺 大小 定位 固定;

     ==简写属性和单个属性同时存在：简写属性写在上面==

### 五、其他常见属性

1. 溢出属性
   1. `overflow`==设置内容溢出部分==
      * `overflow：hidden|scroll|auto`
      * 当内容超出元素显示区域之后*隐藏|滚动条|自动*
   2. 一行文字溢出省略号显示
      * ` white-space:nowrap`一行显示
      * ` overflow:hidden`超出部分隐藏
      * ` text-overflow:ellipsis`超出部分省略号显示
      * ==顺序可变，缺一不可==
2. 字符之间的距离；
   * `letter-spacing：；`
3. 英文字母大小写转换
   * `text-transform:`uppercase|lowercase|capitalize;
4. 首行缩进
   * `text-indent：；`
     * px绝对单位	像素
     * em相对单位     相对于文字大小，默认字体大小为16px   1em=16px
5. 设置英文长单词换行：
   * `word-wrap：normal|break-word`
6. 设置容器中元素和内容的垂直对齐方式（一般配合表格使用）
   * `vertical-align:top|bottom|middle;`
7. 设置元素的透明度
   * `opacity`（0~1）元素中的所有内容
   * `rgba`是只给当前内容设置透明

## 盒模型

### 一、标准盒子模型   W3C盒模型

1. 组成部分
   * content + padding + border + margin
   * 内容            内边距      边框        外边距
   * 水杯             泡沫          快递盒      俩快递之间的距离 

2. 实际宽度
   * ==width + padding x2 + border x2 + margin x2==

3. content（内容区域）
   * `width: x px;`
   * `height: y px;`
   * `min-width|height;`最小宽|高
   * `max-width|height;`最大宽|高

4. border（边框）

   * `border-style:solid|dotted|dashed|double|none;`
     * ​                      实线|  点线   |   虚线  | 双实线 |不显示 
     * 必须属性  默认3px，黑色
   * border-color:#xxxxxx;（边框颜色）
   * border-width:x px;（边框粗细）
     * 可以单独设置一个边的属性

5. padding（内边距）

   * 内边距  不能取负值和auto
   * 设置内容距边框的距离
   * **语法：**
     * padding:value;    四周
     * padding:value value;  上下   左右
     * padding:value value value; 上  左右  下
     * padding:value value value value;  上 右  下 左  （顺时针转）
   * 四周（单独）：
     * padding-top:;  上内边距
     * padding-bottom:;  下内边距
     * padding-left:;  左内边距
     * padding-right:;  右内边距

   ***注意***：==padding会撑大容器==

6. margin（外边距）

   * 外边距可以取正负和auto
   * 设置元素之间的距离
   * 外边距是透明的
   * **语法：**
     * margin:value;    四周
     * margin:value value;  上下   左右
     * margin:value value value; 上  左右  下
     * margin:value value value value;  上 右  下 左  （顺时针转）
   * 四周（单独）：
     * margin-top:;  上外边距
     * margin-bottom:;  下外边距
     * margin-left:;  左外边距
     * margin-right:;  右外边距

***注意*** 

1. 块级元素水平居中
   ```css
   div{
       width:50px;
       margin:0 auto;
   }
   ```

2. 垂直方向上外边距合并问题

   * 当垂直方向上外边距相撞时，取较大值

     ==浮动元素不合并==

3. margin-top问题
   * 第一个块级子元素设置margin-top，父元素会一起走下来
     ==解决：==
     * 父元素加overflow:hidden;
     * 父元素或者子元素浮动
     * 父元素加border:1px solid transparent;
     * 父元素加padding-top:1px

### 二、怪异盒模型   IE盒模型

1. 组成部分
   + content + padding + border + margin
   + 内容            内边距      边框        外边距
   + 水杯             泡沫          快递盒      俩快递之间的距离 
2. 实际宽度
   + ==width+margin(width包含了border和padding)==
3. 盒模型相互转换
   * box-sizing:content-box;默认标准盒模型
   * box-sizing:border-box;怪异盒模型

### 三、伸缩盒模型    flexbox

1. 作用
   * 主要用于移动端布局
   * 弹性盒中浮动属性不生效（float clear vertical-align）
2. 父元素上的属性：
   * 开启弹性盒：`display:flex;`
   * 设置弹性盒的方向：`flex-direction:row|column`
     * `row：`默认值 子元素水平排列
     * `column：`子元素垂直排列
     * ``-reverse：``倒序
   * 设置子元素在主轴的对齐方式
     * 默认主轴为x轴，侧轴为y轴；当弹性盒的方向为column时，主侧轴互换
     * 主轴对齐方式：`justify-content: flex-start|center|flex-end|space-between|space-around;`
       * flex-start：始对齐
       * center：居中
       * flex-end：末对齐
       * space-between：两端对齐
       * space-around：分散对齐
   * 设置子元素在侧轴的对齐方式
     * 侧轴对齐方式：`align-items:flex-start|center|flex-end`
       * flex-start：始对齐
       * center：居中
       * flex-end：末对齐
3. 子元素上的属性：
   * flex-grow:number;
     * 设置子元素的宽度比例

## 块级元素和行内元素的区别：


* 块级元素独占一行，行内元素在同一行显示

* 块级元素默认宽度为100%，行内元素宽度由内容撑开

* 块级元素可以设置宽高，行内元素设置宽高不生效

* 块级元素可以设置margin和padding四周，行内元素只能设置margin和padding左右

* 块级元素的默认display：block；行内元素默认display：inline；

* 布局时，块级元素可以嵌套行内元素和块级元素，行内元素一般不要包含块级元素

* 块级元素

  `hn,p,hr,div,ul,ol,li,dl,dt,dd,table,tr,td,th、form,header,nav,footer,aside,article,section....`

* 行内元素

  `span,a,img,b,i,u,s,del,sup,sub,small,big,em,strong,input,button,video,audio、textarea....`

## 居中问题

1. 元素内容水平居中

   * text-align

2. 一行文字垂直居中

   * line-hignt等于高度

3. 块级元素水平居中
```css 
	div{
  		width:20px;
        margin:0 auto;
     		}	
```

4. 多行内容垂直居中

   * padding撑开

5. 子元素在父元素中垂直居中（块级元素）

   * margin计算法
   * padding计算法
   * 移动端flex布局
   * 绝对定位计算法
   * 绝对定位

## 浮动和定位

1. 普通流定位

   * 块级元素垂直排列
   * 行内元素水平排列

2. 浮动定位

   * 原理

     * 浮动以后排除到普通文档流之外
     * 浮动后不占据位置（原位置不保留）
     * 浮动是碰到父元素边框或者浮动元素边框就会停止
     * 浮动不会重叠
     * 只有左右浮动，没有上下
     * 浮动后所有元素转换为块级元素

   * 语法

     * `float:left|right|none;`

   * ==清除浮动的影响==

     * 浮动元素的父元素加overflow：hidden；（自动找高）

     * 浮动元素的父元素加height（高度已知）

     * 受影响的元素加clear:both

     * 空div法：浮动元素的后面加空div  div{clear:both}

     * 伪对象法

       ```浮动元素的父元素```

       ```::after{```

       ```}```

3. 相对定位

   

   * relative：相对定位
     * 相对于自己定位，定位后原位置保留
       * 配合left、top、right、bottom；
     * 应用场景：
       * 配合绝对定位使用
       * 元素自己小范围移动

4. 绝对定位

   * absolute：绝对定位

   + 相对于已经定位（`relative、absolute、fixed`）的父元素定位，定位后原位置不保留
   + 应用场景：
     + 形成独立的一层

5. 固定定位

   * fixed：固定定位
   * 相对于浏览器窗口定位，固定定位后，原位置不保留
   * 应用场景：
     * 固定在页面的某个地方

6. static：静态定位（默认值）

7. z-index:number；堆叠顺序

   + 默认值为1
   + 取值越大，层级越往上,可以取负值（考虑兼容性问题）
   + 必须配合定位（relative、absolute、fixed）使用
   + 同时定位，后面的元素会覆盖前面的元素

## display属性

1. none：不显示，隐藏对象，不占据位置，原位置不保留
2. block：块级元素
3. linline：行内元素
4. inline-block：既可以设置宽高，又可以在同一行显示
   * 常见行内块元素：img、button、input
   * 行内块元素可以识别代码之间的空白
5. flex：弹性盒









## 设置属性后原位置问题

* 设置属性后原位置不保留：
  1. float
  2. position：absolute；
  3. position：fixed；
  4. display：none；
     * 原位置不保留的元素，宽高默认由内容撑开

* display；none和overflow：hidden；和visibility：hidden和opacity：0的区别
  * display：none；隐藏自己，原位置不保留
  * visibility：hidden；隐藏后原位置保留
  * opacity：0；透明度为0，隐藏自己保留原位置
  * overflow：hidden；溢出部分隐藏

## 圆角和阴影













## Transform

1. 转换的作用
   * 使元素在位置或者形状上发生一定的改变
2. 属性
   * transform:;（对行内元素不生效）
3. 属性值
   * 位移
     * transform:translate(x,y);
     * 当只有一个值时，代表水平方向
     * 当有两个值时，代表水平和垂直方向
     * 单一属性值：
       * transform:translateX();
       * transform:translateY();
   * 旋转
     * transform:rotate(x==deg==);
     * 取正值顺时针旋转
     * 取负值逆时针旋转
     * 默认旋转中心为中心（宽高的一半处）
     * transform-origin:;设置旋转的中心点
       * ==旋转会旋转整个坐标轴，当位移和旋转同时存在，建议位移写在旋转之前==
   * 缩放
     * transform:scale(x,y)
       * 取值（0，1）缩小
       * 取值（1.∞）放大
       * 只取一个值，等比例缩放
       * 取两个值，代表水平和垂直方向
         * transform:scaleX();
         * transform:scaleY();
   * 倾斜 单位deg
     * transform:skew()
     * 一个值表示水平方向
     * 两个值表示水平方向和垂直方向