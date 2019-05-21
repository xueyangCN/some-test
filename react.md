# React

commonjs与es6  
react项目的搭建  
jsx  
什么是react  
react和fish的区别  
react组件  
redux  

## commonjs
common通过require导入外部模块，通过module.exports输出模块
```javascript
var http = require('http')

module.exports = {
    name: 'module name'
}
```
### commonjs 包规范  

包结构  
如果严格按照规范来说   
包目录应包含以下文件或目录  

package.json：包描述文件  
bin：存放可执行二进制文件的目录  
lib：存放js代码的目录  
doc：存放文档的目录  
test：存放单元测试用例代码的目录  

parke.json包描述文件

```json
{
  "name": "demo",
  "version": "1.0.0",
  "description": "this is a demo",
  "main": "main.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "payson",
  "license": "ISC"
}
```
规范字段解释如下：  

name：名  
description：简介  
version：版本号  
keywords：关键词数组  
maintainers：维护者列表  
contributors：贡献者列表  
bugs：可以反馈bug的网页或邮箱地址  
licenses：许可证列表  
respositories：托管源码的位置列表  
dependencies：依赖项列表  
homepage：网站地址  
os：操作系统支持列表  
cpu：CPU架构支持列表  
engine：支持的JS引擎列表   
builten：是否内建在底层系统的标准组件   
directories：目录说明   
implements：实现规范的列表   
scripts：脚本说明对象   

除了规范之外，还有扩展的字段：   

authoer：作者   
bin：配置为命令行工具   
main：入口文件   
devDependencies：开发依赖项列表   

react 的package.json
```json
{
  "_args": [
    [
      "react@16.6.0",
      "G:\\hj_pro\\c_center\\1.28\\unicorm-custmer-center"
    ]
  ],
  "_development": true,
  "_from": "react@16.6.0",
  "_id": "react@16.6.0",
  "_inBundle": false,
  "_integrity": "sha512-zJPnx/jKtuOEXCbQ9BKaxDMxR0001/hzxXwYxG8septeyYGfsgAei6NgfbVgOhbY1WOP2o3VPs/E9HaN+9hV3Q==",
  "_location": "/react",
  "_phantomChildren": {},
  "_requested": {
    "type": "version",
    "registry": true,
    "raw": "react@16.6.0",
    "name": "react",
    "escapedName": "react",
    "rawSpec": "16.6.0",
    "saveSpec": null,
    "fetchSpec": "16.6.0"
  },
  "_requiredBy": [
    "/umi-build-dev",
    "/umi-test"
  ],
  "_resolved": "https://registry.npmjs.org/react/-/react-16.6.0.tgz",
  "_spec": "16.6.0",
  "_where": "G:\\hj_pro\\c_center\\1.28\\unicorm-custmer-center",
  "browserify": {
    "transform": [
      "loose-envify"
    ]
  },
  "bugs": {
    "url": "https://github.com/facebook/react/issues"
  },
  "dependencies": {
    "loose-envify": "^1.1.0",
    "object-assign": "^4.1.1",
    "prop-types": "^15.6.2",
    "scheduler": "^0.10.0"
  },
  "description": "React is a JavaScript library for building user interfaces.",
  "engines": {
    "node": ">=0.10.0"
  },
  "files": [
    "LICENSE",
    "README.md",
    "index.js",
    "cjs/",
    "umd/"
  ],
  "homepage": "https://reactjs.org/",
  "keywords": [
    "react"
  ],
  "license": "MIT",
  "main": "index.js",
  "name": "react",
  "repository": {
    "type": "git",
    "url": "git+https://github.com/facebook/react.git"
  },
  "version": "16.6.0"
}

```

### npm
NPM是随同NodeJS一起安装的包管理工具，能解决NodeJS代码部署上的很多问题，常见的使用场景有以下几种：  

允许用户从NPM服务器下载别人编写的第三方包到本地使用。  
允许用户从NPM服务器下载并安装别人编写的命令行程序到本地使用。  
允许用户将自己编写的包或命令行程序上传到NPM服务器供别人使用。  

NPM（node package manage）实践了CommonJS的包规范   
利用它，我们可以发布、安装和依赖第三方模块   
我们下载Node的时候，其实已经内置了npm，所以我们不用再下载  

常用命令  

npm -v  
查看当前npm版本  

npm init  
初始化包
输入这个命令后   
会让你填写包名、包简介等等信息   
然后我们的文件就会动态生成一个package.json文件 

npm update moduleName  
更新node模块

npm uninstall moudleName    
卸载node模块

npm install \<package\>@version  
依赖包安装

npm config set registry https://registry.npm.taobao.org  
npm修改源地址 
npm config get registry  
修改后通过这个命令来测试  


package.json的scripts字段提供了钩子机制
```json
"scripts": {
  "preinstall": "preinstall.js",
  "install": "install.js",
  "uninstall": "uninstall.js",
  "test": "test.js",
  "start": "node server.js",
}
```
那么在执行$ npm install \<package\>的时候   
就会执行preinstall的属性值preinstall.js脚本   
然后执行install的属性值install.js脚本   
执行$ npm uninstall \<package\>的时候   
又会执行uninstall.js脚本做一些清理工作   
执行$ npm test又会执行test.js  

## webpack
### 为什要使用WebPack  
现今的很多网页其实可以看做是功能丰富的应用，它们拥有着复杂的JavaScript代码和一大堆依赖包。为了简化开发的复杂  度，前端社区涌现出了很多好的实践方法  

模块化，让我们可以把复杂的程序细化为小的文件;  
类似于TypeScript这种在JavaScript基础上拓展的开发语言：使我们能够实现目前版本的JavaScript不能直接使用的特  性，并且之后还能转换为JavaScript文件使浏览器可以识别；  
Scss，less等CSS预处理器  
...  
这些改进确实大大的提高了我们的开发效率，但是利用它们开发的文件往往需要进行额外的处理才能让浏览器识别,而手动处  理又是非常繁琐的，这就为WebPack类的工具的出现提供了需求。  

### 什么是Webpack  
WebPack可以看做是模块打包机：它做的事情是，分析你的项目结构，找到JavaScript模块以及其它的一些浏览器不能直接  运行的拓展语言（Scss，TypeScript等），并将其转换和打包为合适的格式供浏览器使用。  
Webpack的工作方式是：把你的项目当做一个整体，通过一个给定的主文件（如：index.js），Webpack将从这个文件开始  找到你的项目的所有依赖文件，使用loaders处理它们，最后打包为一个（或多个）浏览器可识别的JavaScript文件。  

## es6
ECMAScript 6.0（简称 ES6）是 JavaScript 语言的下一代标准，在 2015 年 6 月正式发布。它的目标，是  使得 JavaScript 语言可以用来编写复杂的大型应用程序，成为企业级开发语言。 
### 模块化
通过import 和export来实现模块化  
### 变量声明  
新增了let（块级变变量）和const（常量）变量声明  
### 字符串扩展
字符串模板 
```javascript
`${variable}string`
```
### 函数扩展
增加了函数默认值  
```javascript
function foo(name = 1){
    console.log(name)
}
foo()
// 1
```
扩展了箭头函数
```javascript
const foo = name => {
    console.log(name);
}
const obj = {
    name: 'coo',
    getName: function(){
        console.log(this.name)
    },
    getName2: () => {
        console.log(this.name)
    }
}
obj.getName();//coo
obj.getName2();//undefind
```

增加了class声明
```javascript
//es5
function Point(x, y) {
  this.x = x;
  this.y = y;
}

Point.prototype.toString = function () {
  return '(' + this.x + ', ' + this.y + ')';
};

var p = new Point(1, 2);
//es6
class Point {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }

  toString() {
    return '(' + this.x + ', ' + this.y + ')';
  }
}
```
### 对对象进行了扩展
```javascript
let birth = '2000/01/01';

const Person = {

  name: '张三',

  //等同于birth: birth
  birth,

  // 等同于hello: function ()...
  hello() { console.log('我的名字是', this.name); }

};
```
### 扩展运算符
```javascript
let z = { a: 3, b: 4 };
let n = { ...z };
n // { a: 3, b: 4 }
```
### 变量的解构赋值
```javascript
let a = 1;
let b = 2;
let c = 3;
//可以写成
let [a, b, c] = [1, 2, 3];

let { foo, bar } = { foo: 'aaa', bar: 'bbb' };
foo // "aaa"
bar // "bbb"
```
### Promise对象

```javascript
const promise = new Promise((resolve,reject) => {
    function asyncfunction(){
        resolve(data)
        ...reject(error)
    }
    asyncfunction()
})
```
## jsx
JSX就是Javascript和XML结合的一种格式。React发明了JSX，利用HTML语法来创建虚拟DOM。当遇到<，JSX就当HTML解  析，遇到{就当JavaScript解析。
```jsx
var child1 = React.createElement('li', null, 'First Text Content');
var child2 = React.createElement('li', null, 'Second Text Content');
var root = React.createElement('ul', { className: 'my-list' }, child1, child2);
//等同于
var root =(
  <ul className="my-list">
    <li>First Text Content</li>
    <li>Second Text Content</li>
  </ul>
);
```

## 什么是React

React 起源于 Facebook 的内部项目，由于 React 的设计思想极其独特，属于革命性创新，性能出众，代码逻辑却非常简  单。所以，越来越多的人开始关注和使用，认为它可能是将来 Web 开发的主流工具。  
在Web开发中，我们总需要将变化的数据实时反应到UI上，这时就需要对DOM进行操作。而复杂或频繁的DOM操作通常是性能  瓶颈产生的原因（如何进行高性能的复杂DOM操作通常是衡量一个前端开发人员技能的重要指标）。  

### 虚拟DOM
React为此引入了虚拟DOM（Virtual DOM）的机制：在浏览器端用Javascript实现了一套DOM API。基于React进行开发时  所有的DOM构造都是通过虚拟DOM进行，每当数据变化时，React都会重新构建整个DOM树，然后React将当前整个DOM树  和上一次的DOM树进行对比，得到DOM结构的区别，然后仅仅将需要变化的部分进行实际的浏览器DOM更新。而且React能够  批处理虚拟DOM的刷新，在一个事件循环（Event Loop）内的两次数据变化会被合并，例如你连续的先将节点内容从A变成  B，然后又从B变成A，React会认为UI不发生任何变化，而如果通过手动控制，这种逻辑通常是极其复杂的。尽管每一次都  需要构造完整的虚拟DOM树，但是因为虚拟DOM是内存数据，性能是极高的，而对实际DOM进行操作的仅仅是Diff部分，因而  能达到提高性能的目的。这样，在保证性能的同时，开发者将不再需要关注某个数据的变化如何更新到一个或多个具体  的DOM元素，而只需要关心在任意一个数据状态下，整个界面是如何Render的。

### 组件化
虚拟DOM(virtual-dom)不仅带来了简单的UI开发逻辑，同时也带来了组件化开发的思想，所谓组件，即封装起来的具有独立  功能的UI部件。React推荐以组件的方式去重新思考UI构成，将UI上每一个功能相对独立的模块定义成组件，然后将小  的组件通过组合或者嵌套的方式构成大的组件，最终完成整体UI的构建。例如，Facebook的instagram.com整站都采用了  React来开发，整个页面就是一个大的组件，其中包含了嵌套的大量其它组件。  
组件化的思考方式是UI功能模块之间的分离。  
在React中，按照界面模块自然划分的方式来组织和编写代码，每个组件只关心自己部分的逻辑，彼此独立。

React认为一个组件应该具有如下特征：  
（1）可组合（Composeable）：一个组件易于和其它组件一起使用，或者嵌套在另一个组件内部。如果一个组件内部创建了  另一个组件，那么说父组件拥有（own）它创建的子组件，通过这个特性，一个复杂的UI可以拆分成多个简单的UI组件。  
（2）可重用（Reusable）：每个组件都是具有独立功能的，它可以被使用在多个UI场景。  
（3）可维护（Maintainable）：每个小的组件仅仅包含自身的逻辑，更容易被理解和维护。  

### 一个组件的生命周期

挂载  
当组件实例被创建并插入 DOM 中时，其生命周期调用顺序如下：  

constructor()  
static getDerivedStateFromProps()  
render()  
componentDidMount()  

更新  
当组件的 props 或 state 发生变化时会触发更新。组件更新的生命周期调用顺序如下：  

static getDerivedStateFromProps()  
shouldComponentUpdate()  
render()  
getSnapshotBeforeUpdate()  
componentDidUpdate()  

卸载  
当组件从 DOM 中移除时会调用如下方法：  

componentWillUnmount()  


```jsx
import React, { Component } from 'react';

class LifeCycle extends Component {
    constructor(props){
        super(props);
        this.state = {
            title: '111'
        }
    }
    static getDerivedStateFromProps(nextPprops,prevState){

    };
    render(){
        return (
            <div>{this.state.title}</div>
        )
    };
    componentDidMount(){

    };
    shouldComponentUpdate(){

    };
    getSnapshotBeforeUpdate(prevProps, prevState){
        return snapshot;
    };
    componentDidUpdate(prevProps, prevState, snapshot){

    };
    componentWillUnmount(){

    }
}

```
### react router

```jsx
import React from 'react'
import { render } from 'react-dom'

// First we import some modules...
import { Router, Route, IndexRoute, Link, hashHistory } from 'react-router'

// Then we delete a bunch of code from App and
// add some <Link> elements...
const App = React.createClass({
  render() {
    return (
      <div>
        <h1>App</h1>
        {/* change the <a>s to <Link>s */}
        <ul>
          <li><Link to="/about">About</Link></li>
          <li><Link to="/inbox">Inbox</Link></li>
        </ul>

        {/*
          next we replace `<Child>` with `this.props.children`
          the router will figure out the children for us
        */}
        {this.props.children}
      </div>
    )
  }
})

// Finally, we render a <Router> with some <Route>s.
// It does all the fancy routing stuff for us.
render((
  <Router history={hashHistory}>
    <Route path="/" component={App}>
      <IndexRoute component={Home} />
      <Route path="about" component={About} />
      <Route path="inbox" component={Inbox} />
    </Route>
  </Router>
), document.body)
```

## react 与 fish 的区别

### 模块化
react一般基于es6来进行模块化  
fish基于AMD进行模块化  
### 基本单元
react的基本逻辑单元为组件  
fish的基本逻辑单元为视图  
### 数据流
react通过props的单向数据流实现组件的嵌套信息传递，通过state来管理组件的内部状态  
fish通过调用子页面的函数来传参，通过this.options来获取参数  
### 渲染
react通过props或者state的改变触发diff算法比对虚拟dom生成新的虚拟dom，最后渲染虚拟dom树改变的分支  
fish通过dom操作来改变视图  
### 运行环境
由于react开发需要用到jsx文件以及es6规范，所以需要通过webpack打包之后才能在浏览器环境运行  
fish可以直接在浏览器环境运行  




