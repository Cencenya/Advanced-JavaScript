# 理解JavaScript 中的执行上下文和执行栈
### 定义
执行上下文：在运行JavaScript代码时由JavaScript引擎创建的一个环境。这个环境决定了代码在执行时变量如何被访问以及如何被求值。

### 执行上下文的类型
 * **全局执行上下文`GlobalExectionContext`**：只有一个，浏览器中的全局对象就是indow对象，`this`指向这个全局对象。
 * **函数执行上下文`FunctionExectionContext`**:存在无数个，只有函数被调用的时候才会被创建，每次调用函数都会创建一个新的执行上下文。
 * **Eval函数执行上下文**：指的是运行在 eval 函数中的代码，很少用而且不建议使用。

```js

GlobalExectionContext = {  // 全局执行上下文
  LexicalEnvironment: {    	  // 词法环境
    EnvironmentRecord: {   		// 环境记录
      Type: "Object",      		   // 全局环境
      // 标识符绑定在这里 
      outer: <null>  	   		   // 对外部环境的引用
  }  
}

FunctionExectionContext = { // 函数执行上下文
  LexicalEnvironment: {  	  // 词法环境
    EnvironmentRecord: {  		// 环境记录
      Type: "Declarative",  	   // 函数环境
      // 标识符绑定在这里 			  // 对外部环境的引用
      outer: <Global or outer function environment reference>  
  }  
}
```
  
### 执行上下文的组成
* **变量对象（Varible Object VO）**:存储着上下文中所有的变量、函数声明以及函数参数。函数中的参数也被存储在变量对象中。对于函数执行上下文来说，变量对象也被称为活动对象（Activation Object，AO）。
* **作用域链（Scope Chain）**：每个执行上下文都有一个与之关联的作用域链，它是用于解析变量的一个对象列表。作用域链的前端是当前执行上下文的变量对象。当访问一个变量时，Js引擎首先查找当前执行上下文的变量对象，如果找不到，就会沿着作用域链向上查找知道找到该变量或者到达全局执行上下文的变量对象。
* **this Bind**：在上下文中，有一个特殊的关键字this，它在代码执行过程中可能指向不同的对象。在全局执行上下文中，this通常指向全局对象（浏览器中是window）。在函数执行上下文中，this的值取决于函数是如何被调用的。如果它是一个方法，this通常指向调用它的对象。
  
### 执行栈


### 执行上下文的创建