# 理解页面结构

![](/assets/成本-page-layout.jpg)

上图是主页面的布局结构，其中MainController作为全局模块app的主控制器，主要负责$rootScope作用域，子页面间切换时其生命周期的处理以及curProject等全局变量。

ui-view对应的页面结构是各个菜单页面主要实现功能的子页面。

* toolbar:主要是对应content view页面过滤，查询的实现。
* content:内容页面
* right:通常对应页面数据的增加，修改等操作
* ys-loading:全局设置在一些延时操作中调用。

```
 amp_main.loading_show（）
 amp_main.loading_hide（）
```

### 在menu\_list.js中配置完整菜单后，功能页面的引入还需要下面三个步骤：

1.页面元素依赖\(引入页面对应的js,css,图片资源\)

2.module依赖\(在amp模块中注入页面实现需要的模块\)

```
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

