# css\_补充规范

```
/*这部分内容是给css导入时使用的原则，尽量用link
```

```
<!-- Use link elements -->
<link rel="stylesheet" href="core.css">

不要使用 @import
与 <link> 标签相比，@import 指令要慢很多，不光增加了额外的请求次数，还会导致不可预料的问题。替代办法有以下几种：

使用多个 <link> 元素
通过 Sass 或 Less 类似的 CSS 预处理器将多个 CSS 文件编译为一个文件
通过 Rails、Jekyll 或其他系统中提供过 CSS 文件合并功能
*/


/* Good CSS
对于属性值或颜色参数，省略小于 1 的小数前面的 0 （例如，.5 代替 0.5；-.5px 代替 -0.5px）。

所有声明语句都应当以分号结尾。最后一条声明语句后面的分号是可选的，但是，如果省略这个分号，你的代码可能更易出错。

不要在 rgb()、rgba()、hsl()、hsla() 或 rect() 值的内部的逗号后面插入空格。这样利于从多个属性值（既加逗号也加空格）中区分多个颜色值（只加逗号，不加空格）

避免为 0 值指定单位，例如，用 margin: 0; 代替 margin: 0px;
```

```
 .selector,
.selector-secondary,
.selector[type="text"] {
    padding: 15px;
    margin-bottom: 15px;
    background-color: rgba(0,0,0,.5);
    box-shadow: 0 1px 2px #ccc, inset 0 1px 0 #fff;
}
```

> ```
> /*Positioning声明顺序相关的属性声明应当归为一组，并按照下面的顺序排列：
>
> Positioning
> Box model
> Typographic
> Visual
>
> 由于定位（positioning）可以从正常的文档流中移除元素，并且还能覆盖盒模型（box
> model）相关的样式，因此排在首位。盒模型排在第二位，因为它决定了组件的尺寸和位置。
>
> 其他属性只是影响组件的内部（inside）或者是不影响前两组属性，因此排在后面。
> */
> ```

```
.declaration-order {
    position: absolute;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    z-index: 100;

    /* Box-model */
    display: block;
    float: right;
    width: 100px;
    height: 100px;

    /* Typography */
    font: normal 13px "Helvetica Neue", sans-serif;
    line-height: 1.5;
    color: #333;
    text-align: center;

    /* Visual */
    background-color: #f5f5f5;
    border: 1px solid #e5e5e5;
    border-radius: 3px;

    /* Misc */
    opacity: 1;
}
```



