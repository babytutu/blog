---
title: vue-unit-test
date: 2018-07-19 09:07:25
tags:
  - test
  - vue
categories:
  - code
---

## 单元测试

> 一切为了更靠谱的代码和更少的bug

有个demo可以看看[vue-unit-test-demo](https://github.com/babytutu/vue-unit-test-demo)
<!--more-->

## npm依赖包

> 为了在不修改原有代码的基础上写测试代码，选用了以下搭配
> 因为用了webpack@4，必须搭配使用mocha-webpack@2

- mocha & mocha-webpack
- jsdom & jsdom-global (for setting up DOM environment in tests)
- webpack-node-externals (for excluding NPM deps from test bundle)
- expect (for assertions)
- nyc & babel-plugin-istanbul (for coverage)

## webpack配置

> 建议单独写一个用于test的webpack配置文件

### webpack.test.js

```js
module.exports = {
  mode: 'development',
  module: {
    rules: [
      {
        test: /\.vue$/,
        loader: 'vue-loader'
      },
      {
        test: /\.js$/,
        loader: 'babel-loader',
        exclude: /node_modules/
      },
      {
        test: /\.(png|jpg|gif|svg)$/,
        loader: 'file-loader',
        options: {
          name: '[name].[ext]?[hash]'
        }
      }
    ]
  },
  // 不处理node_modules目录
  externals: [require('webpack-node-externals')()],
  resolve: {
    alias: {
      'vue$': 'vue/dist/vue.esm.js'
    },
  },
}
```


### 文件目录
```
├── src                  // resource
│   └── components       // components
├── test                 // test
├── .babelrc             // babel
├── .gitignore           // git
├── package-lock.json    // npm
├── package.json         // npm
├── README.md            // readme
└── webpack.test.js      // webpack
```

### 脚本命令

package.json

```json
"test": "corss-env BABEL_ENV=test mocha-webpack --webpack-config webpack.test.js --require test/setup.js test/*.spec.js"
```


## 配置nyc

> 用于生成覆盖率报告文件
> reporter=html生成一个网页
> reporter=text在控制台直接输出结果

.babelrc

> 通过设置NODE_ENV=test，加载测试覆盖率需要的特殊配置

```json
{
  "presets": [
    ["env", { "modules": false }],
    "stage-0"
  ],
  "env": {
    "test": {
      "presets": [
        ["env", {
          "modules": false,
          "targets": { "node": "current" }
        }],
        "stage-0"
      ],
      "plugins": ["istanbul"]
    }
  }
}
```

package.json

```json
  "script": {
    "cover": "corss-env BABEL_ENV=test nyc --reporter=html --reporter=text npm run test"
  },
  "nyc": {
    "include": [
      "src/**/*.(js|vue)"
    ],
    "instrument": false,
    "sourceMap": false
  }
```

## 一个简单的例子

- 参考了[vue官方文档](https://vuejs.org/v2/guide/unit-testing.html)


### 简单的组件
> src/commponent/msg.vue

```html
<template>
  <span>{{ message }}</span>
</template>

<script>
  export default {
    data () {
      return {
        message: 'hello!'
      }
    },
    created () {
      this.message = 'bye!'
    }
  }
</script>
```

### 测试代码

> test/msg.spec.js

```js
// 导入 Vue.js 和组件，进行测试
import Vue from 'vue'
import MyComponent from './../src/components/msg.vue'

// 这里是一些 Jasmine 2.0 的测试，你也可以使用你喜欢的任何断言库或测试工具。

describe('MyComponent', () => {
  // 检查原始组件选项
  it('has a created hook', () => {
    expect(typeof MyComponent.created).toBe('function')
  })

  // 评估原始组件选项中的函数的结果
  it('sets the correct default data', () => {
    expect(typeof MyComponent.data).toBe('function')
    const defaultData = MyComponent.data()
    expect(defaultData.message).toBe('hello!')
  })

  // 检查 mount 中的组件实例
  it('correctly sets the message when created', () => {
    const vm = new Vue(MyComponent).$mount()
    expect(vm.message).toBe('bye!')
  })

  // 创建一个实例并检查渲染输出
  it('renders the correct message', () => {
    const Constructor = Vue.extend(MyComponent)
    const vm = new Constructor().$mount()
    expect(vm.$el.textContent).toBe('bye!')
  })

  // 在状态更新后检查生成的 HTML
  it('updates the rendered message when vm.message updates', done => {
    const vm = new Vue(MyComponent).$mount()
    vm.message = 'foo'

    // 在状态改变后和断言 DOM 更新前等待一刻
    Vue.nextTick(() => {
      expect(vm.$el.textContent).toBe('foo')
      done()
    })
  })
})
```

## 官方工具

> 封装了很多方法用于快捷的测试vue组件

[Vue Test Utils](https://vue-test-utils.vuejs.org/zh/guides/#%E8%B5%B7%E6%AD%A5)