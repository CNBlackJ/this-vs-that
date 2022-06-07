---
title: 'display: none vs opacity: 0 vs visibility: hidden __zh'
category: CSS
---

有三种常见的CSS属性让元素变得不可见：

-   `display: none`
-   `opacity: 0`
-   `visibility: hidden`

### 不同点

1. `display: none` 在元素渲染是不占用空间。其他方式则正常占用空间。

2. 浏览器不会响应设置了`display: none`、`visibility: hidden`属性的元素的任何事件。
   `visibility: hidden`的行为与`opacity: 0`和`pointer-events: none`结合的行为相似。

3. 考虑到可访问性，`opacity: 0`是唯一一个可以通过`Tab`进行元素访问的属性，并且元素内容能被屏幕阅读者看见。

4. 应用了`display: none` 或者 `opacity: 0`属性将会影响到子元素。`visibility: hidden`则不会改变任何子元素的可视性。

5. 值得注意的是，如果要测量元素的大小，则不能使用 `display: none`。

如第一个不同点中所述，一个元素使用了`display: none`，不会在页面中有任何空间。因此，所有和元素大小尺寸有关的属性，比如`clientHeight`, `clientWidth`, `height`, `offsetHeight`, `offsetWidth`, `scrollHeight`, `scrollWidth` 和 `width`都会是0。

`getBoundingClientRect()` 方法返回的所有属性也为零。

同样，具有 `visibility: hidden` 的元素将具有空的内部文本（等效于 `innerText` 属性）。

### Tip

使用 Chrome DevTools，您可以通过右键单击元素来隐藏页面中的任何元素，然后单击_Hide element_。

![使用 Chrome DevTools 隐藏元素](/assets/hide-element-chrome.png)

为了在不破坏布局的情况下做到这一点，Chrome 为元素添加了一个名为 __web-inspector-hide-shortcut__ 的 CSS 类：

```css
.__web-inspector-hide-shortcut__ {
    visibility: hidden !important;
}
```

如上所述，将可见性样式应用于元素不会影响任何子元素，因此 Chrome 添加了以下样式以使所有子元素不可见：

```css
.__web-inspector-hide-shortcut__ * {
    visibility: hidden !important;
}
```

### Good to know

如今，我们很容易用一行 CSS 为给定元素及其子元素设置不透明度：

```css
.overlay {
    opacity: 0.75;
}
```

很多年前，当 Web 开发人员不得不处理 Internet Explorer 6、7、8 等旧版浏览器时，为了支持各种浏览器，我们必须做以下事情：

```css
.overlay {
    /* For IE 5, 6, 7 */
    filter: alpha(opacity=75);

    /* For IE 8 */
    -ms-filter: 'progid:DXImageTransform.Microsoft.Alpha(Opacity=75)';

    /* For Netscape */
    -moz-opacity: 0.75;

    /* For Safari 1.x */
    -khtml-opacity: 0.75;

    /* Our good friends */
    opacity: 0.75;
}
```
