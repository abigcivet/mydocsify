# vux UI库

## 安装
```bash
    npm install vux --save

    npm install vux-loader --save-dev

    npm install less less-loader --save-dev
```

## build/webpack.base.conf.js配置

```js
    const vuxLoader = require('vux-loader')
    const webpackConfig = originalConfig

    // 原来的 module.exports 代码赋值给变量 webpackConfig，

    //即将原来的module.exports 改为 const webpackConfig
    module.exports = vuxLoader.merge(webpackConfig, { plugins: ['vux-ui'] })

--------------------------------------------------------------------------------------

    resolve: {
        extensions: ['.js', '.vue', '.json','.less'],  // 这里不要忘记加'.less'
        alias: {
          'vue$': 'vue/dist/vue.esm.js',
          '@': resolve('src'),
        }
      },

```

## main配置

```js
    const FastClick = require('fastclick') // 移除移动端点击延迟
    FastClick.attach(document.body)
```

## .babelrc配置

```js
    "plugins": [
        "transform-vue-jsx",
        "transform-runtime",
        {
          "name": "duplicate-style"   //  添加name
        }
      ],
```

## App.vue配置

```html
    <style lang="less">
      @import '~vux/src/styles/reset.less';
    </style>
```

## meta标签

```html
    <meta charset="utf-8">
    <!--<meta name="viewport" content="width=device-width,initial-scale=1.0">-->
    <meta name="viewport" content="width=device-width, initial-scale=1, user-scalable=no" />
    <!-- 删除苹果默认的工具栏和菜单栏 -->
    <meta name="apple-mobile-web-app-capable" content="yes" />
    <!-- 设置苹果工具栏颜色 -->
    <meta name="apple-mobile-web-app-status-bar-style" content="black" />
    <!-- 忽略页面中的数字识别为电话，忽略email识别 -->
    <meta name="format-detection" content="telphone=no, email=no" />
    <!-- 启用360浏览器的极速模式(webkit) -->
    <meta name="renderer" content="webkit">
    <!-- 避免IE使用兼容模式 -->
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <!-- 针对手持设备优化，主要是针对一些老的不识别viewport的浏览器，比如黑莓 -->
    <meta name="HandheldFriendly" content="true">
    <!-- 微软的老式浏览器 -->
    <meta name="MobileOptimized" content="320">
    <!-- uc强制竖屏 -->
    <meta name="screen-orientation" content="portrait">
    <!-- QQ强制竖屏 -->
    <meta name="x5-orientation" content="portrait">
    <!-- UC强制全屏 -->
    <meta name="full-screen" content="yes">
    <!-- QQ强制全屏 -->
    <meta name="x5-fullscreen" content="true">
    <!-- UC应用模式 -->
    <meta name="browsermode" content="application">
    <!-- QQ应用模式 -->
    <meta name="x5-page-mode" content="app">
    <!-- windows phone 点击无高光 -->
    <meta name="msapplication-tap-highlight" content="no">
```