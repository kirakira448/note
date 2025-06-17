## 效果
### 阴影效果
```css
box-shadow: 0 1px 3px 0 rgb(0 0 0 / 12%), 0 0 3px 0 rgb(0 0 0 / 4%);
```
### 旋转图标
给图标添加点击旋转动画
1. 使用vue动态绑定class方法，在不同状态使用不同CSS
```vue
<el-icon
	:class="{ 'iconTransform': !flag, 'iconTransformReturn': flag }"
	@click="closeMenu"
>
<Expand />
</el-icon>
```
2. 声明flag
3. 为不同状态的class添加效果
```CSS
.iconTransform {
    transition: 0.2s;
    transform-origin: center;
    transform: rotateZ(180deg);
} 

.iconTransformReturn {
    transition: 0.2s;
    transform-origin: center;
    transform: rotateZ(0deg);
}
```
