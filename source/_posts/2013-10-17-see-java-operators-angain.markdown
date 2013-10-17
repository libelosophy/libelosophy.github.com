---
layout: post
title: "再看Java操作符"
date: 2013-10-17 09:20
comments: true
categories: java 
---

刚开始学java的时候，我看的《java 语言的艺术与科学--计算机科学导论》，后来我开始看Oracel的《The Java turorials》,觉得这个讲得很清楚，当时我觉得看这个就很好，虽然也在这个教程里面看见了 The Java Language Specification》，也觉得这东西肯定很精确，不过没有进去看，主要是时间问题，当时觉得专注一点比较好。不过Turorials 确实比较浅一点，毕竟只是教程而已，教程只是教会你怎么使用--即ＨＯＷ，而如果你想理解的精确（如ＷＨＹ），就必须看其他的，甚至应该了解底层。
在看书或者文档之前，也许我要搞清楚这书（或者其他文档/资料）到底是定位，比如仅仅只是教程，又比如是精确的定义，又或者是其他教程加上个人理解。拿android来说，开发者页面有几个选项卡，		
+ Training  
+ API Guide  
+ Reference  
其中 trianing 会告诉你如何开始写安卓应用，但是点到即止。而API Guide 则对每个类和接口提供了详细说明，还包括了一些重要概念的说明与解释。 至于Reference 则是参考手册了，javadoc，针对代码
而写的注释。


好吧，开始正题。


再说操作符之前先看看java语言的数据类型。
###java数据类型：  

#### 1. 原始数据类型
+ boolean 类型
+ 数值类型（ numeric types）
	+ 整数类型 （integer types）
		+ byte
		+ char
		+ short
		+ int
		+ long
	+ 浮点类型 （floating -point types）
		+ float
		+ double

#### 2. 引用数据类型
+ array 
+ Object
 </br>
#### 3. null 类型
空类型没有名字，可视为常量。

****************************************************
</br></br>

Java 为原始数据类型值定义了操作符（为 引用数据类型 String 定义了连接操作符 “+” ）。操作符是什么东西，不过是一个符号表示，人来定义其意义，加上具体实现即可。看操作符根据类型来看最好，    

### 操作符
####1. 针对boolean 类型的操作符有：

+. 关系运算符 （==）  和 （！=）
+. 逻辑补 （!）
+. 逻辑与(&)，逻辑异或（^）， 逻辑或（|）
+. 条件与（&&）, 条件或（||） 
+. 三目条件运算符 （ ？ ：）
+. 字符串连接运算符 （+） {连接字符串时，将boolean值装换为 true / false 的字符串}


####2. 针对整数类型的操作符 Numeric 之 Integer Operations       
   
+ 比较操作符
	- < , <= , > , >=
	- == ， ！=

+ 数学运算（结果为 int 或 long）  
	- 一元正/负操作符: +  ,  -
	- 乘/除/取余： * , / , %
	- 加/减：+ ， -
	- 自增/自减 ： ++ ， --
	- 带符号左移/带符号右移/无符号右移： << , >> , >>>
	- 位补（bitwise complement）: ~
	- 整型位操作符： & ， ^ , |
+ 条件运算符
	- ？ ：
+ 强制类型转换
	由一种整型转换到其他整型
+ 字符串连接操作符 
	+ 十进制值型字符串 如 "value:" + 0x80 >>>> value:128

其中需要注意的有：   

+ 移位运算符：
	+ n << s  =  n * power(2,s)  （2的s 次方）
	+ ｎ >> s  =  n / power(2,s)   
	+ n  >>> s    (其中 2<<-s)是为了去掉符号位
		+ n为正数 ：n >>> s  = ( n >> s )
		+ n 为 int 型负数 ： n >>> s = (n >> s) + (2<<-s)  = (n >>s) + (2>>(31-s))
		+ n 为 long 型负数： n >>> s = (n >> s) + (2<<-s)  = (n>>s) + (2<<(63-s))


按位运算符 -- ～， & ， ^, |  

字符串连接：字符串连接输出的是十进制值字符串





#### 浮点数操作符
##### 浮点数
Java 中的浮点数有两种，1. IEEE 754 单精度浮点数， 2. IEEE 754 双精度浮点数。
IEEE 浮点数的值有， 正负无穷， 有限数，正负零，NaN(Not-a number value), 除了NaN， IEEE浮点数是有序的，从最小的到最大的，   
负无穷 》》 有限负数 》》 正负零 》》 有限负数 》》 负无穷

其中有限非零值都可以表示为： s * m * 2^(e-N+1)
其中：
s为 +1/-1 
m < 2^N
e 位于Emax 和 Emin 之间 ， Emin = -( 2^(K-1)- 2 )  Emax= 2^(K-1)-1 
K , N 取决与浮点数属于那个浮点数集合。

下面这张表说明了单精度浮点数和双精度浮点数的K N 取值

<table border="1"  cellpadding="10"  width="400">
<caption>浮点数 K N 取值</caption>
<tr>
	<th><b>row</b>     </th>
	<th><b>float</b>   </th>
	<th><b>double</b>  </th>
</tr>
<tr>
	<td>N</td>
	<td>24</td>
	<td>53</td>
</tr>
<tr>
	<td>K</td>
	<td>8</td>
	<td>11</td>
</tr>
<tr>
	<td>Emin</td>
	<td>-127</td>
	<td>-1022</td>
</tr>
<tr>
	<td>Emax</td>
	<td>126</td>
	<td>1023</td>
</tr>
</table>
</br>
######其他说明：
+ 零： 0.0>-0.0  = false  ;  0.0 == -0.0 = true  ; 1.0/0.0 = 正无穷； 1.0/-0.0 = 负无穷		
+ NaN： <, <=, >, >= ， ==  有一个操作数为ＮａＮ则结果为false,    但是 ！= 有一个操作数为NaN，则值为true


##### 针对浮点数的操作符
+, -正负
+, -, *, /, %
++, --

==, >, >=, <, <=, !=
? : 

字符串连接

强制类型转换。


#### 操作符优先级
<table border="1" cellpadding="8" summary="This table lists operators according to precedence order" width="150%">
<caption id="nutsandbolts-precedence"><strong>Operator Precedence</strong></caption>
<tr>
<th id="h1">Operators</th>
<th id="h2">Precedence</th>
</tr>
<tr>
<td headers="h1">postfix</td>
<td headers="h2"><code><em>expr</em>++ <em>expr</em>--</code></td>
</tr>
<tr>
<td headers="h1">unary</td>
<td headers="h2"><code>++<em>expr</em> --<em>expr</em> +<em>expr</em> -<em>expr</em> ~ !</code></td>
</tr>
<tr>
<td headers="h1">multiplicative</td>
<td headers="h2"><code>* / %</code></td>
</tr>
<tr>
<td headers="h1">additive</td>
<td headers="h2"><code>+ -</code></td>
</tr>
<tr>
<td headers="h1">shift</td>
<td headers="h2"><code>&lt;&lt; &gt;&gt; &gt;&gt;&gt;</code></td>
</tr>
<tr>
<td headers="h1">relational</td>
<td headers="h2"><code>&lt; &gt; &lt;= &gt;= instanceof</code></td>
</tr>
<tr>
<td headers="h1">equality</td>
<td headers="h2"><code>== !=</code></td>
</tr>
<tr>
<td headers="h1">bitwise AND</td>
<td headers="h2"><code>&amp;</code></td>
</tr>
<tr>
<td headers="h1">bitwise exclusive OR</td>
<td headers="h2"><code>^</code></td>
</tr>
<tr>
<td headers="h1">bitwise inclusive OR</td>
<td headers="h2"><code>|</code></td>
</tr>
<tr>
<td headers="h1">logical AND</td>
<td headers="h2"><code>&amp;&amp;</code></td>
</tr>
<tr>
<td headers="h1">logical OR</td>
<td headers="h2"><code>||</code></td>
</tr>
<tr>
<td headers="h1">ternary</td>
<td headers="h2"><code>? :</code></td>
</tr>
<tr>
<td headers="h1">assignment</td>
<td headers="h2"><code>= += -= *= /= %= &amp;= ^= |= &lt;&lt;= &gt;&gt;= &gt;&gt;&gt;=</code></td>
</tr>
</table>

</br>
规律： 

+ 赋值运算符及其各种组合优先级最低
+ 一元 > 二元 > 三元 
+ 二元： 算数 > 移位 > 关系 (> Equality) > 按位运算 > 逻辑
+ 算数： 先乘除（包括余）， 后加减
+ 按位： 与 > 异或 > 或
+ 逻辑： 与 > 或

结合性： 除赋值外，都是左结合

 












