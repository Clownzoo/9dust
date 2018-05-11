## for...of 麻瓜用法
在我们程序中，`循环` 这个字眼可谓经常可见，上来就是`for`,`forEach`...,下面我们来说说es6中新增的for...of，废话不说，上代码

```js
// 举个例子,我要循环一个数组拿值；
var array = ['hello', 'es5'];
for(var a = 0; a<=array.length; a++) {
    console.log(array[a]);
};
// hello, es5

```
先来看一个最简单的for…of循环。
```js
// 让我们试试es6新增的东西
let array = ['hello', 'es6'];
for (let item of array) {
    console.log(item);
};
// hello, es6
```
for…of之获取 `数组索引 keys()`
```js
let arr=['hello','es6','数组索引'];
for (let index of arr.keys()){
    console.log(index);
};
// 0,1,2
```
for…of之获取 `数组的内容和索引 entries()`
```js
let arr=['hello','es6','数组的内容和索引'];
for (let [index,val] of arr.entries()){
    console.log(index + ':' + val);
};
// 1:hello, 2:es6, 3:数组的内容和索引
```

下面我们附带一个好玩的东西，`entries()` 和 `next()` 的配合
```js
let arr = ['第一次见面', '第二次见面', '第三次见面'];
let visit = arr.entries();
console.log(visit.next().value);  // 用力敲一次
console.log(visit.next().value);  // 用力再敲一次
console.log(visit.next().value);  // 用力最后敲一次
/*
* 是不是很有意思。
* */
```

## 字符串查找骚气用法之 `includes()`
ES6增加了字符串的查找功能，并且支持中文。那么我们来看看以前怎么玩这些字符串查询的；
```js
let str = '你能找到我九某人算我输，算我输';
if (str.indexOf('九某人') > 0) {
    console.log('你赢了');
} else {
    console.log('你输了，嘿嘿嘿嘿');
};
```
看了上面代码，是不是觉得很烦，我明明是想要判断这个 `九某人` 到底存不存在这个字符串，你却给我返回一个 `number` 类型,还要再做一次判断，也许是大大们听到了我们的心声，设计了下面这个玩意。
```js
let str = '你能找到我九某人算我输，算我输';
if (str.includes('九某人')) {
    console.log('你赢了');
} else {
    console.log('你输了，嘿嘿嘿嘿');
};
// 这样，是不是简单很多，暴力很多，而且可读性也更强了。
```
**接下来拓展几个较为少用的 `startsWith()`, `endsWith()`, `repeat()`** ，使用时要注意前两个的单词 `s` 别漏了。
- startsWith  

*检查字符前面是否存在；*
```js
let str = '你能找到我九某人算我输，算我输';
console.log(str.startsWith('你能找到'));
// true 
```

- endsWith  

*检查字符结尾是否存在；*
```js
let str = '你能找到我九某人算我输，算我输';
console.log(str.endsWith('算我输'));
// true 
```

- repeat(num) 注：{num：复制的数量}

*复制字符串*
```js
let dust = '我好帅';
console.log(dust.repeat(3))
// 我好帅我好帅我好帅
```












 
