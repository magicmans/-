/*看此文档建议打开自动换行,观看体验更佳哦~~*/
由于上次有事所以写了这个类似摸鱼性质的总结还多请老师学长们包含~~~
为了避免再次出现这样的情况所以这篇总结多半会以日志作为大体结构还请老师多多包含。
而且对于学习微信小程序的前端来说对于基础组件仅仅只看其中的一部分是有点不行的所以我选择从头
看到尾其中属于我的那一部分会着重看，否则后期设计小程序的话不好统一，所以我都看了一点~~~

///////////**分割线**////////////


一般视图组件<view>（视图容器）
hover-class	String	none	指定按下去的样式类。当 hover-class="none" 时，没有点击态效果
hover-class：指定按下去的样式类。当 hover-class="none" 时，没有点击态效果
eg:
<view hover-class=‘red‘ class=‘view‘ >hover可不是鼠标滑过哦</view>

.red{
  color: red;
}
/*这个就可以可以点文字变颜色*/
这个容器可以将其改造成一这个点击按钮就可以缩放的方式
/*代码*/
<view id="{{id}}">内容</view>
<button bindtap="show">dian</button>
<view class='ui-share-icon' hover-class="ui-share-hover"> 
     <image class='ui-share-img'  src='../../images/share-icon.png'></image>
</view-->
首先会编写一个view，然后在里面添加一张图片。接下去，对view加上hover-class的属性。
.ui-share-icon{
  text-align: center;
}

 .ui-share-img{
  width: 115rpx;
  height: 121rpx;
 }

 .ui-share-hover{
   opacity: 0.9;
   transform: scale(0.9,0.9);
 }

第二步，编写对应的样式，其中hover-class 指定了对应的样式ui-share-hover，当中样式-关键-使用transform: scale(0.9,0.9) 的方式对view进行一个缩放产生一个缩小的效果。

hover-stop-propagation	Boolean	false	指定是否阻止本节点的祖先节点出现点击态
用发防止其父节点出现点击态（其实这个组件简绍不多我理解也不多，可能别人工程需要用这个~）代码
<view hover-stop-propagation="ture">takeme </view>
/*我在网上看了一些东西，当然是复制粘贴啦~~*/
hover-stop-propagation：阻止事件冒泡，指定是否阻止本节点的祖先节点出现点击态，遗憾的发现无论指定值为true或者false，或者0 或者 -1,亦或是什么都不指定 ，只要出现hover-stop-propagation他就阻止冒泡了。
eg：
<view hover-class=‘bg_black‘>
<view>另一部分内容</view>
<view hover-stop-propagation="true" hover-class=‘yellow‘>hover-stop-propagation了解</view>
</view>

hover-start-time	Number	50	按住后多久出现点击态，单位毫秒
hover-start-time：按住后多久出现点击态，单位毫秒
eg：
<view hover-start-time=‘1000‘ hover-class=‘red‘>一秒后出状态</view> 

hover-stay-time	Number	400	手指松开后点击态保留时间，单位毫秒
hover-stay-time：手指松开后点击态保留时间，单位毫秒
eg:
 <view hover-stay-time="3000" hover-class=‘red‘>我能点亮三秒钟</view>
/////****在使用red时在wxss里提出.red样式******//////////
.red{
  color: red;
}
这个就是.red样式，可以多种变化让你的首页更骚包~~~
注：我jio得那个让图片变小的操作还是十分不错的可以利用多种样式进行图片的变化起非常nice的作用~~~
///////////**分割线**////////////
高级视图插件
scroll-view

scroll-x	Boolean	false	允许横向滚动
开启
一般样式设计法

<scroll-view scroll-x="true" style=" white-space: nowrap; display: flex" >
  <view style="background: red; width: 200px; height: 100px; display: inline-block" ></view>
  <view style="background: green; width: 200px; height: 100px; display: inline-block"></view>
  <view style="background: blue; width: 200px; height: 100px; display: inline-block"></view>
  <view style="background: yellow; width: 200px; height: 100px; display: inline-block"></view>
</scroll-view>

wxss样式设计法：
<scroll-view class="box" scroll-x="true" >
  <view class="box-item" >1</view>
  <view class="box-item" >2</view>
  <view class="box-item" >3</view>
</scroll-view>
wxss的样式申请
.box {
    width:100vw;
    hight: 200rpx;
    white-space: nowrap;
    border: 1px solid red;
    box-sizing: border-box
}
.box-item {
    width: 45%;
    hight:100%;
    border:2rpx solid green;
    box-sizing: border-box;
    display: inline-block
}
注：white-space: nowrap;必须要申请不然会出事会换行~~~
垂直滚动

/////////////////////**************************//////////////////////////////
关于white-space的函数
  normal: 正常无变化(默认处理方式.文本自动处理换行.假如抵达容器边界内容会转到下一行)
  pre: 保持HTML源代码的空格与换行,等同与pre标签
  nowrap: 强制文本在一行,除非遇到br换行标签
  pre-wrap: 同pre属性,但是遇到超出容器范围的时候会自动换行
  pre-line: 同pre属性,但是遇到连续空格会被看作一个空格
  inherit: 继承
/////////////////////**************************//////////////////////////////
scroll-y	Boolean	false	允许纵向滚动

在开始一定要注意关于高度的申请
<scroll-view scroll-y="true" style="height: 200px">
    <view style="background: red; width: 100px; height: 100px" ></view>
    <view style="background: green; width: 100px; height: 100px"></view>
    <view style="background: blue; width: 100px; height: 100px"></view>
    <view style="background: yellow; width: 100px; height: 100px"></view>
</scroll-view>

其余组件
upper-threshold	Number / String	50	距顶部/左边多远时（单位px，2.4.0起支持rpx），触发 scrolltoupper 事件
lower-threshold	Number / String	50	距底部/右边多远时（单位px，2.4.0起支持rpx），触发 scrolltolower 事件
scroll-top	Number / String		设置竖向滚动条位置（单位px，2.4.0起支持rpx）
scroll-left	Number / String		设置横向滚动条位置（单位px，2.4.0起支持rpx）
scroll-into-view	String		值应为某子元素id（id不能以数字开头）。设置哪个方向可滚动，则在哪个方向滚动到该元素
scroll-with-animation	Boolean	false	在设置滚动条位置时使用动画过渡
enable-back-to-top	Boolean	false	iOS点击顶部状态栏、安卓双击标题栏时，滚动条返回顶部，只支持竖向
bindscrolltoupper	EventHandle		滚动到顶部/左边，会触发 scrolltoupper 事件
bindscrolltolower	EventHandle		滚动到底部/右边，会触发 scrolltolower 事件
bindscroll	EventHandle		滚动时触发，event.detail = {scrollLeft, scrollTop, scrollHeight, scrollWidth, deltaX, deltaY}
aria-label	String		无障碍访问，（属性）元素的额外描述 2.5.0

关于滚动条的设计可以丰富微信小程序的UI看情况使用

其中可以重点注意bindscrolltoupper，bindscrolltolower的使用
并且使用此组件可以实现上拉加载，下拉刷新
详见https://blog.csdn.net/huang100qi/article/details/80666310
贼有用
///////////**分割线**////////////
swiper 滑块视图容器
根据官方文档，在自己的程序上运行，并打进代码的效果图，swiper滑块视图容器，是用来展示图片，控制图片的
由于这个模块是用来作为一般展示的，所以直接上属性，先看属性在看代码


indicator-dots	表示显示面板的指示点，图片下的小圆圈
indicator-color	表示指示点的颜色
indicator-active-color	表示当前选中的指示点颜色
autoplay	表示为是否自动切换
current	表示当前所在的滑块 index
current-item-id	当前所在滑块的 item-id，不能与current被同时指定
interval	表示自动切换时间间隔
duration	表示为滑动动画时长
circular	表示是否采用衔接滑动
previous-margin	表示前边距，用于露出前一项的一小部分，接受 px 和 rpx 值，就是在整块模板中露出前一项的一小部分
next-margin	表示后边距，与上述同理
display-multiple-items	表示显示的滑块数量，就是显示多少张图在界面上，默认为1，如果定位2，那么就两张图片设定在界面上，界面各自分一半
skip-hidden-item-layout	表示是否跳过未显示的滑块布局，设为 true 可优化复杂情况下的滑动性能，但会丢失隐藏状态滑块的布局信息
bindchange	current 改变时会触发 change 事件，event.detail = {current: current, source: source}
bindanimationfinish	动画结束时会触发 animationfinish 事件，event.detail 同上

代码：
<swiper indicator-dots="{{indicatorDots}}" autoplay="{{autoplay}}" interval="{{interval}}" duration="{{duration}}" circular='{{circular}}' current="0">
// 用于展示轮播图效果
  <block wx:for="{{imgUrls}}">
    <swiper-item>
      <image src="{{item}}" class="slide-image" width="355" height="150" />
    </swiper-item>
  </block>
</swiper>
// 用于定义是否显示面板指示点
<button bindtap="changeIndicatorDots"> indicator-dots </button>
// 用于定义是否自动切换
<button bindtap="changeAutoplay"> autoplay </button>
// 滑动进度，这个按钮效果用于更改自动切换时间间隔
<slider bindchange="intervalChange" show-value min="500" max="2000" /> interval
// 滑动进度，这个按钮效果用于更改滑动动画时长
<slider bindchange="durationChange" show-value min="1000" max="10000" /> duration
//wxml配置

Page({
  data: {
    imgUrls: [
      'http://img02.tooopen.com/images/20150928/tooopen_sy_143912755726.jpg',
      'http://img06.tooopen.com/images/20160818/tooopen_sy_175866434296.jpg',
      'http://img06.tooopen.com/images/20160818/tooopen_sy_175833047715.jpg'
    ],
    indicatorDots: true,
    circular: true,
    autoplay: true,
    interval: 2000,
    duration: 1000
  },
  changeIndicatorDots: function(e) {
    this.setData({
      indicatorDots: !this.data.indicatorDots
    })
  },
  changeAutoplay: function(e) {
    this.setData({
      autoplay: !this.data.autoplay
    })
  },
  intervalChange: function(e) {
    this.setData({
      interval: e.detail.value
    })
  },
  durationChange: function(e) {
    this.setData({
      duration: e.detail.value
    })
  }
})
//js逻辑层设计在j
s中图片资源来源于官方文档，四种改变效果函数，changeIndicatorDots（显示指示点），changeAutoplay（是否自动轮播），intervalChange（展示效果时长），durationChange（切换时间时长）可以根据自定义进行函数更改。

.slide-image{
  width: 100%;
}
//wxss设计只是让图片宽度占满父元素而已。


说明一下：
swiper为滑块视图容器，其实就是轮播图的效果。
代码中indicator-dots="{{indicatorDots}}"的效果是用来显示指示点的，就是图片中下方的小圆圈。
autoplay="{{autoplay}}"为是否可以自动切换的效果，如果不设置，那就只有一张图片显示到界面中。
current="0"为当前显示在哪个滑块，为啥为0，因为默认值为0，可知从零开始算起嘛。
interval="{{interval}}"为自动切换时间的间隔，表示每张图片显示到它设定的时间就开始切换到下一个视图即图片，如果设定为3000即3秒，那么图片展示到3秒后，进入到下一个图片。
duration="{{duration}}"为滑动动画时长，怎么理解呢？就是第一张图片切换到第二张图片的时长，即第一张滑出，第二张滑入到完，所用的时间长而已。
circular="{{circular}}"为是否采用衔接滑动，怎么理解呢？衔接？如果这个属性不设定，那么如果轮播图是三张图片，第一张展示到第三张即最后展示完，它会返回到第一张，那样的效果会不好看。如果设定了该属性，且为true的话，那么展示完后，直接进入到第一张图的界面。
其实还有两个属性本列子也未使用，可以自己设定然后优化UI。
///////////**分割线**////////////
movable-view 可移动的视图容器，在页面中可以拖拽滑动
对于这个新增的api一定要配合movable-area一起使用已达到最完美的效果

上属性定义：


direction	String	none	movable-view的移动方向，属性值有all、vertical、horizontal、none	
inertia	Boolean	false	movable-view是否带有惯性	
out-of-bounds	Boolean	false	超过可移动区域后，movable-view是否还可以移动	
x	Number / String		定义x轴方向的偏移，如果x的值不在可移动范围内，会自动移动到可移动范围；改变x的值会触发动画	
y	Number / String		定义y轴方向的偏移，如果y的值不在可移动范围内，会自动移动到可移动范围；改变y的值会触发动画	
damping	Number	20	阻尼系数，用于控制x或y改变时的动画和过界回弹的动画，值越大移动越快	
friction	Number	2	摩擦系数，用于控制惯性滑动的动画，值越大摩擦力越大，滑动越快停止；必须大于0，否则会被设置成默认值	
disabled	Boolean	false	是否禁用	1.9.90
scale	Boolean	false	是否支持双指缩放，默认缩放手势生效区域是在movable-view内	1.9.90
scale-min	Number	0.5	定义缩放倍数最小值	1.9.90
scale-max	Number	10	定义缩放倍数最大值	1.9.90
scale-value	Number	1	定义缩放倍数，取值范围为 0.5 - 10	1.9.90
animation	Boolean	true	是否使用动画	2.1.0
bindchange	EventHandle		拖动过程中触发的事件，event.detail = {x: x, y: y, source: source}，其中source表示产生移动的原因，值可为touch（拖动）、touch-out-of-bounds（超出移动范围）、out-of-bounds（超出移动范围后的回弹）、friction（惯性）和空字符串（setData）	1.9.90
bindscale	EventHandle		缩放过程中触发的事件，event.detail = {x: x, y: y, scale: scale}，其中x和y字段在2.1.0之后开始支持返回	1.9.90


为了配合movable-view的学习将movable-area合并在了一起学习
其实这个组件说白了就是movable-view 的可移动区域~~
上movable-area属性

scale-area	Boolean	false	当里面的movable-view设置为支持双指缩放时，设置此值可将缩放手势生效区域修改为整个movable-area	1.9.90

注意：movable-area 必须设置width和height属性，不设置默认为10px

当movable-view小于movable-area时，movable-view的移动范围是在movable-area内；

当movable-view大于movable-area时，movable-view的移动范围必须包含movable-area（x轴方向和y轴方向分开考虑）

对于这个组件我决定不去过多深究其本身的属性已经简绍得十分清楚组件自己使用时直接调用就可以了，
如果有额外需求查一查属性表即可~~~


上测试代码：
<movable-area style="height: 200px;width: 200px;background: red;">

 <movable-view direction="all" style="height: 50px; width: 50px; background: blue;">

 </movable-view>

</movable-area>
剩下的属性可以一一测试还是比较nice的

















