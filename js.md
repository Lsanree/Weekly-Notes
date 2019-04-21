#js

标签（空格分隔）：  前端

---

<h1>一.基本语法</h1>
<h2>1.引入方式</h2>
> ####内部：<script></script>
> ####外部：src="a.js"

<h2>2.换行</h2>
> ####换行标签置于双引号内

<h2>3.变量</h2>
> ####javaScript是弱类型语言，统一用var定义变量

<h2>4.基本数据类型</h2>
> ####数字类型，字符串类型（双引号或单引号都可以），布尔类型，undefined类型（变量不含有值），
null（变量值置空）

<h2>5.运算符</h2>
> ####e.g:var x=10;x=='10':true;x!=='10',true;x==='10':false(类型也要相等)

<h2>6.函数</h2>
> ####function fun(param1,...){}(返回值可有可无)

<h1>二.DOM</h1>
<h2>1.处理DOM事件</h2>
> ####onclick="fun()"

<h2>2.操作DOM节点</h2>
> ####修改:getElementById().innerHTML="";容器修改
> ####    :getElementById().value="";非容器修改
```
function fun1(){
        	document.getElementById("txt").innerHTML="用户名：";
        	document.getElementById("userName").value="jack";
        }
```

> ####添加:前添加：创建节点后创建文本，节点appendChild文本，获取容器Id，insertBefore(新节点名称）
> ####，（原节点名称）
> ####     后添加：直接append子节点

```
  function fun2(){
        var para=document.createElement("p");
        var norm=document.createTextNode("...前...")
        var para2=document.createElement("p");
        var norm2=document.createTextNode("...后...")
        para.appendChild(norm);
        para2.appendChild(norm2);
        var parent=document.getElementById("parent");
        var son1=document.getElementById("son1");
        parent.insertBefore(para,son1);
        parent.append(para2);
        }
```
> ####删除：获取父节点和子节点，removeChild（）;
```
function fun3(){
        	var parent=document.getElementById("parent");
            var son1=document.getElementById("son1");
            parent.removeChild(son1);
        }
```

<h2>3.设置DOM节点样式</h2>
> ####document.getElemnetById().style.color="";(或其他属性)

<h1>三.对象</h1>
<h2>1.属性和方法</h2>
> ####动态添加属性和方法
```
function fun2(something){
      alert(something);
}
var p=new Object();
    p.name="";
    p.fun1=fun2;
    p.fun1("hello");
```
> ####动态删除属性和方法
* delete p.name;delete p.fun1;
* p.name="undefined";

<h2>2.对象构造方法</h2>
> ####对应参数需要单引号
> ####调用函数不用加括号
> ####嵌套函数直接声明，外部this关键字调用

<h2>3.字符串对象</h2>
> * **字符串对象实例化方法**：1.直接实例化，2.String构造
> * **length属性**
> * **indexof方法**：indexof("",0)
> * **replace方法**

<h2>4.日期对象</h2>
> * **日期对象实例化**：var date=new Date();
> * **年月日时分秒方法**：getFullYear,getMonth（0~11）,getDate,getHours,getMinutes,getSeconds
> * **getTime方法**：返回1970.1.1至今毫秒数
> * **getDay方法**：从Date对象返回一周中某一天（0~6）（周日为0）

<h2>5.数组</h2>
> * **遍历**：for(var i in arr)(in关键字)
> * **sort()方法**:元素排序
> * **join()方法**:元素组合成字符串，默认逗号隔开，可以换成（.）
> * **concat()方法**：合并数组元素；arr.concar(arr2);
> * **reversa()方法**：颠倒数组元素

<h1>四.函数</h1>
<h2>1.全局函数</h2>
> * **eval函数**：字符串求和

<h2>2.window对象方法和事件</h2>
> * **setTimeout**:某个时间段后显示，第一个参数为函数名，第二个参数单位为毫秒
```
 window.setTimeout("fun2()",3000);
```
> * **setInterval**:重复显示，多用于计时器
```
window.setInterval("fun1()",1000);
```
> * **open**:打开网页
```
window.open("http://www.java1234.com");
```