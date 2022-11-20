## css小技巧

#### 实现 0.5px 边框

```html
<div class="box">
	<div class="scale_border"></div>
</div>
```

```css
.box {
    width: 100px;
    height: 100px;
    position: relative;
}

.scale_border {
    border: 1px solid #000;
    position: absolute;
    top: -50%;
    bottom: -50%;
    left: -50%;
    right: -50%;
    transform: scale(0.5);
}
```

#### 伪类，伪元素，选择器的权重进制

```css
// 伪类
:hover 当鼠标悬浮在元素上方时，向元素添加样式
:active 向被激活的元素添加样式
:first-child 向元素的第一个子元素添加样式
:focus 向拥有键盘输入焦点的元素添加样式
:link	向未被访问的链接添加样式
:visited	向已被访问的链接添加样式
:lang 向带有指定 lang 属性的元素添加样式

// 伪元素
:before 在元素之前添加内容
:after 在元素之后添加内容
:first-letter 向文本的第一个字母添加特殊样式
:first-line 向文本的首行添加特殊样式

// 选择器的权重进制：256
// 伪类选择器和属性选择器的权重相当于类选择器的权重，权级为 2 级
// 伪元素选择器的权重相当于元素选择器的权重，权级为 1 级
```

![image-20210927112147513](https://aliyun-oss-lpj.oss-cn-qingdao.aliyuncs.com/images/by-picgo/image-20210927112147513.png)

#### 修改 `<a href="" />` 超链接标签的颜色样式

```css
a:link {
  color: #C8C8C8;
}
a:hover {
  color: #00d4ff;
}
a:visited {
  color: #C8C8C8;
}
/* a:active 用处不大，且颜色优先级低于 a:hover */
a:active {
  color: red;
}
```
