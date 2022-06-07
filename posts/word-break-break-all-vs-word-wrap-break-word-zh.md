---
title: 'word-break: break-all vs word-wrap: break-word __zh'
category: CSS
---

### 区别

假设我们有一个字符串 `This is a sample text in a paragraph` 显示在一个宽度有限的容器中，例如它最多可以显示 9 个字符。

`word-break: break-all` 将尝试在每行中容纳最大字符数。 所以有些单词被分成不同的行，例如_text_和_paragraph_：

```shell
/* word-break: break-all */
┌───────────┐
| This is a |
| sample tex|
| t in a par|
| agraph.   |
└───────────┘
```

另一方面，`word-wrap: break-word` 不会破坏能够适合每一行的单词。 所以 _text_ 和 _paragraph_ 单词不会分成不同的行。

```shell
/* word-wrap: break-word */
┌───────────┐
| This is a |
| sample    |
| text in a |
| paragraph.|
└───────────┘
```

如果每行可以包含较少数量的字符，那么 `break-word` 将中断不适合每行的长单词。

```shell
/* word-wrap: break-word */
┌─────────┐
| This is |
| a       |
| sample  |
| text in |
| a       |
| paragrap|
| h.      |
└─────────┘
```

### Good to know

1. `word-wrap` was a non standard and unprefixed Microsoft extension. It was renamed to `overflow-wrap`.

    However, `word-wrap: break-word` is identical to `overflow-wrap: anywhere`, not `overflow-wrap: break-word`.

2. A browser might break a long text at unexpected places. For example, the specific path (`/this/is/.../folder`) in the following text is placed at the second line:

    ```shell
    ┌───────────────────────────────────────────────────────┐
    | Copy file to the folder:                              |
    | /this/is/a/very/long/path/to/the/destination/folder   |
    └───────────────────────────────────────────────────────┘
    ```

    To prevent this behavior, HTML5 provides the `<wbr>` element. It stands for _Word Break Opportunity_, and is used to specify the positions that a line break would be created.

    Getting back to the example above. If we use `<wbr>` elements right before each path separator (`/`) as follow:

    ```html
    Copy your file to the folder: <wbr />/this <wbr />/is <wbr />/a ... <wbr />/destination <wbr />/folder
    ```

    The browser will break the paths in between the directory names:

    ```shell
    ┌───────────────────────────────────────────────────────┐
    | Copy your file to the folder: /this/is/a/very/long    |
    | /path/to/the/destination/folder                       |
    └───────────────────────────────────────────────────────┘
    ```

    Note that `<wbr>` element is [not supported](https://caniuse.com/wbr-element) in IE 11 and earlier versions.
