# js的一些tips

- 数组中根据对象某一属性排序
```javascript
function compare(property) {
  return function(a, b) {
    var value1 = a[property];
    var value2 = b[property];
    return value1 - value2;
  };
}
```

- 数据去重

```javascript
function removeRepeatArray(arr) {
  return arr.filter(function(item, index, self) {
    return self.indexOf(item) === index;
  });
}
```

- 数组打乱顺序

```javascript
function upsetArr(arr) {
  return arr.sort(function() {
    return Math.random() - 0.5;
  });
}
```

- 绑定回车事件

```javascript
document.doucumentElement.onkeydown = e => {
  let ecode = e.keyCode ? e.keyCode : e.which ? e.which : e.charCode;
  if (ecode === 13) {
    // do something
  }
};
```

- 移动端适配

```javascript
var rem = {
  baseRem: 40,
  // 基准字号，按照iphone6应该为20，此处扩大2倍，便于计算
  baseWidth: 750,
  // 基准尺寸宽，此处是按照ihpone6的尺寸
  rootEle: document.getElementsByTagName("html")[0],
  initHandle: function() {
    this.setRemHandle();
    this.resizeHandle();
  },
  setRemHandle: function() {
    var clientWidth =
      document.documentElement.clientWidth || document.body.clientWidth;
    this.rootEle.style.fontSize =
      (clientWidth * this.baseRem) / this.baseWidth + "px";
  },
  resizeHandle: function() {
    var that = this;
    window.addEventListener("resize", function() {
      setTimeout(function() {
        that.setRemHandle();
      }, 300);
    });
  }
};
rem.initHandle();
```

- ios弹出键盘遮挡表单

```javascript
window.addEventListener("resize", function() {
  if (
    document.activeElement.tagName === "INPUT" ||
    document.activeElement.tagName === "TEXTAREA" ||
    document.activeElement.getAttribute("contenteditable") == "true"
  ) {
    window.setTimeout(function() {
      if ("scrollIntoView" in document.activeElement) {
        document.activeElement.scrollIntoView();
      } else {
        document.activeElement.scrollIntoViewIfNeeded();
      }
    }, 0);
  }
});
```


