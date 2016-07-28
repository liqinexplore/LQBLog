---
title: React.js  WebPack  Babel ES6 React-router Redux 项目搭建
category: [React.js,Webpack,router,Redux]
tags: [React.js,WebPack,Babel,ES6,React-router,Redux]
---
```
下面来详细介绍一下
 React.js  WebPack  Babel ES6 React-router Redux 项目搭建
```

# 1 创建项目
首先 搭建一个这样的结构

```
--your project
  |--app
    |--components
      |--productBox.jsx
    |--main.js
  |--build
    |--index.html
    |--bundle.js(该文件是webpack打包后生成的)
```
<!-- more -->


```

下面来详细介绍一下
 React.js  WebPack  Babel ES6 React-router Redux 项目搭建
```

# 1 创建项目
首先 搭建一个这样的结构

```
--your project
  |--app
    |--components
      |--productBox.jsx
    |--main.js
  |--build
    |--index.html
    |--bundle.js(该文件是webpack打包后生成的)
```

### （1） 创建package.json
    npm init    
    帮助我们跟踪节点模块
### （2） 安装react和react DOM

```
npm install react --save-dev
或者是 npm install --save-dev react@5.10.0
npm install react-dom --save-dev
```

### (3) 安装webpack和webpack-dev-server

```
需要注意的是 webpack-dev-server 为服务器需要装全局的
npm install webpack --save-dev
npm install webpack-dev-server -g
```

### （4）安装babel-loader 和下面几个组件

```
npm install babel-loader --save-dev
npm install babel-core --save-dev
npm install babel-preset-es2015 --save-dev //支持ES2015
npm install babel-preset-react --save-dev //支持jsx
```

#### (5) 在文件夹app下创建hello.jsx

```
首先创建自己的第一组件，当你创建一个组件，您定义所有这些通过重写的反应，组件来呈现功能
在hello.jsx中输入：
import React from 'react';
class Hello extends React.Component{
    render(){
    return <h1>你好</h1>
}
}
需要注意的是：我们运用的是ES6语法，可以使我们的代码不用写React.createClass更加简洁。
下面的代码是不用ES6和JSX的代码
var React =require('react');
var Hello =React.createClass({
    displayName:'Hello',
    render:function(){
    return React.createElement("h1",null,"Hello");
}
});
当我们使用JSX时,我们可以更简练地定义虚拟DOM元素,而无需调用反应。createElement和通过哪些属性的元素。我们简单的你好组件可能有相同数量的行代码但JSX使事情更容易,继续构建组件和结合在一起。所以我们不用这种方式了
```

### （6）引入DOM的渲染功能，传递一个组件对象来连接一个实际的DOM元素
 ```
import React from 'react';
import ReactDOM from 'react-dom';
   class Hello extends React.Component{
    render(){
    return <h1>你好</h1>
}
}
ReactDOM.render(<Hello/>,document.getElementById('hello'));
```

### （7）同样的方式早app文件夹下添加world.jsx组件

```
import React from 'react';
import ReactDOM from 'react-dom';

class World extends React.Component {
  render() {
    return <h1>World</h1>
  }
}

ReactDOM.render(<World/>, document.getElementById('world'));
//调用html中的id="world"。对应的是World组件
```

### （8）在build 文件夹下的index.html中添加如下代码:

```
<!doctype html>
<html>
 <head>
  <meta charset="UTF-8">
  <title>Hello React</title>
 </head>
 <body>
  <div id="hello"></div>
  <div id="world"></div>
 </body>
</html>
```



### (9) 在app文件夹下的main.js添加如下代码

```
作用是：导入这两个反应组件。
import Hello from'./hello.jsx';
import World from'./world.jsx';
```


### （10）我们需要告诉Webpack,这将是我们的入口点和加载器使用在创建包。

```
在项目目录下创建webpack.config.js
varpath=require('path');
varwebpack=require('webpack');

module.exports={
 entry:path.resolve(__dirname, './app/main.js'),
 output:{
     path:path.resolve(__dirname, './build'),
filename:'bundle.js'},
 module:{
   loaders:[
      {
        test:/.jsx?$/,// 用正则来匹配文件路径，这段意思是匹配 js 或者 jsx
        loader:'babel-loader',
        exclude:/node_modules/,
        query:{
          presets:['es2015','react']
        }
      }
    ]
 },
};
其中entry指定了webpack的入口程序，好比c++和java中的main程序一样，我们把最终要插入到页面指定位置的react模板写入main.js中。

而output则指定了webpack打包成功之后文件名称以及文件的存放位置。
```

### （11）我们需要在html中添加bundle.js.依照之前指定的项目结构，我们可以在index.html中直接引入打包生成的bundle.js

```
<!doctype html>
<html>
 <head>
  <meta charset="UTF-8">
  <title>Hello React</title>
 </head>
 <body>
  <div id="hello"></div>
  <div id="world"></div>
  <script src="bundle.js"></script>
 </body>
</html>
```

### （12）使用webpack-dev-server：监听代码自动刷新！
#### （12.1、在控制台上输入   

```
npm install webpack-dev-server --save-dev
npm install --save-dev react-hot-loader //热加载

我们先打开package.json，并找到scripts代码块。在没引入webpack-dev-server之前，我们运行这个项目的姿势是这样的
"scripts": {
        "test": "echo \"Error: no test specified\" && exit 1",
        "build": "webpack"
}
并且执行：
npm run build
```


#### （12.2）项目就跑起来啦，但是每次修改程序我们都要手动输入npm run build来跑项目，这无疑是一件非常蛋疼的事情。但有了webpack-dev-server光环，我们的姿势应该是这样的：

```
为scripts添加
"scripts": {

        "test": "echo \"Error: no test specified\" && exit 1",
        "build": "webpack",
          "dev": "webpack-dev-server --devtool eval --progress --colors --hot --content-base build"
}
    ps：dev里各属性值的意思是：
    1.  webpack-dev-server: 在 localhost:8080 建立一个 Web 服务器
    2.  --devtool eval:为你的代码创建源地址。当有任何报错的时候可以让你更加精确地定位到文件和行号
    3.  --progress: 显示合并代码进度
    4.  --colors: 在命令行中显示颜色
    5.  --content-base build:指向设置的输出目录
```

#### （12.3）并且在index.html里加入：build/index.html


```
<!DOCTYPE html>
<html>
<head lang="en">
<meta charset="UTF-8">
<title>hello react</title>
</head>
<body>
<div id="hello"></div>
<div id="world"></div>
<script src="http://localhost:8080/webpack-dev-server.js"></script>
<script src="bundle.js"></script>
</body>
</html>
```

#### （12.4）在webpack.config.js的入口处加入：

```
var path=require('path');
var webpack =require('webpack');
module.exports={
 entry:['webpack/hot/dev-server',
        'webpack-dev-server/client?http://localhost:8080',
        path.resolve(__dirname, './app/main.js')],
output:{
path: path.resolve(__dirname, './build'),
filename:'bundle.js'
},
module:{
loaders:[{
test:/.jsx?$/,
loader:'babel-loader',
exclude:/node_modules/,
query:{
                presets:['es2015','react']
            }

        }

        ]
    },
plugins: [
new webpack.DefinePlugin({
        'process.env.NODE_ENV': '"development"'
    }),
new webpack.HotModuleReplacementPlugin()
]
};
最后执行：
npm run dev
在浏览器中打开localhost：8080


修改端口为8090
"dev": "webpack-dev-server --devtool eval --port 8090 --progress --colors --hot --content-base build"
开发环境
"compile": "webpack -p --progress --colors --config webpack.production.config.js",
```
添加本文件，开发js
![image](http://o6znw17tt.bkt.clouddn.com/clipboard.png)

```
var path=require('path');
var webpack =require('webpack');
var CommonsChunkPlugin = require("webpack/lib/optimize/CommonsChunkPlugin");
module.exports={
resolve:{
root:[
path.resolve('./app/_global/components')
        ],
extensions:['','.js','.jsx']
    },
entry:[
path.resolve(__dirname, './app/main.js')
    ],
output:{
path: __dirname + '/build',
filename: 'bundle.js',
chunkFilename: '[id].chunk.js'
},
module:{
loaders:[{
test:/.jsx?$/,
loader:'babel-loader',
exclude:/node_modules/,
query:{
presets:['es2015','react']
            }
        },
{test: /\.css$/, loader: 'style!css'},
{test: /\.scss$/, loader: "style!css!sass"},
{test: /\.less$/,loader: 'style!css!less'},
{test: /\.(png|jpg)$/, loader: 'url?limit=25000'}


        ]
    },
plugins: [
new webpack.DefinePlugin({
'process.env.NODE_ENV': '"development"'
}),
new webpack.HotModuleReplacementPlugin()
    ]
};

开发环境发布时执行命令 npm run compile
然后将build里面的东西放在服务器上

package.json
{
"name": "pack_react3",
"version": "1.0.0",
"description": "",
"main": "index.js",
"scripts": {
"test": "echo \"Error: no test specified\" && exit 1",
"build": "webpack",
"compile": "webpack -p --progress --colors --config webpack.production.config.js",
"dev": "webpack-dev-server --devtool eval --port 8090 --progress --colors --hot --content-base build"
},
"author": "",
"license": "ISC",
"devDependencies": {
"babel-core": "^6.7.4",
"babel-loader": "^6.2.4",
"babel-preset-es2015": "^6.6.0",
"babel-preset-react": "^6.5.0",
"css-loader": "^0.23.1",
"file-loader": "^0.8.5",
"less": "^2.6.1",
"less-loader": "^2.2.3",
"react": "^0.14.8",
"react-dom": "^0.14.8",
"react-hot-loader": "^1.3.0",
"reqwest": "^2.0.5",
"style-loader": "^0.13.1",
"url-loader": "^0.5.7",
"webpack": "^1.12.14",
"webpack-dev-server": "^1.14.1"
},
"dependencies": {
"antd": "^0.12.13",
"babel-preset-react": "^6.5.0",
"rc-select": "^6.0.6",
"react": "^0.14.8",
"react-dom": "^0.14.8",
"react-router": "^2.2.2"
}
}
```

#### webpack.config.js

```
var path=require('path');
var webpack =require('webpack');

module.exports={
resolve:{
root:[
            path.resolve('./app/_global/components')
        ],
extensions:['','.js','.jsx']
    },
entry:['webpack/hot/dev-server',
'webpack-dev-server/client?http://localhost:8090',
path.resolve(__dirname, './app/main.js')],
output:{
//path: path.resolve(__dirname, 'build/bundles'),
        //filename:'bundle.js'
path: __dirname + '/build',
filename: 'bundle.js',
chunkFilename: '[id].chunk.js'
},
module:{
loaders:[{
test:/.jsx?$/,
loader:'babel-loader',
exclude:/node_modules/,
query:{
presets:['es2015','react']
            }
        },
{test: /\.css$/, loader: 'style!css'},
{test: /\.scss$/, loader: "style!css!sass"},
{test: /\.less$/,loader: 'style!css!less'},
{test: /\.(png|jpg)$/, loader: 'url?limit=25000'}


        ]
    },
plugins: [
new webpack.DefinePlugin({
'process.env.NODE_ENV': '"development"'
}),
new webpack.HotModuleReplacementPlugin()
]
};
```

### 创建路由

```
在webpack.config.js中输入
resolve:{
root:[
        path.resolve('./app/_global/components') //这个是根目录，进来之后先去找这个
    ],
extensions:['','.js','.jsx']//拓展，以后带有'','.js','.jsx'可以省略不写，如：dome.js 可以写成dome
},
在目录下面创建下面的地址

在customComponents.js中调用写的默认模板
import React from 'react';
require('customComponents/customComponents.css') ;//引用customConponents文件中的css样式，其实这里省略了root中的./app/_global/components
import NavBox from 'customComponents/NavBox.js'//定义默认模块
module.exports={NavBox}//模块输出，输出默认模块
```
## 路由搭建逻辑：
### 1 首先创建子路由


```
import React from 'react';
import { render } from 'react-dom'
import { Router, Route, hashHistory, IndexRoute,Link } from 'react-router';
import Home from './modules/_public/Home';
import Dashboard from './modules/_public/Dashboard';
import NotFound from './modules/_public/NotFound';
const routerConfig = [
    {
path: '/',
component: Dashboard, //默认面板
indexRoute: { component: Home },//当刚开始进入，什么路由也没有的时候加载
breadcrumbName:'首页',
childRoutes: [
require('./modules/circle')//子路由地址
]
    },
{
path: '*',
component: Dashboard,
indexRoute:{component:NotFound}//当什么路由地址没有的时候加载
}
];
render((
<Router  history={hashHistory} routes={routerConfig} />
), document.getElementById('app'));
上面的Home Dashboard NotFound 分别对应下面的三个模块
```

### 2 子路由地址


```
require('./modules/circle')//子路由地址
从这个地址进入子路由

进入这个子路由 ，先执行getChildRoutes 然后执行 getComponent这个
getChildRoutes  这个是子路由地址
getComponent    这个是 面板地址 就是本页加载的地方

module.exports={
path:'circle',
breadcrumbName:"圈子",
getChildRoutes(location,callback){
require.ensure([],(require)=>{
            callback(null,[
                require('./routes/items')//这个子路由
])
        });
},
getComponent(nextState,callback){
require.ensure([],(require)=>{

            callback(null,require('./components/circle.jsx'))//这个是跳转的面板
})
    }
};
走到这里，先进入这个页面的circle.jsx中

这是circle.jsx
当点击圈子的时候 进入子路由的index.js

module.exports={
path:'items',
getChildRoutes(location,callback){
require.ensure([],(require)=>{
           callback(null,[
               require('./routes/item')
           ])
        });
},
getComponents(nextSate,callback){
require.ensure([],(require)=>{
            callback(null,{
header:require('./components/header.jsx'),
main:require('./components/items.jsx'),
footer:require('./components/footer.jsx')
            });
});
}
};
传递 header main footer 三个面板给circle.jsx
import React,{Component} from 'react';
import ReactDOM from 'react-dom';
import Dashboard from './dashboard.jsx';
import {Affix} from 'antd';

class Circle extends Component{
render() {
        console.log("adsfa this.props: ", this.props);
let { header, main, footer, children, params } = this.props,content;
console.log("这是header",header);
if (header || main || footer) {
            content = (
<div className="content_group">
{(!!header) ? (<Affix offset={20}><div className="content_header">{header}</div></Affix>) : ""}
                    {(!!main) ? (<div className="content_main">{main}</div>) : ""}
                    {(!!footer) ? (<div className="content_footer">{footer}</div>) : ""}
</div>
)
        } else if (children) {
            content = children
} else {
            content = <Dashboard />
}

return (
<div>
{content}
</div>
)
    }
}
module.exports=Circle;
```

```
在某一个路由中需要执行

首先执行第一个index.js,这是index.jsx内容
module.exports={
path:'items',
getChildRoutes(location,callback){
require.ensure([],(require)=>{
           callback(null,[
               require('./routes/item')
           ])
        });
},
getComponents(nextSate,callback){
require.ensure([],(require)=>{
            callback(null,{
header:require('./components/header.jsx'),
main:require('./components/items.jsx'),
footer:require('./components/footer.jsx')
            });
});
}
};
然后又会从mian.js中开始加载（每一次执行一个路由都会从头开始加载），加载到circle.jsx,这是circle
import React, { Component } from 'react'
import Dashboard from './dashboard.jsx'
import { Affix } from 'antd';

class Circle extends Component {
render() {
let { header, main, footer, children, params } = this.props, content
if (header || main || footer) {
            content = (
<div className="content_group">
{(!!header) ? (<Affix offset={20}><div className="content_header">{header}</div></Affix>) : ""}
                    {(!!main) ? (<div className="content_main">{main}</div>) : ""}
                    {(!!footer) ? (<div className="content_footer">{footer}</div>) : ""}
</div>
)
        } else if (children) {
            content = children
} else {
            content = <Dashboard />
}

return (
<div>
{content}
</div>
)
    }
}
在本页面中加载header main footer数据，并调用了3中的items.js中的数据。这是items.jsx
class CircleItems extends Component {
render() {
return (
<div>
{
this.props.children
||
<Table columns={columns} dataSource={data}
expandedRowRender={record => <p>{record.description}</p>}/>
}
</div>
)
    }
}
module.exports = CircleItems;
这里有一个或（||）的判断，如果this.props.children为true时，下面的就不执行了，如果为false的时候，就会执行下面的table
因为没有执行子路由，这里的this.props.children为false，执行下面的table
然后就会给circle.jsx传递数据，加载出来下面的页面


当点击详细信息的时候就会执行4步的index.js
module.exports = {
path: 'id/:circleID',
breadcrumbName:"项目 :circleID",
getComponent(nextState, callback) {
require.ensure([], (require) => {
            callback(null, require('./components/item'))
        })
    }
}
这里执行了1中index.js的子路由
就会触发items.jsx中的this.props.children为true，然后就会走子路由。然后走4步的index.js
跳到item.jsx中
import React, { Component } from 'react'

class circleItem extends Component {
render() {
let properties = this.props;
return (
<div>
此处是具体某一条数据的详细信息页，根据传入的参数（{properties.params.circleID}）读取接口，显示数据，进行逻辑操作。
</div>
)
    }
}
module.exports = circleItem
```
