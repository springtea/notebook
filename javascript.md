# 面试题 

## == 和 === 区别

- ==， 两边值类型不同的时候，要先进行类型转换，再比较
- ===，不做类型转换，类型不同的一定不等。

==类型转换过程：

1. 如果类型不同，进行类型转换
2. 判断比较的是否是 null 或者是 undefined, 如果是, 返回 true .
3. 判断两者类型是否为 string 和 number, 如果是, 将字符串转换成 number
4. 判断其中一方是否为 boolean, 如果是, 将 boolean 转为 number 再进行判断
5. 判断其中一方是否为 object 且另一方为 string、number 或者 symbol , 如果是, 将 object 转为原始类型再进行判断

>  经典面试题：[] == ![] 为什么是true

转化步骤：

1. !运算符优先级最高，`![]`会被转为为false，因此表达式变成了：`[] == false`
2. 根据上面第(4)条规则，如果有一方是boolean，就把boolean转为number，因此表达式变成了：`[] == 0`
3. 根据上面第(5)条规则，把数组转为原始类型，调用数组的toString()方法，`[]`转为空字符串，因此表达式变成了：`'' == 0`
4. 根据上面第(3)条规则，两边数据类型为string和number，把空字符串转为0，因此表达式变成了：`0 == 0`
5. 两边数据类型相同，0==0为true





## 防抖(debounce)

> 函数的防抖和节流在我们的工作中经常会用到,在面试中也经常会出现.因此今天我们来聊聊防抖和节流

首先我们来看下面这张用竖线画成的图:

![防抖和节流](/Users/macos/study/web/es6/ es6笔记/防抖和节流.png)

这其中的每一条竖线都代表着一次函数调用(如鼠标mousemove事件,input输入事件等) 正常执行的时候,调用的频率很快.但有时,我们并不需要这么高的频率去调用这个函数.假如这是一个调用后台接口的操作,那么就容易造成网络堵塞,大大的增加服务器的压力 函数防抖的时候,每次调用事件都是在正常执行暂停后一段时间(等你歇菜了我再上) 函数节流的时候,则是每隔一定的时间间隔就触发一次(管你频率那么快,我就保持自己的节奏) 现在我们大致明白函数的防抖和节流是怎么一回事了,接下来我们就来具体的学习下它们



### 概念

在任务频繁触发的情况下,一个事件在被触发的一段时间后再执行回调,假如在这段时间内又被触发了,则重新开始计时.

### 应用场景

防抖在我们的日常生活中,也是随处可见.就比如我们平时坐电梯的时候,总是要等到没有人进来了再一小会儿的工夫,电梯门才会关上.而在项目中,防抖的应用场景也是挺多的.当我们在一个搜索框输入内容进行远程搜索的时候,往往就是在我们停下输入的一小刻时间后.前台向服务器发起了请求来获得匹配的结果.我们甚至于可以将防抖的过程,看成一个英雄在技能读条,只有技能读条结束了,技能才能扔出来.要是中途被人打断了,那么下次又要重新读条了.

### 简易版

```html
<input id="ipt1" />
```

我们先来看下没有防抖的效果:

```javascript
let ipt1 = document.querySelector('#ipt1')
ipt1.onkeydown = function(e){
    console.log(e.target.value)
}
```

再来看一下加了防抖效果的代码

```javascript
let ipt1 = document.querySelector('#ipt1')
let timer = null
ipt1.onkeydown = function(e){
    clearTimeout(timer)
    timer = setTimeout(() => {
        console.log(e.target.value)
    },500)
}

```

大家可以将代码copy到编辑器中运行一下看看效果,是不是加了防抖效果的用户体验会更好

### 函数版

```javascript
<div id="div1"></div>

#div1 {
  height: 300px;
  background-color: orange;
  overflow: auto;
}

let div1 = document.querySelector('#div1')
function move(e){
  this.innerText = `${e.offsetX},${e.offsetY}`
}
function debounce(fn, wait){
  let timer = null
  return function(){
    let args = arguments
    clearTimeout(timer)
    timer = setTimeout(() => {
      fn.apply(this, args)
    }, wait)
  }
}
let debounceMove = debounce(move, 500)
div1.onmousemove = debounceMove

```

其中`debounce`就是我们的核心防抖函数了

# 语言基础

## 数据类型

ECMAScript有6种简单数据类型（也称为原始类型）：

+ Number
+ String
+ Boolean
+ Undefined
+ Null
+ Symbol

一种复杂数据类型：

+ Object

### typeof 操作符

对一个值使用typeof操作符会返回下列字符串之一：

+ "undefined"表示值为定义
+ "boolean"
+ "string"
+ "number"
+ "object"
+ "function"
+ "symbol"

```javascript
console.log(typeof(1)) //number
console.log(typeof('string')) //string
console.log(typeof(true)) //boolean
console.log(typeof({})) //object
console.log(typeof(function(){})) //function
console.log(typeof([1,2,3,4])) //object
console.log(typeof(undefined)) //undefined
```

严格来讲，函数在ecmascript中被认为是对象，并不代表一种数据类型。可是，函数也有自己特殊的属性，为此，就有必要通过typeof操作符来区分函数和其他对象。

### Undefined类型

undefined类只有一个值，就是undefined。当声明里变量没有初始化，就相当于给变量赋于里undefined值：

```javascript
let a
console.log(a) //undefined

//上面这个例子等同于：
let a = undefined
console.log(a)
```

包含undefined值的变量和为定义的变量是有区别的：

```javascript
let a
console.log(a) //undefined
console.log(b) //RefferenceError
```

无论声明还是未声明，typeof操作符返回的都是字符串"undefined"

```javascript
let a
console.log(typeof(a)) //undefined
console.log(typeof(b)) //undefined
```

建议在声明变量的同时进行初始化，这样，当typeof返回undefined值的时候，我们就知道这时是因为给定的变量未声明，而不是没有初始化。

undefined值是假值

### Null类型

null类型同样只有一个值，即特殊值null，null表示一个空对象指针。

```javascript
let a = null
console.log(typeof(a)) //object
```

### Boolean类型

boolean类型有两个字面值：true,false

布尔值字面量是区分大小写的，True和False不是布尔值。

Boolean()函数可以在任意类型的数据上调用，它会将一个其他类型的值转换为布尔值。

下表是不同类型与布尔值之间的转换规则：

| 数据类型  | 转换为true的值         | 转换为false的值 |
| --------- | ---------------------- | --------------- |
| Boolean   | true                   | False           |
| String    | 非空字符串             | ""（空字符串）  |
| Number    | 非零数值（包括无限值） | 0，NaN          |
| Object    | 任意对象               | Null            |
| Undefined | N/A(不存在)            | Undefined       |

### Number类型

Number类型使用IEEE754格式表示整数和浮点值。不同的数值类型相应的有不同的数值字面量格式。



#### NaN

有一个特殊的数值叫做NaN(not a number)，用于表示本来要返回数值的操作失败了。比如：用0除任意数值在其他语言中通常都会导致错误，从而中止代码执行，但在ecmascript中，0，+0或-0相除都会返回NaN。

NaN有几个独特的属性：

1. 任何涉及NaN的操作始终返回NaN
2. NaN不等于包括NaN在内的任何值

为此，ecmascript提供了isNaN()函数。该函数接收一个参数，可以是任意数据类型，然后判断这个参数是否“不是数值”。把一个值传给isNaN()后，该函数会尝试把它转换为数值。某些非数值的值也可以直接转换为数值。任何不能转换为数值的值都会导致这个函数返回true。

#### 数值转换

有三个函数可以将非数值转换为数值：`Number()`,`parseInt()`,`parseFloat()`

`Number()`: 可用于任意数据类型

`parseInt()`,`parseFloat()`:主要用于将字符串转换为数值。

Number()转换规则：

1. 布尔值，true转换为1，false转换为0
2. 数值，直接返回
3. null，返回0
4. Undefined,返回NaN
5. 字符串，应用以下规则：
   1. 如果字符串仅包含数值字符或前面带加号，减号，转换为一个十进制数值，0开头的整数会省掉前面的0（空格会被忽略）
   2. 如果字符串包含有效的十六进制格式，如“0xf"，则转换为与该十六进制对应的十进制数值
   3. 如果是空字符串，返回0
   4. 包含除上述情况之外的其他字符，返回NaN
6. 对象，调用`valueOf()`方法，并按照上述规则转换返回的值，如果转换结果是NaN，则调用toString()方法，再按照转换字符串的规则转换

```javascript
console.log(Number(12)) // 12
console.log(Number("hello world"))  // NaN
console.log(Number("22 hello world")) // NaN
console.log(Number("22")) // 22
console.log(Number(" 22   ")) //22
console.log(Number("")) // 0
console.log(Number("050")) // 50
console.log(Number("0.5")) // 0.5
console.log(Number("0x45 hello world")) // NaN
console.log(Number("0x45")) // 69
console.log(Number(true)) // 1
console.log(Number({age:1}))  // NaN
console.log(Number(undefined)) // NaN
console.log(Number(null)) //0

```

`parseInt()`:专注于字符串是否包含数值模式**。字符串最前面的空格会被忽略，从第一个非空字符开始转换。如果第一个字符不是数值字符，加号或者减号，`parseInt（）`立即返回NaN。**这意味着空字符串也会返回NaN。如果第一个字符是数值字符，加号或者减号，则一次检测每个字符，知道字符串末尾，或碰到非数值字符。

```javascript
console.log(parseInt(12)) // 12
console.log(parseInt("hello world"))  // NaN
console.log(parseInt("22 hello world")) // 22
console.log(parseInt("22")) // 22
console.log(parseInt(" 22   ")) // 22
console.log(parseInt("")) // NaN
console.log(parseInt("050")) // 50
console.log(parseInt("0.5")) // 0
console.log(parseInt("0x45 hello world")) // 69
console.log(parseInt("0x45")) // 69

// parseInt()通常用于转换字符串，所以下面的用法不常用
console.log(parseInt(true)) // NaN
console.log(parseInt({age:1}))  // NaN
console.log(parseInt(undefined)) // NaN
console.log(parseInt(null)) // NaN
```

`parseInt()`接收第二个参数，用于指定进制数。

```javascript
console.log(parseInt("100",2)) // 4
console.log(parseInt("100",8)) // 64
console.log(parseInt("100",10)) // 100
console.log(parseInt("100",16)) // 256
```

## 操作符

### 一元操作符

只操作一个值的操作符称为一元操作符

#### 递增递减操作符

```javascript
let num1 = 1
let num2 = 2
let num3 = ++num1 + num2
let num4 = num1++ + num2
console.log(num3) // 4
console.log(num4) // 4
```

`a++`,`a--`,`--a`,`a--`这四个操作符可以作用于任何值：

将会使用Number（）转换为数值再应用改变

```javascript
let num1 = 2
let str1 = "2"
let str2 = "2hello"
let str3 = ""
let str4 = "0x33"
let bool1 = true
let bool2 = false
let n = null
let u = undefined
let obj = {age:18}
console.log(--num1) // 1
console.log(--str1) // 1
console.log(--str2) // NaN
console.log(--str3) // -1
console.log(--str4) // 50
console.log(--bool1) // 0
console.log(--bool2) //-1
console.log(--n) // -1
console.log(--u) // NaN
console.log(--obj) // NaN
```

#### 一元加和一元减

对数值使用一元加相当于对数值使用`Number()`,一元减是在一元加的基础上在前方添加一个减号

```javascript
let num1 = 2
let str1 = "2"
let str2 = "2hello"
let str3 = ""
let str4 = "0x33"
let bool1 = true
let bool2 = false
let n = null
let u = undefined
let obj = {age:18}
console.log(+num1) // 2
console.log(+str1) // 2
console.log(+str2) // NaN
console.log(+str3) // 0
console.log(+str4) // 51
console.log(+bool1) // 1
console.log(+bool2) // 0
console.log(+n) // 0
console.log(+u) // NaN
console.log(+obj) // NaN
```

### 位操作符

### 相等操作符

#### 等于和不等于

在转换操作数的类型时，相等和不相等操作符遵循以下规则：

1. 如果任一操作数是布尔值，则将其转换为数值再进行比较
2. 如果任一操作数是字符串，另一个操作数是数值，则尝试将字符串转换为数值，在比较是否相等
3. 如果一个操作数是对象，另一个操作数不是，则调用对象的valueOf()方法取得其原始值，再根据前面的规则进行比较

在进行比较时：

1. null和undefined相等
2. null和undefined不能转换为其他类型的值再进行比较
3. 如果有任一操作数是NaN，则相等操作符返回false,不相等操作符返回true。注意：NaN不等于NaN
4. 如果两个操作数都是对象，则比较它们是不是同一个对象。如果两个操作数都指向同一个对象，则相等操作符返回true。

```javascript
console.log("" == false) // true
console.log("22" == 22) // true
console.log(null == undefined) // true
console.log("NaN" == NaN) // false
console.log(5 == NaN) // false
console.log(NaN == NaN) // false
console.log(NaN != NaN) // true
console.log(false == 0) // true
console.log(true == 1) // true
console.log(true == 2) // fasle
console.log(undefined == 0) // false
console.log(null == 0) // false
console.log("5" == 5)  // true
```

#### 全等和不全等

全等和不全等操作符与相等和不相等操作符类似，只不过它们在比较操作数时不转换操作数。

```javascript
console.log("" === false) // false
console.log("22" === 22) // false
console.log(null === undefined) // false
console.log("NaN" === NaN) // false
console.log(5 === NaN) // false
console.log(NaN === NaN) // false
console.log(NaN !== NaN) // true
console.log(false === 0) // false
console.log(true === 1) // false
console.log(true === 2) // fasle
console.log(undefined === 0) // false
console.log(null === 0) // false
console.log("5" === 5)  // false
```



# 对象，类与面向对象编程

## 理解对象

创建自定义对象的方式：

1. 通常方式是创建Object的一个新实例，然后再给它添加属性和方法

   ```javascript
   let person = new Object()
   person.name = 'Nicholas'
   person.age = 29
   person.job = "Software Engineer"
   person.sayName() = function(){
     console.log(this.name)
   }
   ```

2. 另一种更流行的方式是对象字面量

   ```javascript
   let person = {
     name:"Nicholas",
     age:29,
     job:"Software Engineer"
   }
   ```

   

### 属性的类型

属性分两种：数据属性和访问器属性

#### 数据属性

数据属性包含一个保存数据值的位置。值会从这个位置读取，也会写入到这个位置。数据属性有4个特性描述它们的行为。

+ [[Configurable]]:表示属性是否可以通过delete删除并重新定义，是否可以修改它的特性，以及是否可以把它改为访问器属性。默认情况下，所有直接定义在对象上的属性的这个特性都是true。
+ [[Enumberable]]：表示属性是否可以通过for-in循环返回。默认情况下，所有直接定义在对象上的属性的这个特性都是true。
+ [[Writable]]：表示属性的值是否可以被修改。默认情况下，所有直接定义在对象上的属性的这个特性都是true。
+ [[Value]]：包含属性实际的值。这个特性的默认值是undefined。



要修改属性的默认特性，就必须使用`Object.defineProperty()`方法。这个方法接收3个参数：

1. 要给其添加属性的对象
2. 属性的名称
3. 描述符对象。对象上的属性可以包含：configurable,enumerable,writable,value

```javascript
let person = {}
Object.defineProperty(person,"name",{
  writable:false,
  value:"Nicholas"
})
console.log(person.name)//Nicholas
person.name = "Greg"
console.log(person.name)//Nicholas

Object.defineProperty(person,"age",{
    configurable:false,
    value:19
})
console.log(person.age)//19
delete person.age
//configurable设置为false,意味着这个属性不能从对象上删除。
//非严格模式下对这个属性调用delete没有效果，严格模式下会抛出错误。
//此外，一个属性被定义为不可配置之后，就不能再变回可配置的了。
//再次调用Object.defineProperty()并修改任何非writable属性会导致错误。
//因此，虽然可以对同一个属性多次调用Object.defineProperty(),但在把configurable设置为false之后就会受到限制了
console.log(person.age)//19
```

在调用`Object.defineProperty()`时，configurable，enumerable和writable的值如果不指定，则都默认为false。

#### 访问器属性

访问器属性不包含数据值。相反，它们包含一个获取函数和一个设置函数，不过这两个函数不是必需的。在读取访问器属性时，会调用获取函数，这个函数的责任就是返回一个有效的值。在写入访问器属性时，会调用设置函数并传入新值，这个函数必需决定对数据做出什么修改。访问器属性有4个特性描述它们的行为。

+ [[Configurable]]：表示属性是否可以通过delete删除并重新定义，是否可以修改它的特性，以及是否可以把它改为数据属性。默认情况下，所有直接定义在对象上的属性的这个特性都是true。
+ [[Enumerable]]：表示属性是否可以通过for-in循环返回。默认情况下，所有直接定义在对象上的属性的这个特性都是true。
+ [[Get]]：获取函数，在读取属性时调用。默认值为undefined。
+ [[Set]]：设置函数，在写入属性时调用。默认值为undefined。

访问器属性是不能直接定义的，必须使用`Object.defineProperty()`。

```javascript
let book = {
    year_ :2017,
    edition:1
}
Object.defineProperty(book,"year",{
    get(){
        return this.year_
    },
    set(newValue){
        if(newValue > 2017){
            this.year_ = newValue
            this.edition += newValue - 2017
        }
    }
})

book.year= 2018
console.log(book.year)//2018
book.year = 2017
console.log(book.year)//2018
console.dir(book)
//year_中的下划线常用来表示该属性并不希望在对象方法的外部被访问
//另一个属性year被定义为一个访问器属性，其中获取函数简单的返回year_的值，而设置函数会做一些计算以决定正确的版本
//获取函数和设置函数不一定都要定义。
//只定义获取函数一位这属性时只读的，尝试修改属性会被忽略。
//在严格模式下，尝试写入只定义了获取函数的属性会抛出错误。类似地，只有一个设置函数的属性时不能读取的，非严格模式下读取会返回undefined,严格模式下会抛出错误。
```



### 定义多个属性

```javascript
let book = {}
Object.defineProperties(book,{
    year_:{
        value:2017
    },
    edition:{
        value:1
    },
    year:{
        get(){
            return this.year_
        },
        set(newValue){
           if(newValue>2017){
              this.year_ = newValue
           }
        }
    }
})

console.log(book.edition)//1
book.year = 2100
console.log(book.year)//2017
//不知道哪里敲错了，得到结果不符合预期。
//预期输出是2100

```



### 读取属性的特性

`Object.getOwnPropertyDescriptor()`：可以取得指定属性的属性描述符。

这个方法接收两个参数：

1. 属性所在的对象
2. 要取得其描述符的属性名

返回值是一个对象，对于访问器属性包含`configurable`，`enumerable`，`get`和`set`属性

对于数据属性包含`configurable`,`enumerable`,`writable`和`value`属性

```javascript
let book = {}
Object.defineProperties(book,{
    year_:{
        value:2017
    },
    edition:{
        value:1
    },
    year:{
        get:function(){
            return this.year_
        },
        set:function(newValue){
           if(newValue>2017){
              this.year_ = newValue
           }
        }
    }
})

let descriptor = Object.getOwnPropertyDescriptor(book,"year_")
console.log(descriptor.value)//2017
console.log(descriptor.configurable)//false
console.log(typeof descriptor.get)//undefined
let descriptor2 = Object.getOwnPropertyDescriptor(book,"year")
console.log(descriptor2.value)//undefined
console.log(descriptor2.enumerable)//false
console.log(typeof descriptor2.get)//function
```

ECMAScript2017新增了`Object.getOwnPropertyDescriptors()`静态方法。这个方法实际上会在每个自有属性上调用`Object.defineProperties()`并在一个新对象中返回它们。

```javascript
let book = {}
Object.defineProperties(book,{
    year_:{
        value:2017
    },
    edition:{
        value:1
    },
    year:{
        get:function(){
            return this.year_
        },
        set:function(newValue){
           if(newValue>2017){
              this.year_ = newValue
           }
        }
    }
})

let descriptor = Object.getOwnPropertyDescriptors(book)
console.log(descriptor)
// year_:
// { value: 2017,
//   writable: false,
//   enumerable: false,
//   configurable: false },
// edition:
// { value: 1,
//   writable: false,
//   enumerable: false,
//   configurable: false },
// year:
// { get: [Function: get],
//   set: [Function: set],
//   enumerable: false,
//   configurable: false } }
```



### 合并对象

ECMAScript6专门合并对象提供了`Object.assign()`方法。这个方法接收一个目标对象和一个或多个源对象作为参数，然后将每个源对象中可枚举和自有属性复制到目标对象。以字符串和符号为键盘、的属性会被复制。对每个符合条件的属性，这个方法会使用源对象上的[[Get]]取得属性的值，然后使用目标对象上的[[Set]]设置属性的值。

```javascript
let dest,src,result

dest = {name:'dest'}
src = {id:'src'}

result = Object.assign(dest,src)

console.log(dest === result)//true
console.log(dest !== src)//true
console.log(result)//{ name: 'dest', id: 'src' }
console.log(dest)//{ name: 'dest', id: 'src' }

//多个源对象

dest = {}
result = Object.assign(dest,{a:'foo'},{b:'bar'},{c:'car'})
console.log(dest === result)//true
console.log(dest)//{ a: 'foo', b: 'bar', c: 'car' }
console.log(result)//{ a: 'foo', b: 'bar', c: 'car' }

```



### 对象标识及相等判定

在ECMAScript6之前，有些特殊情况即使是`===`操作符也无能为力

```javascript
//这些是符合预期的情况
console.log(true === 1 )//false
console.log({} === {})//false
console.log("2" === 2)//false

//这些情况在不同javascript引擎中表现不同，但仍被认为相等
console.log(+0 === -0)//true
console.log(+0 === 0)//true
console.log(-0 === 0)//true

//要确定NaN的相等性，必须使用极为讨厌的isNaN()
console.log(NaN === NaN)//false
console.log(isNaN(NaN))//true

console.log(Object.is(true,1))//false
console.log(Object.is({},{}))//false
console.log(Object.is("2",2))//false

console.log(Object.is(+0,-0))//false
console.log(Object.is(+0,0))//true
console.log(Object.is(-0,0))//false

console.log(Object.is(NaN,NaN))//true
```

### 增强的对象语法

#### 属性值简写

#### 可计算属性

在引入可计算属性之前，如果想使用变量的值作为属性，那么必须先声明对象，然后使用中括号语法来添加属性。换句话说，不能在对象字面量中直接动态命名属性。

#### 简写方法名

在给对象定义方法时，通常都要写一个方法名，冒号，然后再引用一个匿名表达式

```javascript
let person = {
    sayName:function(name){
        console.log('My name is', name)
    }
}

person.sayName('Elaine')
```



### 对象解构



## 创建对象

### 工厂模式

工厂模式抽象了创建具体对象的过程，用函数来封装以特定借口创建对象的细节

```javascript
function createPerson(name,age,job){
  var o = new Object()
  o.name = name
  o.age = age
  o.job = job
  o.sayName = function(){
    console.log(this.name)
  }
  return o 
}
var person1 = createPerson("nicholas",29,"engineer")
var person2 = createPerson("Greg",27,"Doctor")
console.log(person1)
console.log(person2)
```

工厂模式解决了创建多个相似对象的问题，但没有解决对象识别的问题（即怎样知道一个对象的类型）

### 构造函数模式

任何函数，只要通过new操作符调用，那它就可以作为构造函数；如果不通过new操作符调用，就是普通函数

```javascript
 function Person(name,age,job){
   this.name = name
   this.age = age
   this.job = job
   this.sayName = function(){
     console.log(this.name)
   }
 }
var person1 = new Person("nocholas",29,"engineer")
var person2 = new Person("greh",27,"Doctor")

```

与工厂模式对比，存在以下不同之处：

+ 没有显式地创建对象
+ 直接将属性和方法赋给了this对象
+ 没有return语句
+ 按照惯例，构造函数始终都应该以一个大写字母开头，而非构造函数则应该以小写字母开头。这个做法借鉴自其他oo语言，主要是为了区别E
  CMAScript中的其他函数；因为构造函数也是函数，只不过可以用来创建对象而已



1. 将构造函数当作函数

   1. 构造函数与其他函数的唯一区别，就是调用它们的方式不同。不过，构造函数也是函数，不存在定义构造函数的特殊语法。**任何函数，只要通过new操作符来调用，那它就可以作为构造函数；而任何函数，如果不通过new操作符来掉哟哦那个，那它就是普通函数**

   2. ```javascript
      //当作构造函数使用
      var person = new Person("nicholas",29,"engineer")
      person.sayName()
      //当作普通函数调用
      Person("greg",27,"doctor)
      window.sayName()
      //在另一个对象的作用域中调用
      var o = new Object()
      Person.call(o,"kristen",25,"Nurse")
      o.sayName()
      
      ```

2. 构造函数的问题

   1. 构造函数的主要问题，就是每个方法都要在每个实例上重新创建一遍。在前面的例子中，person1和person2都有一个`sayName()`方法,但那两个方法不是同一个Function的实例.在ECMAScript中的函数是对象，因此每定义一个函数，也就是实例化了一个对象。不同实例上的同名函数是不相等的，以下代码可以证明这一点

      ```javascript
      person1.sayName == person2.sayName //false
      ```

   2. 然而，创建两个完成相同任务的function实例的确没必要，况且有this对象在，根本不用在执行代码前就把函数绑定在特定对象上，因此，可以通过把函数定义转移到构造函数外部来解决这个问题

      ```javascript
       function Person(name,age,job){
         this.name = name
         this.age = age
         this.job = job
         this.sayName = sayName
       }
      function sayName(){
        	console.log(this.name)
      }  
      var person1 = new Person("nocholas",29,"engineer")
      var person2 = new Person("greh",27,"Doctor")
      ```

   3. 上面的代码确实解决了两个函数做同一件事的问题，可是新问题又来了：在全局作用域中定义的函数实际上可能只被某个对象调用，这让全局作用域有点名不副实。而且，如果对象需要定义很多方法，那么就要定义很多个全局函数，于是我们这个自定义的引用类型就丝毫没有封装性可言了。

### 原型模式

我们创建的每个函数都有一个prototype属性，这个属性是一个对象，而这个对象的用途是包含可以由特定类型的所有实例共享的属性和方法，即prototype就是通过调用构造函数而创建的那个对象的实例的原型对象。使用原型对象的好处是可以让所有对象实例共享它包含的属性和方法。换句话说，不必在构造函数中定义对象实例的信息，而是可以将这些信息直接添加到原想对象中

```javascript
function Person(){

}
Person.prototype.name = "Nicholas"
Person.prototype.age = 29
Person.prototype.job = "engineer"
Person.prototype.sayName = function(){
  console.log(this.name)
}
var person1 = new Person()
person1.sayName()
var person2 = new Person()
person2.sayName()
console.log(person1.sayName===person2.sayName)//true
```

1. 理解原型对象

   1. 无论什么时候，只要创建了一个新函数，就会根据一组特定的规则为该函数创建一个prototype属性，这个属性指向函数的原型对象。在默认情况下，所有原型对象都会自动获得一个constructor属性，指回与之关联的构造函数。

   2. 创建了自定义的构造函数之后，其原型对象默认只会取得constructor属性；至于其他方法，则都是从Object继承而来的。当调用构造函数创建一个实例后，该实例内部将包含一个指针，指向构造函数的原型对象，ECMA-262第五版中管这个指针叫[[Prototype]]

   3. 可以通过`isPrototypeOf()`方法来确定对象之间是否存在关系。如果[[prototype]]指向调用`isPrototypeOf()`方法的对象，那么这个方法就返回true

      ```javascript
      Person.prototype.isPrototypeOf(person1)//true
      ```

   4. ECMAScript5增加了一个新方法：`Object.getPrototypeOf()`，这个方法返回[[Prototype]]的值.支持这个方法的浏览器有IE9+,Firefox3.5+,Opera12+,Chrome

      ```javascript
      Object.getPrototypeOf(person1)===Person.prototype//true
      Object.getPrototypeOf(person1).name //"Nicholas"
      ```

   5. 每当代码读取某个对象的属性时，都会执行一次搜索，目标是具有给定名字的属性。搜索首先从对象实例本身开始。如果在实例中找到了具有给定名字的属性，则返回该属性的值；如果没有找到，则继续搜索指针指向的原型对象，在原型对象中查找具有给定名字的属性。如果在原型对象中找到了这个属性，则返回该属性的值。

   6. 虽然可以通过对象实例访问保存在原型中的值，但却不能通过对象实例重写原型中的值。如果我们在实例中添加了一个属性，而该属性与实例原型中的一个属性同名，那我们就在实例中创建该属性。该属性将会屏蔽原型中的那个属性

      ```javascript
      function Person(){
      
      }
      Person.prototype.name = "Nicholas"
      Person.prototype.age = 29
      Person.prototype.job = "engineer"
      Person.prototype.sayName = function(){
        console.log(this.name)
      }
      var person1 = new Person()
      
      var person2 = new Person()
      
      console.log(person1.sayName===person2.sayName)
      console.dir(Object.getPrototypeOf(person1))
      person1.name="greg"
      console.log(person1.name)//"greg"--来自实例
      console.log(person2.name)//"Nicholas"--来自原型
      //当为对象实例添加一个属性时，这个属性就会屏蔽原型对象中保存的同名属性。换句话说，添加这个属性只会阻止我们访问原型中的那个属性，但不会修改那个属性。及时将这个属性设置为null,也只会在实例中设置这个属性。不过，使用delete操作符则可以完全删除实例属性，从而让我们能够重新访问原型中的属性
      delete person1.name
      console.log(person1.name)//"Nicholas"--来自原型
      ```

   7. 使用`hasOwnProperty()`方法可以检测一个属性是存在于实例中，还是存在于原型中。这个方法（不要忘了它是从Object继承来的）只在给定属性存在于对象实例中时，才会返回true

      ```javascript
      function Person(){
      
      }
      Person.prototype.name = "Nicholas"
      Person.prototype.age = 29
      Person.prototype.job = "engineer"
      Person.prototype.sayName = function(){
        console.log(this.name)
      }
      var person1 = new Person()
      
      var person2 = new Person()
      console.log(person1.hasOwnProperty("name"))//false
      person1.name="greg"
      console.log(person1.hasOwnProperty("name"))//true
      console.log(person2.hasOwnProperty("name"))//false
      delete person1.name
      console.log(person1.hasOwnProperty("name"))//false
      console.log(person1.name)
      console.log(person2.name)
      ```

2. 原型与in操走符

   1. 在单独使用中，in操作符会在通过对象能够访问给定属性时返回true，无论该属性存在于实例中还是原型中

      ```javascript
       function Person(){
      
       }
      Person.prototype.name = "Nicholas"
      Person.prototype.age = 27
      Person.prototype.job = "engineer"
      Person.sayName = function(){
        console.log(this.name)
      }
      var person1 = new Person()
      person1.hobby = "reading"
      console.log("hobby" in person1)//true
      console.log(person1.hasOwnProperty("hobby"))//true
      console.log("name" in person1)//true
      console.log(person1.hasOwnProperty("name"))//false
      
      
      ```

3. 更简单的原型语法

   1. 前面例子中每添加一个属性和方法就要敲一遍Person.prototype。为减少不必要的输入，也为了从视觉上更好的封装原型的功能，更常见的做法是用一个包含所有属性和方法的对象字面量来重写整个原型对象

      ```javascript
       function Person(){
      
       }
      Person.prototype = {
        name:"Nicholas",
        age:29,
        job:"engineer",
        sayName:function(){
          console.log(this.name)
        }
      }
      var person = new Person()
      //用instanceof测试仍然返回true，但constructor属性等于Object而不等于Person了
      console.log(person instanceof Object)//true
      console.log(person instanceof Person)//true
      console.log(person.constructor == Person)//false
      console.log(person.constructor == Object)//true
      console.log(person.hasOwnProperty("constructor"))//false
      console.log("constructor" in person)//true
      //
      ```

   2. 这种写法，constructor属性不再指向Person了。前面介绍过，每创建一个函数，就会同时创建它的prototype对象，这个对象也会自动获得constructor属性。而我们在这里使用的语法，本质上完全重写了默认的prototype对象，因此constructor属性也就变成了新对象下的constructor 属性（指向object构造函数)，不再指向Person函数。尽管instanceof操作符还能返回正确的结果，但通过constructor已经无法确定对象的类型了

      ```javascript
      function Person(){
      
      }
      Person.prototype.name = "Nicholas"
      Person.prototype.age = 27
      Person.prototype.job = "engineer"
      Person.sayName = function(){
        console.log(this.name)
      }
      var person1 = new Person()
      
      console.log("person1.constructor===Person",person1.constructor === Person)
      //true
      //person1的原型对象上的constructor指向构造函数Person
      console.log("person1.constructor===Object",person1.constructor === Object)
      //fase
      ```

   3. 如果constructor的值真的很重要，可以像下面这样特意将它设置回适当的值

      ```javascript
       function Person(){
      
       }
      Person.prototype = {
        constructor:Person,
        name:"Nicholas",
        age:29,
        job:"engineer",
        sayName:function(){
          console.log(this.name)
        }
      }
      ```

   4. 注意：用上面这种方式重置`constructor`属性会导致它的`[[Enumerable]]`特性被设置为true.默认情况下，原生的`constructor`属性是不可枚举的,可以试一试`Object.defineProperty()`

      ```javascript
      //只适用于ECMAScript5兼容的浏览器
      Object.defineProperty(Person.prototype,"constructor",{
        enumerable:false,
        value:Person
      }
                            )
      ```

4. 原型的动态性

   1. 由于原型中查找值的过程是一次搜索，因此我们对原型对象所做的任何修改都能够立即从实例上反映出来——即使是先创建了实例后修改原型也照样如此。

      ```javascript
      function Person(){
      
      }
      var friend = new Person()
      Person.prototype.sayHi = function(){
        console.log("hi")
      }
      friend.sayHi()//"hi"(没有问题）
      ```

   2. 以上代码先创建了Person的一个实例，并将其保存在person中。然后，下一条语句在Person.prototype中添加了一个方法`sayHi()`.即使person实例是在添加新方法之前创建的，但它仍然可以访问这个新方法。其原因可以归结为实例与原型之间的松散连接关系。因为实例与原型之间的连接只不过是一个指针，而非一个副本。

   3. 尽管可以随时为原型添加属性和方法，并且修改能够立即在所有对象实例中反映出来，但如果是重写整个原型对象，那么情况就不一样了。我们知道，调用构造函数时会为实例添加一个指向最初原型的[[Prototype]]指针，而把原型修改为另外一个对象就等于切断了构造函数与最初原型之间的联系。请记住：实例中的指针仅指向原型，而不指向构造函数。

      ```javascript
      function Person(){
      
      }
      var friend = new Person()
      Person.prototype = {
        constructor:Person,
        name:"Nicholas",
        age:29,
        job:"engineer",
        sayName:function(){
          console.log(this.name)
        }
      }
      friend.sayName()//error
      //因为friend指向的原型中不包含以改名字命名的属性
      ```

      ![js](/Users/macos/study/web/es6/js.png)

5. 原生对象的原型
   1. 原型模式的重要性不仅体现在创建自定义类型方面，就连所有原生的引用类型，都是采用这种模式创建的。所有原生引用类型（Object,Array,String等等)都在其构造函数原型上定义了方法。
   2. 通过原生对象的原型，不仅可以取得所有默认方法的引用，而且也可以定义新方法。可以像修改自定义对象的原型一样修改原生对象的原型。因此可以随时添加方法。
6. 原型对象的问题

### 组合使用构造函数模式和原型模式

创建自定义类型的最常见方式，就是组合使用构造函数模式和原型模式。构造函数模式用于定义实例属性，而原型模式用于定义方法和共享的属性。

```javascript
function Person(name,age,job){
  this.name = name
  this.age = age
  this.job = job
  this.friends = ["shelby","Court"]
}
Person.prototype ={
  constrctor:Person,
  sayName:function(){
    console.log(this.name)
  }
}
var person1 = new Person("nicholas",29,"engineer")
var person2 = new Person("greg",27,"doctor")
person1.friends.push("van")
console.log(person1.friends)//"nicholas"
console.log(person2.friends)//"greg"
console.log(person1.friends === person2.friends)//false
console.log(person1.sayName === person2.sayName)//true
```

在这个例子中，实例属性都是在构造函数中定义的，而由所有实例共享的属性constructor和方法`sayName()`则是在原型中定义的。而修改了`person1.friends`并不会影响到`person2.friends`因为它们分别引用了不同的数组。

这种构造函数和原型混成的模式，是目前在ECMAScript中使用最广泛，认同度最高的一种创建自定义类型的方法。可以说，这是用来定义引用类型的一种默认模式

### 动态原型模式

有其他OO语言经验的开发人员在看到独立的构造函数和原型时，很可能会感到非常困惑。动态原型模式正是致力于解决这个问题的一个方案。它把所有信息都封装在了构造函数中，而通过在构造函数中初始化原型（仅在必要的情况下），又保持了同时使用构造函数和原型的优点。换句话说，可以通过检查某个应该存在的方法是否有效，来决定是否需要初始化原型

## 继承

ECMAScript的实现继承主要是通过原型链来实现的

### 原型链

原型对象，构造函数，实例之间的关系：

+ 每个构造函数都有一个原型对象（prototype)
+ 原型对象都包含一个指向构造函数的指针（constructor)
+ 实例包含一个指向原型对象的内部指针（`__proto__`)

实现原型链的基本模式

```javascript
function SuperType(){
  this.property = true
}

SuperType.prototype.getSuperValue = function(){
  return this.property
}
function SubType(){
  this.subproperty = false
}

SubType.prototype = new SuperType()//

SubType.prototype.getSubValue = function(){
  return this.subproperty
}

var instance = new SubType()
alert(instance.getSuperValue())//true
```

![原型链](/Users/macos/study/web/es6/原型链.jpg)



Function,Object关系

```javascript
console.dir(Object.__proto__.__proto__===Object.prototype)
//true  
console.log(Function.__proto__=== Function.prototype)
//true
console.log(Object.__proto__=== Function.prototype)
//true
console.log(Object.prototype.isPrototypeOf(Function))
//true
console.log(Function.prototype.isPrototypeOf(Object))
//true
console.log(Object.prototype.__proto__)
//null
```

### 借用构造函数

有时候也叫伪造对象或经典继承。

这种技术的基本思想是：在子类型构造函数的内部调用超类型构造函数

```javascript
 function SuperType(){
   this.colors = ["red","blue","green"]
 }
function SubType(){
  //继承了SuperType
  SuperType.call(this)
}
var instance1 = new SubType()
instance1.colors.push("black")
console.log(instance1.colors)
var instance2 = new SubType()
instance2.colors.push("yellow")
console.log(instance2.colors)

function SuperType2(name){
  this.name = name
}

function SubType2(){
  //继承了SuperType,同时还传递了参数
  SuperType2.call(this,"nicholas")
  this.age = 29
}

var instance = new SubType2()
console.log(instance.name)
console.log(instance.age)
//1.相对于原型链而言，借用构造函数有一个很大的优势，即可以在子类型构造函数中向超类型构造函数传递参数
//2.借用构造函数的方法都在构造函数中定义，因此函数复用就无从谈起了。而且在超类型中定义的方法，对子类型而言也是不可见的，结果所有类型都只能使用 构造函数模式
```

### 组合继承

也叫伪经典继承

```javascript
function SuperType(name){
  this.name = name
  this.colors = ["red","blue","green"]

}
SuperType.prototype.sayName = function(){
  console.log(this.name)
}
function SubType(name,age){
  //继承属性
  SuperType.call(this,name)
  this.age = age
}
//继承方法
SubType.prototype = new SuperType()
SubType.prototype.constructor = SubType
SubType.prototype.sayAge = function(){
  console.log(this.age)
}
var instance = new SubType("elaine",29)
instance.colors.push('pink')
console.dir(instance)
var instance2 = new SubType('mary',27)
instance2.colors.push('grey')
console.dir(instance2)
```

组合继承避免了原型链和借用构造函数的缺陷，融合了它们的优点，成为js中最常用的继承模式。而且，`instanceof`和`isPrototypeOf`也能识别基于组合继承创建的对象

### 原型式继承

原型式继承的思想是：基于已经有的对象创建新对象，同时还不必因此创建自定义类型.如下：

```javascript
function object(o){
  function F(){}
  F.prototype = 0
  return new F()
}
//从本质上来讲，object()对传入其中的对象执行了一次浅复制
```

es5通过新增Object.create()方法规范化了原型式继承。这个方法接收两个参数：一个用作新对象原型的对象和（可选）一个为新对象定义额外属性的对象。

在没有必要创建构造函数，而只想让一个对象与另一个对象保持类似的情况下，原型式继承是完全可以胜任的。注意：包含引用类型值的属性始终都会共享相应的值，就像使用原型模式一样。

```javascript
 var person = {
   name:"nicholas",
   friends:['shelby','court','van']
 }
 var anotherPerson = Object.create(person)
 anotherPerson.name = 'greg'
anotherPerson.friends.push('rob')

var yetAnotherPerson = Object.create(person)
yetAnotherPerson.name = "Linda"
yetAnotherPerson.friends.push('barbie')

console.log(person.friends)
console.log(anotherPerson)
console.log(yetAnotherPerson)
```

### 寄生式继承

寄生式继承的思路与寄生构造函数和工厂模式类似，即创建一个仅用于封装继承过程的函数，该函数在内部以某种方式来增强对象，最后再像真的是它做了所有工作一样返回对象。

```javascript
function createAnother(original){
  var clone = Object.create(original)//通过调用函数创建一个新对象
  clone.sayHi = function(){ //以某种方式来增强这个对象
    console.log('hi')
  }
  return clone //返回这个对象
}
var person = {
  name:'Nicholas',
  friends:["shelby","court","van"]
}
var anotherPerson = createAnother(person)
anotherPerson.sayHi()
```

### 寄生组合式继承

组合继承是javascript最常用的继承模式；不过，它也有自己的不足。组合继承最大的问题就是无论什么情况下，都会调用两次超类型构造函数

```javascript
function SuperType(name){
  this.name = name
  this.colors = ["red","blue","green"]

}
SuperType.prototype.sayName = function(){
  console.log(this.name)
}
function SubType(name,age){
  //继承属性
  SuperType.call(this,name)//第二次调用SuperType()
  this.age = age
}
//继承方法
SubType.prototype = new SuperType()//第一次调用SuperType()
subType.prototype.constructor = subType
SubType.prototype.sayAge = function(){
  console.log(this.age)
}
```



所谓寄生组合式继承，即通过借用构造函数来继承属性，通过原型链的混成形式来继承方法。背后的思路是：不必为了指定子类型的原型而调用超类型的构造函数，我们所需要的无非就是超类型的一个副本而已

```javascript
function inheritPrototype(subType,superType){
  var prototype = Object(superType.prototype)//创建对象
  prototype.constructor  = subType//增强对象
  subType.prototype = prototype//指定对象
}

function SuperType(name){
  this.name = name
  this.colors = ["red","blue","green"]
}
SuperType.prototype.sayName = function(){
  console.log(this.name)
}

function SubType(name,age){
  SuperType.call(this,name)
  this.age = age
}
inheritPrototype(SubType,SuperType)
SubType.prototype.sayAge = function(){
  console.log(this.age)
}

var instance = new SubType('mary',18)
instance.colors.push('pink')
console.dir(instance)
console.dir(SuperType)
console.dir(SubType)
```

## 类

前几节深入讲解了如何只使用ECMAScript5的特性来模拟类似于类（class-like）的行为。不难看出，各种策略都有自己的问题，也有相应的妥协。正因为如此，实现继承的代码也显得非常冗长和混乱。

为解决这些问题，ECMAScript6新引入的`class`关键字具有正式定义类的能力。类（class）是ECMAScript中新的基础性语法糖结构，因此刚开始接触时可能不太习惯。



### 类定义

与函数类型相似，定义类也有两种主要方式：

1. 类声名

   ```javascript
   class Person{}
   ```

2. 类表达式

   ```javascript
   const Animal = class {}
   ```

与函数表达式类似，类表达式在它们被求值前也不能引用。不过，与函数定义不同的是，虽然函数声明可以提升，但类定义不能：

```javascript
console.log(FunctionExpression)//undefined
var FunctionExpression = function(){}
console.log(FunctionExpression)//function() {}

console.log(FunctionDeclaration)//FunctionDeclaration(){}
function FunctionDeclaration(){}
console.log(FunctionDeclaration)//FunctionDeclaration(){}

console.log(ClassExpression)//undefined
var ClassExpression = class{}
console.log(ClassExpression)//class{}

console.log(ClassDeclaration)
//ReferenceError:ClassDeclaration is not defined
class ClassDeclaration {}
console.log(ClassDeclaration)//class ClassDeclaration{}
```

另一个跟函数声明不同的地方是，函数受函数作用域限制，而类受块作用域限制。



类的构成

类可以包含构造函数方法，实例方法，获取函数，设置函数和静态类方法，但这些都不是必需的。空的类定义照样有效。默认情况下，类定义中的代码都在严格模式下执行。

与函数构造函数一样，多数变成风格都建议类名的首字母大写，以区别于通过它创建的实例

```javascript
//空类定义，有效
class Foo{

}
//有构造函数的类，有效
class Bar{
    constructor(){}
}
//有获取函数的类，有效
class Baz{
    get myBaz(){}
}
//有静态方法的类，有效
class Qux{
    static myQux(){}
}
```

类表达式的名称是可选的。在把类表达式赋值给变量后，可以通过name属性取得类表达式的名称字符串。但不能在类表达式作用域外部访问这个标识符。

```javascript
let Person = class PersonName{
    identify(){
        console.log(Person.name,PersonName.name)
    }
}
let p = new Person()
p.identify() //PersonName PersonName
console.log(Person.name)//PersonName
console.log(PersonName)//ReferenceError:PersonName is not defined

```

###  类构造函数

constructor关键字用于在类定义块内部创建类的构造函数。方法名constructor会告诉解释器在使用new操作符创建类的新实例时，应该调用这个函数。构造函数的定义不是必需的，不定义构造函数相当于将构造函数定义为空函数。

#### 实例化

使用new操作符实例化Person的操作等于使用new调用其构造函数。唯一可感知的不同之处就是,javascript解释器知道使用new和类意味着应该使用constructor函数进行实例化。

使用new调用类的构造函数会执行如下操作：

1. 在内存中创建一个新对象。
2. 这个新对象内部的[[Prototype]]指针被赋值为构造函数的prototype属性
3. 构造函数内部的this被赋值为这个新对象（即this指向新对象）
4. 执行构造函数内部的代码（给新对象添加属性）
5. 如果构造函数返回非空对象，则返回该对象；否则，返回刚创建的新对象

```javascript
class Animal{}

class Person{
    constructor(){
        console.log('person ctor')
    }
}

class Vegetable{
    constructor(){
        this.color = 'orange'
    }
}

let a = new Animal()

let p = new Person()

let v = new Vegetable()
console.log(v.color)

```

类实例化时传入的参数会用作构造函数的参数。如果不需要参数，则类名后面的括号也是可选的

```javascript
class Person{
    constructor(name){
        console.log(arguments.length)
        this.name = name || null
    }
}

let p1 = new Person//0
console.log(p1.name)
//null
let p2 = new Person()//0
console.log(p2.name)
//null
let p3 = new Person("Jake")//1
console.log(p3.name)
//Jake
```

默认情况下，类构造函数会在执行之后返回this对象。构造函数返回的对象会被用作实例化的对象，如果没有什么引用新创建的this对象，那么这个对象会被销毁。不过，如果返回的不是this对象，而是其他对象，那么这个对象不会通过instanceof操作符检测出跟类有关联，因为这个对象的原型指针并没有被修改。

```javascript
class Person{
    constructor(override){
        this.foo = "foo"
        if(override){
            return{
                bar:"bar"
            }
        }
    }
}

let p1 = new Person(),
    p2 = new Person(true)

console.log(p1)//Person { foo: 'foo' }

console.log(p2)//{ bar: 'bar' }

console.log(p1 instanceof Person)//true

console.log(p2 instanceof Person)//false

```

类构造函数与构造函数的主要区别是，调用类构造函数必须使用new操作符。而普通构造函数如果不使用new调用，那么就会以全局的this（通常是window对象）作为内部对象。调用类构造函数时如果忘了使用new则会抛出错误

```javascript
function Person(){}
class Animal{}

let p = Person()

let a = Animal()
//TypeError: Class constructor Animal cannot be invoked without 'new'

```

类构造函数没有什么特殊之处，实例化之后，它会成为普通的实例方法（但作为类构造函数，仍然要使用new调用）。因此，实例化之后可以在实例上引用它

```javascript
class Person{}

let p1 = new Person()

p1.constructor()
//TypeError: Class constructor Person cannot be invoked without 'new'

let p2 = new p1.constructor()
```

#### 把类当成特殊函数

ECMAScript中没有正式的类这个类型。从各方面来看，ECMAScript类就是一种特殊函数。声明一个类之后，通过typeof操作符检测类标识符，表明它是一个函数：

```javascript
class Person{}
console.log(Person) //class Person{}
console.log(typeof Person) //function
```

类标签符有prototype属性，而这个原型也有一个constructor属性指向类自身：

```javascript
class Person{}
console.log(Person.prototype)//{constructor:f()}
console.log(Person.prototype.constructor === Person)//true
```

由此可知，可以使用instanceof操作符检查一个对象与类构造函数，以确定这个对象是不是类的实例。只不过此时的类构造函数要使用类标签符。

如前所述，类本身具有与普通构造函数一样的行为。在类的上下文中，类本身在使用new调用时就会被当成构造函数。重点在于，类中定义的constructor方法不会被当成构造函数，在对它使用instanceof操作符时会返回false。但是，如果在创建实例时直接将类构造函数当成普通的构造函数来使用，那么instanceof操作符的返回值会反转。

```javascript
class Person{}

let p1 = new Person()

console.log(p1.constructor === Person)//true
console.log(p1 instanceof Person )//true
console.log(p1 instanceof Person.constructor)//false

let p2 = new Person.constructor()

console.log(p2.constructor = Person)//false
console.log(p2 instanceof Person)//false
console.log(p2 instanceof Person.constructor)//true
```

类是javascript的一等公民，因此可以像其他对象或函数引用一样把类作为参数传递。

```javascript
let classList = [
    class{
        constructor(id){
            this.id_ = id
            console.log('instance',this.id_)
        }
    }
]

function createInstance(classDefinition, id){
    return new classDefinition(id)
}
let foo  = createInstance(classList[0],3141)
//instance 3141
```

与立即调用函数表达式相似，类也可以立即实例化

```javascript
let p = new class Foo{
    constructor(x){
        console.log(x)
    }
}('bar')//bar

console.log(p)//Foo{}
```

### 实例，原型和类成员

#### 实例成员

每次通过new调用类标识符时，都会执行类构造函数。在这个函数内部，可以为新创建的实例(this)添加“自有“属性。至于添加什么样的属性，则没有限制。另外，在构造函数执行完毕后，仍然可以给实例继续添加新成员。

每个实例都对应一个唯一的成员对象，这意味着所有成员都不会在原型上共享。

```javascript
class Person{
    constructor(){
        this.name = new String('Jack')
        this.sayName = () => console.log(this.name)
        this.nickName = ['Jake','J-Dog']
    }
}

let p1 = new Person(),
    p2 = new Person()

p1.sayName()//Jack
p2.sayName()//Jack

console.log(p1.name === p2.name)//false
console.log(p1.sayName === p2.sayName)//false
console.log(p1.nickName === p2.nickName)//false

p1.name = p1.nickName[0]
p2.name = p2.nickName[1]

p1.sayName()//Jake
p2.sayName()//J-Dog
```

#### 原型方法与访问器

为了实例间共享方法，类定义语法把在类块中定义的方法作为原型方法。

在类块中定义的所有内容都会定义在原型上

可以把方法定义在类构造函数或者类块中，但不能在类块中给原型添加原始值或对象作为成员数据。

```javascript
class Person{
    name:'jake'
}
//unexpected token
```

#### 静态类方法

可以在类上定义静态方法。这些方法通常用于执行不特定于实例的操作，也不要求存在类的实例。

**与原型成员类似，每个类上只能有一个静态成员。**

静态类成员在类定义中使用static关键字作为前缀。在静态成员中，this指向类自身。其他所有约定跟原型成员一样

```javascript
class Person{
    constructor(){
        this.locate = () => console.log('instance',this)
    }
    locate(){
        console.log('prototype',this)
    }
    static locate(){
        console.log('class',this)
    }
}

let p = new Person()
p.locate()//instance,Person{}
Person.prototype.locate()//prototype,{constructor:..}
Person.locate()//class,class Person{}
```

静态类方法非常适合作为实例工厂

```javascript
class Person{
    constructor(age){
        this.age_ = age
    }
    sayAge(){
        console.log(this.age_)
    }
    static create(){
        return new Person(Math.floor(Math.random()*100))
    }
}

console.log(Person.create())

```

#### 非函数原型和类成员

虽然 类定义并不显示支持在原型或类上添加成员数据，但在类定义外部，可以手动添加。

```javascript
class Person{
    sayName(){
        console.log(Person.greeting, this.name)
    }
}
Person.greeting =  "My name is"

Person.prototype.name = 'Jake'

let p = new Person()
p.sayName()
//My name is Jake
```

注意：类定义中之所以没有显式支持添加数据成员，时因为在共享目标（原型和类）上添加可变数据成员时一种反模式。一般来说，对象实例应该独自拥有通过this引用的数据

#### 迭代器与生成方法

类定义语法支持在原型和类本身上定义生成器方法：

### 继承

虽然类继承使用的是新语法，但背后依旧使用的是原型链。

#### 继承基础

ES6类支持单继承。使用extends关键字，就可以继承任何拥有[[constructor]]和原型的对象。很大程度上，这意味着不仅可以继承一个类，也可以继承普通的构造函数。

```javascript
class Vihicle{}

class Bus extends Vihicle{}

let b = new Bus()
console.log(b instanceof Vihicle)//true
console.log(b instanceof Bus)//true

function Person(){}
class Engineer extends Person{} 

let e = new Engineer()
console.log(e instanceof Engineer)//true
console.log(e instanceof Person)//true
```

类和原型上定义的方法都会带到派生类。this的值会反映调用相应方法的实例或者类。

```javascript
class Vihicle{
    identifyprototype(id){
        console.log(id,this)
    }
    static identifyprototype(id){
        console.log(id,this)
    }
}
class Bus extends Vihicle{

}

let v = new Vihicle()

let b = new Bus()

b.identifyprototype('bus')//bus Bus {}
v.identifyprototype('Vihicle')//Vihicle Vihicle {}

Bus.identifyprototype('bus')//bus class Bus extends Vihicle{}
Vihicle.identifyprototype('Vihicle')//Vihicle class Vihicle{}

```

注意：extends关键字也可以在类表达式中使用，因此let Bar = class extends Foo{}是有效的语法。

#### 构造函数，HomeObject和super()

派生类的方法可以通过super关键字引用它们的原型。这个关键字只能在派生类中使用，而且仅限于类构造函数，实例方法和静态方法内部。在类构造函数中使用super可以调用父类构造函数。

```javascript
class Vehicle{
    constructor(){
        this.hasEngine = true
    }
}

class Bus extends Vehicle{
    constructor(){
        super()
        console.log(this instanceof Vehicle)//true
        console.log(this)//Bus{ hasEngine:true }
    }
}

new Bus()
```

在**子类静态方法**中可以通过super调用继承的类上定义的静态方法

```javascript
class Vehicle{
    static identify(){
        console.log('Vehicle static')
    }
}

class Bus extends Vehicle{
    static identify(){
        super.identify()
    }
}

Bus.identify()//Vehicle static
```

使用super要注意的问题：

+ super只能在派生类构造函数和静态方法中使用

  ```javascript
  class Vehicle{
    constructor(){
      super()
      //SyntaxError:'super' keyword unexpected
    }
  }
  ```

  

+ 不能单独引用super关键字，要么用它调用构造函数，要么用它引用静态方法

  ```javascript
  class Vehicle{}
  class Bus extends Vehicle{
    constructor(){
      console.log(super)
      //SyntaxErrot:'super' keyword unexpected here
    }
  }
  ```

  

+ 调用`super()`会调用父类的构造函数，并将返回的实例赋值给this

  ```javascript
  class Vehicle{}
  class Bus extends Vehicle{
    constructor(){
      super()
      console.log(this instanceof Bus)
    }
  }
  new Bus()//true
  ```

  

+ `super()`的行为如同调用构造函数，如果需要给父类构造函数传参，则需要手动传入

  ```javascript
  class Vehicle{
    constructor(licensePlate){
      this.licensePlate = licensePlate
    }
  }
  class Bus extends Vehicle{
    constructor(licensePlate){
      super(licensePlate)
    }
  }
  console.log(new Bus('1337H4X'))//Bus {licensePlate:'1337H4X'}
  ```

  

+ 如果没有定义类构造函数，在实例化派生类时会调用`super()`，而且会传入所有传给派生类的参数

  ```javascript
  class Vehicle{
    constructor(licensePlate){
      this.licensePlate = licensePlate
    }
  }
  class Bus extends Vehicle{}
  console.log(new Bus('1337H4X'))//Bus {licensePlate:'1337H4X'}
  ```

  

+ 在类构造函数中，不能调用`super()`之前引用this

  ```javascript
  class Vehicle{}
  class Bus extends Vehicle{
    constructor(){
      console.log(this)
    }
  }
  new Bus()
  //ReferenceError:Must call super constructor in derived class
  ```

  

+ 如果在派生类中显示定义了构造函数，则要么必须在其中调用`super()`，要么必须在其中返回一个对象

  ```javascript
  class Vehicle{}
  
  class Bus extends Vehicle{
      constructor(){
          super()
      }
  }
  
  class Car extends Vehicle{
      constructor(){
          return {
              brand:'BMW'
          }
      }
  }
  
  class Van extends Vehicle{}
  
  let b = new Bus()
  let c = new Car()
  let v = new Van()
  ```



#### 抽象基类

有时候可能需要定义这样一个类，它可供其他类继承，但本身不会被实例化。虽然ECMAScript没有专门支持这种类的语法，但通过new.target也很容易实现。new.target保存通过new关键字调用的类或函数。通过在实例化时检测new.target是不是抽象基类，可以阻止对抽象基类的实例化。

```javascript
/抽象基类
class Vehicle{
    constructor(){
        console.log(new.target)
        if(new.target === Vehicle){
            throw new Error('Vehicle cannot be deirectly instantiated')
        }
    }
}
class Bus extends Vehicle{}

let b = new Bus()
let v = new Vehicle()
//Error: Vehicle cannot be deirectly instantiated

```



另外，通过在抽象基构造函数中进行检查，可以要求派生类必须定义某个方法。因为原型方法在调用类构造函数之前就已经存在了，所以可以通过this关键字来检查相应的方法：

```javascript
class Vehicle{
    constructor(){
        console.log(this)
        if(new.target === Vehicle){
            throw new Error('Vehicle cannot be directly instantiated')
        }
        if(!this.foo){
            throw new Error('Inheriting class must define foo()')
        }
    }
}

class Bus extends Vehicle{}

class Car extends Vehicle{
    foo(){
        console.log('hello')
    }
}

new Car()//Car {}
new Bus()//Error: Inheriting class must define foo()

```



#### 继承内置类型

ES6类为继承内置引用类型提供了顺畅的机制，开发者可以方便地扩展内置类型

#### 类混入

# 集合引用类型

## Object

## Array

### 创建数组

有几种基本的方式可以创建数组：

1. ```javascript
   let colors = new Array()
   ```

2. 如果知道数组中元素的数量，可以向构造函数传入一个数组

   ```javascript
   let colors = new Array(20)//创建一个初始length为20的数组
   ```

3. 也可以给`Array`构造函数传入要保存的元素

   ```javascript
   let colors = new Array("red","blue","green")
   ```

4. 在使用构造函数时，也可以省略new操作符。结果是一样的

   ```javascript
   let colors = Array(2)
   ```

5. 另一种创建数组的方式是使用数组字面量表示法

   ```javascript
   let colors = ["red","blue","green"]
   let values = [1,3,5]
   //注意：在使用数组字面量表示法创建的数组不会调用Array构造函数
   ```

Array构造函数还有两个es6新增的用于创建数组的静态方法：

1. `Array.from()`:用于将类数组结构转换为数组实例。第一个参数是一个类数组对象，即任何可迭代的结构，或者有一个length属性和可索引元素的结构。

   ```javascript
   console.log(Array.from("Matt"))//M,a,t,t
   
   const a1 = [1,2,3,4]
   const a2 = Array.from(a1)
   console.log(a2)
   console.log(a1 === a2)//false
   ```

   `Array.from（）`还接收第二个可选的映射函数参数。这个函数可以直接增强新数组的值，而无须调用`Array.from().map()`那样先创建一个中间数组。还可以接收第三个可选参数，用于指定映射函数中this的值。但这个重写的this在箭头函数中不适用。

   ```javascript
   const a1 = [1,2,3,4]
   const a3 = Array.from(a1, x => x * 2)
   const a4 = Array.from(a1, function (x) {return x * this.exponent},{exponent:3})
   console.log(a3)//[2,4,6,8]
   console.log(a4)//[3,6,9,12]
   ```

2. `Array.of()`: 用于把一组参数转换为数组。这个方法用于替代在es6之前常用的Array.prototype.slice.call(arguments),一种异常笨拙的将arguments对象转换为数组的写法

   ```javascript
   Array.of(1,2,3,4) //[1,2,3,4]
   Array.of(undefined,null)//[undefined,null]
   ```

### 数组空位

使用数组字面量初始化数组时，可以用一串逗号来创建空位（hole)。ECMAScript会将逗号之间相应索引位置当成空位。ES6规范重新定义了该如何处理这些空位

```javascript
//ES6新增方法普遍将这些空位当成存在的元素，只不过值为undefined。
const options = [1,,,,5]
for(const option of options){
  console.log(option === undefined)
}
//false
//true
//true
//true
//false

 const a1 = Array.from([,,,])
 for (const val of a1){
   console.log(val === undefined)
 }
//true
//true
//true

console.log(Array.of(...[,,,]))
//[undefined,undefined,undefined]

//es6之前的方法则会忽略这个空位，但具体的行为也会因方法而异
//map()会跳过空位置
//join()视空位置为空字符串

//注意：由于行为不一致和存在性能隐患，因此实践中要避免使用数组空位。如果确实需要使用，则可以显式的用undefined值代替。
```

### 数组索引

数组length属性的独特之处在于，它不是只读的。通过修改length属性，可以从数组末尾删除或添加元素。

```javascript
let color  = ["red","blue","green"]
color.length = 2
console.log(color[2])//undefined

color.length = 4
for(const val of color){
    console.log(val)
}
//red
//blue
//undefined
//undefined
console.log(color.length)
//4
```

使用length属性可以方便的向数组末尾添加元素

```javascript
let colors = ["red","blue","green"]
colors[colors.length] = "yellow"
//数组中最后一个元素的索引始终是length-1，因此下一个新增槽位的索引就是length

//每次在数组最后一个元素后面新增一项，数组的length属性都会自动更新，以反映变化
let colors = ["red","blue","green"]
colors[99] = "grey"
console.log(colors.length)
//100
//这里，这中间的所有元素，即3~98，实际并不存在，因此在访问时会返回undefined
//数组最多可以包含4,294,967,295个元素。如果尝试添加更多项，会导致抛出错误。以这个最大值作为初始值创建数组，可能导致脚本运行时间过长的错误。
```

### 检测数组

一个经典的ECMAScript问题时判断一个对象是不是数组。在只有一个网页（只有一个全局作用域时）的情况下，使用`instanceof`操作符就足够了

```javascript
if(value instanceof Array){
  
}
```

使用`instanceof`的问题在于，如果网页里有多个框架，则可能涉及两个不同的全局执行上下文，因此就会有两个不同版本的Array构造函数。如果要把数组从一个框架传给另一个框架，则这个数组的构造函数将有别于在第二个框架内本地创建的数组。

`Array.isArray()`

这个方法的目的就是确定一个值是否为数组，而不用管它时在哪个全局执行上下文中创建的

```javascript
if(Array.isArray(value)){
  
}
```

### 迭代器方法

在ES6中，Array的原型上暴露了3个用于检索数组内容的方法：

1. `keys()`：返回数组索引的迭代器

   ```javascript
   const a = ["foo","bar","baz","qux"]
   const aKeys = Array.from(a.keys())
   //[ 0, 1, 2, 3 ]
   
   ```

2. `values()`：返回数组元素的迭代器

   ```javascript
   const a = ["foo","bar","baz","qux"]
   const aValues = Array.from(a.values())
   //[ 'foo', 'bar', 'baz', 'qux' ]
   
   ```

3. `entries()`：返回索引/值对的迭代器

   ```javascript
   const a = ["foo","bar","baz","qux"]
   const aEntries = Array.from(a.entries())
   //[ [ 0, 'foo' ], [ 1, 'bar' ], [ 2, 'baz' ], [ 3, 'qux' ] ]
   
   ```

使用ES6的解构可以非常容易的在循环中拆分键/值对

```javascript
const a = ["foo","bar","baz","qux"]
for (const [idx,element] of a.entries()){
    console.log(idx)
    console.log(element)
}
//0
//foo
//1
//bar
//2
//baz
//3
//qux

```

### 复制和填充方法

1. `fill()`：向一个已有的数组中插入全部或部分相同的值。开始索引用于指定开始填充的位置，它是可选的。如果不提供结束索引，则一直填充到数组末尾。负值索引从数组末尾开始计算。也可以将负索引想象成数组长度加上它得到的一个正索引。

```javascript
const zeros = [0,0,0,0,0]

//用1填充整个数组
zeros.fill(1)
console.log(zeros) //	[1,1,1,1,1]

//用0填充索引大于等于2的元素
zeros.fill(0,2)		
console.log(zeros) //[1,1,0,0,0]

//用3填充索引大于等于0，小于3的元素
zeros.fill(3,0,3)
console.log(zeros) //[3,3,3,0,0]
```

`fill()`静默忽略超出数组边界，零长度及其方向相反的索引范围

```javascript
//书上没有说明，经过自己测试得到的仅供参考的一个结论:
//1.start索引值为负数时，自动转换为0<=（数组长度*n+start值）<length
//例如：数组长度5，start = -23,则转换为（-23+5*5）=2
//2.end索引值为负数，自动转换为(数组长度+end值）
//例如：数组长度5，end = -6, 转换为-1，仍然是负数，转换失败，数组不发生改变
//3.索引部分可用，填充可用部分
//例如：[0,0,0,0,0].fill(1,3,10)=>[0,0,0,1,1]
//4.索引反向，忽略
//例如：[0,0,0,0,0].fill(1,4,2)
const zeros = [0,0,0,0,0]

zeros.fill(1,-8,4)
console.log(zeros)
//[ 1, 1, 1, 1, 0 ]

zeros.fill(0)
zeros.fill(1,-8,-7)
console.log(zeros)
//[ 0, 0, 0, 0, 0 ]

zeros.fill(0)
zeros.fill(1,-23,-1)
console.log(zeros)
//[ 1, 1, 1, 1, 0 ]

zeros.fill(0)
zeros.fill(1,2,10)
console.log(zeros)
//[ 0, 0, 1, 1, 1 ]

```

2. `copyWithin()`：按照指定范围浅复制数组中的部分内容，然后将它们插入到指定索引开始的位置，开始索引和结束索引和`fill()`使用相同的计算方法

```javascript
let ints = [1,2,3,4,5,6,7,8,9,10]
ints.copyWithin(3)
console.log(ints)
//[ 1, 2, 3, 1, 2, 3, 4, 5, 6, 7 ]

ints = [1,2,3,4,5,6,7,8,9,10]
ints.copyWithin(0,4)
console.log(ints)
//[ 5, 6, 7, 8, 9, 10, 7, 8, 9, 10 ]

ints = [1,2,3,4,5,6,7,8,9,10]
ints.copyWithin(4,0,2)
console.log(ints)
//[ 1, 2, 3, 4, 1, 2, 7, 8, 9, 10 ]

ints = [1,2,3,4,5,6,7,8,9,10]
ints.copyWithin(4,-30,-8)
console.log(ints)
//[ 1, 2, 3, 4, 1, 2, 7, 8, 9, 10 ]

```

### 转换方法

所有对象都有`toLocaleString()`，`toString()`，`valueOf()`方法。其中，`valueOf()`返回的还是数组本身。而`toString()`返回由每个值的等效字符串拼接而成的一个逗号分隔的字符串。也就是说，对数组的每个值都会调用其`toString()`方法，以得到最终的字符串。

`toLocaleString()`方法也可能返回跟以上两种方法相同的结果，但也不一定。在调用数组的`toLocaleString()`方法时，会得到一个逗号分隔的数组值的字符串。它与另外两个方法唯一的区别是，为了得到最终的字符串，会调用数组的每个值的`toLocaleString()`方法，而不是`toString()`方法。

```javascript
let person1 = {
  toLocaleString(){
    return "Nikolaos"
  },
  toString(){
    return "Nicholas"
  }
}

let person2 = {
  toLocaleString(){
    return "Grigorios"
  },
  toString(){
    return "Greg"
  }
}

let people = [person1,person2]
alert(people)
//Nicholas,Greg

console.log(people.toString())
//Nicholas,Greg

console.log(people.toLocaleString())
//Nikolaos,Grigorios

```

继承的方法`toString()`，`toLocaleString()`都返回数组值的逗号分隔的字符串 ，如果想使用不同的分隔符，则可以使用方法`join()`

`join()`方法接受一个参数，即字符串分隔符，返回包含所有项的字符串。

```javascript
console.log(colors.join('--'))
//red--blue--green

console.log(colors.join("||"))
//red||blue||green
```

如果不给`join()`传入任何参数，或者传入`undefined`,则仍然使用逗号作为分隔符。

**注意：**如果数组中某一项是null或者undefined，则在`join()`，`toLocaleString()`，`toString()`，`valueOf()`返回的结果中会以空字符串表示。



### 栈方法

ECMAScript数组提供了`push()`和`pop()`方法，以实现类似栈的行为。

栈是一种后进先出（LIFO,last-in-first-out)的结构，也就是最近添加的项目先被删除。

`push()`方法接收任意数量的参数，并将它们添加到数组末尾，返回数组的最新长度。

`pop()`方法则用于删除数组的最后一项，同时减少数组的length值，返回被删除的项。

```javascript
let colors = new Array()
let count  = colors.push('red','green')
console.log(count)//2

count = colors.push("black")
console.log(count)//3

let item = colors.pop()
console.log(item)//black
console.log(colors.length)//2
console.log(colors)//['red','green']
```



### 队列方法

就像是以LIFO形式限制访问的书籍结构一样，队列以先进先出（FIFO,first-in-first-out)形式限制访问。

`shift()`：删除数组的第一项并返回它，数组长度减1。

使用`shift()`和`push()`，可以把数组当初队列来使用。

```javascript
let colors = new Array()
let count = colors.push("red","blue","black")
console.log(count)//3

let item = colors.shift()
console.log(item)//red
console.log(colors.length)//2

```

`unshift()`执行跟`shift()`相反的操作：在数组开头添加任意多个值，然后返回新的数组长度。

通过使用`unshift()`和`pop()`可以在相反方向上模拟队列。

```javascript
let colors2 = new Array()
let count2 = colors2.unshift('red','blue','green')
console.log(colors2)//['red','blue','green']
console.log(count2)//3

let item = colors2.pop()
console.log(item)//green
console.log(colors2)//['red','blue']
```

### 排序方法

数组有两个方法可以用来对数组重新排序：

1. `reverse()`：将数组元素反向排列

   ```javascript
   let values = [1,5,10,15]
   values.reverse()
   console.log(values)
   //[ 15, 10, 5, 1 ]
   
   ```

2. `sort()`：按照升序重新排列数组元素，即最小的值在前面，最大的值在后面。`sort（）`会在每一项上调用`toString()`转型函数，然后比较字符串来决定顺序。即使数组中的元素都是数值，也会先把数组转换为字符串再比较，排序。

   ```javascript
   let values2 = [0,1,5,10,15]
   values2.sort()
   console.log(values2)
   //[ 0, 1, 10, 15, 5 ]
   
   ```

   

### 操作方法

1. `concat()`：可以在现有数组全部元素的基础上创建一个新数组。它首先会创建一个当前数组的副本，然后再把它的参数添加到副本末尾，最后返回这个构建的新数组。如果传入一个或多个数组，则`concat()`会把这些数组的每一项都添加到结果数组。如果参数不是数组，则直接把他们添加到结果数组末尾。

   ```javascript
   let a1 = [1,2,3,4,5]
   let a2 = a1.concat('hello','world',[6,7,[8,9]])
   console.log(a1)
   //[ 1, 2, 3, 4, 5 ]
   
   console.log(a2)
   //[ 1, 2, 3, 4, 5, 'hello', 'world', 6, 7, [ 8, 9 ] ]
   
   ```

   打平数组参数的行为可以重写，方法是在参数数组上指定一个特殊的符号：`Symbol.isConcatSpreadable`，这个符号可以阻止打平数组。相反，把这个值设置为`true`可以强制打平类数组对象

   ```javascript
   let colors = ["red","blue","green"]
   let newColors = ["black","brown"]
   let moreNewColors = {
       [Symbol.isConcatSpreadable]:true,
       length:2,
       0:"pink",
       1:"cyan"
   }
   newColors[Symbol.isConcatSpreadable] = false
   
   //强制不打平数组(false)
   let colors2 = colors.concat("yellow",newColors)
   
   //强制打平类数组对象(true)
   let colors3 = colors.concat(moreNewColors)
   
   console.log(colors2)
   //[ 'red','blue','green','yellow',[ 'black', 'brown']]
     
   console.log(colors3)
   //[ 'red', 'blue', 'green', 'pink', 'cyan' ]
   
   
   ```

2. `slice()`：用于创建一个包含原有数组中一个或多个元素的新数组。`slice()`方法可以接收一个或两个参数：返回元素的开始索引和结束索引。如果只有一个参数，则返回该索引到数组末尾的所有元素。如果有两个参数，则返回从开始索引到结束索引对应的所有元素，其中不包含结束索引对应的元素。

   注意：这个操作不影响原始数组。

   ```javascript
   let colors = ["red","green","blue","yellow","purple"]
   let colors2 = colors.slice(1)
   let colors3 = colors.slice(1,4)
   
   console.log(colors)
   //[ 'red', 'green', 'blue', 'yellow', 'purple' ]
   
   console.log(colors2)
   //[ 'green', 'blue', 'yellow', 'purple' ]
   
   console.log(colors3)
   //[ 'green', 'blue', 'yellow' ]
   
   //书上没有说明，但根据个人测试得出以下结论：
   //1.当第一个参数start为负数时，转换为（start+length),若得到的值仍然小于0，将start值作为0处理
   //2.当第二个参数end为负数时，转换为（end + length),若得到的值仍然小于0,slice()方法返回空数组
   //3.如果end值小于start值，返回空数组
   
   ```

3. `splice()`：主要目的是在数组中间插入元素，但有3种不同的方式使用这个方法：

   1. 删除：需要传2个参数：要删除的第一个元素的位置和要删除的元素数量可以从数组中删除人意多个元素。例如：`splice(0,2)`会删除2个元素。
   2. 插入：需要传3个参数：开始位置，0（要删除的元素数量）和要插入的元素。可以在数组中指定的位置插入元素。第三个参数之后还可以传第4个，第5个参数，乃至任意多个要插入的元素。例如：`splice(2,0,'red','blue')`
   3. 替换：传入3个元素：开始位置，要删除的元素数量和要插入的元素。

   ```javascript
   let colors = ['red','green','blue']
   
   //从索引为0的元素开始删除，删除一个元素
   let removed = colors.splice(0,1)
   console.log(colors)//[ 'green', 'blue' ]
   
   console.log(removed)//[ 'red' ]
   
   let people = ["kobe bryant","Stephen","John Lenon"]
   
   //从索引为1的元素开始删除，删除0个，并从该位置依次添加元素
   removed = people.splice(1,0,"Faye","Yang")
   console.log(people)//[ 'kobe bryant', 'Faye', 'Yang', 'Stephen', 'John Lenon' ]
   
   console.log(removed)//[]
   
   let songs = ["Let it go","Innocent","Young and Beautiful"]
   
   //从索引为0的位置开始删除，删除1个元素，并从该位置依次添加元素
   removed = songs.splice(0,1,"Sometime","Paul","July")
   console.log(songs)//[ 'Sometime', 'Paul', 'July', 'Innocent', 'Young and Beautiful' ]
   
   console.log(removed)//[ 'Let it go' ]
   
   ```



### 搜索和位置方法

1. 严格相等

   ECMAScript提供了3个严格相等的搜索办法：`indexOf()`，`lastIndexOf()`，`includes()`。前两个办法在所有版本中都可以用，第三个方法是ECMAScript7中新增的。这些方法都接收两个参数：要查找的元素和一个可选的起始搜索位置。

   ```javascript
   let numbers = [1,2,3,4,5,4,3,2,1]
   
   //inlucdes()和indexOf()从数组开头开始向后搜索
   //lastIndexOf()从数组末尾开始向前搜索
   console.log(numbers.indexOf(4))//3
   console.log(numbers.lastIndexOf(4))//5
   console.log(numbers.includes(4))//true
   
   console.log(numbers.indexOf(4,4))//5
   console.log(numbers.lastIndexOf(4,4))//3
   console.log(numbers.includes(4,7))//false
   
   ```

   `indexOf()`和`lastIndexOf()`都返回要查找的元素在数组中的位置，如果没找到则返回-1.`includes()`返回布尔值，表示是否至少找到一个指定元素匹配的项。在比较第一个参数跟数组每一项时，会使用全等（===）比较。

2. 断言函数

   ECMAScript也允许按照定义的断言函数搜索数组，每个索引都会调用这个函数。

   断言函数接收3个参数：元素，索引和数组本身。其中元素是数组中当前搜索的元素，索引是当前元素的索引，而数组就是正在搜索的数组。断言函数返回真值，表示是否匹配。

   `find()`和`findIndex()`方法使用了断言函数。这两个方法都从数组的最小索引开始。`find()`返回第一个匹配的元素，`findIndex()`返回第一个匹配元素的索引值。这两个方法也都接收第二个可选的参数，用于指定断言函数内部this的值。

   ```javascript
   const people = [
       {
           name:"Matt",
           age:27
       },
       {
           name:"Nicholas",
           age:29
       }
   ]
   console.log(people.find((element,index,array) => element.age<28))
   //{ name: 'Matt', age: 27 }
   
   console.log(people.findIndex((element,index,array) => element.age <28))
   //0
   
   //找到匹配项后，这两个方法都不再继续搜索。
   
   const evens = [2,4,6]
   
   evens.find((element,index,array) => {
       console.log(element)
       console.log(index)
       console.log(array)
       return element === 4
   })
   //2
   //0
   //[ 2, 4, 6 ]
   //4
   //1
   //[ 2, 4, 6 ]
   
   ```

   

### 迭代方法

ECMAScript为数组定义了5个迭代方法。

每个方法接收两个参数：以每一项为参数运行的函数，以及可选的座位函数运行上下文的作用域对象（影响函数中this的值）。

传给每个方法的函数接收3个参数：数组元素，元素索引和数组本身。

数组的5个迭代方法如下：

1. `every()`：对数组每一项都运行传入的函数，如果对每一项函数都返回true,则这个方法返回true。

2. `some()`：对数组每一项都运行传入的函数，如果有一项函数返回true，则这个方法返回true。

3. `filter()`：对数组每一项都运行传入的函数，函数返回true的项会组成数组返回。

4. `map()`：对数组每一项都运行传入的函数，返回每次函数调用的结果构成的数组。

5. `forEach()`：对数组每一项都运行传入的函数，没有返回值。

   ```javascript
   let numbers = [1,2,3,4,5,4,3,2,1]
   
   let everyResult = numbers.every(item => 
       item > 2
   )
   console.log(everyResult)
   //false
   
   let someResult = [1,2,3,4].some(item => 
       item > 2
   )
   console.log(someResult)
   //true
   
   let filterResult = numbers.filter(item => 
       item > 2
   )
   console.log(filterResult)
   //[3,4,5,4,3]
   
   let mapResult = numbers.map(item=>
       item * 2
   )
   console.log(mapResult)
   //[2,4,6,8,10,8,6,4,2]
   let forEachResult = numbers.forEach((item) => {
       if(item > 2)
       console.log(item)
   })
   //3
   //4
   //5
   //4
   //3
   ```



### 归并方法

ECMAScript为数组提供了两个归并方法：`reduce()`和`redecuRight()`，这两个方法都会迭代数组的所有项，并在此基础上构建一个最终返回值。`reduce()`方法从数组第一项开始遍历到最后一项，而`reduceRight()`从最后一项开始遍历到第一项。

这两个方法都接收两个参数：

1. 对每一项都会运行的归并函数
2. （可选）以之为起点的初始值

传给`reduce()`和`reduceRight()`的函数接收4个参数：

1. 上一个归并值
2. 当前项
3. 当前项的索引
4. 数组本身

函数返回的任何值都会作为下一次调用同一个函数的第一个参数。如果没有给这两个方法传入可选的第二个参数（作为归并的起始值），则第一次迭代将从数组的第二项开始，因此传给归并函数的第一个参数是数组的第一项，第二个参数是数组的第二项。

```javascript
let values = [3,4,5,6,7]
let sum = values.reduce((prev,cur,index,array) => prev+cur)
console.log(sum)
//25
let product = values.reduce((prev,cur)=> prev * cur)
console.log(product)
//2520
//究竟是使用reduce()还是reduceRight(),只取决于遍历数组元素的方向。除此之外，这两个方法没什么区别。
```



## 定型数组

定型数组（typed array)是ECMAScript新增的结构，目的是提升向原生库传输数据的效率。实际上，Javascript中并没有“TypedArray"类型，它所指的是一种特殊的包含数值类型的数组。

### 历史

### ArrayBuffer

ArrayBuffer()是一个普通的javascript构造函数，可用于在内存中分配特定数量的字节空间

```javascript
const buf = new ArrayBuffer(16)
//在内存中分配16个字节
console.log(buf.byteLength)
//16
```



## Map

作为ECMAScript6的新增特性，Map是一种新的集合类型，为这门语言带来了真正的键/值存储机制。Map的大多数特性都可以通过Object类型实现，但二者之间还是存在一些细微的差异。具体实践中使用哪一个，还是值得细细甄别。

### 基本API

食用哦`new`关键字和`Map`构造函数可以创建一个空映射。

```javascript
const m = new Map()
```

如果想在创建的同时初始化实例，可以给Map构造函数传入一个可迭代对象，需要包含键/值对数组。可迭代对象中的每个键/值对都会按照迭代顺序插入到新映射实例中。

```javascript
const  m1 = new Map([
    ["key1","value1"],
    ["key2","value2"],
    ["key3","value3"]
])
console.log(m1.size)
//3

```

初始化之后，可以用`set()`方法再添加键值对。

可以使用`get()`和`has()`进行查询，可以通过`size`属性获取映射中的恶键值对的数量。

可以使用`delete()`和`clear()`删除值

```javascript
const m = new Map()

console.log(m.has("firstName"))//false
console.log(m.get("firstName"))//undefined
console.log(m.size)//0

m.set("firstName","Matt")
 .set("lastName","Frisbie")

console.log(m.has("firstName"))//ture
console.log(m.get("firstName"))//Matt
console.log(m.size)//2

m.delete("firstName")

console.log(m.has("firstName"))//false
console.log(m.get("firstName"))//undefined
console.log(m.size)//1

m.clear()

console.log(m.has("firstName"))//false
console.log(m.get("firstName"))//undefined
console.log(m.size)//0
```

与Object只能用数值，字符串或符号作为键不同，Map可以使用任何javascript数据类型作为键。Map内部使用`SameValueZero`比较操作（ECMAScirpt规范内部定义，语言中不能使用），基本傻姑娘相当于使用严格对象相等的标准来检查键的匹配性。与Object类似，映射的值是没有限制的。

## WeakMap



## Set



## WeakSet



## 迭代与扩展操作

