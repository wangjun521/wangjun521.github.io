# 页面滚动


- scrollingElement

  该对象可以非常兼容地获取 scrollTop、scrollHeight 等属性，在移动端跟 PC 端都屡试不爽`document.scrollingElement.scrollHeight`标准模式返回 documentElement，怪异模式返回 body

- 滚动到底部

```javascript
window.scrollTo({
  left: 0,
  top: document.scrollingElement.scrollHeight
});
```

- 判断浏览器已滚动到底部

```java
window.addEventListener("scroll", () => {
  const { scrollTop, scrollHeight, clientHeight } = document.scrollingElement;
  // 当前滚动高度 + 视口高度 >= 文档总高度
  if (scrollTop + clientHeight >= scrollHeight) {
    console.log("已到达底部");
  }
});
```

- ios设备局部滚动不顺畅

```css
.box {
  -webkit-overflow-scrolling: touch;
}
```

- 滚动传播

  指有多个滚动区域，当一个滚动区域滚动完之后，继续滚动会传播到到父区域继续滚动的行为

```css
.box {
  overscroll-behavior: contain; // 阻止滚动传播
}
```

- 滚动结束后强制滚动到指定元素

```css
ul {
  scroll-snap-type: x mandatory;
  li {
    scroll-snap-align: start;
  }
}
```

- 移动端适配

```css
html {
  font-size: 13.3333vw;
}
```

- input的placeholder样式

  `input`输入框的`placeholder`在移动端并非垂直居中 尤其不要尝试用`height === line-height`(这个会出现光标问题) 此时给`input` 添加属性`line-height:normal`可解决

- 滑动穿透

```javascript
document.querySelector(“.mask").addEventListener("touchmove", event => {
  event.preventDefault();
})
在vue中也可以直接使用`@touchumove.prevent`
```

- ios上input失焦后未回弹

```javascript
focus() {
  this.scrollTop = document.scrollingElement.scrollTop
},
blur() {
  document.scrollingElement.scrollTo(0, this.scrollTop)
}
```

- 网页忽略自动识别

```html
<!— 忽略浏览器自动识别数字为电话号码 —>
<meta name="format-detection" content="telephone=no" />
<!-- 忽略浏览器自动识别邮箱账号 -->
<meta name="format-detection" content="email=no" />
```

- 弹出数字键盘

```html
<!— 有”#" "*"符”输入 ——>
<input type="tel" novalidate="novalidate" pattern="[0-9]*" />
type="tel", 是 HTML5 的一个属性, 表示输入框类型为电话号码, 在 Android 和 IOS上表现差不多, 都会有数字键盘, 但是也会有字母, 略显多余
pattern="[0-9]", pattern 用于验证表单输入的内容, 通常 HTML5 的 type 属性, 比如email、tel、number、data 类、url 等, 已经自带了简单的数据格式验证功能了, 加上pattern 后, 前端部分的验证更加简单高效了。IOS 中, 只有 [0-9]\*才可以调起九宫格数字键盘, \d 无效, Android 4.4以下（包括X5内核）, 两者都调起数字键盘
novalidate="novalidate", novalidate属性规定当提交表单时不对其进行验证, 由于 pattern校验兼容性不好, 可以不让其校验, 只让其唤起纯数字键盘, 校验工作由 js 去做
<!— 纯数字 -->
<input pattern="“\d*”" />
```

- 解决伪类失效

```html
<body ontouchstart ></body>
```

- 网页状态栏背景色

```html
apple-mobile-web-app-capable是设置Web应用是否以全屏模式运行;语法:
<meta name="apple-mobile-web-app-capable" content="yes" /> //content设置为yes
Web应用会以全屏模式
<meta name="apple-mobile-web-app-status-bar-style" content="black" />
```

- ios键盘默认首字母大写解决方案

```html
<input autocapitalize=“off" autocorrect="off" />
```

- ios上使用input但弹出自定义键盘

  input 的 readonly属性 在 ios 下 获取焦点时仍会弹出虚拟键盘 此时使用unselectable="on" onfocus="this.blur()"解决

- 安卓上弹出的键盘覆盖文本框

  安卓微信 H5 弹出软键盘后挡住 input 输入框 也可以在文本框获取焦点时不判断机型 直接加延时

```javascript
focus(){
  let u = navigator.userAgent, app = navigator.appVersion;
  let isAndroid = u.indexOf('Android') > -1 || u.indexOf('Linux') > -1;
  if(isAndroid){
    setTimeout(function() {
      document.activeElement.scrollIntoViewIfNeeded();
      document.activeElement.scrollIntoView();
    }, 500);
  }
}
```

- 锚点跳转

  scrollIntoView()中可以传入Boolean类型的参数，默认是true，就是滚动定位到浏览器的顶部，如果传入false，就是滚动定位到浏览器的底部

```javascript
document.getElementById(IdSlector).scrollIntoView();
```

[scrollIntoView文档](https://developer.mozilla.org/zh-CN/docs/Web/API/Element/scrollIntoView)


