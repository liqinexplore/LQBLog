---
title:  devtool 安装应用
category: [React.js,devtool]
tags: [React.js,devtool]
---
为了方便redux开发，更好的了解数据的变化，我们安装测试环境下的devtool
### 1 安装 到开发模式
npm install redux-devtools --save-dev
 npm install redux-devtools-dock-monitor --save-dev
npm install redux-devtools-log-monitor --save-dev
### 安装到正式环境
npm install redux-thunk --save
npm install redux-logger --save
创建 DevTools: devTools.js
<!-- more -->
```
/**
 * Created by Administrator on 2016/7/22.
 */
// 调试工具
import React from 'react'
import { createDevTools } from 'redux-devtools'
import LogMonitor from 'redux-devtools-log-monitor'
import DockMonitor from 'redux-devtools-dock-monitor'

const DevTools = createDevTools(
<DockMonitor toggleVisibilityKey="ctrl-h" changePositionKey="ctrl-q">
        <LogMonitor theme="tomorrow" preserveScrollTop={false} />
    </DockMonitor>
)

export default DevTools
```
### store配置  rootStore.js
```
/**
 * Created by Administrator on 2016/7/22.
 */

import thunk from 'redux-thunk' // redux-thunk 支持 dispatch function，并且可以异步调用它
import createLogger from 'redux-logger' // 利用redux-logger打印日志
import { createStore, applyMiddleware, compose } from 'redux' // 引入redux createStore、中间件及compose
import DevTools from './devtools' // 引入DevTools调试组件

// 调用日志打印方法
const loggerMiddleware = createLogger()

// 创建一个中间件集合
const middleware = [thunk, loggerMiddleware]

// 利用compose增强store，这个 store 与 applyMiddleware 和 redux-devtools 一起使用
const finalCreateStore = compose(
    applyMiddleware(...middleware),
DevTools.instrument()
)(createStore)

export default finalCreateStore
```
### index.js
```
import 'babel-polyfill'
import React from 'react'
import { render } from 'react-dom'
import { Provider } from 'react-redux'
import { createStore } from 'redux'
import App from './containers/App'
import todoApp from './reducers'

import DevTools from './devTools' // 引入Redux调试工具DevTools
import finalCreateStore from './rootStore'//引入增强后的store
const store =finalCreateStore(todoApp);
const rootElement=document.getElementById('root');

render(
<Provider store={store}>
       <div>
           <DevTools/>
       <App />

       </div>
   </Provider>,
rootElement
)
```
下面是效果图
![image](http://o6znw17tt.bkt.clouddn.com/clipboard2.png)
