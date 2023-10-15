# 1，什么是BEM
对于一个前端开发团队来说，随着项目的规模越来越大，良好的代码规范越显得重要。

在 CSS 命名方面，经常会遇到的问题：

绞尽脑汁的去想一个 class，还得和其他类似的 class 做区分。
修改旧代码时，得去仔细确认每个 class 的作用，是修改、删除，还是添加一个新的 class 覆盖。
协作开发时 class 命名的冲突。
BEM 可以解决这些问题，让代码更容易阅读和控制，规范团队的代码风格。

## 1.1，介绍
BEM 是一种CSS命名规范。由 B（block）模块，E（element）元素，M（modifier）修饰符组成。

书写规范：

连接 element 用 __双下划线
连接 modifier 用 --双中划线
1个 class 中，B、E、M 尽量都只有1个（比如：尽量避免block__el1__el2）
具体表现如下：

```css
.block {}
.block__element {}
.block__element--modifier {}
.block--modifier {}
```

在前端项目中，一般是由多个组件构成的，组件就是一个模块 block。
element 表示 block 内更细粒度的元素，一般以布局或功能区分这些元素。
modifier 用于标记 block 或 element 的不同版本或状态。


## 1.2，使用

**举例**：弹出框组件 dialog
```html
<div class="dialog center">
  <div class="header">
    <div class="title"></div>
    <div class="closebtn"></div>
  </div>
  <div class="body"></div>
  <div class="footer"></div>
</div>

```

这样的命名方式，在阅读时并不能确定：

1. `center` 是一个通用的 class，还是只对 dialog 生效。
2. `body` 等是否也只在 dialog 中用到。如果`body` 中又嵌套了一个组件，也有类似`body` 的结构，命名就有点麻烦了。

BEM改造：
```html
<div class="dialog dialog--center">
  <div class="dialog__header">
    <div class="dialog__title"></div>
    <div class="dialog__closebtn"></div>
  </div>
  <div class="dialog__body"></div>
  <div class="dialog__footer"></div>
</div>

```


## 1.3，问题

问题1：注意到定义的是`dialog__title` 而不是`dialog__header__title`。

满足 BEM 书写规范。
在BEM规范中，不关心 DOM 元素的层级结构，关注的是在BEM三者之间的关系：block 下有哪些 element，block 和 element 下又有哪些 modifier。
所以对于同一个 block（`dialog`），`header` 和 `title` 都是它的 element。

问题2：如果元素有很多的话，BEM规范还适用吗？

适用。因为 block 可以嵌套，就像组件之间的嵌套。


```html
<div class="dialog dialog--center">
  <div class="dialog__body">
    <form class="form form--default">
      <div class="form-item">
        <div class="form-item__label"></div>
        <div class="form-item__content"></div>
	  </div>
	</form>
  </div>
</div>

```

问题3： 注意到上面定义的是`form-item`，而不是`form__item`。

和问题1的区别是：因为后面还有`form-item__label`，如果命名为`form__item`，那 label 就变成`form__item__label`，不符合BEM命名规范。

这种情况，`item` 被称为blockSuffix，本质上`form-item`整体是一个block。

## 1.4，总结

可以看到通过BEM规范化后，代码更易阅读和控制：

1. 增加了代码的自解释性，能够直观的看到层级和依赖关系。
2. class 单一职责。
3. 避免了命名污染（污染外层或公共的同名 class）。


# 2，命名空间

命名空间（namespace）也是一种CSS命名规范，一般会配合 BEM 使用。

作用：进一步增加代码的自解释性，能够更快定位。

分类：命名空间并没有明确的分类，常用的有3种

## 2.1，组件类
用 c- 表示（Component）

```css
.c-table {}
.c-form {}
```

## 2.2，状态类

用 is- 和 has- 表示

```css
.has-footer {}
.is-disabled {}
```

>在介绍BEM时，modifier 用于标记 block 或 element 的不同版本或状态。
>当 BEM 结合状态类之后，M 就可以专注的表示版本，状态由 is- 来表示。

## 2.3，作用域类

用 `s-` 或自定义的字母来表示。

**作用**：和整个站点的样式做隔离。最常见的使用就是**组件库**，每个组件库都有自己的命名空间。

|组件库|命名空间|
|---|---|
|element-plus|el-|
|vant|van-|
|ant design|ant-|



