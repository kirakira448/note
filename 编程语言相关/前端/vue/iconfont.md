# 在Vue3中使用

1. 将代码下载到本地
2. 在`src/assets`目录下，创建`icons`文件夹
3. 将下载的内容，解压到`icons`文件夹下（不包括demo文件，demo文件是演示文件）
	1. 如果设定了前缀，需要[[#需要修改前缀的情况 |修改CSS文件]]
4. 在`main.js`中，引入css文件
```js
import '@/assets/icons/iconfont.css'
```
5. 使用
```html
<i class="iconfont icon-language" style="font-size: 40px;"></i>
```

## 需要修改前缀的情况

如果在下载代码前，选择了配置前缀，需要修改CSS文件

>一般为了避免与element-plus组件重名，会进行前缀设置

例如：当前缀被设定为`icon-third-`
`iconfont.css`修改前
```css
.iconfont {
  font-family: "iconfont" !important;
  font-size: 16px;
  font-style: normal;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
```

`iconfont.css`修改后
```css
[class^="icon-third"],[class*="icon-third"] 
{
  font-family: "iconfont" !important;
  font-size: 16px;
  font-style: normal;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
```

>[[class#选择所有|class^="icon-third"的效果]]

## 子组件接收动态class

当想要在父组件中，使用多次子组件，通常会动态传递值。
子组件需要动态接收父组件传递的class

父组件
```vue
<HomeCard v-for="(iconName,index) of iconNames" :key="index" :name="iconName"/>
```
>**注意：**
>使用`:name`而不是`:class`
>因为class可能会导致父级也被添加icon

子组件
```vue
<i class="iconfont" :class="$attrs.name" style="font-size: 40px;"></i>
```
使用`$attrs.父组件属性`接收传递数据