# 术语

- DOM（Document Object Model）文档对象模型
- JSON（JavaScript Object Notation）JavaScript对象符号（本质是字符串）
- AJAX（Asynchronous JavaScript and XML）异步的 JavaScript 和 XML。AJAX 最大的优点是在不重新加载整个页面的情况下，可以与服务器交换数据并更新部分网页内容
- NaN（Not a Number）非数
- BOM（Browser Object Model）浏览器对象模型



# 基础

- 只能在 HTML 输出中使用 document.write。如果在文档加载后使用该方法，会覆盖整个文档。

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

- 可以在文本字符串中使用反斜杠对代码行进行换行

  ```javascript
  document.write("你好 \
  世界!");
  ```

- === 为绝对相等，即数据类型与值都必须相等。

- `var`、`let`、`const`

  -  `var` 声明是全局作用域或函数作用域，而 `let` 和 `const` 是块作用域。
  -  `var` 变量可以在其作用域内更新和重新声明；`let` 变量可以更新但不能重新声明；`const` 变量既不能更新也不能重新声明。
  -  它们都被提升到了作用域的顶部。但是，`var` 变量是用 `undefined` 初始化的，而 `let` 和 `const` 变量不会被初始化。
  -  `var` 和 `let` 可以在不初始化的情况下声明，而 `const` 必须在声明时初始化。

- javascript:void(0) 中最关键的是 void 关键字， void 是 JavaScript 中非常重要的关键字，该操作符指定要计算一个表达式但是不返回值。void(0) 计算为 0， Javascript 没有任何效果，即阻止默认行为。

  ```javascript
  void func()
  javascript:void func()
  
  void(func())
  javascript:void(func())
  ```

- 通常使用 4 个空格符号来缩进代码块。不推荐使用 TAB 键来缩进，因为不同编辑器 TAB 键的解析不一样。

- 在 JavaScript 中函数是对象。JavaScript 函数有它的属性和方法。call() 和 apply() 是预定义的函数方法。两个方法可用于调用函数，两个方法的第一个参数必须是对象本身，在 JavaScript 严格模式(strict mode)下，在调用函数时第一个参数会成为 this 的值， 即使该参数不是一个对象。通过 call() 或 apply() 方法你可以设置 this 的值，且作为已存在对象的新方法调用。

  apply传入的是一个参数数组，也就是将多个参数组合成为一个数组传入，而call则作为call的参数传入（从第二个参数开始）。

- javascript 中大部分情况下，只有两种作用域类型：

  -  全局作用域：全局作用域为程序的最外层作用域，一直存在。
  -  函数作用域：函数作用域只有函数被定义时才会创建，包含在父级函数作用域 / 全局作用域内。

  由于作用域的限制，每段独立的执行代码块只能访问自己作用域和外层作用域中的变量，无法访问到内层作用域的变量。

  - 块级作用域呢，花括号内 {...} 的区域就是块级作用域区域。ES6 标准提出了使用 let 和 const 代替 var 关键字，来“创建块级作用域”。

- 闭包：就是函数内部定义的函数，被返回了出去并在外部调用，能够访问其函数内部变量的函数（向上查找父级函数作用域的变量）。

  -  应用场景：单例模式；模拟私有属性；柯里化；
  -  闭包过度使用会导致性能问题。闭包会导致内存泄露（javascript 内部的垃圾回收机制用的是引用计数收集）。解决内存泄露方案：
     -  使用严格模式，避免不经意间的全局变量泄露
     -  关注 DOM 生命周期，在销毁阶段记得解绑相关事件
     -  避免过度使用闭包