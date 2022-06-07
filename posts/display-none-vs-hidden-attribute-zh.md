---
title: 'display: none vs [hidden]__zh'
category: CSS
---

HTML5新增了`hidden`属性，该属性和CSS的`display: none`对元素有相同的影响。
如果设置了`hidden`属性，那这个元素将不会显示：


```html
<div hidden>
    <!-- This will disappear from the screen -->
</div>
```

两者都是从屏幕中隐藏内容。

### 不同点

1. `display: none`和`hidden`生效方式相同。但是`hiden`属性提供了更好的语法语义。
2. `display: none`支持更老的浏览器，但是`hidden`[不支持](https://caniuse.com/#feat=hidden)IE10及以下的浏览器。

为了解决这个问题，我们可以简单的设置一下：

```css
[hidden] {
    display: none;
}
```

这个解决方式应用在一些现代化的CSS标准库中，比如[Normalize.css](https://necolas.github.io/normalize.css)。

但是修改`display`属性值(比如：`display: flex`)将会重写`hidden`属性的行为。

常用库通过设置`!important`来防止被重写：

```css
[hidden] {
    display: none !important;
}
```

在Bootstrap 4's [Reboot](https://getbootstrap.com/docs/4.1/content/reboot/#html5-hidden-attribute), [PureCSS](https://purecss.io/base/)中能找到这种实践。
