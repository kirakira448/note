[示例网站](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_grid_layout)

父级定义网格结构
```css
.wrapper {
	/* 声明grid布局 */
	display: grid;
	/* 子元素对齐方式（可选） */
	justify-items: center;
	/* 表示分成 3 列 ，每列的宽度为1/3 */
	grid-template-columns: repeat(3, 1fr);
	/* 网格间距 */
	grid-gap: 10px;
	/* 指定隐式创建的行轨道大小。minimax(最小值，最大值) */
	grid-auto-rows: minmax(100px, auto);
}
```
>fr单位:表示剩余空间中占多少份。
>例如：
>`grid-template-columns: 1fr 2fr 10px;`表示
>1. 第三列占10px
>2. 在剩下的空间中：
>	1. 第一列占 1/(1+2) 比例的空间；
>	2. 第二列占 2/(1+2) 比例的空间；

子级决定占用范围
```css
.child-one {
	/* 占用列 1/3 ：起点/终点*/
    grid-column: 1/3;
    /* 占用行 */
    grid-row: 1;
}
```