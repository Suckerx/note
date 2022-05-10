# CSS ——层叠样式表

Cascading style sheets

作用：给html设置样式

## 语法规则

```
选择器 {
    属性名: 属性值;
}
```

## 书写位置

```
<head>
    <title></title>

    <style>
        /* 这里写css */
    </style>
<head>
```

## CSS 引入方式

| 引入方式 | 书写位置                   | 作用范围 | 使用场景     |
| -------- | -------------------------- | -------- | ------------ |
| 内嵌式   | style 标签                 | 当前页面 | 小案例       |
| 外链式   | link 标签引入单独 css 文件 | 多个页面 | 项目中       |
| 行内式   | 标签 style 属性中          | 当前标签 | 配合 js 使用 |

（1）内嵌式

- CSS 写在 style 标签中
- style 标签可以写在页面任意位置，一般放在 head 标签中，title标签下面

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible"
          content="IE=edge">
    <meta name="viewport"
          content="width=device-width, initial-scale=1.0">
    <title>Document</title>

    <style>
        p {
            /* 这里是注释，快捷键ctrl + /  */
            /* 文字颜色设置为红色 */
            color: red;

            /* 字体大小设置为30像素 */
            font-size: 30px;

            /* 背景颜色 */
            background-color: green;

            /* 设置宽度和高度 */
            width: 600px;
            height: 100px;
            line-height: 100px;
            text-align: center;
        }
    </style>

</head>

<body>
    <p>这是一段设置了css样式的文字</p>
</body>

</html>
```

![](css.assets/image-20220422170955077.png)

（2）外链式

- CSS 写在单独的`.css`文件中
- 通过 link 标签引入到网页中

```css
p {
  color: red;
}
```

```css

<!DOCTYPE html>
<html lang="en">

<head>
    <link rel="stylesheet" /* 这里表示：关系是：样式表*/
          href="./css-2.css">
</head>

<body>
    <p>这是一段设置了css样式的文字</p>
</body>

</html>
```

![](css.assets/image-20220422171505412.png)

（3）行内式

- CSS 写在标签 style 属性中

```html
<div style="color: green; background-color: #f1f1f1;">
  这是一段设置了css样式的文字
</div>
```

![image-20220422171621702](css.assets/image-20220422171621702.png)

## 基础选择器

- 标签选择器
- 类选择器
- id 选择器
- 通配符选择器

（1）标签选择器

- 标签选择器选择的是一类标签，而不是单独某一个
- 标签选择器无论嵌套关系有多深，都能找到对应的标签

```html
标签名 {
    属性名：属性值;
}
<style>
    p {
        color: red;
    }
</style>


<p>你好，世界</p>
```

![image-20220422172248006](css.assets/image-20220422172248006.png)

（2）类选择器

```
.类名{
    属性名：属性值;
}
```

- 合法的类名：数字、字母、下划线、中划线
- 一个元素可以有多个类名，空格隔开

![image-20220422172450154](css.assets/image-20220422172450154.png)

```html
<style>
    .red {
        color: red;
    }

    .size {
        font-size: 60px;
    }
</style>

<p class="red">你好，世界</p>
<div class="red size">你好，世界</div>
```

![image-20220422172628194](css.assets/image-20220422172628194.png)

（3）id 选择器

```
#元素id{
    属性名：属性值;
}
```

- 页面中唯一，不能重复
- 一个标签只能有一个 id
- 一个id选择器只能选中一个标签
- id 选择器一般与 js 配合使用

```html
<style>
    #name {
        color: green;
    }
</style>

<div id="name">你好，世界</div>
```

![image-20220422173041366](css.assets/image-20220422173041366.png)

（4）通配符选择器

```
* {
   属性名：属性值;
}
```

- 选中页面所有标签
- 一般用于统一设置页面样式

```css
/* 清除内外边距 */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
```

# CSS 字体和文本样式

## 字体大小

属性名：font-size

取值：数字+px

```css
/* 谷歌浏览器默认字体大小 16px */
font-size: 16px;
<div style="font-size: 16px;">Hello World!</div>
<div style="font-size: 26px;">Hello World!</div>
```

![image-20220510180431729](css.assets/image-20220510180431729.png)

## 字体粗细

纯数字提供100-900得整百数

不是所有字体都提供了九种粗细，实际开发种以正擦汗给你、加粗两种取值使用更多

```css
font-weight: 400;
font-weight: normal 这两种效果相同

还可以把别的加粗得字体变细
<style>
    h1 {
        font-weight:400
    }
</style>
```

| 属性值 | 数值 | 效果 |
| ------ | ---- | ---- |
| normal | 400  | 正常 |
| bold   | 700  | 加粗 |

```html
<div style="font-weight: normal">Hello World!</div>
<div style="font-weight: bold">Hello World!</div>
```

![image-20220510180504203](css.assets/image-20220510180504203.png)

## 字体样式

用<em>标签也可以实现变倾斜

```css
font-style: normal;
```

| 属性值 | 效果 |
| ------ | ---- |
| normal | 正常 |
| italic | 倾斜 |

```html
<div style="font-style: normal;">Hello World!</div>
<div style="font-style: italic;">Hello World!</div>
```

![image-20220510181805431](css.assets/image-20220510181805431.png)

## 字体系列

![image-20220510181952777](css.assets/image-20220510181952777.png)

```css
/* 优先使用：微软雅黑 > 黑体 */
/* 如果客户端都没有这些字体就选择一种无衬线字体 */
font-family: 微软雅黑, 黑体, sans-serif;
```

![image-20220510182112689](css.assets/image-20220510182112689.png)

| 操作系统 | 默认字体    |
| -------- | ----------- |
| windows  | 微软雅黑    |
| Mac      | PingFang SC |

常见字体系列

| 常见字体系列             | 特点                               | 场景         | 该系列常见字体        |
| ------------------------ | ---------------------------------- | ------------ | --------------------- |
| 无衬线字体（sans-serif） | 文字笔画粗细均匀，并且首尾无装饰   | 网页         | 黑体、Arial           |
| 衬线字体（serif）        | 文字笔画粗细不均匀，并且首尾有装饰 | 报刊书籍     | 宋体、Times New Roman |
| 等宽字体（monospace）    | 每个字母或文字的宽度相等           | 程序代码编写 | Consolas、 fira Code  |

```html
<div style="font-family: 微软雅黑, 黑体, sans-serif;">Hello World!</div>
<div style="font-family: 宋体, Times New Roman, serif;">Hello World!</div>
<div style="font-family: Consolas, fira Code, monospace;">Hello World!</div>
```

![image-20220510182152927](css.assets/image-20220510182152927.png)

![image-20220510182547209](css.assets/image-20220510182547209.png)

## 文本缩进

```css
/* 首行缩进2个字符 */
text-indent: 2em;
```

取值

- 数字 + px
- 数字 + em(推荐：1em=当前标签的 font-size 大小,一个字得大小)

```html
<p>Hello World!</p>
<p style="text-indent: 2em;">Hello World!</p>
```

![image-20220510182635963](css.assets/image-20220510182635963.png)

## 文本水平对齐方式

```css
text-align: center;
```

| 属性值 | 效果           |
| ------ | -------------- |
| left   | 左对齐（默认） |
| center | 居中对齐       |
| right  | 右对齐         |

可居中的标签

- 文本
- span a
- input img

内容居中需要给`父元素`设置居中属性，例如是img图片，则需要给body设置

```html
<p>Hello World!</p>
<p style="text-align: center;">Hello World!</p>
```

## 文本修饰

```css
/* 常用于清除a标签默认下划线 */
text-decoration: none;
```

| 属性值       | 效果   |
| ------------ | ------ |
| underline    | 下划线 |
| line-through | 删除线 |
| overline     | 上划线 |
| none         | 无     |

```html
<p style="text-decoration: none;">Hello World!</p>
<p style="text-decoration: underline;">Hello World!</p>
<p style="text-decoration: line-through;">Hello World!</p>
<p style="text-decoration: overline;">Hello World!</p>
```

![image-20220510184513411](css.assets/image-20220510184513411.png)

## 行高

![image-20220510184925341](css.assets/image-20220510184925341.png)

```css
line-height: 1.5;
```

取值

- 数字 + px
- 倍数（当前标签 font-size 的倍数）

文本高度

- 上间距
- 文本高度
- 下间距

应用：

- 单行文本垂直居中：line-height=文字父元素高度
- 网页精准布局时，取消上下间距：line-height=1

```HTML
<p style="line-height: 1">Hello World!</p>
<p style="line-height: 1.5;">Hello World!</p>
<p style="line-height: 3;">Hello World!</p>
```

Hello World!

Hello World!

Hello World!

![image-20220510185427561](css.assets/image-20220510185427561.png)

```css
font: italic 700 66px/2 宋体
```

## font 属性简写

![image-20220510183038254](css.assets/image-20220510183038254.png)

层叠性：后面的样式覆盖前面的样式

复合属性

```css
font: [font-style font-weight] font-size/line-height font-family;
```

在线配置 font 简写形式

https://developer.mozilla.org/en-US/docs/Web/CSS/font#live_sample

<div style="font: italic normal 700 24px/3 sans-serif;">Hello World!</div>



![image-20220510191307040](css.assets/image-20220510191307040.png)

