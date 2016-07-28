---
title: React 组件之间的传值
category: "React.js" 
tags: [React.js,ES6,React-router] 
---
### React 父组件和子组件之间的传值
  #### 主要是通过 this.props之间传值
 _输出语句:export命令规定的是对外的接口，必须与模块内部的变量建立一一对应关系。
使用export命令定义了模块的对外接口以后，其他JS文件就可以通过import命令加载这个模块（文件）。
_
<!-- more -->
## index.js
### 这是父组件
```
module.exports = {
    path: 'tinymce',
breadcrumbName:"redux测试",

getComponent(nextState, callback) {
        require.ensure([], (require) => {
            callback(null, require('./components/circle.jsx'))
        })
    }
}
circle.jsx
import React,{Component} from 'react';
import ReactDom from 'react-dom';
import Newout from './NewOUtSide.js'
class test extends Component{
constructor(props){
//构造方法
super(props);
this.state={
dataname:'属性了，一个基本的属性',
newtestname:'',
newreftest:'',
isTrue:'你去给我买好吃的去',
isout:'我是外面的'
}
//点击事件
this.onSubmit=this.onSubmit.bind(this);
//实时传递数据
this.newtest=this.newtest.bind(this);
//实时传递数据
this.reftest=this.reftest.bind(this);
//组件之间传值
this.newContent=this.newContent.bind(this);
//这是外面传值
this.outContent=this.outContent.bind(this);
};
//加载就执行
componentDidMount(){
this.setState({
name:'我是加载就执行的name，我是react一个方法'
})
  }
//点击事件
onSubmit(){

this.setState({
dataname:'我是修改之后的属性'
})
  }
//修改input
newtest(value){

this.setState({
newtestname:value.target.value
    })

  }
//修改input的内容
reftest(value){
this.state.newreftest=ReactDom.findDOMNode(this.refs.inputname).value;
this.forceUpdate();

}
//修改组件的值
newContent(value){
this.setState({
iszi:value
    })

  }
//外面传递的值
outContent(value){
this.setState({
isoutzi:value
    })
  }
render(){
return (
<div>
这是个测试:
        {this.state.dataname}，
<h4>这是一个componentDidMount的方法：</h4>{this.state.name}
<h3>这是一个按钮：</h3>
            <button type="primary" htmlType="submit" ref="submit" onClick={this.onSubmit}>点击</button>
            <h3>实时传值</h3>
            <input type="test" onChange={this.newtest} />
            <span>{this.state.newtestname}</span>
              <input type="test" ref="inputname" onChange={this.reftest} />
            <span style={{color:'red'}}>{this.state.newreftest}</span>
            <span>这是同页面之间传值：</span>
              <NewModuleTest isAll={this.state.isTrue} cdContent={this.newContent} />
              <h5>这是子组件给我传递的值：{this.state.iszi}</h5>
            <span>这是从外面传值</span>
            <Newout isOutAll={this.state.isout} isOutContet={this.outContent} />
            <span>这是外面给传递的值：{this.state.isoutzi}</span>
      </div>
)
  }

}
```
### 这是子组件
```
class NewModuleTest extends Component{
constructor(props){
super(props);
this.state={
isnew:'',
isdata:'我没有钱，没法给你买东西'
}

   }
componentDidMount(){
this.setState({
isnew:this.props.isAll
});
setTimeout(()=>{
this.props.cdContent(this.state.isdata)
    },100)

   }
render(){
return (
<div>
            <h1>我是子组件，我在同一个页中实现的，我要给父组件传值</h1>
            <h3>我是父组件传给我值：{this.state.isnew}</h3>

       </div>
)
   }

 }
```
### 这是模块之前的传值方式
```
//模块输出
module.exports=test;
NewOUtSide.js
import React,{Component} from 'react';
import ReactDom from 'react-dom';

class OutSide extends Component{
constructor(props){
super(props);
this.state={
isout:'',
outlist:"我是外面给父组件传递值"
}
  }
componentDidMount(){
this.setState({
isout:this.props.isOutAll
});
setTimeout(()=>{this.props.isOutContet(this.state.outlist)},100)


  }
render(){
return(
<div>
          <h3>这是外面的组件：{this.state.isout}</h3>
      </div>
)
  }
}

module.exports=OutSide;

```