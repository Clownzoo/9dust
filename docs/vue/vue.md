## 关于vue中打包大小优化 {docsify-ignore}
你是否遇到，当我们要发布代码的时候，运行`npm run build`后，打包出来的 `dist` 目录里面的某js文件简直不能直视，是巨尼玛的大，有木有，都到了兆级别了，看着就很难受，于是博主搜索了很多网上的案例，整理出来给大伙看看，肯定不全，但是都是博主项目所用。

## 代码分割
用过webpack的同学们都知道,webpack会打包出一个`app.js`这个东西，这个文件是主宰我们整个项目的灵魂文件，但是很多时候我们打开的这个页面也许不需要加载整个项目代码，我们只是需要加载当前展示页面或者说当前页面所涉及的业务代码而已，那么就是说分割出很多的js出来对应很多的页面。

**正常状态，如下**
```js
// 在我们的vue项目里面，我们打开我们的路由配置，大概如以下
import Vue from 'vue';
import Router from 'vue-router';
import testView from './src/view/testView.vue';
Vue.use(Router);
export default new Router({
  routes: [
    {
        path: '/testView',
        component: testView,
        name: '测试文件',
        meta: {
            title: ''
        }
    }
  ]
});
```


。。。待续，下班了。。
