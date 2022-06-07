---
title: border vs outline __zh
category: CSS
---

### Differences

1. `outline`属性不占用空间，意味着是否使用轮廓不会影响元素的尺寸。

2. `border` 支持圆角属性`border-radius`，`outline`是没有的。

3. 我没可以通过`border-top`、`border-left`、`border-bottom`和`border-right`定义变宽的样式。`outline`则不能设置任何边框的样式。

4. 元素的`outline`可能是非矩形的。

    在下面的示例代码中，轮廓以非矩形形状显示：

    ```html
    <div>
        ...
        <span style="outline: 0.25rem solid blue"> ... </span>
        ...
    </div>
    ```

### 最佳实践

`outline`的主要目的是支持元素的可访问性。当用户使用 _Tab_ 键在链接、按钮之间跳转时，它能提供视觉反馈。

当元素被聚焦时，你不能移除`outline`样式。设置 `outline: none` 或 `outline: 0` 将导致不使用鼠标或有视觉障碍的人无法访问该元素。

最早的时候，一个流行的CSS[重置库](https://meyerweb.com/eric/tools/css/reset/reset200802.css)，移除了`outline`属性，但是作者留下了评论，提醒我们去定义`:focus`状态下的样式：

```css
/* remember to define focus styles! */
:focus {
    outline: 0;
}
```

但是在[最新版本](https://meyerweb.com/eric/tools/css/reset/reset.css)中，`outline`重置已经被移除了。

如果您必须删除轮廓样式，则建议提供替代样式。
以下是一些纯CSS得解决方案：

-   设置背景颜色：

    ```css
    a:focus {
        background: ...;
    }
    ```

-   设置文本颜色：

    ```css
    a:focus {
        color: ...;
    }
    ```

-   结合上述两种方式：

    ```css
    a:focus {
        background: ...;
        color: ...;
    }
    ```

-   使用不同的样式去规范化轮廓外观，比如：

    ```css
    a:focus {
        outline: thin dotted;
    }
    ```

还有另一种方式，使用JavaScript来处理。如果检测到元素有鼠标世界，则移除`outline`样式。
相反，如果检测到键盘事件，则恢复`outline`样式。

这里提供了代码演示这一想法：

```js
// Append a custom style to `head`
const style = document.createElement('style');
document.head.appendChild(style);

const remove = () => (style.innerHTML = ':focus { outline: 0 }');
const restore = () => (style.innerHTML = '');

// Remove the outline initially
remove();

document.addEventListener('mousedown', () => restore());
document.addEventListener('keydown', () => remove());
```

一些其他网站，比如[Github](https://github.com)使用了类似的方法。从一个重置`outline`属性的CSS类开始。

```css
.intent-mouse a:focus {
    outline: 0;
}
```

初始化的时候，这个CSS类被添加到body元素：

```html
<body class="intent-mouse">
    ...
</body>
```

通过监测键盘和鼠标事件，我们可以移除这个类或者添加这个类到body元素：

```js
document.addEventListener('mousedown', () => {
    document.body.classList.add('intent-mouse');
});

document.addEventListener('keydown', (e) => {
    // If users press the Tab key
    // then we assume that they intent to use the keyboard to navigate
    if (e.key === 'Tab') {
        document.body.classList.remove('intent-mouse');
    }
});
```

### Tip

当你想要页面的元素可视化，`outline`属性是很有用的。
在下面的[示例代码](https://htmldom.dev/loop-over-a-nodelist)中，我们读取所有的元素并且给`outline`设置一个随机的[颜色属性](https://1loc.dev/#generate-a-random-hex-color):

```js
[].forEach.call(document.querySelectorAll('*'), (ele) => {
    const color = `#\${Math.random().toString(16).slice(2, 8).padEnd(6, '0')}`;
    ele.style.outline = `1px solid \${color}`;
});
```

当然，你将会需要一个反转的命令去[重置](https://htmldom.dev/set-css-style-for-an-element)`outline`属性：

```js
[].forEach.call(document.querySelectorAll('*'), (ele) => ele.style.removeProperty('outline'));
```

你可以改变选择器`*`去匹配任何你想要去设置的元素，比如：

```js
// Set the outline for links only
[].forEach.call(
    document.querySelectorAll('a'),
    ...
);
```
