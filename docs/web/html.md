> HTLM专栏

## meta之各种属性之用法

这些是我整理的比较常见的 `meta` 属性，这一块内容偏多，就不一一放上。
```html
<!--移动端viewport-->
<meta name="viewport" content="width=device-width,initial-scale=1,maximum-scale=1,minimum-scale=1,user-scalable=no" />

<!-- 是否启动webapp功能，会删除默认的苹果工具栏和菜单栏。 -->
<meta name="apple-mobile-web-app-capable" content="yes" />

<!-- 禁止客户端中的数字识别为电话号码,email识别 -->
<meta name="format-detection" content="telephone=no, email=no" />

<!-- 启用浏览器的极速模式(webkit) -->
<meta name="renderer" content="webkit">

<!-- 避免IE使用兼容模式 -->
<meta http-equiv="X-UA-Compatible" content="IE=edge">

<!-- uc强制竖屏 -->
<meta name="screen-orientation" content="portrait">

<!-- QQ强制竖屏 -->
<meta name="x5-orientation" content="portrait">

<!-- UC强制全屏 -->
<meta name="x5-fullscreen" content="true">
```

## favicon

[比特虫](http://www.bitbug.net/) 是我最常用的一个在线转换工具了。站内有 `16*16` `32*32` `64*64` `128*128` 规格的图标制作。
```html
<!--然后引入即可-->
<head>
    <link rel="shortcut icon" href="/favicon.ico" />
</head>
```

## 自定义部分input标签

关于input标签，属性也很多 `text botton password radio file checkbox ...等等`，但是现在很多开发人员都选择了使用UI框架，例如：饿了吗出品的`element ui`,蚂蚁金服出品的`ant design`,或者`bootstrap`,但是有时候我们按照我们的业务场景，不需要用到庞大的UI架子，这时候就需要我们自己去写。
这里我们讨论一下关于如何自定义自己的表单UI的实现。下面我们由file推演出自定义radio，checkbox的自定义U。

```html
<div class="demo">
    <p>请选择文件</p>
    <input type="file" placeholder="这个是文件选择">
</div>
```

```css
.demo{
    width: 100px;
    height: 30px;
    position: relative;
    overflow: hidden; // 这个是为input的font-size服务的
}
.demo >input{
    width: 100px;
    height: 30px;
    font-size: 99999px;  // 这个你们试试就知道为什么要这么大了
    position: absolute;
    left: 0;
    top: 0;
    opacity: 0;  // 透明度很关键
}
.demo >p{
    width: 100px;
    height: 30px;
    position: absolute;
    left: 0;
    top: 0;
}
```
*原理就是将透明的input层叠在p标签的上层，然后样式全部交给p标签来处理。另外由于file类型比较特殊，左边按钮，右边文件路径，所有要让按钮占满p元素，只能去设置font-size的css去撑大按钮，相应的radio和checkbox自定义亦可以用同样的方法实现，只是不需要font-size了。*





