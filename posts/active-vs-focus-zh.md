---
title: :active vs :focus
category: CSS
---

`:active`和`:focus`选择器都是用来表示一个元素的不同状态。

`:focus`选择器作用于支持交互的元素。发生在以下情况：

-   用户按下`Tab`键如获取某个元素焦点
-   用户使用鼠标点击某个元素
-   在触摸屏设备上，用户点击某个元素


`:active`选择器在元素被激活时触发。在用户单击元素并释放鼠标期间一直保留该状态。

在 iOS 上运行的 Safari 浏览器有一个不同点。 支持 `:focus` 选择器，但是 `:active` 选择器仅适用于 `body` 元素或支持 `touchstart` 事件的相关元素。

### 最佳实践

有许多用户喜欢用键盘浏览网页。通过`Tab`键用户可以快速跳到支持焦点选择的元素。
一些原生 HTML 元素（例如 `<a>`、`<button>`、`<input>`、`<select>`和`<textarea>`）提供了内置的键盘可访问性。

但是，如果你正在构建一个自定义的标签元素，并且希望能通过键盘获取焦点和可访问性，那么需要为元素添加`tabindex`属性。

两种设置`tabindex`的常见方式：

-   `tabindex="0"` 让元素支持tab键访问
-   `tabindex="-1"` 移除元素支持tab键访问，用户则无法通过键盘访问元素

许多库都使用了这种技术，比如[Bootstrap的模态框](https://getbootstrap.com/docs/4.4/components/modal) or [Foundation's reveal](https://get.foundation/sites/docs/reveal.html).

通过将 `tabindex="-1"` 设置为模态元素或其覆盖元素，用户将无法将元素集中在主页中。 只有模态框内的元素是可聚焦的。

下面是Bootstrap模态框的结构

```html
<!-- The overlay which takes full size -->
<div
    tabindex="-1"
    style="
        height: 100%;
        left: 0;
        position: fixed;
        top: 0;
        width: 100%;
    "
>
    <!-- The modal element -->
    ...
</div>
```

建议不要将 `tabindex` 设置为大于 0，因为用户按 DOM 顺序而不是 Tab 顺序浏览网页。

### Tips

1. 使用 Chrome DevTools，您可以在不激活元素的情况下查看用于 `:active` 和 `:focus` 状态的 CSS 类。

    首先，您需要检查元素，然后选择 _Styles_ 选项卡下的 _:hov_ 选项卡：

    ![使用 Chrome DevTools 切换 :active 和 :focus 选择器](/assets/active-hover-classes-chrome.png)

    在 Firefox 上，可以在 _Inspector_ 选项卡下的 _:hov_ 选项卡中找到类似的选项。

    ![使用 Firefox 开发者工具切换 :active 和 :focus 选择器](/assets/active-hover-classes-firefox.png)

2. 测试网站中的键盘可访问性。

    有一种情况是按下 _Tab_ 键会跳转到在视口中不可见的特定元素。

    Chrome DevTools 提供了跟踪焦点元素的能力。

    - 打开 _Console_
    - 单击位于过滤框右侧的眼睛图标以创建实时表情
    - 输入 `document.activeElement`

    这个命令会输出当前具有焦点的活动元素。 可以右键单击表达式的结果，然后选择 _Reveal in Elements panel_ 来检查焦点元素。

    ![选中焦点元素](/assets/track-focused-element.png)
