---
title: React组件属性类型（propTypes）
category: [React.js,Webpack,router,Redux]
tags: [React.js,PropTypes]
---
## Prop 验证

为了验证组件之间传入的值，我们引入propTypes。React.PropTypes 提供很多验证器 (validator) 来验证传入数据的有效性。当向 props 传入无效数据时，JavaScript 控制台会抛出警告。注意为了性能考虑，只在开发环境验证 propTypes。
<!-- more -->
下面是各个验证情况的介绍：
```
React.createClass({
propTypes: {
// 可以声明 prop 为指定的 JS 基本类型。默认
        // 情况下，这些 prop 都是可传可不传的。

React.PropTypes.array           // 数组

React.PropTypes.bool.isRequired // Boolean 且必要。

React.PropTypes.func            // 函数

React.PropTypes.number          // 数字

React.PropTypes.object          // 对象

React.PropTypes.string          // 字符串

React.PropTypes.node            // 任何类型的: numbers, strings, elements 或者任何这种类型的数组 节点

React.PropTypes.element         // React 元素

React.PropTypes.instanceOf(XXX) // 某种类型的实例，对象

React.PropTypes.oneOf(['foo', 'bar']) // 其中一个字串

React.PropTypes.oneOfType([React.PropTypes.string, React.PropTypes.array]) // 其中一格式类型

React.PropTypes.arrayOf(React.PropTypes.string)  // 某种类型的数组(字串类型)，任意一种类型字符串

React.PropTypes.objectOf(React.PropTypes.string) // 任意一种类型的对象(字串类型)

React.PropTypes.shape({                          // 是否符合指定格式的对象

color: React.PropTypes.string,
fontSize: React.PropTypes.number
});
React.PropTypes.any.isRequired  // 可以是任何格式，且必要。


// 自定义格式(当不符合时，会显示Error)

// 不要用`console.warn` 或者 throw, 因为它在`oneOfType` 的情况下无效。

// 所有可以被渲染的对象：数字，
        // 字符串，DOM 元素或包含这些类型的数组。
optionalNode: React.PropTypes.node,

// React 元素
optionalElement: React.PropTypes.element,

// 用 JS 的 instanceof 操作符声明 prop 为类的实例。
optionalMessage: React.PropTypes.instanceOf(Message),

// 用 enum 来限制 prop 只接受指定的值。
optionalEnum: React.PropTypes.oneOf(['News', 'Photos']),

// 指定的多个对象类型中的一个
optionalUnion: React.PropTypes.oneOfType([
            React.PropTypes.string,
React.PropTypes.number,
React.PropTypes.instanceOf(Message)
        ]),

// 指定类型组成的数组
optionalArrayOf: React.PropTypes.arrayOf(React.PropTypes.number),

// 指定类型的属性构成的对象
optionalObjectOf: React.PropTypes.objectOf(React.PropTypes.number),

// 特定形状参数的对象
optionalObjectWithShape: React.PropTypes.shape({
color: React.PropTypes.string,
fontSize: React.PropTypes.number
}),

// 以后任意类型加上 `isRequired` 来使 prop 不可空。
requiredFunc: React.PropTypes.func.isRequired,

// 不可空的任意类型
requiredAny: React.PropTypes.any.isRequired,

// 自定义验证器。如果验证失败需要返回一个 Error 对象。不要直接
        // 使用 `console.warn` 或抛异常，因为这样 `oneOfType` 会失效。
customProp: function(props, propName, componentName) {
if (!/matchme/.test(props[propName])) {
return new Error('Validation failed!');
}
        }
    },
/* ... */
});
```
下面是项目中应用
```
TopBar.propTypes = {
    handleSubmit: React.PropTypes.func
}
module.exports = TopBar;
```
