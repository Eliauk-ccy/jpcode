# HTML学习笔记

[TOC]
## 一、HTML基本结构

#### 1.文档类型声明
` <!DOCTYPE html>`
* 作用：告诉浏览器按当前标准解析代码
* HTML5  不区分大小写，双标记结束标签可以省略（不推荐）
* HTML4.01   严格（strict）  过渡（transitional）  框架（frameset）
* XHTML  严格的HTML，区分大小写，双标记结束标签必须写
* doctype不是标签
* DTD   等同于文档类型声明   DOCTYPE
#### 2.head

* 作用：
	- 标明作者信息、关键字、描述
	- 设置字符集、引入外部文件
	- 标题（只有标题能被用户看到）
#### 3.body
* 作用：
   body里边的所有信息都是展示给用户的
    此区域内展示HTML的所有内容
<a href="#HTML学习笔记">返回目录</a>

***
## 二、常用标签

####  1.标题标签

` <hn></hn>`
* 作用: 设置标题

* 说明：h1~h6，h1最大，h6最小，默认加粗居左 ==块级元素==
* 属性：
  - align设置内容水平对齐方式
    - left        （左对齐、默认值）
    - center   （居中对齐）
    - right         (右对齐)  

***
#### 2.图片

` <img/>`
* 作用：引入图片
* 说明：src属性必须得有，==行内元素==
* 属性：
  - src：图片路径
  - alt：图片加载失败时提示
  - title：鼠标悬停时出现的文字  

***
#### 3.超链接
` <a></a>`
* 作用：跳转到目标（地址、位置、文件等）
* 说明：==行内元素==
* 属性：
  - href：链接目标
  - target：打开方式（在哪个窗口打开）
    - _blank     （新窗口打开）
    - _self         （当前窗口打开   默认值）
* 应用：
  + 锚点定位
    + a标签到a标签
    + a标签到块级元素
    + 空标签 点击返回顶部

***
#### 4.段落标记

` <p></p>`
* 作用：标记一个段落
* 说明： ==块级元素==
* 属性：
	+ align：水平对齐方式（同上）

***
#### 5.强制换行
` <br/>`
* 作用：强制换行
* 说明：没有任何属性
#### 6.水平分割线
` <hr/>`
* 作用：在网页中添加水平分割线
* 说明：==块级元素==
* 属性：
	+ color：设置分割线的颜色
		- 关键字：red、blue、yellow...
		- rgb颜色：#000000...
	+ width：设置水平线的长度，默认单位px
	+ size：设置水平线的粗细，默认单位px
	+ align同上

***
#### 7.文本格式化标签

` <b></b>`加粗bold
` <i></i>`倾斜italic
` <u></u>`下划线underline
` <del></del><s></s>`删除线
` <em></em>`强调，倾斜显示
` <strong></strong>`强调，加粗显示
` <sup></sup>`上标
` <sub></sub>`下标
` <big></big>`大号字体
` <small></small>`小号字体

==双标记，行内元素==
<a href="#HTML学习笔记">返回目录</a>

***
## 三、列表   
==块级元素==
#### 1.无序列表

``` html
<ul>
    <li></li>
    <li></li>
    <li></li>
</ul>
```
*  效果
    * 
    * 
    * 
* 属性：
   * type：设置项目符号
     * disk 
     * circle
     * square
     * none
#### 2.有序列表

``` html
<ol>
    <li></li>
    <li></li>
    <li></li>
</0l>
```
*  效果
    1. 
    2. 
    3. 
*  属性：
   * type："1/a/A/i/I"设置序号符号
   * reversed："reversed"倒序，当属性等于属性值时，可以简写为属性
   * start="number" 设置从第几个开始
#### 3.自定义列表

``` html
    <dl>
        <dt>主题一</dt>
        <dd>描述一（多个描述）</dd>
        <dt>主题二</dt>
        <dd>描述二</dd>
    </dl>
```

*  一般用来放置图片以及相关描述
<a href="#HTML学习笔记">返回目录</a>

***
## 四、表格

```html
<table>
	<caption>表格的标题</caption>
    <tr>
        <th>特殊单元格</th>table header
        <th>替换td</th>
        <th>默认水平居中且加粗</th>
    </tr>
    <tr> 行 table row
        <td>列 单元格 table data cell</td>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td></td>
        <td></td>
        <td></td>
    </tr>
</table>
```
* 效果：
|      |      |      |
| ---- | ---- | ---- |
|      |      |      |


* 作用：向用户展示数据
* table属性：
   - border             设置边框（默认没有），像素单位px;
   - align                 水平对齐方式（表格）
   - width               宽度
   - height              高度
   - cellpadding     单元格内边距
   - cellspacing      单元格间距  
   - bgcolor            背景颜色
   - background    背景图片
   - bordercolor     边框颜色
* tr的属性
   * height 行高
   * align 行内容的水平对齐方式
   * valign   *vertical*  行内容的垂直对齐方式，取值top/middle/bottom 
* td的属性

   * width     宽度
   * height    高度
   * align       单元格内容的水平对齐方式
   * valign     单元格内容的垂直对齐方式
   * bgcolor   背景颜色
   * background背景图片
   * colspan   水平合并（跨列） 删除同一行的td
   * rowspan  垂直合并（跨行）删除下面行的td
<a href="#HTML学习笔记">返回目录</a>

***
## 五、表单

  ` <form></form>` ==块级元素==

  * 作用：采集数据，将数据提交到服务器

* 说明：不能相互嵌套，一个HTML文件可以包含多个form表单

* 属性

  * name：表单名称
  * method：提交方式，默认值get
    * get：提交数据不安全，提交的数据会在地址栏中显示；get提交的数据大小有限制（不能超过2kb）；
    * post：比较安全；提交的数据理论上没有限制；
  * action：提交的地址

* 表单元素

  * 单行文本框：  ` <input type="text"/>`
  * 密码框：          ` <input type="password"/>`
  * 单选框：          ` <input type="radio" name=""/>`
  * 多选框：          ` <input type="checkbox"/>`
  * 提交： 
       * ` <input type="submit" value="登录"/>`
       * ` <button type="submit">提交</button/>`
  * 重置：
       * `<input type="reset" value="重置">` 
       * `<button type="reset">重置</button>` 
  * 无功能按钮： 
       * `input type="button" value="无功能">`
       * `<button type="button">无功能</button>`
  * 图片提交按钮：` <input type="image" src="URL"/>`
  * 文本框：`  <textarea cols：文字区块的宽度rows：文字区块的行数，即其高度><textarea>`
  * 隐藏域：` <input type="hidden">`
  * 文件：` <input type="file" enctype="multipart/form-data">`二进制传输
  * 下拉列表：
``` html
<select>
    <optgroup label="分组名">
    <option>选项一</option>
    <option>选项二</option>
    <option>选项三</option>
</select>
```
  * label：配合单选和复选框使用，提升用户体验度（for和input的id绑定）
  * fieldset ：给表单元素分组，组名legend标签（双标签）
* 表单元素属性
  * type：表单元素类型
  * name：表单元素名称
  * value：当前值
  * checked：默认被选中，配合单选按钮和多选按钮使用
  * disabled：禁用
  * readonly：只读
  * selected：默认显示，配合option显示
  * size：显示数量，取值为number，配合selected使用
* HTML新增属性：
  * paceholder    默认提示
  * autofocus    自动获取焦点，推荐写在表单的第一个元素上
  * require     必填项
  * minlength   最小长度
  * maxlength   最大长度
  * multiple    可以输入多个 ，用","隔开，配合邮箱和网址使用
<a href="#HTML学习笔记">返回目录</a>
***
## 六、div+span
`div`
* 无语义的容器、盒子、==块级元素==

`span`

* 无语意的容器、盒子、==行内元素==
<a href="#HTML学习笔记">返回目录</a>
***
## 七、HTML新增标签

#### 1.语义化标签

* 正确的标签做相关的事情
* 示例：
  * 
#### 2.视频
` video`
* 作用：在网页中插入视频
* ==行内元素==，支持的视频格式：mp4 ogg  webM（高清）
* 属性：
  * src：视频地址，必须属性
  * width：宽度
  * height：高度
  * autoplay：自动播放
  * controls：显示控制面板
  * loop：循环播放
  * poster：视频播放前显示一张图片
  * muted：静音
***
#### 4.音频
` audio`
* 作用：在网页中插入音频
* ==行内元素==支持的格式有 mp3 ogg wav
* 属性：
  * src：路径  必须属性
  * auto：自动播放
  *  loop：循环播放
  * controls：控制面板
  * muted：静音
#### 3.资源
` source`
* 作用：给浏览器提供多个不同格式视频或者音频的选择

<a href="#HTML学习笔记">返回目录</a>