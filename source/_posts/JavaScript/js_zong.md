---
title:  javascript总结
category: JavaScript
tags: [js]
---
### js 常用知识总结
下面总结一下我们在项目中常用的程序介绍
** 字符串和json对象之间的转换**
- parse从字符串中解析出json对象
 <!-- more -->
  ```
    //数组
    var str = '{"name":"huangxiaojian","age":"23"}'
    结果：
        JSON.parse(str)
        Object
        age: "23"
        name: "huangxiaojian"
        __proto__: Object
   ```
    **注意：单引号写在{}外，每个属性名都必须用双引号，否则会抛出异常。**
    - stringify()用于从一个对象解析出字符串，
    ```
    //json对象
        var a = {a:1,b:2}
        结果：
        JSON.stringify(a)
        //字符串
        "{"a":1,"b":2}"
    ```
    ### 创建数组
    * 使用Array构造函数
    ```
    var a = new Array()
    var b = new Array(5);  //创建长度为5的数组
    var c = new Array("a","b","c");
    ```
    * 使用数组字面量表示法
    ```
    var a = [];
    var b = [5];  //创建一个含数字5的数组
    var c = ["a","b","c"];
    ```
    ### 数组属性
    * length表示数组的长度
    ```
    var colors = ["red","green","blue","black"];
    colors.length   //4
    ```
    * length属性并不是只读的，通过设置该值可以从数组末尾删除项或向数组中添加项
    ```
    var colors = ["red","green","blue","black"];
colors.length = 2;        //colors:["red","green"]
colors.length = 4;        //colors:["red","green",undefined,undefined]
    ```
    ### 数组方法
    * 栈、队列方法
     数组的模拟栈(FILO) 和队列(FIFO) 方法(均改变原来数组)
 
```
    var a = [6, 2, 3, 'a', 'x', 20],
    b = a.push('ab'),    //末尾添加元素，并返回新长度
    c = a.pop(),         //删除并返回数组的最后一个元素
    d = a.unshift('xy'), //开头添加元素，并返回新长度
    e = a.shift();       //删除并返回数组的第一个元素
    console.log(a);
    console.log(b);
    console.log(c);
    console.log(d);
    console.log(e);
    结果：
    [6, 2, 3, "a", "x", 20]
    7
    ab
    7
    xy
```
    1. push(item...) 向数组中添加元素，返回修改后数组的长度
        
```
        var numbers= [1,2,3,4];
        numbers.push(5)   //5   numbers:[1,2,3,4,5]
        numbers.push(6,7) //7   numbers:[1,2,3,4,5,6,7]
```

    
        2. pop() 从数组末尾移除一项，减少数组的长度，返回移除的项
       
       
```
        var numbers= [1,2,3,4];
        numbers.pop()   //4         numbers:[1,2,3]
```

       
        3. unshift(item...) 向数组前端添加任意项，返回 修改后数组的长度
    
```
var numbers= [1,2,3,4];
        numbers.unshift(5)   //5   numbers:[5,1,2,3,4]
        numbers.unshift(6,7) //7   numbers:[6,7,5,1,2,3,4]
```

        4. shift() 移除数组第一项，减少数组的长度，返回移除的项
        
       
```
var numbers= [1,2,3,4];
        numbers.shift()   //1         numbers:[2,3,4]
```

        
* 排序方法
    1. 数组反序 reverse() 反转数组项的顺序，改变原数组
    ```
    var a = [6, 2, 3, 'a', 'x', 20],
    b = a.reverse();       //返回a的引用
    console.log(a);
    console.log(b);
    结果 [20, "x", "a", 3, 2, 6]
    [20, "x", "a", 3, 2, 6]
    ```
    2. 数组排序 sort
    sort()默认情况下，即无参数情况，sort()方法按升序排列数组。该方法会调用每个数组项的tostring()方法，然后比较字符串，因此即使数组中每一项都是数值，sort()方法比较的也是字符串。
    ```
    var a = [6, 2, 3, 'a', 'x', 20],
    b = a.sort();          //ASC表顺序，先看首位，因此20排在3前面
    console.log(a);            //a变化了
    console.log(b);
    a.push('k');
    console.log(b);            //a和b指向同一个对象，b相当于a的别名
    结果：
    [2, 20, 3, 6, "a", "x"]
    [2, 20, 3, 6, "a", "x"]
    [2, 20, 3, 6, "a", "x", "k"]
    ```      
    * 操作、位置方法
   合并数组的值为字符串 join
     
```
var a = [1, 2, 3],
        b = a.join('*'); //默认为之间加上 ，          
        console.log(a);      //a并没有变
        console.log(b);    
        结果
        [1, 2, 3]
        1*2*3
```
   
    1. 合并数组 concat
    concat()其参数可以是一个或多个项，也可以是一个或多个数组。创建一个当前数组的副本，然后在数组末尾添加参数项，并返回** 新的数组 **，原数组不变
  ```
        var a = [1, 2, 3],
        b = [4, 5, 6],
        c;
        c = b.concat(a);     //将a加在b上,返回新数组，a和b并没有变。参数数量不限
        console.log(b);
        console.log(c);
        结果
        [4, 5, 6]
        [4, 5, 6, 1, 2, 3]
 ```
        2. 取数组中需要的部分 slice
        获取截取数组，如果是一个参数，则获取从该参数位置开始到数组结束所有值，如果有两个参数，则获取从起始值位置到结束值位置的值（不包括结束值位置项），返回新的数组。原数组不变
        如果结束值小于起始位置则返回空数组。


```
var a = [6, 2, 3, 'a', 'x', 20],
        b = a.slice(0, 2);//下标从0取到2(不包括2)，没有第二个参数则默认到末尾。第一个参数为负表示从末尾开始数。第一个参数小于第二个参数则为空。
        console.log(a);
        console.log(b);   //b是a一部分的副本,a本身不变
        结果
         [6, 2, 3, "a", "x", 20]
         [6, 2]
```

注意： 如果参数中存在负数，则将参数值加上数组长度来计算。如：
```

var numbers= [1,2,3,4];
numbers.slice(-1)          //[4]         numbers:[1,2,3,4]
numbers.slice(-4,-2)       //[1,2]         numbers:[1,2,3,4]
```
    3. 修改数组 splice (既然是修改数组，肯定数组本身会变的啦)
 ```
var a = [1, 2, 3, 4],
    b = a.splice(0, 2, 6);
console.log(a);          
console.log(b);          //b为被删掉的数组部分
结果：
[6, 3, 4]
[1, 2]
```
　　a.splice(index, num, newItem1, newItem2...):index为开始选择的元素下标，num为接下来要删除元素的个数，newItem为接下来(在删完的地方)要添加的新元素(非必须)。这个方法用途最多，如

　　删除指定下标(2,也就是第三个)元素,此时不设置需要添加的newItem，而num设为1
```
var a = [1, 2, 3, 4],
    b = a.splice(2, 1);
console.log(a);
console.log(b); 
　　在任意位置添加任意多个元素(如在下标2后添加两个元素'7','8'),此时num设为0

var a = [1, 2, 3, 4],
    b = a.splice(2, 0, 7,8);
console.log(a);
console.log(b);   //没有删除，b返回[]
结果
[1, 2, 4]
[3]
```
　　根据元素值删除元素(结合jquery)


```
var a=['one','da','xiao','ha'];
a.splice($.inArray('da',a),1);
console.log(a);
结果
["one", "xiao", "ha"]
```

  4.  indexOf()从前向后查找，接受两个参数：查找的项和查找的起点位置（可选），默认从数组的起始位置向后查找，返回索引值
    
```
var numbers= [1,2,3,4,4,5,3,1,2];
numbers.indexOf(2)              //1        numbers:[1,2,3,4,4,5,3,1,2]
numbers.indexOf(2,4)              //8       numbers:[1,2,3,4,4,5,3,1,2]
```
5. lastIndexOf()从后向前查找，接受两个参数：查找的项和查找的起点位置（可选），默认从数组的结束位置向前查找，返回索引值
```
var numbers= [1,2,3,4,4,5,3,1,2];
numbers.lastIndexOf(2)              //8        numbers:[1,2,3,4,4,5,3,1,2]
numbers.lastIndexOf(4,3)            //3        numbers:[1,2,3,4,4,5,3,1,2], 从[3]位向前查找
```
* 遍历方法

1. every(fn)对数组中的每一项运行给定的函数，如果该函数对每一项都返回true,则返回true
```
var numbers= [1,2,3,4,5];
numbers.every(function(item,index,array){
  return (item>0);
})                                                          //true       
numbers.every(function(item,index,array){
  return (item>2);
})  //false
```                                                       
2. filter(fn)对数组中的每一项运行给定的函数，返回该函数会返回true的项组成的数组
```
var numbers= [1,2,3,4,5];
numbers.filter(function(item,index,array){
   return (item>2);
})  //[3,4,5]
```                                                        
3. forEach(fn)对数组中的每一项运行给定的函数，没有返回值
4. map(fn)对数组中的每一项运行给定的函数，返回每次函数调用的结果组成的数组
```
var numbers= [1,2,3,4,5];
numbers.map(function(item,index,array){
  return (item+10);
})//[11,12,13,14,15]
```                                                          
5. some(fn)对数组中的每一项运行给定的函数，如果该函数对任一项返回true,则返回true
```
var numbers= [1,2,3,4,5];
numbers.some(function(item,index,array){
  return (item>3);
})                   
```
6. 遍历数组 (同时也是对象遍历属性的方法)
    ```
    var a = [1, 2, 3];
    for (x in a) {
    console.log(x);
    }
    结果 0 1 2

    ```
 
- 小结:综上所述，js数组的原生方法里面
- 修改自身的有: splice, pop, push, shift, unshift, sort, reverse
- 不修改自己身的: slice, concat, join

**Jquery常用js方法**
　1. 遍历
　可以对所有的元素进行操作。如果想要满足条件退出，用return false(       绝大部分jquery方法都可以这么退出)。 
```
　　$.each(arr, callback(key, val));      //可以链式调用，返回arr，为本身
　var a = [1, 2, 3, 4];
$.each(a, function(key, val) {     //以jQuery对象的方法调用，兼容性好;也可以用$(a)将a转化为jquery对象，然后以$(a).each(function(){})的形式调用,下面的方法同
console.log(a[key] + '下标为' + key + '值为' + val);
});
结果
1下标为0值为1
2下标为1值为2
3下标为2值为3
4下标为3值为4
```
2. 筛选
　　$.grep(arr, callback, invert)

　　invert为false表示对callback的筛选取反。 默认为true。


```
var a = [1, 2, 3, 4];
$.grep(a, function(val, key) {  //不能链式调用，返回[],所以可以加上return实现链式,返回满足条件的副本
　　if (a[key] > 2) {
　　　　console.log(key);
　　}
　　return val;
});

　　常用做获取两个数组中相同(或不相同)的部分
var a= [1, 2, 3, 4],
    b=[1,3,5,7];
$.grep(a,function(val,key){
    if(b.indexOf(val)>=0){
        return val;
    }
},false)

结果：[1, 3]
```

4.合并
　　$.merge(arr1,arr2)  arr1后面加上arr2后返回arr1


```
var a=[1,2,3],
    b=[4,5,6];
$.merge(a,b);             //可以有多个参数(居然不报错!)，但是第三个及以后的没用(test in FF and Chrome)
```

　　
　　　5.过滤相同元素
　　$.unique(arr)//过滤Jquery对象数组中重复的元素(内部实现为===)(不同版本不一样，不要用)


```
var a = [ 1 , 1 , 2 , 3 , 7 , 4 , 5 , 5 , 6 , 6 ];
$.unique(a)
```
　　6.判断
　　$.inArray(val,arr)  判断val是否在arr里面


```
var a = [1, 2, 3, 4];
$.inArray(2, a);     //有的话返回下标，没有的话返回-1
```

