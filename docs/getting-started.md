# 5 分钟快速上手

- order: 2
- category: arale

---

## 先看个例子吧

新建一个文件，把以下代码复制进去，然后用浏览器打开

```html
<style>
.target{width:50px;height:50px;border-radius:25px;background:#000;transition:All 1s ease;-webkit-transition:All 1s ease;-moz-transition:All 1s ease;}
</style>
<script charset="utf-8" id="seajsnode"src="http://static.alipayobjects.com/seajs/??seajs/2.1.1/sea.js,seajs-combo/1.0.0/seajs-combo.js,seajs-style/1.0.0/seajs-style.js"></script>
<script>
  seajs.config({
    alias: {
      '$': 'gallery/jquery/1.7.2/jquery',
      'position': 'arale/position/1.0.0/position'
    }
  });
  seajs.use(['$', 'position'], function($, Position){
    var stop = false;
    var target = $('<div class="target"></div>')
      .hover(function(){stop = true;},function(){stop = false;})
      .appendTo(document.body);
    setInterval(function() {
      if (stop) return;
      var x = Math.floor(Math.random() * 100);
      var y = Math.floor(Math.random() * 100);
      Position.pin(
        { element: target, x: 'center', y: 'center' }, 
        { element: Position.VIEWPORT, x: x + '%', y: y + '%' }
      ); 
    }, 800);
  });
</script>
```

看到有个球在飞来飞去么，你能抓到他么？[线上演示](http://jsfiddle.net/afc163/zPYqx/1/show/)

## 使用 SeaJS

看过 Arale 的简介，大家已经知道 Arale 是基于 Sea.js 和 CMD 模块开发的，所以使用 Arale 之前要先引入 Sea.js，它是一个模块加载器，会异步请求需要的模块。

在这个例子里，使用了 `jquery` 和 [position](http://aralejs.org/position) 两个组件。大家可能会注意到 `seajs.config` 的配置，是的，这就是 Arale 组件的 ID，通过这个 ID 可以找到这个组件。

比如模块 `position` 的完整路径就是：

```
http://static.alipayobjects.com/arale/position/1.0.1/position.js
```

Arale 的 ID 由四部分组成：`{{family}}/{{module}}/{{version}}/{{file}}`

 -  Arale 的 family 除了 arale 外还有外部引入的 [gallery](https://github.com/cmdjs/gallery/) 和 [jquery](https://github.com/cmdjs/jquery/)
 -  module 为组件的名字
 -  version 为版本
 -  file 为具体的文件，可以有多个，一般与组件名相同

这个 ID 和 seajs 的所在路径拼合后就是模块文件的具体地址了。当你拿到上面的 ID 后，就可以直接用 `seajs.use` 来使用这个模块了。

```js
seajs.use(['arale/position/1.0.1/position'], function(Position) {
    // use Position ...
});
```

当然老这么写全 ID 会比较麻烦，这时你可以用 seajs.config 中的 alias 属性来统一配置别名（像最开始的代码里那样做）。

这样就可以直接 `seajs.use(['position'])` 了，请求完成后会调用回调函数，这时就可以使用这两个组件了。

## 安装到本地

非常欢迎直接通过支付宝的 cdn 来调用 Arale 模块，但如果你需要在自己的网站上部署 Arale，建议使用 spm 工具来下载模块。

```
$ spm install arale/position
```

这行命令会把对应模块以及相关依赖安装到 sea-modules 目录中。像支付宝的 cdn 路径这样部署你的静态文件，就可以自由使用了。

## 查找组件

Arale 是一个基础类库，有自己开发的组件，也有精心挑选由外部引入的组件，那如何找到这些组件呢？

在 [Arale 首页](http://aralejs.org/) 能找到这些组件，选好组件后可以[查看组件是否可用](http://aralejs.org/docs/online-status.html)。

Arale 使用了最优秀的业界组件，比如负责操作 Dom 和 Ajax 的 jQuery，负责时间日期的 MomentJS，本地存储 Store 等。如果你发现了优秀的业界模块不在其中，请告诉我们。

Arale 拥有丰富实用的基础前端组件，比如负责表单校验的 [Validator](http://aralejs.org/validator) ，负责区块切换的 [Switchable](http://aralejs.org/switchable) ，负责定位元素的 [Positioin](http://aralejs.org/position)。
如果你需要用到浮层类的组件，你可以试试基础浮层 [Overlay](http://aralejs.org/overlay)、负责浮层触发逻辑的 [Popup](http://aralejs.org/popup)、日历组件 [Calendar](http://aralejs.org/calendar)、自动完成 [Autocomplete](http://aralejs.org/autocomplete) 等等。如果找不到你需要的组件，请联系我们进行开发。

## 才刚刚开始

现在你已经可以在你的博客、网站等各种地方使用 Arale 了，如果你有更复杂的需求可以继续跟着我们学习[如何写组件](develop-components.html)。如果有任何问题，欢迎[提问](https://github.com/aralejs/aralejs.org/issues)。
