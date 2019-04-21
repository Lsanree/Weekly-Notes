# HTML NOTES


---

#一.设置文本
##1.基本结构
> < html>< head>< title>< body>

##2.文本排版
> < p>段落标签< p/>
> < br/>换行标签
> < blockquote> 文字段落缩进标签< blockquote/>
> < h1~h6>< h1>标题标签< h1/>(自动换行）

##3.设置文字列表
>### ①.无序
> < ul>
> < li>< li/>
> < ul/>
> ###②.有序
> < ol>
> < li>< li/>
> < ol/>

##4.标记与属性
> ###①align控制段落水平位置
> < p align="center"> < p/>
> ###②bgcolor控制背景色
> < p bgcolor="red||bgcolor="(十六进制表示RGB)"> < p/>
> ###③文字特殊样式
> < b>粗体</b>
< i>斜体< /i>
< u>下划线< /u>
< s>下删除< /s>
< big>放大< /big>
< small>缩小< /small>
< strong>强调< /strong>
< em>斜体强调< /em>
< address>邮件地址< /address>
< code>代码< /code>
> ###④字体颜色大小font标签
< font color="green" size="15" face="宋体">宋体< /font>

##5.特殊文字符号
> &lt;特殊文字符号&gt;(&lt &gt)
版权所有&copy;(&copy)
2<sup>3</sup>;(上标)
2<sub>3</sub>;(下标)

#二.设置图像
##1.相对路径vs绝对路径
###①相对路径
> < img src="相对路径"/>
> < img src="../同级路径">
###②绝对路径
> < img src="绝对路径">
##2.设置图片尺寸
> < img width="100" height="200" src="路径"/>
##3.用alt属性为图像设置替换文本
> < img alt="" src="">
##4.用title属性为图像设置标题
> < img title="" src="">

#三.设置超链接
##1.基本文字超链接
> < a href="路径">名称</a>
##2.图片超链接
> < a href="路径">< img src=""/></a>
##3.新窗口显示链接页面
> < a href="路径" target="_blank">名字或图片</a>
##4.电子邮件链接
< a href="mailto:邮件地址">名称</a>
##5.框架之间链接
###①上下左右嵌套切分窗口并插入网页
> < frameset cols="30%,*">
< frame src="a.html">
< frameset row="50%,*">
< frame src="b.html">
< frame src="c.html">
< /frameset>
< /frameset>
###②框架间链接
> > < frameset cols="30%,*">
< frame src="a.html">
< frame name="">
< /frameset>
##6.嵌入式框架iframe
> < iframe src="">< /iframe>

#四.创建表格
##1.表格基本结构
###①.建表
<table>
       <tr>
           <th>monday</th>
           <th>tuesday</th>
           <th>wednesday</th>
       </tr>
       <tr>
           <td>1-1</td>
           <td>1-2</td>
           <td>1-3</td>
       </tr>
       <tr>
           <td>2-1</td>
           <td>2-2</td>
           <td>2=3</td>
       </tr>
           <td>3-1</td>
           <td>3-2</td>
           <td>3-3</td>
       <tr>
       </tr>
</table>
###②设置边框
> ####< table border="1">

##2.合并单元格
###①行和并
> ####< td corspan="2">1-1-2(1.2列合并)< /td>
###②列合并
> ####< td rowspan="2">2-3-3(1.2行合并)< /td>

##3.align属性设置对齐方式
##4.bgcolor属性设置表格背景色和边框颜色 
##5.设置边距
> #### cellspadding

#七.块
##1.大容器
> ####< div>< /div>自动换行

##2.小容器
> ####< span>< /span>不换行