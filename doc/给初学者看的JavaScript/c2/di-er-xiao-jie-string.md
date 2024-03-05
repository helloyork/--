# 第二小节 - String

### 给初学者看的JavaScript

![](https://news-cdn.softpedia.com/images/news2/ecmascript-2016-new-version-of-the-javascript-language-released-505625-2.jpg)

\
\


## 第三期 - 第二章 · 基元类型 · 第二小节：String

#### 语言

语言是人类极其重要的一个交流组成部分，这使得人类能够更方便快捷的提供信息

当人们交流信息的时候，文字总是我们最佳的交流方式，就如JavaScript本身，就是通过解析文本并且解释来执行逻辑语句

而JavaScript则为我们提供了处理文本的方案：字符串String

### 第二节 · String

#### 1. 基础概念

在JavaScript中，我们能通过单引号，双引号和反引号来定义字面量字符串

> 概念：字面量是什么？\
> 字面量指的是在程序中直接写出来的字面上的量，例如：`1`和`"abc"`就是字面量

例如：

```javascript
let MyFirstString = "我是一个字符串！";
let MySecondString = '我也是一个字符串！';
let MyThirdString = `我同样是一个字符串！`;

console.log(MyFirstString); // "我是一个字符串！"
```

但是请注意，不同引号之间允许套娃，但是不允许同种引号的套娃，例如：

```javascript
"你知道单引号吗，单引号长成这样：' ，怎么样，你看见了吗"; // 没有错误
"你知道双引号长啥样嘛，其实长成这样："，怎么样，看见了吗？"; // 出现了错误
```

这是因为你不能直接将同种引号套在同种引号之下，如果你想要显示同种引号，你需要字符：\来转义（详见未来的章节），例如：

```javascript
"你知道双引号长啥样嘛，其实长成这样：\"，怎么样，看见了吗？"; // 没有错误
console.log(" \" "); // " " "
```

引号必须成对存在，不能使用被转义的引号作为结束：

```javascript
"你好！\"; // 出现了错误
```

> 扩展：`\`可以转义很多字符，如果你想要输出这个反斜杠，可以用反斜杠来转义反斜杠：`console.log('\\'); // "\"`

同时，我们能用加号来拼接字符串，例如：

```javascript
let stringA = "A";
let stringB = "b";

console.log(stringA + stringB); // Ab
```

\


#### 2. String构造器

String构造器能够在没有new的情况下使用，当没有new的时候，其行为模式与函数一样:

```javascript
let MyFirstString = new String("a string"); // 'a string'
let MySecondString = String("a string"); // 'a string'
```

> 但是，包含或不包含new之间存在一定差异；**划重点!** 当带有new的构造器函数模式下实例化的时候，会获得一个String对象，而没有new的函数模式下运行的时候，返回的是一个字符串基元类型

这可能很难理解，但是让我们看一个例子:

```javascript
new String("nOmEn"); // [String: 'nOmEn']
String("nOmEn"); // 'nOmEn'
"nOmEn"; // 'nOmEn'
```

看出来了吗？当带有new的时候，我们获得的是一个对象类型的字符串，而没有，则获得一个普通的基元字符串

> 扩展：这是因为创建时，String构造函数返回了一个String的实例

而我们可以用一些方法来证明他们的区别:

```javascript
new String("nOmEn") === new String("nOmEn"); // false，因为实例的地址不一样
String("nOmEn") === String("nOmEn"); // true，因为基元字符串之间只判断值

let StringWithNew = new String("nOmEn");
StringWithNew.awa = 1;
console.log(StringWithNew.awa); // 1

let StringWithoutNew = String("nOmEn");
StringWithoutNew.awa = 1;
console.log(StringWithoutNew.awa); // undefined
```

> 扩展：如上述示例，大家肯定发现了对象String能够赋予字段，而基元String不一样
>
> 这是因为基元String不是一个对象，而实例String能够有自己的字段\
> 那为什么即使基元String不能拥有自己的字段，我们还可以调用其上面的方法呢？例如`"qwq".startsWith("q")`？这是因为基元String拥有一套包装器机制，这一套机制能够为基元String调用包装器上的方法，然后调用完毕之后String的包装器立即销毁，故此，被赋予到包装器上的字段被立即销毁了（详见JavaScript进阶中的包装器一章）

而String函数可以更稳定的将数值转换为字符串，并且不会出现报错，例如:

```javascript
String(Symbol("awa")); // 'Symbol(awa)'
String({}); // '[object Object]'
String(3); // '3'
```

\


#### 3. 不可修改的String?

那么既然是Nomen写的教程，就不可避免地会出现一些可能的高级知识，这就叫做特性（？

在JavaScript中，字符串在被创建之后就是不可变的，这意味着你无法修改这个字符串的值，那为什么我们可以修改变量的值呢？这是因为JavaScript自动创建了一个新的字符串，然后修改这个变量的引用，例如:

```javascript
let AString = "aa";
let BString = "bb";
AString = AString + BString; // aabb
```

在这上面中，JavaScript创建了一个字符串aa和一个字符串bb，然后创建一个长度为4（也就是aa的长度加上bb的长度的和）的字符串，填充aa和bb，然后将AString的引用改为新的字符串;

\


#### 4. 模板字符串

ES6新增了很多语言都会有的带有插值的字符串，这在JavaScript中被称为模板字符串

模板字符串允许我们在声明模板字符串字面量时带有表达式插值和换行，而表达式内的内容在字符串被创建的时候按照字符串的顺序被求值，例如：

```javascript
let worldString = "world";
let TemplateString = `hello ${worldString}!`;
console.log(TemplateString); // hello world!
```

模板字符串还会保留声明时的换行

```javascript
let TemplateString = `hello!
world!
by
Nomen`;
console.log(TemplateString); // hello!
                             // world!
                             // by
                             // Nomen
```

注意，模板字符串也会保留声明的时候的缩进，有时在代码中看起来格式化正确的字符串打印出来会变得奇怪;

\


#### 5. 字符串属性与方法

在JavaScript中，内置了很多字符串处理的方法

每一个字符串本身就有一个length属性，用于表示这个字符串的长度;

```javascript
console.log("awa".length); // 3
```

也有很多的方法用于处理字符串，但是请注意，他们中的大部分都是返回一个新的，经过处理的字符串，而不会修改原来的字符串，例如:

```javascript
let myString = "awa";
myString.slice(1); // 'wa'
console.log(myString); // 'awa'，因为slice方法返回新字符串，不会修改原来的字符串
```

`indexOf` 方法返回指定文本在字符串中首次出现的索引，如果未找到则返回 -1。 `lastIndexOf` 方法返回指定文本在字符串中最后一次出现的索引，如果未找到则返回 -1。

slice() 方法从字符串中提取一个子字符串并返回它。这个方法接受两个参数，分别是子字符串开始和结束的位置。

```javascript
let MyString = "Hello, World!";
console.log(MyString.slice(0, 5)); // "Hello"
console.log(MyString.slice(7, 12)); // "World"
```

\


#### 6. 小节

在本章中，我们浅浅探讨了一下String的特性，构造器和模板字符串，如果你想要了解更多有关String本身方法，你可以访问[MDN技术社区](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global\_Objects/String)

那么，我是Nomen，我们下期不见不散！

欢迎来Nomen小队唠嗑！`2418207411`

提示：如果你想要点击教程中的链接，你可以在github仓库：helloyork/york-javascript-tutorials 中找到教程的md源文件！

> 信息来源：
>
> https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global\_Objects/String\
> https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/String/String#return\_value\
> https://zhuanlan.zhihu.com/p/309194559\
> 《JavaScript高级程序设计（第4版）》
