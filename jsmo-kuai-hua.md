# 模块

采用"宽放大模式"。

```
var module1 = ( function (mod){

　　　　//...

　　　　return mod;

　　})(window.module1 || {});
```

```

```

```
var pageView=(function($){
    var pageView={};

    pageView.eventInit=function(){
        ...
    }


    pageView.init=function(){
        $("#preloader").fadeOut("fast");
        pageView.eventInit()

    };

    return pageView;

})(jQuery);


$(document).ready(function(){
    pageView.init();

});
```



