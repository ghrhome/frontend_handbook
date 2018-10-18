# 理解页面结构

![](/assets/成本-page-layout.jpg)

上图是主页面的布局结构，其中MainController作为全局模块app的主控制器，主要负责$rootScope作用域，子页面间切换时其生命周期的处理以及curProject等全局变量。

ui-view对应的页面结构是各个菜单页面主要实现功能的子页面。

* content:内容页面
* right:\(页面预留的钩子页面，通常对应页面数据的增加，修改等操作，在amp中有对应功能实现）
* ys-loading:全局设置在一些延时操作中调用。

```
  $rootScope.loading_show（）
  $rootScope.loading_hide（）
```

### 在menu\_list.js中配置完整菜单后，功能页面的引入还需要下面两个步骤：

1.页面元素依赖\(引入页面对应的css,图片资源\)

2.路由配置（实现对应菜单页面与view的绑定）

