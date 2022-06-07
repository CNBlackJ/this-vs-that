---
title: 'style="width: ___" vs width="___" __zh'
category: CSS
---

有两种方法可以定义元素的尺寸：

-  使用 `height` 或 `width` 属性：

```html
<img height="100" />
```

- 或者在 CSS 样式中使用 `height` 或 `width` 属性：

```html
<img style="height: 100px" />
```

### 区别

1. CSS中的`width` 和 `height` 属性适用于所有 HTML 元素。 但是HTML中的 `width` 和 `height` 属性仅适用于某些元素，例如 `canvas`、`image`、`table`、`td` 等。

    ```html
    <!-- Work -->
    <img width="200px" />

    <!-- Does NOT work -->
    <div width="200px"></div>
    ```

2. 对于`canvas`，显示的效果有点不同。

    根据[HTML规范](https://html.spec.whatwg.org/multipage/canvas.html#attr-canvas-width)如果缺少 `width` 和 `height` 属性，则将使用默认值。

    `width` 属性默认为 300，`height` 属性默认为 150。

    建议直接或通过 JavaScript 设置画布的 `height` 和 `width` 属性，以避免画布被拉伸的问题。

    ```html
    <!-- Work -->
    <canvas height="100" width="100">
        <!-- Does NOT work -->
        <canvas style="height: 100px; width: 100px;"></canvas
    ></canvas>
    ```

    canvas 的 `width` 和 `height` 属性必须是没有单位的正数。`width="100px"` 不会有任何影响，尽管它似乎是其他元素的有效属性声明。

3. CSS 样式属性的优先级高于 HTML 属性。

    在以下示例中，`height: 200px` 属性将覆盖 `height="100px"` 属性：

    ```html
    <!-- The image will have the width of 200px -->
    <img height="100px" style="height: 200px" />
    ```

### Good to know

`width` 和 `height` 属性仍然在电子邮件中广泛使用，我们必须支持多种屏幕尺寸（移动设备、桌面）和各种电子邮件客户端。
