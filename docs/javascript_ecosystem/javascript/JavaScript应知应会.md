# 术语

- DOM（Document Object Model）文档对象模型
- JSON（JavaScript Object Notation）JavaScript对象符号（本质是字符串）
- AJAX（Asynchronous JavaScript and XML）异步的 JavaScript 和 XML。AJAX 最大的优点是在不重新加载整个页面的情况下，可以与服务器交换数据并更新部分网页内容。AJAX 只能向同源网址（协议、域名、端口都相同）发出 HTTP 请求，如果发出跨域请求，就会报错。
- NaN（Not a Number）非数
- BOM（Browser Object Model）浏览器对象模型
- ECMA（European Computer Manufacturers Association）欧洲计算机制造商协会
- SPA（single-page app framework）单页面应用程序框架
- ECMAScript 版本

  ECMAScript 6 也称为 ECMAScript 2015。

  ECMAScript 7 也称为 ECMAScript 2016。

  | 年份 | 名称           | 描述                                              |
  | :--- | :------------- | :------------------------------------------------ |
  | 1997 | ECMAScript 1   | 第一个版本                                        |
  | 1998 | ECMAScript 2   | 版本变更                                          |
  | 1999 | ECMAScript 3   | 添加正则表达式 添加 try/catch                     |
  |      | ECMAScript 4   | 没有发布                                          |
  | 2009 | ECMAScript 5   | 添加 "strict mode"，严格模式 添加 JSON 支持       |
  | 2011 | ECMAScript 5.1 | 版本变更                                          |
  | 2015 | ECMAScript 6   | 添加类和模块；ES6 新增了箭头函数。                |
  | 2016 | ECMAScript 7   | 增加指数运算符 (**) 增加 Array.prototype.includes |

- CORS（Cross-origin resource sharing）跨源资源共享



# ES5 基础

## 数据类型

- 对象采用大括号表示，如果行首是一个大括号，则

  ```javascript
  // 代码块
  { foo: 123 }
  
  // 表达式，加上 () ，括号内的是对象
  ({ foo: 123 })
  ```

- 对象属性可以动态创建，不必在对象声明时就指定

  ```javascript
  var obj = {};
  obj.foo = 123;
  obj.foo // 123
  ```

- 可以在文本字符串中使用反斜杠对代码行进行换行

  ```javascript
  document.write("你好 \
  世界!");
  ```

- === 为绝对相等，即数据类型与值都必须相等。

- 所谓 Base64 就是一种编码方法，可以将任意值转成 0～9、A～Z、a-z、`+`和`/`这64个字符组成的可打印字符。使用它的主要目的，不是为了加密，而是为了不出现特殊字符，简化程序的处理。

- 函数的声明方式

  ```javascript
  // function 命令
  function print(s) {
    console.log(s);
  }
  
  // 函数表达式，将一个匿名函数赋值给变量
  var print = function(s) {
    console.log(s);
  };
  
  // Function 构造函数(无人使用)
  var add = new Function(
    'x',
    'y',
    'return x + y'
  );
  ```

- 函数作用域（**ES5**）

  - 全局作用域，变量在整个程序中一直存在，所有地方都可以读取（全局变量）
    - 在其他区块中声明，一律都是全局变量。如 if 区块。
  - 函数作用域，变量只在函数内部存在（局部变量）
    - 函数内部定义的变量，会在该作用域内覆盖同名全局变量。

- 函数本身也是一个值，也有自己的作用域。它的作用域与变量一样，就是其声明时所在的作用域，与其运行时所在的作用域无关。

- 闭包：**就是函数内部定义的函数**，其被返回了出去并在外部调用，即能够访问函数内部变量的函数（**JavaScript 语言特有的"链式作用域"结构（chain scope），子对象会一级一级地向上寻找所有父对象的变量。所以，父对象的所有变量，对子对象都是可见的，反之则不成立**）。

  -  作用
     -  可以读取外层函数内部的变量
     -  让这些变量始终保持在内存中，即闭包可以使得它诞生环境一直存在
     -  封装对象的私有属性和私有方法
  -  闭包过度使用会导致性能问题。闭包会导致内存泄露（javascript 内部的垃圾回收机制用的是引用计数收集）。解决内存泄露方案：
     -  使用严格模式，避免不经意间的全局变量泄露
     -  关注 DOM 生命周期，在销毁阶段记得解绑相关事件
     -  避免过度使用闭包

- 立即调用的函数表达式

  根据 JavaScript 的语法，圆括号()跟在函数名之后，表示调用该函数。比如，print()就表示调用print函数。不能在函数的定义（语句，function出现在行首）之后加上圆括号，这会产生语法错误。当作表达式时，函数可以定义后直接加圆括号调用。

  ```javascript
  // 表达式
  var f = function f(){ return 1}();
  
  // 表达式
  (function(){ /* code */ }());
  
  // 表达式
  (function(){ /* code */ })();
  ```



## 运算符

- javascript:void(0) 中最关键的是 void 关键字， void 是 JavaScript 中非常重要的关键字，该操作符指定要计算（执行）一个表达式但是不返回值。void(0) 计算为 0， Javascript 没有任何效果，即阻止默认行为（防止网页跳转）。

  ```javascript
  void func()
  javascript:void func()
  
  // 建议加括号
  void(func())
  javascript:void(func())
  ```

- 逗号运算符，先执行逗号之前的操作，然后返回逗号后面的值。

  ```javascript
  'a', 'b' // "b"
  
  var x = 0;
  var y = (x++, 10);
  x // 1
  y // 10
  ```

- 圆括号 ()

  - 把表达式放在圆括号之中，提升运算的优先级，不求值
    - 函数放在圆括号中，会返回函数本身
    - 圆括号之中，只能放置表达式，如果将语句放在圆括号之中，就会报错
  - 跟在函数的后面，作用是调用函数



## 浏览器模型

- 只能在 HTML 输出中使用 document.write。如果在文档加载后使用该方法，会覆盖整个文档。



## 编程风格

- 通常使用 4 个空格符号来缩进代码块。不推荐使用 TAB 键来缩进，因为不同编辑器 TAB 键的解析不一样。
- HTML 语言的属性值使用双引号，约定 JavaScript 语言的字符串只使用单引号。
- 不要使用 with 语句，会发生混淆。



## 标准库

- Number、String和Boolean 这三个对象作为**构造函数**使用（带有new）时，可以将原始类型的值转为对象；作为普通函数使用时（不带有new），可以将任意类型的值，转为原始类型的值。

- 正则表达式

  - 新建正则表达式

    ```javascript
    // 字面量，以斜杠表示开始和结束
    // 在引擎编译代码时，就会新建正则表达式，效率更高
    var regex = /xyz/;
    
    // 使用RegExp构造函数
    // 在运行时新建
    var regex = new RegExp('xyz');
    ```

  - 正则表达式实例属性

    - 修饰符相关
      - `RegExp.prototype.ignoreCase`：返回一个布尔值，表示是否设置了`i`修饰符。
      - `RegExp.prototype.global`：返回一个布尔值，表示是否设置了`g`修饰符。
      - `RegExp.prototype.multiline`：返回一个布尔值，表示是否设置了`m`修饰符。
      - `RegExp.prototype.flags`：返回一个字符串，包含了已经设置的所有修饰符，按字母排序。
    - 与修饰符无关
      - `RegExp.prototype.lastIndex`：返回一个整数，表示下一次开始搜索的位置。该属性可读写，但是只在进行连续搜索时有意义。
      - `RegExp.prototype.source`：返回正则表达式的字符串形式（不包括反斜杠），该属性只读。

  - 正则表达式实例方法

    - RegExp.prototype.test()，正则实例对象的`test`方法返回一个布尔值，表示当前模式是否能匹配参数字符串。
    - RegExp.prototype.exec()，用来返回匹配结果。如果发现匹配，就返回一个数组，成员是匹配成功的子字符串，否则返回null。

  - 字符串的实例方法

    - `String.prototype.match()`：返回一个数组，成员是所有匹配的子字符串。
    - `String.prototype.search()`：按照给定的正则表达式进行搜索，返回一个整数，表示匹配开始的位置。如果没有任何匹配，则返回-1。
    - `String.prototype.replace()`：按照给定的正则表达式进行替换，返回替换后的字符串。
    - `String.prototype.split()`：按照给定规则进行字符串分割，返回一个数组，包含分割后的各个成员。

  - 匹配规则

    - 字面量字符和元字符

      - 点字符（.）匹配除回车（\r）、换行(\n) 、行分隔符（\u2028）和段分隔符（\u2029）以外的所有字符。注意，对于码点大于0xFFFF字符，点字符不能正确匹配，会认为这是两个字符。
      - 位置字符用来提示字符所处的位置。
        - ^ 表示字符串的开始位置
        - $ 表示字符串的结束位置
      - 竖线符号（|）在正则表达式中表示“或关系”（OR），即cat|dog表示匹配cat或dog。

    - 转义符

      需要反斜杠转义的，一共有12个字符：^、.、[、$、(、)、|、*、+、?、{和\。需要特别注意的是，如果使用RegExp方法生成正则对象，转义需要使用两个斜杠，因为字符串内部会先转义一次。

    - 特殊字符

      - `\cX` 表示`Ctrl-[X]`，其中的`X`是A-Z之中任一个英文字母，用来匹配控制字符。
      - `[\b]` 匹配退格键(U+0008)，不要与`\b`混淆。
      - `\n` 匹配换行键。
      - `\r` 匹配回车键。
      - `\t` 匹配制表符 tab（U+0009）。
      - `\v` 匹配垂直制表符（U+000B）。
      - `\f` 匹配换页符（U+000C）。
      - `\0` 匹配`null`字符（U+0000）。
      - `\xhh` 匹配一个以两位十六进制数（`\x00`-`\xFF`）表示的字符。
      - `\uhhhh` 匹配一个以四位十六进制数（`\u0000`-`\uFFFF`）表示的 Unicode 字符。

    - 字符类 []

      - 一系列字符可供选择，只要匹配其中一个就可以了。所有可供选择的字符都放在方括号内。
      - 脱字符（^）。如果方括号内的第一个字符是[^]，则表示除了字符类之中的字符，其他字符都可以匹配。如果方括号内没有其他字符，即只有[^]，就表示匹配一切字符，其中包括换行符。相比之下，点号作为元字符（.）是不包括换行符的。
      - 连字符（-）。连字符（-）用来提供简写形式，表示字符的连续范围。比如，[abc]可以写成[a-c]，[0123456789]可以写成[0-9]，同理[A-Z]表示26个大写字母。

    - 预定义模式

      - `\d` 匹配0-9之间的任一数字，相当于`[0-9]`。
      - `\D` 匹配所有0-9以外的字符，相当于`[^0-9]`。
      - `\w` 匹配任意的字母、数字和下划线，相当于`[A-Za-z0-9_]`。
      - `\W` 除所有字母、数字和下划线以外的字符，相当于`[^A-Za-z0-9_]`。
      - `\s` 匹配空格（包括换行符、制表符、空格符等），相等于`[ \t\r\n\v\f]`。
      - `\S` 匹配非空格的字符，相当于`[^ \t\r\n\v\f]`。
      - `\b` 匹配词的边界。（词必须独立）
      - `\B` 匹配非词边界，即在词的内部。（没有明显边界分割，是一个词）

    - 重复类 {}

      模式的精确匹配次数，使用大括号（{}）表示。{n}表示恰好重复n次，{n,}表示至少重复n次，{n,m}表示重复不少于n次，不多于m次。

    - 量词符

      - 贪婪模式：默认情况下都是最大可能匹配，即匹配到下一个字符不满足匹配规则为止
        - ? 问号表示某个模式出现0次或1次，等同于{0, 1}。 
        - \* 星号表示某个模式出现0次或多次，等同于{0,}。 
        - \+ 加号表示某个模式出现1次或多次，等同于{1,}。
      - 非贪婪模式：一旦条件满足，就不再往下匹配
        - +?：表示某个模式出现1次或多次，匹配时采用非贪婪模式。
        - *?：表示某个模式出现0次或多次，匹配时采用非贪婪模式。
        - ??：表格某个模式出现0次或1次，匹配时采用非贪婪模式。

    - 修饰符

      ```javascript
      var regex = new RegExp('xyz', 'i');
      // 等价于
      var regex = /xyz/i;
      ```

      - g 默认情况下，第一次匹配成功后，正则对象就停止向下匹配了。g 修饰符表示全局匹配（global），加上它以后，正则对象将匹配全部符合条件的结果，主要用于搜索和替换。

      - i 默认情况下，正则对象区分字母的大小写，加上 i 修饰符以后表示忽略大小写（ignoreCase）。

      - m 多行模式（multiline），会修改^和$的行为。默认情况下（即不加m修饰符时），^和$匹配字符串的开始处和结尾处，加上m修饰符以后，^和$还会匹配行首和行尾，即^和$会识别换行符（\n）。

        ```javascript
        // 如果不加m修饰符，就相当于b只能处在字符串的开始处。加上m修饰符以后，换行符\n也会被认为是一行的开始。
        // b 是第二行的起始字符
        /^b/m.test('a\nb') // true
        ```



- JSON

  JSON 对值的类型和格式有严格的规定

  - 复合类型的值只能是数组或对象，不能是函数、正则表达式对象、日期对象。
  - 原始类型的值只有四种：字符串、数值（必须以十进制表示）、布尔值和`null`（不能使用`NaN`, `Infinity`, `-Infinity`和`undefined`）。
  - 字符串必须使用双引号表示，不能使用单引号。
  - 对象的键名必须放在双引号里面。
  - 数组或对象最后一个成员的后面，不能加逗号。

  以下不合法

  ```javascript
  { name: "张三", 'age': 32 }  // 属性名必须使用双引号
  
  [32, 64, 128, 0xFFF] // 不能使用十六进制值
  
  { "name": "张三", "age": undefined } // 不能使用 undefined
  
  { "name": "张三",
    "birthday": new Date('Fri, 26 Aug 2011 07:13:10 GMT'),
    "getName": function () {
        return this.name;
    }
  } // 属性值不能使用函数和日期对象
  ```

  注意，`null`、空数组和空对象都是合法的 JSON 值。



## 面向对象编程

- 典型的面向对象编程语言（比如 C++ 和 Java），都有“类”（class）这个概念。所谓“类”就是对象的模板，对象就是“类”的实例。但是，JavaScript 语言的对象体系，不是基于“类”的，而是**基于构造函数（constructor）和原型链（prototype）**。

  JavaScript 语言使用构造函数（constructor）作为对象的模板。所谓”构造函数”，就是专门用来生成实例对象的函数。它就是对象的模板，描述实例对象的基本结构。一个构造函数，可以生成多个实例对象，这些实例对象都有相同的结构。

  构造函数就是一个普通的函数，但具有自己的特征和用法。

  - 函数体内部使用了**this**关键字（必须有），代表了所要生成的对象实例。
  - 生成对象的时候，必须使用**new**命令。

  ```javascript
  // Vehicle就是构造函数。为了与普通函数区别，构造函数名字的第一个字母通常大写
  var Vehicle = function () {
    'use strict';	// 避免忘记写 new，导致price变成全局变量；即 函数内部的this不能指向全局对象
    this.price = 1000;
  };
  
  // new命令的作用，就是执行构造函数，返回一个实例对象。
  var v = new Vehicle();
  v.price // 1000
  ```



- 绑定 this 的方法

  call，apply 本质是通过新对象实例作为参数传递到函数中，改变 this 的指向，并立即执行。

  - func.call(thisValue, arg1, arg2, ...)，call 的参数可以指定 this 对象。

    ```javascript
    var obj = {};
    
    var f = function () {
      return this;
    };
    
    f() === window // true
    // 立即执行
    f.call(obj) === obj // true
    ```

  - func.apply(thisValue, [arg1, arg2, ...])，apply方法的作用与call方法类似，也是改变this指向，然后再调用该函数。唯一的区别就是，它接收一个数组作为函数执行时的参数。

    ```javascript
    function f(x, y){
      console.log(x + y);
    }
    
    f.call(null, 1, 1) // 2
    // 立即执行
    f.apply(null, [1, 1]) // 2
    ```

  - func.bind(thisValue)，绑定指定对象到 this，并返回一个新函数。

- 对象的继承

  - 构造函数 + this + new（属性、方法不共享）
  - 构造函数.prototype.x = 属性、方法（所有**实例对象**共享**原型对象prototype**的属性、方法）

- 构造函数的继承

  ```javascript
  function Shape() {
    this.x = 0;
    this.y = 0;
  }
  
  Shape.prototype.move = function (x, y) {
    this.x += x;
    this.y += y;
    console.info('Shape moved.');
  };
  
  // 
  // 第一步，子类继承父类的实例
  function Rectangle() {
    Shape.call(this); // 调用父类构造函数
  }
  
  // 第二步，子类继承父类的原型
  Rectangle.prototype = Object.create(Shape.prototype);
  Rectangle.prototype.constructor = Rectangle;
  
  //
  
  var rect = new Rectangle();
  rect instanceof Rectangle  // true
  rect instanceof Shape  // true
  ```



- 模块

  ```javascript
  // 外部代码无法读取内部的_count变量
  var module1 = (function () {
  　var _count = 0;
  　var m1 = function () {
  　  //...
  　};
  　var m2 = function () {
  　　//...
  　};
  　return {
  　　m1 : m1,
  　　m2 : m2
  　};
  })();	// 立即执行函数
  ```



- Object 对象的相关方法

  - Object.getPrototypeOf()

    返回参数对象的原型

    ```javascript
    var F = function () {};
    var f = new F();
    Object.getPrototypeOf(f) === F.prototype // true
    
    // 空对象的原型是 Object.prototype
    Object.getPrototypeOf({}) === Object.prototype // true
    
    // Object.prototype 的原型是 null
    Object.getPrototypeOf(Object.prototype) === null // true
    
    // 函数的原型是 Function.prototype
    function f() {}
    Object.getPrototypeOf(f) === Function.prototype // true
    ```

  

  - Object.setPrototypeOf()

    为参数对象设置原型，返回该参数对象。它接受两个参数，第一个是现有对象，第二个是原型对象。

    ```javascript
    var a = {};
    var b = {x: 1};
    Object.setPrototypeOf(a, b);
    
    Object.getPrototypeOf(a) === b // true
    a.x // 1
    ```

  

  - Object.create()

    该方法接受一个对象作为参数，然后以它为原型，返回一个实例对象。该实例完全继承原型对象的属性。

    Object.create()方法生成的新对象，动态继承了原型。在原型上添加或修改任何方法，会立刻反映在新对象之上。

    Object.create()方法生成的对象，继承了它的原型对象的构造函数。

    ```javascript
    // 原型对象
    var A = {
      print: function () {
        console.log('hello');
      }
    };
    
    // 实例对象
    var B = Object.create(A);
    
    Object.getPrototypeOf(B) === A // true
    B.print() // hello
    B.print === A.print // true
    ```

    

# ES6
