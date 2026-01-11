## JaveScript

1.操作浏览器的能力

2.广泛的使用领域

![image-20251224212454567](.\img\image-20251224212454567.png)

ECMAScript和javascript的关系是，前者是后者的规格，后者是前者的一种实现，在日常场合，这两个词可以互换的

ES62015出新

## 1.标识符

用来识别各种值的合法名称，最常见的标识符就是变量名，由字母、美元符号、下划线和数字组成，其中数字不能开头

## 2.变量和常量

定义变量的：var let 区别在var声明的变量具有函数作用域 let声明的变量具有块级作用域

var num =10;

变量本质（固定空间）-停车位

变量名（通过名字操作空间） -车位编号

数据（变化的量） -车

##### 变量的重新赋值

##### 变量提升

js引擎的工作方式是，先解析代码，获取所有被声明的变量，然后再一行一行的运行，这造成的结果，就是所有变量的声明语句，都会被提升到代码的头部，这就叫做变量提升（hoisting）

console.log(num);

var num =10;       

执行： var num;  //undefined

console.log(num);

num=10;

##### 常量

使用const定义常量后，常量无法改变（ES6新特性）

const URL =“http://itbaizhan.cn”;

URL =    //错误 

当需要条件判断时，这个值被当作是true还是false，当作true的值归类未truthy，当作false的值归类未falsy

falsy：false  Nullish（null，underfiend）  0，On，NaN.'',"",``

truthy：“false”，“0”，[],{}

### 对象类型

1.function 函数名（参数）{//函数体  return 结果；}

没有定义 undefined，undefined做数学运算结果就是NaN

2.匿名函数

（function（参数）{//函数体 return 结果；}）

（function（参数）{//函数体 return 结果；}）

使用情况：（参数） 调用一次或者

作为其他对象的方法，

3.箭头函数

（参数） =>{//函数体  return结果；}

如果只有一个参数，（）可以省略

如果函数体内只有一行代码，{}可以省略

#### 函数是对象

1.可以参与赋值

2.有属性、有方法

console.dir() 查看函数/prototype scopes

3.可以作为方法参数

```js
function a(){
    console.log('a')
}
function b(fn){   //fn将来可以是一个函数对象   高阶函数 
    console.log('b')
    fn();    //调用函数对象
}
b(a)
```

4.可以作为方法返回值

### 函数作用域

以函数为分界线划定作用域，所有函数之外是全局作用域

查找变量时，由内向外查找，

在内层作用域找到变量，就会停止查找，不会再找外层

所有作用域都找不到变量，报错

作用域本质上是函数对象的属性，可以通过console.dir来查看

### 闭包

```js
var =10；
function a(){
    var y =20;
    function b(){
        console.log(x,y);
    }
    return b;
}
a()()  //在外面执行了b
```

函数定义时，它的作用域已经确定好了，因此无论函数将来去了哪，都能从它的作用域中找到当时那些变量

别被概念忽悠了，闭包就是指**函数能够访问自己的作用域中变量**  java中lamda的参数捕获

![image-20260107213153232](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20260107213153232.png)

### map、filter、forEach

```js
let arr=[1,2,3,6];
function a(i){ //代表新旧元素之间的变换格则
  return i*10
}
//arr.map(a) //具名函数，结果[10,20,30,60]
//arr.map((i)=>{return i*10});
arr.map(i =>i*10); //箭头函数
```

传给map的函数，参数代表旧元素，返回值代表新元素

map的内部实现（伪代码）

```js
function map(){ //参数是一个函数
    let narr=[];
    for(let i =0;i < arr.length;i++){
        let o=arr[i];//旧元素
        let n=a(o);//新元素
        narr.push(n);
    }
    return narr;
}
```

filter

```js
let arr=[1,2,3,6];
arr.filter((i) => i%2 ==1);//结果[1,3]
```

传给filter的函数，参数代表旧元素，返回true表示要留下的元素

forEach例子

```js
let arr =[1,2,3,6];
for(let i =0;i <arr.length;i++){
    console.log(arr[i]);
}
arr.forEach((i) =>console.log(i));
```

高阶函数：map、filter、forEach

回调函数，例如作为参数传入的函数

### object

语法

```js
let obj= {
    属性名：值，
    方法名：函数，
    get 属性名（）{}，
    set 属性名（新值）{}
}
```

### 特色：原型继承

```js
let father={
    f1:'父属性',
    m1:function(){
        console.log("父方法");
    }
}
let son =object.create(father);
console.log(son.f1); //打印 父属性
son.ml();   //打印 父方法
```

father 是父对象，son去调用.m1或.f1时，自身对象没有，就到父对象找

son自己可以添加自己的属性和方法

son里有特殊属性 _proto_ 代表它的父对象，js术语：son的原型对象

不同浏览器对打印son的_proto_ 属性时显示不同

 edge打印console.dir(son) 显示[[prototype]]

firefox 打印console.dir（son）显示<prototype>

### 特色：基于函数的原型继承

出于方便，js又提供了一种基于函数的原型继承

函数职责

1.负责创建子对象，给子对象提供属性、方法，功能上相当于构造方法

2。函数有个特殊的属性prototype，它是函数创建的子对象的父对象

注意：名字有差异，这个属性的作用就是为新对象提供原型

```js
function cons(f2){
    //创建子对象（this），给子对象提供属性和方法
    this.f2=f2;
    this.m2=function(){
        console.log("子方法");
    }
}
//cons.prototype 就是父对象
cons.prototype.f1="父对象";
cons.prototype.m1=function(){
    console.log("父方法");
}
```

配合new关键字，创建子对象

```js
let son =new cons("子属性")
```

子对象的__proto__ 就是函数的prototype属性

### json和js的区别

1.本质不同：json对象本质上是个字符串，它的职责是作为客户端和服务器之间传递数据的一种格式，它的属性只是样子货。而js对象是切切实实的对象，可以有属性方法

2.语法细节不同：json中只能有null、布尔、数字、字符串（只有双引号）、对象、数组

json中不能有除以上的其他js对象的特性，如方法等。json中属性必须用双引号引起来

**json字符串与js对象的转换**

```js
JSON.parse(json字符串); //返回js对象
JSON.stringify(js对象); //返回json字符串
```

### 动态类型

静态类型语言，java，值有类型，变量也有类型、赋值给变量时，类型要相符

```java
int a =10;
String b ="aabc";
int c ="abc";//错误
```

而js属于动态类型语言，值有类型，但变量没有类型，赋值给变量时，没有要求

```js
let a =200;
let b =100;
b ='abc';
b=true;
```

动态类型看起来比较灵活，但变量没有类型，会给后期维护带来困难



## 3.js引入到html文件中

##### 嵌入到html文件中（内联脚本）

```js
<body>

      <script>
          var age =20;
           console.log(age);
      </script>
</body>

```

##### 引入本地独立JS文件（外部脚本)

```
<body> <script type="text/" src="> </body>"
```

##### 引入网络来源文件

jquery cdn

CDN：网络加速资源

## 4.数据类型分类

js语言的每一个值，都属于某一种数据类型，js的数据类型，共有6种，（ES6又新增了Symbol类型的值和BigInt类型，本课程暂不涉及）数值、字符串、布尔值、对象、null和undefined

数据类型分类：

原始类型（基础类型）：数值字符串布尔   合成类型（复合类型）:对象

狭义对象：键值对的集合

广义对象：在javascript中，一切皆对象

**undefined和null的区别：**

 **类型不同：**undefined是一个类型，表示变量未定义，null是一个对象，表示空对象指针

**使用场景不同：**undefined通常用于变量声明但未赋值的情况，null通常用于显式的表示“空‘或”无值“的情况

**赋值方式不同：**undefined是JavaScript引擎自动赋予未初始化变量的值，null是开发者可以显示赋予变量的值

**比较不同：**undefined == null返回true，因为他们都表示”空值“，undefined === null 返回false，因为类型不同

首先undefined和null都是基本数据类型，这两个基本数据类型分别都只有一个值，就是undefined和null。

undefined代表的含义就是未定义，null代表的含义是空对象，一般变量声明了但还没有定义的时候会返回undefined，null主要用于赋值给一些可能会返回对象的变量，作为初始化。

## 5.typeof运算符

确定数据类型：typeof instanceof、object.prototype.toString.call 、 Array.isArray

当对null和undefined这两种类型使用typeof进行判断，null返回object，这是

## 6.算数运算符

加 减 乘 除 余 自增、自减运算符

加法：1.数值相加 2.非数值相加 true+true //2  true是1 false是0  

3.比较特殊是，如果两个字符串相加，这时加法运算符会变成连接运算符，返回一个新的字符串，将两个原字符串连接在一起。如果一个运算子是字符串，另一个运算子是非字符串，这时非字符串会转成字符串，再连接再一起。

余数运算符：%

自增和自减运算符：放在变量之后，会先返回变量操作前的值，再进行自增/自减操作；放在变量之前，先进行自增/自减操作，再返回变量操作后的值。

## 7.赋值运算符

=  赋值运算符

x += y 相对于 x= x+y

x -=y 相对应 x = x-y

x ×=y 相当于 x = x*y

 x /=y 相当于 x= x/y

x %=y 相当于 x = x%y

## 8.比较运算符

比较运算符用于比较两个值的大小，然后返回一个布尔值，表示是否满足指定的条件

![image-20251228190227978](.\img\image-20251228190227978.png)

“==”和“===”的区别：

双等比较“值”，而三等比较“值”和“类型”

## 9.布尔运算符

**取反运算符 ：！**

对于非布尔值，取反运算符会将其转为布尔值，以下六个值取反为true，其他值均为false：underfined null false 0 NaN 空字符串（“”）

且运算符：&&

或运算符：||

## 10.类型转换

#### 1.自动转换

遇到以下两种情况时，JavaScript会自动转换数据类型，即转换是自动完成的，用户不可见

1.不同类型的数据互相运算

2.对非布尔值类型的数据求布尔值

#### 2.强制转换-Number

强制转换主要指使用Number、string和boolean三个函数，手动将各类的值，分布转换为数字、字符串或布尔值

使用Number函数，可以将任意类型的值转为数值。

使用string函数，可以将任意类型的值转为字符串。

使用boolean函数，可以将任意类型的值转为布尔值。

## 11.条件语句

#### -if语句

if

if.. else

if..else if...else if

if..if(){ } else...else

#### switch语句

```js
switch(day){
    case 1:
        console.log("星期一")；
        break;
    case 2:
        console.log("星期二")；
        break；
    case 3:
        console.log("星期三")；
        break；
    default：
        console.log("输入错误");
        break;
}
```

## 12.三元运算符

（条件）？表达式1：表达式2

## 13.循环语句

#### for语句

for（初始化表达式；条件；迭代因子）{

​          语句

}；

#### while语句

while（条件）{

​        语句；

}

## 14.break 和continue

break语句用于跳出代码块或循环

continue语句用于立即终止本轮循环，返回循环结构的头部，开始下一轮循环

![image-20251228201450882](.\img\image-20251228201450882.png)

## 15.字符串

字符串默认只能写在一行内，分成多行将会报错

如果长字符串必须分成多行，可以在每一行的尾部使用反斜杠

#### 转义

反斜杠\在字符串内用来表示一些特殊字符，所以又称为转义符

![image-20251228202033498](.\img\image-20251228202033498.png)

#### length属性

返回字符串的长度，空格也包括

#### 字符串常用方法

##### concat（）方法

用于连接两个字符串，返回一个新字符串，不改变原字符串

##### slice（）

用于从原字符串取出子字符串并返回，不改变原字符串，第一个参数是子字符串的开始位置，第二个参数是子字符串的结束位置（不含该位置）

##### substring（）

用于从原字符串取出子字符串并返回，与slice方法相似，

##### indexOf（）

用于确定一个字符串在另一个字符串中第一次出现的位置，返回结果是匹配开始的位置，如果返回-1，就表示不匹配

##### trim（）

用于去除字符串两端的空格，返回一个新字符串，不改变原字符串

##### replace（）

用于替换匹配的子字符串

##### split（）

按照给定规则分割字符串，返回一个由分割出来的子字符串组成的数组

## 数组

array是按次序排列的一组值，每个值的位置都有编号（从0开始），整个数组用方括号表示

两端的方括号是数组的标志，sxt是0号位置，

var arr = ['sxt','baizhan','it']；

任何类型的数组，都可以放入数组

#### 数组常用方法

##### Array.isArray()

返回一个布尔值，表示参数是否为数组 ，可以弥补’typeof‘运算符的不足

##### push（）/pop（）

push用于在数组的末端添加一个或多个元素，并返回添加新元素后的数组长度，注意该方法会改变原数组

pop用于删除数组的最后一个元素，并返回该元素，会改变原数组

##### join（）

以指定参数作为分隔符，将所有数组成员连接为一个字符串返回，如果不提供参数，默认用逗号分割

##### concat（）

用于多个数组的合并，将新数组的成员，添加到原数组成员的后部，然后返回一个新数组，原数组不变。

##### slice（）

用于提取目标数组的一部分，返回一个新数组，原数组不变，第一个参数是起始位置（从0开始），第二参数为终止位置（但该位置的元素本身不包括在内），如果省略第二个参数，则一直返回到原数组的最后一个成员

## 函数

函数是一段可以反复调用的代码块

函数声明：function命令声明的代码区块，就是一个函数，function命令后面是函数名，函数名后是一对圆括号，里面传入函数的参数，函数体放在大括号里面

function print（s）{

​       console.log(s);

}

除了用function命令声明函数，还可以采用变量赋值的写法，不推荐

var print = function（s）{

​     console.log(s);

}

## 数组去重

## DOM概述

DOM是JavaScript操作网页的接口，全称为文档对象模型（document object model），作用是将网页转为一个JavaScript对象，从而可以用脚本进行各种操作（比如对元素增删内容）

浏览器会根据DOM模型，将结构化文档html解析为一系列的节点，再有这些节点组成一个树状结构（DOM Tree），所有的节点和最终的树状结构都有规范的对外接口

DOM的最小组成单位叫做节点（node），文档的树形结构（DOM树），就是由各种不同类型的节点组成，每个节点可以看作是文档树的一片叶子

节点的类型有七：

document：整个文档树的顶层节点

documentType：doctype标签

element：网页的各种html标签

attribute：网页元素的属性（如class=“right”）

text:标签之间或标签包含的文本

comment：注释

documentfragment：文档的片段

### document对象 方法/获取元素

getelementsbytagname

getelementsbyclassname

getelementsbyname

getelementbyid

queryselector

queryselectorall

### Element对象

 element对象对应网页的html元素，每一个html元素，在dom树上都会转化为一个element节点对象

element对象_属性：

id 

classname

classlist（add/remove）

innerhtml innerText区别：innerText和innerHTML类似，但是innerText无法识别元素，会直接渲染成字符串

### Attribute

getAttribute方法返回当前元素节点的指定属性，如果指定属性不存在，则返回null

setAttribute方法用于当前元素节点新增属性，如果同名属性已存在，则相当于编辑已存在的属性

hasAttribute方法返回一个布尔值，表示当前元素节点是否包含指定属性

removeAttribute用于从当前元素节点移除属性

## Node

textContent 属性返回当前节点和它的所有后代节点的文本内容

appendChild方法接受一个节点对象作为参数，将其作为最后一个子节点，插入当前节点，该方法的返回值就是插入文档的子节点。

## CSS操作

操作css样式最简单的方法，就是使用网页元素节点的setAttribute方法直接操作网页元素的style属性

元素节点的style属性

cssText属性

## 事件处理程序

1.HTML事件

2.DOM0级事件处理

3.DOM2级事件处理

## 事件类型

常见的事件类型:鼠标事件、键盘事件、表单事件、Touch事件等

鼠标事件：

click：按下鼠标时触发

mousedown：按下鼠标键时触发

mouseup：释放按下的鼠标键时触发

mousemove：当鼠标在节点内部移动时触发，当鼠标持续移动时，该事件会连触发

mouseover：鼠标进入一个节点时触发

mouseout：鼠标离开一个节点时触发

键盘事件：

keydown：按下键盘时触发

keypress：按下有值的键时触发，即按下Ctrl、Alt、Shift、Mate这样的无值的键，这个事件不会触发，对于有值的键，按下时先触发keydown事件，再触发这个事件。 keycode=13 回车

keyup：松开键盘时触发该事件

表单事件：在使用表单元素及输入框元素可以监听的一系列事件

input事件

select事件

change事件

touch事件：触摸引发的事件，模拟器

只能用DOM2级事件绑定方式

touchstart：用户开始触摸时触发，它的target属性返回发生触摸的元素节点

touchend：用户不再接触触摸屏时触发

touchmove：用户移动触摸点时触发

## 事件补充-1

事件是文档或浏览器窗口中发生的特定瞬间，例如用户的点击、键盘的按下、页面的加载等。常见的事件：

onClick   点击事件

onMouseOver  鼠标经过

onMouseOut 鼠标移出

onChange  文本内容改变事件

onSelect  文本框选中

onFocus  光标聚集

onBlur 移开光标

## 事件绑定

js绑定事件的方法有三种：1.html属性 2.dom属性 3.addEventlistener方法

## DOM

在web开发中，DOM通常与js一起使用，当网页被加载时，浏览器会创建页面的文档对象模型，也就是DOM（document object model）。每一个HTML或xml文档都可以被视为一个文档树，文档树是整个文档的层次结构表示。

文档节点就是整个文档树的根节点。

DOM为这个文档树提供了一个编程接口，开发者可以使用JavaScript来操作这个树状结构

![image-20260101210753721](.\img\image-20260101210753721.png)

DOM对象常用方法：

appendChild（） 把新的子节点添加到指定节点

removeChild（）删除子节点

replaceChild（）替换子节点

insertBefore（）在指定的子节点前面插入新的子节点

createAttribute（） 创建属性节点

createElement（）创建元素节点

createTextNode（）创建文本节点

getAttribute（）返回指定的属性值

## 事件代理

由于事件会在冒泡阶段向上传播到父节点，因此可以把子节点的监听函数定义在父节点上，由父节点的监听函数统一处理多个子元素的事件，这种方法叫做事件的代理（delegation）

## 原型原型链

对应名称

prototype：原型

_proto_:原型链（链接点）

从属关系

prototype：函数的一个属性：对象{}

__proto__:对象object的一个属性：对象{}

对象的—proto—保存着该对象的构造函数的prototype

## 响应式布局实现方式

主流方式：

1.通过rem、vm/vh等单位，实现在不同设备上显示相同比例进而实现适配

2.响应式布局，通过媒体查询@media实现一套HTML配合多套css实现适配

![image-20260101225235008](.\img\image-20260101225235008.png)

![image-20260101225447833](.\img\image-20260101225447833.png)

## flex弹性盒子

采用flex布局的元素，称为flex容器，它的所有子元素自动成为容器成员，称为flex项目（flex item）

![image-20260102125634150](.\img\image-20260102125634150.png)

flex容器属性

flex-direction

flex-wrap

flex-flow：flex-direction属性和flex-wrap属性的简写形式

justify-content

align-items

align-content：多轴线对齐方式



**flex-direction**决定主轴的方向（即项目的排列方向）

row默认值，主轴为水平方向，起点在左端（项目从左到右排列）

row-reverse 主轴为水平方向，起点在右端（项目从右往左排列）

column 主轴为垂直方向，起点在上沿（项目从上往下排列）

column-reverse 主轴为垂直方向，起点在下沿（项目从下往上排列）

**flex-wrap**默认情况下，项目都排列在一条轴线上，如果一条轴线排不下的换行方式

nowrap 不换行（列）

wrap 主轴为横向时：从上到下换行；主轴为纵向时，从左到右换列

wrap-reverse 主轴为横向时，从下到上换行；主轴为纵向时：从右到左换列

**justify-content** 定义项目在主轴上的对齐方式

flex-start默认 与主轴的起点对齐

flex-end  与主轴的终点对齐

center 与主轴的中点对齐

space-between 两端对齐主轴的起点与终点，项目之间的间隔都相等

space-around 每个项目的两侧间隔相等，项目之间的间隔比项目与边框的间隔大一倍

**align-items**定义项目在交叉轴上如何对齐

flex-start 交叉轴的起点对齐

flex-end 交叉轴的终点对齐

center 交叉轴的中点对齐

baseline 项目的第一行文字的基线对齐

stretch（默认值） 如果项目未设置高度或设为auto，项目将占满整个容器的高度
