---
title: gulp stylus
date: 2018-03-26 11:12:09
tags:
  - gulp
categories:
  - code
---

## gulp
- Automate and enhance your workflow

<!--more-->

## 背景介绍
- webpack没有开始流行前，gulp也是一个不错的选择。即使是现在，gulp还是一个不错的打包工具，更自由更便捷

## 打包样式
- js代码打包，考虑到还要eslint，babel之类的，用webpack相对来说更方便，但样式，不管是css，sass，less，stylus，其实都只要简单的gulp任务就可以搞定

## 以打包stylus举例

- 首先，找找看[gulp插件](https://gulpjs.com/plugins/),搜索`stylus`,第一个就可以，[gulp-stylus](https://www.npmjs.com/package/gulp-stylus),名字简单直接

### 建立个新目录
```bash
mkdir gulp-demo
cd gulp-demo
npm init -y
```

### 安装gulp，gulp-stylus
```bash
npm i gulp gulp-stylus -D
```

### 新建`gulpfile.js`
- 先加个`styl`文件，目录结构这样
```
└─┬ src
  └── css.styl
```

随便写个样式呗
css.styl
```css
body
  font-size: 12px
```

- 开始加默认的gulp任务
gulpfile.js
```js
const gulp = require('gulp')
const stylus = require('gulp-stylus')

gulp.task('default', () => {
  gulp.src('src/css.styl')
      .pipe(stylus())
      .pipe(gulp.dest('build'))
})
```

- 运行`gulp`
发现出来个新的`build`目录，下面有编译好的`css.css`文件，查看`gulp-stylus`的配置项，最基础的就是压缩呗，那咱们加上

gulpfile.js
```js
const gulp = require('gulp')
const stylus = require('gulp-stylus')

gulp.task('default', () => {
  gulp.src('src/css.styl')
-     .pipe(stylus())
+     .pipe(stylus({
+       compress: true
+     }))
      .pipe(gulp.dest('build'))
})
```

- 再次运行`gulp`，会发现css.css文件里的内容被压缩了，搞定收工

## API简单说明

### gulpfile.js
任务入口文件,所有的`gulp`任务都在这个文件内

### gulp.task(name [, deps, fn])
gulp任务，有个默认名称`default`，直接运行`gulp`就可以执行，一般是用`gulp name`来运行，deps，是一个依赖条件，就是得先把deps的任务完成了再执行

一个简单的例子
gulpfile.js
```js
gulp.task('one', (cb) => {
  // 当err不是null或者undefined时，任务会中断
  cb(err)
})

gulp.task('default', ['one'])
```

### gulp.src(globs[, options])
需要打包的文件/文件夹，可以用字符串或数组

### gulp.pipe()
管道，执行插件，以及输出

### gulp.dest(path[, options])
输出文件的路径，一般都是根目录下

### gulp.watch(glob [, opts], tasks) or gulp.watch(glob [, opts, cb])
观察路径下文件的变动，执行对应的任务

## 简单说明下`watch`
### 加入`watch`方法

gulpfile.js
```js
  const gulp = require('gulp')
  const stylus = require('gulp-stylus')

  gulp.task('default', () => {
    gulp.src('src/css.styl')
        .pipe(stylus({
          compress: true
        }))
        .pipe(gulp.dest('build'))
  })

+ const watcher = gulp.watch('src/css.styl', ['default'])
+
+ watcher.on('change', function(event) {
+   console.log('File ' + event.path + ' was ' + event.type + ', running tasks...');
+ })
```

### 再次执行`gulp`
代码首次打包后，任务仍在进行，修改`src/css.styl`
```css
body
  font-size: 12px
+ color: red
```

### gulp打包任务自动执行了
```bash
File /Users/tutu/Downloads/code/gulp-demo/src/css.styl was changed, running tasks...
[13:36:07] Starting 'default'...
[13:36:07] Finished 'default' after 3.38 ms
```

这样每次代码变动都可以自动打包了
