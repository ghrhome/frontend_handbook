# 项目结构（pd-成本系统）

![](/assets/pd_files.png)

> 每个页面对应的view分别在views, css/views/,js/views/下建立自己对应的命名目录,
>
> router里配置如下：

```javascript
.state('sample', {
                    //abstract: true,
                    url: '/sample',
                    views:{
                        'content': {
                            templateUrl: '../views/sample_module_view/sample_view.html',
                            controller:"sampleViewCtrl",
                            controllerAs:"vCtrl"
                        },
                        "right":{
                            templateUrl: '../views/blank_right.html',
                        },
                        "modal":{
                            templateUrl:"../views/blank_modal.html"
                        }
                    },
                    // support to load more controllers, services, filters, ...
                    dependencies: ['views/sample_module_view/sample_view_index'],
                    resolve: {
                        load:function(){
                            var url="../views/blank.css";
                            //_loadCss(url);
                        },
                        //todo:这里service分块有bug,目前解决方案是写appServies下的公共模块，实现渲染前加载
                        preloadData:function(dataPreloadService){
                            return dataPreloadService.getData("name")
                        }

                    }
                })//state main
```

> 注意: dependencies: \['views/sample\_module\_view/sample\_view\_index'\], 把依赖的js,在dependencies里注入实现懒加载。
>
> css懒加载推荐在页面引用，如果自定义样式比较大，可以在resolve里配置load, \_loadCss\(url\)预加载。

```
<!-- 推荐页面加载对应css-->
<link rel="stylesheet" href="../static/css/views/sample_module_view/sample_view.css">
<div>
    <h3>view</h3>
    <h5>{{vCtrl.name}}</h5>
</div>
```

#### js/views/sample\_module\_view,js的自定义涉及到controller,service,自定义directive,filter以及第三方插件，便于管理，在目录中增加一个{module\_name}\_index.js的依赖入口,router&gt;states里dependecies只引用{module\_name}\_index.js.

```
//{module_name}_view_index.js

define(["js/main/app","./sample_view","./services","./controllers"],function(app){
    app.useModule('myApp.sampleView')
});
```

{module}\_view.js用于定义页面命名的module

```
//{module_name}_view.js

define(["angular"],function(angular){

    var viewModule=angular.module('myApp.sampleView', []);
    return viewModule;
});
```

页面对应的controller,service统一以{module}\_view.js命名的module作为命名空间

```
//{module_name}_controllers.js

define(["angular",'./sample_view',"./services"],function(angular,viewModule){

    viewModule.controller('sampleViewCtrl', ["$rootScope","$scope","$timeout","$state", "$stateParams","sampleViewService","preloadData",
        function($rootScope,$scope,$timeout,$state,$stateParams,sampleViewService,preloadData) {
            var self=this;
            console.log("preload data--------------------------");
            console.log(preloadData);
            console.log("preload data--------------------------");

            this.name="Sample View";
            function _cb(data){
                console.log(".....");
                console.log(data);
            }
            sampleViewService.getData("",_cb)
        }]);

});
```



