---
title: 【style-resources-loader】自动化导入CSS
date: 2020-07-10 12:02:06
tags:
---
> 项目开发过程中我们可能会定义一些公共样式、变量、mixin...,然后在单文件中可以随时自由的引用这些公共样式和变量，那么我们就可以使用[style-resources-loader](https://www.npmjs.com/package/vue-cli-plugin-style-resources-loader)，这篇文章将介绍如何使用它。

#### 一、预处理器安装
根据不同预处理器(Sass/Less/Stylus)，安装响应的webpack loader:
```javascript
// Sass
npm install -D sass-loader sass

// Less
npm install -D less-loader less

// Stylus
npm install -D stylus-loader stylus
```

#### 二、安装`style-resources-loader`
```javascript
// 使用vue add安装
vue add style-resources-loader
```

#### 三、配置`vue.config.js`
在pluginOptions>style-resources-loader定义资源的模式。配置项：
| 名称| 类型| 例如|
|---|---|---|
|preProcessor|string|sass, scss, stylus, less中的一种|
|patterns|string, array|资源路径或者资源路径数组|

#### 四、案例
```javascript
// vue.config.js
const path = require('path')
module.exports = {
  pluginOptions: {
    'style-resources-loader': {
      'preProcessor': 'scss', // 项目中使用scss
      'patterns': [
        path.resolve(__dirname, './src/styles/*.scss'),
      ]
    }
  }
}
```
``` scss
// src/styles/_variables.scss
$sideBarWidth: 180px;
$sideBarBackgroundColor:#2a2935;
$sideBarBorderColor:#1b1b22;
```

```vue
// 某vue文件
<style lang='scss' scoped>
.sidebar-container{
    width: $sideBarWidth; // 这里直接使用定义的$sideBarWidth变量，无需引入scss
  }
</style>
```