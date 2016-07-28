---
title: Redux 基础搭建和功能介绍
category: [React.js,Webpack,Redux]
tags: [Redux]
---
state        ———————————>store <-----------------------Action
（数据）                 储存       （仓库）      改变            （触发）


Action 的组成
                (state,action)=>state  的纯函数
  store.dispatch()

<!-- more -->
### redux是管理State的一个东东，所有State都需要经过redux来操作。

#### redux中有三个基本概念，Action，Reducer，Store。
## Action
Actions 是把数据从应用传到 store 的有效载荷。它是 store 数据的唯一来源。用法是通过 store.dispatch() 把 action 传到 store。

Action 有两个作用。
用Action来分辨具体的执行动作。比如是create 还是delete？或者是update？
操作数据首先得有数据。比如添加数据得有数据，删除数据得有ID。。action就是存这些数据的地方
（我的理解：Action 只是执行操作这些数据的动作，就是只下达命令（如：去改变数据））
Reducer

Action 只是描述了有事情发生了这一事实，并没有指明应用如何更新 state。这是 reducer 要做的事情。

Action就像leader，告诉我们应该做哪些事，并且给我们提供‘资源（就是上面说的数据）’，真正干活的是苦逼的Reducer。。

（我的理解：action，只下达命令，告诉了我们怎么操作这些数据，然后让reducer去执行（如：reducer就去执行这个updata动作））

### Store

一个应用只有一个Store。一个应用只有一个Store。一个应用只有一个Store。
重要的事情放在前面说，而且说三遍。。

上面章节中，我们学会了使用 action 来描述“发生了什么”，和使用 reducers 来根据 action 更新 state 的用法。
Store 就是把它们联系到一起的对象。Store 有以下职责：
维持应用的 state；
- 提供 getState() 方法获取 state；
- 提供 dispatch(action) 方法更新 state；
- 通过 subscribe(listener) 注册监听器。
- Store提供了一些方法。让我们很方便的操作数据。
我们不用关心Reducer和Action是怎么关联在一起的，Store已经帮我们做了这些事。。
（我的理解：store是一个仓库，Action发出命令，通过store中的方法（比如dispatch（action））让reducer去执行它，reducer执行完，就更改了store里面的数据。）

```
 reducer，形式为 (state, action) => state 的纯函数 下面就是一个 reducer
functioncounter(state =0, action){switch(action.type){case'INCREMENT':return state +1;case'DECREMENT':return state -1;default:return state;}}

```
详细介绍

这部分主要讲解redux如何在项目中使用。
 #### Action

Action 是一个普通对象。
（我的理解：Action下达命令是通过type来执行的，type就是执行的动作（如：{type:'add'，Num:'1'} 就是说给Num这个数据，增加一些数据。））
redux约定 Action 内使用一个字符串类型的 type 字段来表示将要执行的动作。
```
{
    type:'ADD_ITEM'}
```
除了 type 之外，Action可以存放一些其他的想要操作的数据。例如：
```
{
    type:'ADD_ITEM',
    text:'我是Berwin'}
 ```
上面例子表示
我要创建一条数据
创建的数据为大概是这样的
```
{
    text:'我是Berwin'}
但在实际应用中，我们需要一个函数来为我们创建Action。这个函数叫做actionCreator。它看起来是这样的：
function addItem(text){return{
    type: types.ADD_ITEM,
    text
  }}
  ```
（我的理解：Action通过type去说明这个动作是干什么的，text就是执行这个动作需要的数据，addItem就是把type这个动作和text这个数据提供出来，他们返回的是一个对象，并没有去执行这个动作，只是把需要的数据提供出来了）

### Reducer

Reducer 是一个普通的回调函数。
当它被Redux调用的时候会为他传递两个参数State 和 Action。
Reducer会根据 Action 的type来对旧的 State 进行操作。返回新的State。
看起来是下面这样的：
```
/**
 * 添加
 *
 * @param {String} 添加的文字
 *
 * @return {Object} 将要添加的数据
 */
let createItem = text =>{
  let time =Date.now();return{
    id:Math.random().toString(36).split('.').join(''),
    addTime: time,
    updateTime: time,
    status:false,
    text
  }}/**
 * Reducer
 *
 * @param State
 * @param Action
 *
 * @return new State
 */
let reducer =(state =[], action)=>{switch(action.type){case ADD_ITEM:return[createItem(action.text),...state]default:return state
  }}
  ```
Reducer很简单，但有三点需要注意
不要修改 state。
在 default 情况下返回旧的 state。遇到未知的 action 时，一定要返回旧的 state。
如果没有旧的State，就返回一个initialState，这很重要！！！
这是一部分核心源码：
// currentState 是当前的State，currentReducer 是当前的Reducer
currentState = currentReducer(currentState, action);
如果在default或没有传入旧State的情况下不返回旧的State或initialState。。。那么当前的State会被重置为undefined！！
在使用combineReducers方法时，它也会检测你的函数写的是否标准。如果不标准，那么会抛出一个大大的错误！！
combineReducers

真正开发项目的时候State会涉及很多功能，在一个Reducer处理所有逻辑会非常混乱，，所以需要拆分成多个小Reducer，每个Reducer只处理它管理的那部分State数据。然后在由一个主rootReducers来专门管理这些小Reducer。
Redux提供了一个方法 combineReducers 专门来管理这些小Reducer。
它看起来是下面这样：
  ```
/**
 * 这是一个子Reducer
 *
 * @param State
 * @param Action
 *
 * @return new State
 */
let list =(state =[], action)=>{switch(action.type){case ADD_ITEM:return[createItem(action.text),...state]default:return state
  }}// 这是一个简单版的子Reducer，它什么都没有做。
let category =(state ={}, action)=> state;/**
 * 这是一个主Reducer
 *
 * @param State
 * @param Action
 *
 * @return new State
 */
let rootReducers = combineReducers({list, category});
  ```
combineReducers 生成了一个类似于Reducer的函数。为什么是类似于，因为它不是真正的Reducer，它只是一个调用Reducer的函数，只不过它接收的参数与真正的Reducer一模一样~
** 这是一部分核心源码：**

function combineReducers(reducers){// 过滤reducers，把非function类型的过滤掉~var finalReducers = pick(reducers,(val)=>typeof val ==='function');// 一开始我一直以为这个没啥用，后来我发现，这个函数太重要了。它在一开始，就已经把你的State改变了。变成了，Reducer的key 和 Reducer返回的initState组合。var defaultState = mapValues(finalReducers,()=>undefined);returnfunction combination(state = defaultState, action){// finalReducers 是 reducersvar finalState = mapValues(finalReducers,(reducer, key)=>{// state[key] 是当前Reducer所对应的State，可以理解为当前的Statevar previousStateForKey = state[key];var nextStateForKey = reducer(previousStateForKey, action);return nextStateForKey;});// finalState 是 Reducer的key和stat的组合。。}}
从上面的源码可以看出，combineReducers 生成一个类似于Reducer的函数combination。
当使用combination的时候，combination会把所有子Reducer都执行一遍，子Reducer通过action.type 匹配操作，因为是执行所有子Reducer，所以如果两个子Reducer匹配的action.type是一样的，那么都会成功匹配。

### Store

上面已经介绍什么是Store，以及它是干什么的，这里我就讲讲如何创建Store，以及如何使用Store的方法。
创建Store非常简单。createStore 有两个参数，Reducer 和 initialState。
let store = createStore(rootReducers, initialState);
store有四个方法。
getState： 获取应用当前State。
subscribe：添加一个变化监听器。
dispatch：分发 action。修改State。
replaceReducer：替换 store 当前用来处理 state 的 reducer。
常用的是dispatch，这是修改State的唯一途径，使用起来也非常简单，他看起来是这样的~
  ```
/**
 * 创建Action
 *
 * @param 添加的数据
 *
 * @return {Object} Action
 */function addItem(text){return{
    type: types.ADD_ITEM,
    text
  }}
let list =(state =[], action)=>{switch(action.type){case ADD_ITEM:return[createItem(action.text),...state]default:return state
  }}// 这是一个简单版的子Reducer，它什么都没有做。
let category =(state ={}, action)=> state;/**
 * 这是一个主Reducer
 *
 * @param State
 * @param Action
 *
 * @return new State
 */
let rootReducers = combineReducers({list, category});
let store = createStore(rootReducers, initialState);
// 新增数据
store.dispatch(addItem('Read the docs'));
  ```
这是一部分核心源码：
  ```
function dispatch(action){// currentReducer 是当前的Reducer
  currentState = currentReducer(currentState, action);

  listeners.slice().forEach(function(listener){return listener();});return action;}
    ```
可以看到其实就是把当前的Reducer执行了。并且传入State和Action。
State哪来的？
State其实一直在Redux内部保存着。并且每次执行currentReducer都会更新。在上面代码第一行可以看到。


（我的理解：
1  首先创建Action知道需要干什么
  ```
functionaddItem(text){return{
    type: types.ADD_ITEM,
    text
  }}
    ```
2  然后根据Action创建Reducer，去执行怎么干
  ```
let list =(state =[], action)=>{switch(action.type){case ADD_ITEM:return[createItem(action.text),...state]default:return state
  }
}
  ```
其中有个合并每个小的Reducer的方法
combineReducers();
使用方法如下：
  ```
let list =(state =[], action)=>{switch(action.type){case ADD_ITEM:return[createItem(action.text),...state]default:return state
  }}// 这是一个简单版的子Reducer，它什么都没有做。
let category =(state ={}, action)=> state;/**
 * 这是一个主Reducer
 *
 * @param State
 * @param Action
 *
 * @return new State
 */
let rootReducers = combineReducers({list, category});
3 利用store的方法来联系起来Action和Reducer ，通过这个dispatch()方法来更新store
let store = createStore(rootReducers, initialState);
// 新增数据
store.dispatch(addItem('Read the docs'));
）
  ```
React-Redux

Redux 是独立的，它与React没有任何关系。React-Redux是官方提供的一个库，用来结合redux和react的模块。
React-Redux提供了两个接口Provider、connect。
Provider

Provider是一个React组件，它的作用是保存store给子组件中的connect使用。
通过getChildContext方法把store保存到context里。
后面connect中会通过context读取store。
它看起来是这个样子的：
<Providerstore={this.props.store}><h1>Hello World!</h1></Provider>

这是一部分核心源码：

getChildContext(){return{ store:this.store }}

constructor(props, context){super(props, context)this.store = props.store
}
可以看到，先获取store，然后用 getChildContext 把store保存起来~



connect

connect 会把State和dispatch转换成props传递给子组件。它看起来是下面这样的：
import*as actionCreators from'./actionCreators'import{ bindActionCreators }from'redux'function mapStateToProps(state){return{ todos: state.todos }}function mapDispatchToProps(dispatch){return{ actions: bindActionCreators(actionCreators, dispatch)}}exportdefault connect(mapStateToProps, mapDispatchToProps)(Component)
它会让我们传递一些参数：mapStateToProps，mapDispatchToProps，mergeProps（可不填）和React组件。
之后这个方法会进行一系列的黑魔法，把state，dispatch转换成props传到React组件上，返回给我们使用。

mapStateToProps：

mapStateToProps 是一个普通的函数。
当它被connect调用的时候会为它传递一个参数State。
mapStateToProps需要负责的事情就是 返回需要传递给子组件的State，返回需要传递给子组件的State，返回需要传递给子组件的State，（重要的事情说三遍。。。。）然后connect会拿到返回的数据写入到react组件中，然后组件中就可以通过props读取数据啦~~~~
它看起来是这样的：
function mapStateToProps(state){return{ list: state.list }}
因为state是全局State，里面包含整个项目的所有State，但是我不需要拿到所有State，我只拿到我需要的那部分State即可，所以需要返回 state.list 传递给组件

mapDispatchToProps：

与mapStateToProps很像，mapDispatchToProps也是一个普通的函数。
当它被connect调用的时候会为它传递一个参数dispatch。
mapDispatchToProps负责返回一个 dispatchProps
dispatchProps 是actionCreator的key和dispatch(action)的组合。
dispatchProps 看起来长这样：
{
  addItem:(text)=> dispatch(action)}
connect 收到这样的数据后，会把它放到React组件上。然后子组件就可以通过props拿到addItem并且使用啦。
this.props.addItem('Hello World~');
如果觉得复杂，不好理解，，那我用大白话描述一下
就是通过mapDispatchToProps这个方法，把actionCreator变成方法赋值到props，每当调用这个方法，就会更新State。。。。额，，这么说应该好理解了。。

bindActionCreators：

但如果我有很多个Action，总不能手动一个一个加。Redux提供了一个方法叫 bindActionCreators。
bindActionCreators 的作用就是将 Actions 和 dispatch 组合起来生成 mapDispatchToProps 需要生成的内容。
它看起来像这样：
  ```
let actions ={
  addItem:(text)=>{
    type: types.ADD_ITEM,
    text
  }}

bindActionCreators(actions, dispatch);// @return {addItem: (text) => dispatch({ type: types.ADD_ITEM, text })}

这是一部分核心源码：

function bindActionCreator(actionCreator, dispatch){return(...args)=> dispatch(actionCreator(...args));}// mapValues： map第一个参数的每一项，返回对象，key是key，value是第二个参数返回的数据/*
 * mapValues： map第一个参数的每一项，返回对象，key是key，value是第二个参数返回的数据
 *
 * @param actionCreators
 * @param dispatch
 *
 * @return {actionKey: (...args) => dispatch(actionCreator(...args))}
 */exportdefaultfunction bindActionCreators(actionCreators, dispatch){return mapValues(actionCreators, actionCreator =>
    bindActionCreator(actionCreator, dispatch));}
      ```
可以看到，bindActionCreators 执行这个方法之后，它把 actionCreators 的每一项的 key 不变，value 变成 dispatch(actionCreator(...args)) 这玩意，这表示， actionCreator 已经变成了一个可执行的方法，执行这个方法，就会执行 dispatch 更新数据。。
