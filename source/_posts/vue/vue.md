---
title:  Vue
category: JavaScript
tags: [React.js,devtool]
---
```
<div id="example-1">
  Hello {{ name }}!
</div>
// 这是我们的 Model
var exampleData = {
  name: 'Vue.js'
}

// 创建一个 Vue 实例或 "ViewModel"
// 它连接 View 与 Model
var exampleVM = new Vue({
  el: '#example-1',
  data: exampleData
})
<ul v-for="dataitme in title">
<!--v-for指令基于一个数组渲染一个列表 item in items，items 是数据数组，item 是当前数组元素的别名-->
<li>{{dataitme.test}}</li>
<li>{{dataitme.test2}}</li>
</ul>
```
<!-- more -->
### 双向绑定：
v-model 指令在表单控件元素上创建双向数据绑定。



Mustache 标签也可以用在 HTML 特性 (Attributes) 内：
```
<divid="item-{{ id }}"></div>

Vue.filter('showScore', function (value, size) {}）;

function connectWebViewJavascriptBridge(callback) {
if (window.WebViewJavascriptBridge) {
        callback(WebViewJavascriptBridge);
    } else {
document.addEventListener('WebViewJavascriptBridgeReady', function () {
            callback(WebViewJavascriptBridge);
        }, false);
    }
}

connectWebViewJavascriptBridge(function (bridge) {
_bridge = bridge;

    bridge.init(function (message, responseCallback) {
generateHtml(JSON.parse(message).data);
    });
});
function generateHtml(info) {
Vue.filter('showScore', function (value, size) {
            size = size || 'big';
var h = ["<img src='star_" + size + "_empty.png'/>", "<img src='star_" + size + "_empty.png'/>", "<img src='star_" + size + "_empty.png'/>", "<img src='star_" + size + "_empty.png'/>", "<img src='star_" + size + "_empty.png'/>"];
for (var i = 0; i < value; i++) {
if (i + 1 > value) {
h[i] = "<img src='star_" + size + "_half.png'/>";
                } else {
h[i] = "<img src='star_" + size + "_full.png'/>";
                }
            }
return h.join('');
        });

new Vue({
el: '#container',
data: info,
methods: {
loadPage: function () {

var that = this;
_bridge.callHandler('loadOrderCommentListByPageIndex', {'pageNo': ++pageNo}, function (response) {
//JavaScript调用方法
response = JSON.parse(response)
that.commentlist = that.commentlist.concat(response.date.commentlist);
that.totalscore = response.date.totalscore;
                    });
                },
toggleClass: function (className, index) {
var el = document.getElementsByClassName("comment_context")[index];
if (el.className.lastIndexOf(className) >= 0) {
el.className = "comment_context";
                    }
else {
el.className = "comment_context line_ellipse_5";
                    }
                }
            },
ready: function () {
document.getElementById("container").style.display = "block";
            }
        });
    }
    ```

 ### 过滤器：
 Vue.filter() 注册一个自定义过滤器，它接收两个参数：过滤器 ID 和过滤器函数。

在 Vue.js，我们使用 v-if 指令实现同样的功能：

<p v-if="greeting">Hello!</p>

这里 v-if 指令将根据表达式 greeting 值的真假删除/插入 <p> 元素。
<a v-bind:href="url"></a>
这里 href 是参数，它告诉 v-bind 指令将元素的 href 特性跟表达式 url 的值绑定。可能你已注意到可以用特性插值 href="{{url}}" 获得同样的结果：这样没错，并且实际上在内部特性插值会转为 v-bind 绑定。
另一个例子是 v-on 指令，它用于监听 DOM 事件：
<a v-on:click="doSomething">
这里参数是被监听的事件的名字。我们也会详细说明事件绑定。
