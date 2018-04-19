在我们看别人源码的时候，经常能看到下这两种代码：

```js
function method() {
    'use strict';
    // do something
}
```

```js
(function (){
　　"use strict";
    // do something
})();
```

### 那么这个字符串 **'use strict'** 是做什么用的呢？  
  
  
> 所谓严格模式，顾名思义就是让Javascript在更严格的条件下运行，目的如下；

1. 消除Javascript语法的一些不合理、不严谨之处，减少一些怪异行为;
2. 消除代码运行的一些不安全之处，保证代码运行的安全；
3. 提高编译器效率，增加运行速度；
4. 为未来新版本的Javascript做好铺垫；

像上面的示例代码，进入严格模式只需要在函数内部加上  **use strict** 即可以让该函数进入严格模式，当然，如果你希望整个脚本都在严格模式下运行，你可以在脚本第一行全局加上 **use strict** （注意，这里必须得是脚本文件的第一行） 这个就能让你的整个脚本进入严格模式。

### 那么加了严格模式会不会不兼容其他版本浏览器呢？  

严格模式在高版本的浏览器中遇到 **use strict** 会直接进入严格环境，但是遇到老版本的浏览器，它会把 **use strict** 当成一行普通的字符串，加以忽略，从而进入JS的普通模式，所以不存在浏览器的兼容问题。

### 严格模式下的应用场景
- 不允许未声明的变量被赋值 

有些人喜欢偷懒，比如：

```js
x = 1;
console.log(x)  //1
```
普通模式下有些人喜欢直接给变量名赋值，到了变量都懒得申明的那种（虽然我平时也喜欢这样#滑稽脸），这虽然能够声明一个全局变量，但是到了严格模式，啧啧...

```js
'use strict'
x = 1;  
//Uncaught ReferenceError
```
所以，在严格的模式下，变量必须要声明，let const var 不管你用哪个，总之规则就是这样。
- 禁止使用with  

##### 在我们普通模式下写一个with语句的时候:

```js
!function(){
    var a = {
        x : "hello world !"
    } 
    with(a){
        console.log(a)  //hello world !
    }
}();
```
##### 但是到了严格模式下：

```js
!function(){
    'use strict';
    var a = {
        x : "hello world !"
    } 
    with(a){
        console.log(a)  
        //Uncaught SyntaxError: Strict mode code may not include a with statement
    }
}();
```
- arguments变为参数的静态副本  

#### 普通模式下，这里的a和arguments[0]是有相互的绑定关系的,如果我们修改了argument[0]的值，那么对应的a也会被跟着修改；

```js
!function(a){
    argument[0] = 2;
    console.log(a)
}(1);
// 2
```
#### 但是在严格模式下，arguments已经变成了参数的静态副本，不管你a传或者是不传，都不会和arguments相互影响。

```js
!function(a){
    'use strict';
    argument[0] = 2;
    console.log(a)
}(1);
// 1
```
#### 但是，如果参数a传入的是一个对象的话，那么用arguments修改对象的属性的话，那么还是会和普通模式一样相互影响的。

```js
!function(a){
    'use strict';
    argument[a.hello] = "change world!";
    console.log(a.hello)
}({hello:"hello world!"});
// change world!
```
- delete参数，函数名报错  

在正常的模式下，如果尝试去delete一个参数的话，一般来说是没有什么意义，会返回一个false，并且删除不成功；

```js
!function(a){
    console.log(delete a); 
}(1)
// false
```
但是在严格模式下，如果你这样写，它会直接报一个Uncaught SyntaxError

```js
!function(a){
    'use strict';
    delete a;
}(1)
//Uncaught SyntaxError: Delete of an unqualified identifier in strict mode.
```
- delete不可配置的属性报错  
##### 我一片文章写过 **Object.defineProperty()** 这个方法，里面有三个参数，其中当 **configurable** 的值为 **false** 的时候，说明不可以删除(再次修改)目标属性以及属性的特性（writable, configurable, enumerable），不能被删除或不可以重新设置特性，不能被删除或不能重新设置特性，直接上代码。


```js
//普通模式
!function(a){
    var obj = {};
    Object.defineProperty(obj,"hello",{
        configurable:false
    })
    console.log(delete obj.hello)
}(1);
// false
```
```js
//严格模式
!function(a){
    'use strict';
    var obj = {};
    Object.defineProperty(obj,"hello",{
        configurable:false
    })
    console.log(delete obj.hello)
}(1);
// Uncaught TypeError
```
- 禁止八进制字面量  

这个较为好理解，直接上代码

```js
//普通模式
!function(){
    console.log(0123)
}()
// 83
```
```js
//严格模式
!function(){
    'use strict';
    console.log(0123);
}()
// Uncaught SyntaxError: Octal literals are not allowed in strict mode.
```
- eval独立作用域  


```js
//普通模式
!function(){
    eval('var evalVal = 2;')
    console.log(typeof evalVal);
}();
// number
```

```js
//严格模式
!function(){
    'use strict';
    eval('var evalVal = 2;')
    console.log(typeof evalVal);
}();
// undefined
```
#### 其实严格模式下还有许多属于它自己的规则，总的来说严格模式它就是一种特殊的运行模式，修复了部分语言上的不足，提供了更强的错误检查，并且增强了安全性。











 
