---
title: react.js 组件之间state数据的传值
category: React.js
tags: [React.js,ES6,React-router] 
---
  ## React.cloneElement

参数：TYPE（ReactElement），[PROPS（object）]，[CHILDREN（ReactElement）]
克隆并返回一个新的 ReactElement （内部子元素也会跟着克隆），
新返回的元素会保留有旧元素的 props、ref、key，也会集成新的 props（只要在第二个参数中有定义）。

通过React.cloneElement实现props数据之间的传值
 #### 在父的组件中，将两个子组件的data传递出来
 <!-- more -->
 首先父组件定义header和main两个组件
```
 class Circle extends Component {
     constructor(props){
         super(props);
     }
     render() {
        let { header, main } = this.props
        //此处非不得以判断层级，进而达到底层面板不展示的方式。理论上应该是有其他方式，去设置父组件属性。
       content = ( <div className="content_group">
            {(!!header) ? (<div className="content_header">
                {header && React.cloneElement(header, {brodcast: (message)=>main.props.getNotify(message)})}
            </div>) : ""}
            {(!!main) ? (<div className="content_main">{main}</div>) : ""}
          
        </div>
        ）
                        
                return (
                    <div>
                            {content}
                    </div>
                )
        
 }
 
 module.exports = Circle;
```
### 在header.jsx 中赋值。在center.jsx中拿值
#### header.jsx
```
class header extends Component {
    constructor(props) {
            super(props);
             this.handleSubmit = this.handleSubmit.bind(this);
            this.state = {
                circleID: "1",
                begin_time: "2015.01.01",
                title: "内容",
            };
       }
       handleSubmit(){
          let Data = this.state;
          this.props.brodcast(Data);
       }
    render(){
        return(
            <a onClick={this.handleSubmit}>搜索</a>
        )
    }
}
module.exports = header;
```
###上面通过父组件中的this.props.brodcast()将值传入，在content.jsx接受值
#### content.jsx
  
```
var faThis = null;
  class content extends Component {
      constructor(props) {
              super(props);
            faThis = setTimeout(()=> {
                faThis = this;
                });
              this.state = {
                  newdata: [],
              };
         }
         //获取传递过来的请求参数
             getNotify(data) {
                 //将参数传递给后台。
                 faThis.state.newdata = data;
                faThis.forceUpdate();
             }
      render(){
          return(
              <span>{this.state.newdata.title}<span>
          )
      }
  }
  content.defaultProps = {
      getNotify: content.prototype.getNotify
  };
  module.exports = content;
```
实现了 data之前传值，其中重新定义this为faThis是为了防止跟自身组件冲突。