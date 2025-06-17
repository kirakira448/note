实现圆角

```css
border-radius: 30px;
```

>该属性是一个 [简写属性](https://developer.mozilla.org/zh-CN/docs/Web/CSS/Shorthand_properties)，是为了将这四个属性 [`border-top-left-radius`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-top-left-radius)、[`border-top-right-radius`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-top-right-radius)、[`border-bottom-right-radius` (en-US)](https://developer.mozilla.org/en-US/docs/Web/CSS/border-bottom-right-radius "Currently only available in English (US)")，和 [`border-bottom-left-radius`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-bottom-left-radius) 简写为一个属性。


```css
border-radius: 4px 3px 6px / 2px 4px;

/* 等价于： */

border-top-left-radius: 4px 2px;
border-top-right-radius: 3px 4px;
border-bottom-right-radius: 6px 2px;
border-bottom-left-radius: 3px 4px;

```