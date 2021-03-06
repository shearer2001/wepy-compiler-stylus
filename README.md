# wepy stylus 编译器

[![npm package](https://nodei.co/npm/wepy-compiler-styl.png?downloads=true&downloadRank=true&stars=true)](https://www.npmjs.com/package/wepy-compiler-styl)

> Note: wepy官方提供的插件`wepy-compiler-stylus`对stylus的封装不太友好，不方便开发者配置一些高级特性，因此重新封装了一个stylus的编译插件`wepy-compiler-styl`。

> 如果该插件对您的开发有所帮助，请五星好评哦！^_^ ^_^ ^_^

---

<p align="center">
  <a href="http://stylus-lang.com/">
    <img alt="Stylus" src="http://stylus-lang.com/img/stylus-logo.svg" width="393"/>
  </a>
</p>

## Table of contents

  - [Features](#features)
  - [Installation](#installation)
  - [Usage](#usage)
  - [Examples](#examples)

<br/>

## Features

### Support a few advanced features
  * define
  * rawDefine
  * include
  * import
  * includeCSS
  * url

### Original features
  * globals
  * functions
  * use
  * paths
  * filename
  * Evaluator
  * ...

## Installation

```
cnpm install wepy-compiler-styl --save-dev
```


## Usage

```
// configure wepy.config.js

module.exports = {
  compilers: {
    styl: {
      compress: true
    }
  }
};
```

## Examples

```
// configure wepy.config.js

module.exports = {
  compilers: {
    styl: {
      compress: true,                                 // 压缩
      includeCSS: true,                               // 支持导入css
      supportObject: true,                            // 支持以下参数
      define: {                                       // 外部传入全局变量和函数
        isProd: process.env.NODE_ENV === 'production' // 举例：控制不同环境的样式处理
      },
      include: [],                                    // 等价于 paths: [__dirname, __dirname + '/utils']，将目录暴露给全局
      import: [                                       // 导入自定义的functions和mixins等，千万不要导入全局公共样式，否则你懂的哦
        path.join('src', 'css', 'utils', '**/*.styl')
      ],
      url: 'inline-url',                              // 使用base64将图片转码
      url: {
        name: 'inline-url',
        limit: 30000,                                 // 限制多少B以内的图片被压缩
        paths: []                                     // 从指定的目录下查找图片
      },

      // ============= stylus 内部参数 =============
      globals: {                                      // 外部传入全局变量
        isProd: process.env.NODE_ENV === 'production'
      },
      functions: {}                                   // 外部传入全局函数
      use: [],                                        // 导入插件nib、poststylus等
      paths: [],                                      // 将目录暴露给全局
      filename: [],                                   // 设置文件名
      Evaluator: Object                               // 没用过，我也不知道
    }
  }
};
```
