---
title:  fullPage
category: [fullPage,前端]
tags: [fullPage]
---
```
sectionsColor:
可以给每一个section设置background-colors属性
 sectionsColor:[red,yellow,....]
controArrows：
```
<!-- more -->
 定义是否通过箭头来控制slide幻灯片 默认是true flase表示没有箭头
```
<div class="section">
    <div class="slide" style="background: yellow">slide1</div>

    <div class="slide" style="background: blueviolet">slide1</div>

    <div class="slide" style="background: yellowgreen">slide1</div>

    <div class="slide"  style="background: darkorange">slide1</div>
    <div class="slide" style="background: greenyellow">slide1</div>

</div>
```
- verticalCentered： 每一页的内容是否垂直居中
- resize：字体是否随着窗口的缩放而缩放 ，默认为false
 - scrollingSpeed: 滚动的速度，单位是毫秒，默认为700
 - anchors: 定义锚链接。默认值为[] 有了锚链接，用户就可以快速打开定位到某一个页面
注意定义锚链接的时候，值不要和页面中任意的id和那么相同，尤其是在IE浏览器下。而且定义时不需要加#

 - 在class中添加active能够实现自动定位

 - lockAnchors: 是否锁定锚链接  就是能够锁定一个页面滚动时不变

 - easing：
定义要么section滚动动画方式。默认为easeInOutCubic

 - css3:
能够实现css3样式

 - loopTop：
滚动到最顶部后是否连续滚动到底部，默认为false
 - loopBottom：
滚动到最底部后是否连续滚动回顶部，默认为false
- loopHorizontal：
横向slider幻灯片是否循环滚动。默认为true
- autoScrolling:
是否使用插件的滚动方式。默认为true，如果选择false，则会出现浏览器自带的滚动条，将不会按页滚动。而是按照滚动条的默认行为来滚动
- scrollBar:
是否包含滚动条，默认为false，如果设置为true，则浏览器自带的滚动条出现，不过是按照页滚动的额
- paddingTop/paddingBottom：
设置每一个section顶部和底部的padding ，默认都为0.一般如果我们需要设置一个固定在顶部或者底部的菜单。导航。元素等，可以使用这两个配置项
- fixedElements:
固定的元素，默认为null，需要配置一个jquery选择器。在页面滚动的时候。fixedElements设置的元素固定不动
实现绝对定位标题：


- keyboardScrolling:
是否可以使用键盘方向键导航。默认为true
- touchSensitivity：
在移动设备中滑动页面的敏感性，默认为5，是按百分比来衡量。最高为100，越大则越难滑动
- continuousVertical：
是否循环滚动
- continuousVertical:true

- animateAnchor
锚链接是否可以控制滚动动画。默认为true
如果设置为false，则通过锚链接定位到某个页面显示不再有动画效果

- recordHository：
是否记录历史默认为true
- menu:
绑定菜单，设定的相关属性与anchors的值对应后，菜单可以控制滚动，默认为false，可以设置为菜单的jQuery选择器
```
<style>
ul {
position: fixed;
top:100px;
left: 100px;
    }
</style>

<ul id="fullpageMenu">
<li data-menuanchor="page1" class="active"><a href="#page1">1 section</a></li>
<li data-menuanchor="page2"><a href="#page2">1 section</a></li>
<li data-menuanchor="page3" ><a href="#page3">1 section</a></li>
<li data-menuanchor="page4"><a href="#page4">1 section</a></li>
<li data-menuanchor="page5"><a href="#page5">1 section</a></li>
</ul>

anchors:['page1','page2','page3','page4','page5'],
```
menu:'#fullpageMenu'

- navigation:
是否显示导航，默认为false。如果设置为true，会显示小圆点，作为导航
- navigationPosition：
导航小圆点的位置，可以设置为left 或者为right
- navigationTooltips：
导航小圆点的tooltips设置，默认为[]注意顺序位置
```
anchors:['page1','page2','page3','page4','page5'],
navigation:true,
navigationPosition:'right',
navigationTooltips:['page1','page2','page3','page4','page5']
```
- showActiveTooltip:
是否显示当前页面的导航的tooltip信息。默认为false
- showActiveTooltip:true,

- slidesNavigation：
是否显示横向幻灯片的导航，默认为false
- slidesNavPosition：
横向幻灯导航的位置默认为bottom，可以设置为top或bottom
```
slidesNavigation:true,
slidesNavPosition:'top',
scrollOverflow:
内容超过满屏后是否显示滚动条，默认为false。如果设置为true，则会显示滚动条
```

```

scrollOverflow:true
  $(function(){
        $("#funllpage").fullpage({
            sectionsColor:['green','greenyellow','darkorange','blueviolet'],     //可以给每一个section设置background-colors属性
           /* controlArrows:false,                      //定义是否通过箭头来控制slide幻灯片 默认是true flase表示没有箭头
            verticalCentered:false*/                  // 每一页的内容是否垂直居中
           /* resize:true*/                                 //字体是否随着窗口的缩放而缩放 ，默认为false
           /* scrollingSpeed:100,                   //滚动的速度，单位是毫秒，默认为700
            anchors:['page1','page2','page3','page4','page5'],*/   //: 定义锚链接。默认值为[] .有了锚链接，用户就可以快速打开定位到某一个页面
            //loopTop:true,     //滚动到最顶部后是否连续滚动到底部，默认为false
           // loopBottom:true,//滚动到最底部后是否连续滚动回顶部，默认为false
 loopHorizontal:true,//横向slider幻灯片是否循环滚动。默认为true
            //paddingTop:'100px',设置每一个section顶部和底部的padding ，默认都为0.一般如果我们需要设	置一个固定在顶部或者底部的菜单。导航。元素等，可以使用这两个配置项
           // paddingBottom:'100px'
            //fixedElements:'#header',//固定的元素，默认为null
            //continuousVertical:true//是否循环滚动
          /*anchors:['page1','page2','page3','page4','page5'],
            menu:'#fullpageMenu'*/绑定菜单，设定的相关属性与anchors的值对应后，菜单可以控制滚动，默认为false，
            /*anchors:['page1','page2','page3','page4','page5'],
           navigation:true,//导航小圆点的tooltips设置，默认为[]注意顺序位置
            navigationPosition:'right',
            navigationTooltips:['page1','page2','page3','page4','page5'],
            showActiveTooltip:true,
            slidesNavigation:true,
            slidesNavPosition:'top',*/
            scrollOverflow:true

        });
    })
```
方法
moveSectionUp()
上一页
$("#funllpage").fullpage.moveSectionUp()
moveSectionDown()
下一页
$("#funllpage").fullpage.moveSectionDown()
moveTo（1，2）//第一页 第三个小页
$("#funllpage").fullpage.moveTo(1,2)

回调
afterLoad(anchorLink,index)
滚动到某一个section，且滚动结束后，会触发一次此回调函数，函数接收anchorLink和index两个参数，
anchorLink 是锚链接的名称，index是序号，从1开始计算
我可以根据anchorLink和index参数值得判断，触发相应的事件
 afterLoad:function(anchorLink,index){
                console.log("afterLoad:anchorLink="+anchorLink+";index="+index);
            }
结果：
afterLoad:anchorLink=page3;index=3
 afterLoad:anchorLink=page4;index=4
 afterLoad:anchorLink=page5;index=5
没滚动一次就会触发一次


onLeave(index,nextIndex,direction)
在离开一个section时，会触发一次此回调函数。接收index，nextIndex，
和direction3个参数
index 是离开的“页面”的序号，从1开始计算
nextIndex 是滚动到的目标”页面“序号，从1开始计算
direction判断往上滚动还是往下滚动，值是up或down  
通过return false 可以取消滚动

 onLeave:function(index,nextIndex,direction){
                console.log("onLeave:index="+index+"+nextIndex="+nextIndex+"+direction="+direction);
            }

结果：
```
onLeave:index=1+nextIndex=2+direction=down
onLeave:index=2+nextIndex=3+direction=down
onLeave:index=3+nextIndex=4+direction=down
 onLeave:index=4+nextIndex=3+direction=up
 ```

afterRender:当滚动不是第一个的时候触发
onLeave:
faterLoad
afterRender

顺序是：
渲染完毕，先移到，再滚动

afterResize :改变尺寸的时候

afterSildeLoad(anchorLink,index,slideAnchor,slideIndex)
滚动到某一个幻灯片后回调函数 与afterLoad类似
onslideLeave（anchorLink，index，slideIndex，direction，nextSlideIndex）
在离开一个slide时，触发，和onleave类似
