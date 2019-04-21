# CSS

标签（空格分隔）：前端

---

#一.核心基础
##1.基本语法
> ####< style type="text/css">< style>

##2.基本选择器
> ####①.标记选择器：e.g: p{ color:red; }(属性+值=声明)
> ####②.类别选择器: e.g: .b{ } 引用:class=""
> ####③.ID选择器： e.g: #p1{ } 引用：id=""

##3.html引入CSS
> ####①行内样式（不常用，不易维护）
> ####②嵌入式（+style）
> ####③链接式（<link href red.css> type="text/css" rel="stylesheet"）（常用）
> ####④导入式（< style> @import url(a.css)   < /style>)

##4.优先级比较
> ####行内样式&gt;链接式&gt;内嵌式&gt;导入式（链接式在后面）
> ####行内样式&gt;内嵌式&gt;导入式&gt;链接式（链接式在前面）

#二.制作小网页
##1.设置标题
* color
* background-color
* text-align
* padding
##2.设置图片
* width height
* margin:与文本边距
* float
##3.设置正文
* font-size
* line-height:1.5
* text-indent:2em(段首缩进)
##4.设置整体
* margin:0px(填充)
* background-color:#DFDFDF

#三.高级表达
##1.复合选择器
####* 交集选择器:多个属性合在一起 e.g: p.c{ }
####* 并集选择器:对多个对象进行操作 e.g: p,.c{}(逗号隔开)
####* 后代选择器:在有前提条件下使用 e.g: p span{ }(空格隔开)
####* 子选择器:对直接子类有影响，间接子类无影响 e.g: div>span(大于号)
##2.css继承性：并非所有特性都能继承，如border则不可（多用于菜单）
##3.css层叠性：行内样式&gt; Id样式&gt;类别样式&gt;标记样式

<h1>四.样式设计</h1>
<h2>1.文本</h2>
* 文字字体：font-family:"Times New Roman"Arial
* 文字倾斜：font-style:italic
* 文字加粗：font-weight:bold；style="font-weight:normal"
* 大小写转换：text-transform:capitalize(首字母)；uppercase,lowercase
* 装饰效果：text-decoration:none,underline,line-throuth(删除线)，overline(上划线)
* 字词间距：word-spacing,letter-spacing
* 设置文本水平间距：text-align（中间对齐）:justify,margin:10px,auto(第二个参数表示右)

<h2>2.图片</h2>
* 图片边框：border:1px red solid(实线)dashed（虚线）dotted（点画线）
* 不同边框：border-top||bottom||left||right
* 图片缩放：width:20%
* 图文混排
* 图片与文字对齐：style="vertical-align:baseline;"(常用)，20px(距离基线)

<h2>3.背景</h2>
* 背景图片:style="background-image:url();"
* 图片覆盖:background-repeat:no-repea||repeat-x;
* 图片位置:background-position:(百分比，px,上下左右，常用百分比)；
* 图片固定:background-attachment:fixed;

<h1>五.盒模型</h1>
##1. 基本元素：border(边框);padding(内边距);margin(外边距)
##2. 网页布局与盒模型：
* 标准文档流：元素排版布局过程中，元素会默认自动从左往右，从上往下的流式排列方式。并最终窗体自上而下分成一行行，并在每行中从左至右的顺序排放元素。
* 块级元素和行内元素：
> ####块级元素：跟同级兄弟块一起竖直排列，依次撑满  
> ####行内元素：以普通节点展示，跟同级兄弟块横向排列，排满后，自动换行
##3.盒子在标准流中的定位
* 行内元素之间水平margin：右加左
* 块级元素之间竖直margin:大为参考
* 嵌套盒子之间：子块以父块内容为参考
* margin属性可以为负
##4.盒子浮动与定位
* 浮动：float:left,right;
* 浮动清除：clear:left,right,both,none(允许有浮动)
* 定位：static(以标准流为基准),relative(相对定位：相对于原来的基准),absolute(绝对定位：以包含框为基准),fixed(固定定位：以浏览器窗口为基准)
* ***z-index:常用于文字悬浮图片上 z-index:-1;***
##5.盒子display属性
* inline:元素变成内联元素(div变span)
* block:元素变成块级元素（span变div）

<h1>六.设置表格样式</h1>
<h2>1.边框</h2>
* border-spacing(单元格距离)；
* border-collapse边框分离，合并，默认分离（较粗）(collapse||separate)

<h2>2.宽度</h2>
> table-layout:fixed(默认auto)

<h2>3.列样式</h2>
> th+td选择器

<h2>鼠标经过时行变色效果</h2>
> ####tbody th:hover{background-color:aqua} 

<h1>七.设置超链接样式</h1>
<h2>1.伪链接</h2>
* **a:link(用户未访问时状态)**
* **a:visited(用户已访问时状态)**
* **a:hover**

<h2>2.按钮式</h2>
> 加边框 背景色

<h1>八.设置列表样式</h1>
<h2>1.列表符号</h2>
> list-style-type:形状名称

<h2>2.列表图标</h2>
> list-style-image:url("");

<h3>3.制作导航菜单</h3>
