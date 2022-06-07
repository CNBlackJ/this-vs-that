---
title: Normalize vs Reset CSS __zh
category: CSS
---

每个浏览器都提供一组默认样式，这些样式应用于它呈现的每个网页。
默认样式表也称为用户代理样式表。

你可以查看不同浏览器提供的默认样式：

-   [Chrome](https://chromium.googlesource.com/chromium/blink/+/master/Source/core/css/html.css)
-   [Firefox](https://hg.mozilla.org/mozilla-central/file/tip/layout/style/res/html.css)
-   [Safari](https://trac.webkit.org/browser/trunk/Source/WebCore/css/html.css)

由于默认样式不一样，导致网页在每个浏览器上会有不同的外观。 规范化和重置 CSS 都旨在解决这个问题。

1. 顾名思义，重置 CSS 将重置所有内置样式。

    最流行的 CSS 重置库是 Meyer 的 reset.css，你可以看到完整的[代码](https://meyerweb.com/eric/tools/css/reset/reset.css).
    例如，它将 `body` 的 `margin` 重置为 0：

    ```css
    body {
        margin: 0;
    }
    ```

    如果你使用 Chrome 浏览器的开发者工具，检查任何网页的 body 元素，你会发现它默认有 8px 的边距，而我们通常根本不希望有这样的边距：

    ```css
    body {
        margin: 8px;
    }
    ```

2. 规范化 CSS 是重置 CSS 的另一种选择。

    在这个领域最受欢迎的库是[normalize.css](https://necolas.github.io/normalize.css/). 它试图使内置浏览器样式在浏览器之间保持一致。

    不仅如此，这个库还实现了：

    - 使某些元素看起来像我们期望的那样。

    例如，Chrome、Firefox 和 Safari 浏览器对 `sub` 和 `sup` 标签使用以下样式：

    ```css
    sub {
        vertical-align: sub;
        font-size: smaller;
    }
    sup {
        vertical-align: super;
        font-size: smaller;
    }
    ```

    我们很难从视觉上将这些标签与普通标签区分开来。 normalize.css 通过声明这些标签的位置来改进：

    ```css
    sub {
        bottom: -0.25em;
    }
    sup {
        top: -0.5em;
    }
    ```

    - 跨浏览器修复显示的bug。

    You can look at its [source code](https://github.com/necolas/normalize.css/blob/master/normalize.css) to see there are lot of bug fixes for different browsers such as Internet Explorer, Edge, Firefox, etc.

    你可以查阅这里的[源码](https://github.com/necolas/normalize.css/blob/master/normalize.css)，这里有许多针对不同浏览器的修复方法，例如 Internet Explorer、Edge、Firefox 等。

如果你使用流行的CSS库，可以不需要引入normalize.css，一般都是会包含在里面

-   [Bootstrap's reboot](https://github.com/twbs/bootstrap/blob/master/scss/_reboot.scss#L3)
-   [Tachyons](https://github.com/tachyons-css/tachyons/blob/master/src/_normalize.css)
-   [Tailwindcss](https://unpkg.com/tailwindcss@1.1.4/dist/base.css)

### 更多资料

1. [water.css](https://github.com/kognise/water.css) 为常用标签添加更多视觉样式
2. [minireset](https://github.com/jgthms/minireset.css) 是另一个体积微小的现代 CSS 重置库
3. [This website](https://browserdefaultstyles.com) 允许我们获取特定元素的各种渲染引擎的默认样式
