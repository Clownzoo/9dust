> Object.defineProperty()在IE9及IE9以上才被支持，它接受三个参数，而且都是必填的。


1. 第一个参数:目标对象
2. 第二个参数:需要定义的属性或方法的名字
3. 第三个参数:目标属性所拥有的特性;（descriptor）  
### descriptor  
*descriptor这里我们统称是Object.defineProperty()这个方法的第三个参数，并且它拥有以下的取值*  

- value

```js
var obj = {};
Object.defineProperty(obj,"hello",{
    value:"hello"
})
console.log(obj)  //{hello:"hello"}

//这个参数较为好理解，如果说第一个参数是一个对象A，那么第二个参数则为对象A的一个属性B，那么value即为属性B的一个值;
```
- writable

```js
var obj = {};
Object.defineProperty(obj,"hello",{
    value : "hello",
    writable : false
    //writable有两个值可选 false(不可被重写)，true(可以被重写)
})
console.log(obj.hello)   //hello
obj.hello = "hello world";  //重新定义obj.hello的值
console.log(obj.hello)  //hello 

```

- configurable

```js
/**
* @see：【总开关】
* @see：定义是否可以删除(再次修改)目标属性以及属性的特性（writable, configurable, enumerable）
* @see：true[可以被删除或可以重新设置特性]
* @see：false[不能被可以被删除或不可以重新设置特性] 默认为false
*/

/*--- false情况下删除属性 ---*/
var obj = {};
Object.defineProperty(obj,"hello",{
    value:"hello",
    configurable:false,
    writable:false
})
console.log(obj.hello)  //hello
delete obj.hello;
console.log(obj.hello)  //hello

/*--- true情况下删除属性 ---*/
var obj = {};
Object.defineProperty(obj,"hello",{
    value:"hello",
    configurable:true,
    writable:false
})
console.log(obj.hello)  //hello
delete obj.hello;
console.log(obj.hello)  //undefined

/*--- false情况下修改特性 ---*/
var obj = {};
Object.defineProperty(obj,"hello",{
    value:"hello",
    configurable:false,
    writable:false
})
//重新修改特性
Object.defineProperty(obj,"hello",{
    value:"hello",
    writable:true,
    configurable:true
});
console.log(obj.hello)  //Uncaught TypeError: Cannot redefine property: hello

/*--- true情况下修改特性 ---*/
var obj = {};
Object.defineProperty(obj,"hello",{
    value:"hello",
    configurable:true,
    writable:true
})
//重新修改特性
Object.defineProperty(obj,"hello",{
    value:"hello",
    writable:false,
    configurable:false
});
console.log(obj.hello)  //hello
```


- enumerable

```js
/**
* @see：使用for...in或Object.keys()
* @see：true[可以被枚举]
* @see：false[不能被枚举] 默认为false
*/

/*--- false情况下不能被枚举 ---*/
var obj = {};
Object.defineProperty(obj,"hello",{
    value:"hello",
    enumerable:false
});
for(item in obj){
    console.log(item)
}
// undefined

/*--- true情况下可以被枚举 ---*/
var obj = {};
Object.defineProperty(obj,"hello",{
    value:"hello",
    enumerable:true
});
for(item in obj){
    console.log(item)
}
// hello
```
 **注意**：一旦使用Object.defineProperty给对象添加属性，那么如果不设置属性的特性，那么configurable、enumerable、writable这些值都为默认的false

```js
var obj = {};
Object.defineProperty(obj,'hello',{
    value:"hello"
});
//定义的新属性后，这个属性的特性中configurable，enumerable，writable都为默认的值false
```
- 存取器 get/set

```js
var obj = {};
Object.defineProperty(obj,"hello",{
    set:function(newValue){
        console.log("newValue",newValue)
    },
    get:function(){
        console.log("Return completed ！")
    }
});
obj.hello = "this is hello !"  //newValue this is hello !
/*从对象obj的属性hello设置来看，执行了set方法*/
console.log(obj.hello)  
//this is hello !
//Return completed ！
/*console.log()方法打印除了两段话，说明获取对象属性，执行了get方法*/
```
> 那么就比较好理解了，对象属性的赋值以及取值会分别触发get 和 set 对应的函数  

 **注意**：  
 - get或set不是必须成对出现。如果不设置方法，则get和set的默认值为undefined；
 - 当使用了get或set方法，不允许使用writable和value这两个属性；
