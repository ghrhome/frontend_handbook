# 目录配置

新增菜单项，需要在相应的配置文件里面做相应设置。

1.menu\_list.js

> /static/js/main/menu\_list.js

```
var menu_list={
    amp_menu:[
        {
            name:"综合分析",
            index:"main-0",
            icon:"ys-icon-asset",
            links:"noi",
            target:"#",
            show_sub_menu:false,
            re_locate:true,//点击一级目录直接跳转
            sub_menu:[
                {
                    name:"实际",
                    index:"sub-0",
                    links:"noi",
                    target:"#",
                    re_locate:true//点击一级目录直接跳转
                }

            ]
        },

        ]//end amp_menu
     }//end menu_list
```

菜单配置为amp\_menu对应的一个列表，

* name:菜单名称
* index:左侧第一级菜单ID
* icon:左侧第一级菜单对应的图标 class
* links，re\_locate:_当relocate：true时，点击第一级菜单，会根据配置的links跳转到相应页面。_
* show\_\_sub\_\_menu: 左侧一级菜单下是否显示2级菜单\(**AMP里这个配置请始终保持false**\)
* target:新开页面位置\(AMP由于使用angular做了单页面路由，这里target的相应功能屏蔽了，默认设置成＃即可\)
* sub\_menu:头部菜单，二级菜单（如果show\_\_sub\_\_menu:true时，同样对应左侧二级菜单）

**sub\_menu: 对应一个列表，里面每一项代表一个二级菜单的配置**

* name:二级菜单名称，
* index：AMP中二级菜单id为推算绑定，这里index设置只针对show\_\_sub\_\_menu:true情况有效，默认对每一项写成sub-index的形式即可。
* target:同一级菜单target;
* links,re\_locate:同一级菜单相应配置。



