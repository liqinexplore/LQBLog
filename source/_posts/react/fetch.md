---
title:  Fetch 请求
category: [React.js,Fetch]
tags: [React.js,Fetch]
---
## Fetch 请求
###下面我们介绍一下ajax替代功能Fetch请求

  由于 Fetch API 是基于 Promise 设计
  ```
fetch(url).then(function(response) {//url 请求 response 返回数据
return response.json();//将数据转换为json格式    
}).then(function(data) {
console.log(data);
}).catch(function(e) {
console.log("Oops, error");
});  
```   
<!-- more -->
- Promise 构造函数接受一个函数作为参数，该函数的两个参数分别是 resolve 方法和 reject 方法。
- 如果异步操作成功，则用 resolve 方法将 Promise 对象的状态，从「未完成」变为「成功」（即从 pending 变为 resolved）；
- 如果异步操作失败，则用 reject 方法将 Promise 对象的状态，从「未完成」变为「失败」（-即从 pending 变为 rejected）。
- promises 的奇妙在于给予我们以前的 return 与 throw，每个 Promise 都会提供一个 then() 函数，和一个 catch()，实际上是 then(null, ...) 函数，

** 使用 ES6 的 箭头函数 后：**
```
fetch(url).then(response => response.json())
.then(data => console.log(data))
.catch(e => console.log("Oops, error", e))
现在看起来好很多了，但这种 Promise 的写法还是有 Callback 的影子，而且 promise 使用 catch 方法来进行错误处理的方式有点奇怪。不用急，下面使用 async/await 来做最终优化：
注：async/await 是非常新的 API，属于 ES7，目前尚在 Stage 1(提议) 阶段，这是它的完整规范。使用 Babel 开启 runtime 模式后可以把 async/await 无痛编译成 ES5 代码。也可以直接使用 regenerator 来编译到 ES5。
try {
let response = await fetch(url);
let data = response.json();
console.log(data);
} catch(e) {
console.log("Oops, error", e);
}
// 注：这段代码如果想运行，外面需要包一个 async function
```
duang~~ 的一声，使用 await 后，写异步代码就像写同步代码一样爽。await 后面可以跟 Promise 对象，表示等待 Promise resolve() 才会继续向下执行，如果 Promise 被 reject() 或抛出异常则会被外面的 try...catch 捕获。
下面是我在项目中的实际应用，放在下面供大家参考
```
function streamingDemo() {
var req = newRequest(URL, {method: 'GET', cache: 'reload'});
fetch(req).then(function (response) {
var reader = response.body.getReader();
return reader.read();
}).then(function (result, done) {
if (!done) {// do something with each chunk
}
    });
}
fetch(PRO_URL.gallery.olympic.del_an_item.url, {method: 'POST', body: JSON.stringify({newsId: id})})
    .then((res)=> {
        res.json();
})
    .then((data)=> {
if (data.rc == 0) {
getOlympicAll();
}
    })
    .catch((e)=> {
        message.info("删除失败" + e, 5);
})
```
