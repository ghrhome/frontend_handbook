# 路由配置

> 目录配置请查看：[目录配置](/README.md)
>
> 页面view结构请查看：[理解页面结构](/li-jie-ye-mian-jie-gou.md)

### 在menu\_list.js中配置完整菜单后，功能页面的引入还需要下面三个步骤：

1.页面元素依赖\(引入页面对应的js,css,图片资源\)

2.module依赖\(在amp模块中注入页面实现需要的模块\)

```js
var ampApp = angular.module('amp', [
    'ui.router',
    'noi',
    "ampFilters",
    "ampFilter",
    'commonService',
    'amp-directive-collection',
    "dataTool"
    //'noiFilters'
]);
```

3.路由配置（实现对应菜单页面与view的绑定）

