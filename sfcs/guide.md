---
title: SFCS Docs Wiki.js Guide
description: How to create your first page and more
published: true
date: 2020-10-26T09:25:30.399Z
tags: guide
editor: markdown
dateCreated: 2020-10-26T07:36:53.549Z
---

# Markdown编辑器基本功能
## Bold 加粗
语法： `**` 加粗部分`**`
**快捷键**: Ctrl + B 或 顶端工具栏 `B`

## Italic 斜体
语法： `*` 斜体部分`*`
*快捷键*  Ctrl + I 或者 顶端工具栏 `I`


## Strikethrough 删除线
语法： `~~` 删除部分`~~`  或者顶端 工具栏 ~~T~~
如 ~~Strikethrough 删除线~~

## Headers 标题
1-6级 #  或者顶端工具栏 `H#`
## 2
### 3

## Subscript 下标
语法： `~` 下标部分`~`   或者顶端工具栏  X~2~
如  X~2~

## Superscript 上标

语法： `^` 上标部分`^`   或者顶端工具栏  X^2^
如  X^2^

## Blockquotes 引用块

语法：在每行文本前使用大于号，后跟空格。
通过在blockquote后面的单独一行中添加一个类，您可以更改blockquote的外观。
请注意，这些样式是Wiki.js特有的，在其他应用程序中会退回到标准的blockquote样式。
>This is a default unstyled blockquote.

> .This is a {.is-info} blockquote.
{.is-info}

> .This is a {.is-success} blockquote.
{.is-success}

> .This is a {.is-warning} blockquote.
{.is-warning}

> .This is a {.is-danger} blockquote.
{.is-danger}


## Unordered Lists 无序列表
分三种
### 第一种 默认样式：
- list01, 也可以用 *  替代 -
- list02

### 第二种 `{.grid-list}` 样式：
- Grid Item 1 
- Grid Item 2
- Grid Item 3
{.grid-list}

### 第三种 `{.links-list}` 链接样式：
- [SFCS *Subtitle description here*](/en/sfcs)
- [Consectetur adipiscing elit *Another subtitle description here*](https://www.google.com)
- [Morbi vehicula aliquam *Third subtitle description here*](https://www.google.com)
{.links-list}

> 请注意，这些样式是特定于Wiki.js，在其他应用程序中将回退到标准列表样式
{.is-info}


## Ordered Lists 有序列表

1. Lorem ipsum dolor sit amet

1. Consectetur adipiscing elit

1. Morbi vehicula aliquam
> 虽然您可以按数字顺序为每行编号，但在每行上使用数字1更容易。最终结果将自动递增。这样，在以后添加或删除一行时，您就不需要对每一行重新编号
{.is-info}

## Inline Code 内联代码 和 Code Blocks 代码块
语法：在文本选择前后使用`反勾号` 或者顶端的工具栏 `<>`  `Inline Code `

```markdown
Lorem `ipsum` dolor
- Code Blocks 代码块
```

## Keyboard Keys 键盘按键
语法： `<kbd>`按键部分`/kbd>`  或 选中后，点击顶端工具栏的键盘小图标
如 <kbd>CTRL</kbd> + <kbd>C</kbd>

## Horizontal Line 水平分割线
语法：`---`
---





```plantuml
Bob->Alice : hello
```
## test

- Grid Item 1  *test*
- Grid Item 2
- Grid Item 3
{.grid-list}

## test 02
- [Lorem ipsum dolor sit amet *Subtitle description here*](https://www.google.com)
- [Consectetur adipiscing elit *Another subtitle description here*](https://www.google.com)
- [Morbi vehicula aliquam *Third subtitle description here*](https://www.google.com)
{.links-list}