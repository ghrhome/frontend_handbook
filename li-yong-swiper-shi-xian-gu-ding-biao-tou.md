# 利用Swiper实现固定表头

> 左侧固定，右侧sweiper写法

```
<div class="amp-table-wrapper-swiper">
    <div class="ys-table-main" style="padding-left:160px;">
        <!--ys-table-static-left-->
        <div class="ys-table-static ys-table-static-left" style="width:160px;">
            <table class="table table-no-bordered amp-table table-hover" style="width:100%;">
                <thead>
                   <tr>
                       <th>...</th>
                   </tr>
                </thead>
                <tbody>
                    <tr>
                        <th>...</th>
                    </tr>

                </tbody>
           </table>
       </div><!--end ys-table-static-left-->

       <!--swiper-container-->
       <div class="swiper-container"  style="width:100%;" id="amp_floor_main_table">
            <div class="swiper-wrapper">
                <div class="swiper-slide">
                    <table class="table table-no-bordered amp-table table-hover" style="width:1800px;">
                        <thead>
                            <tr>
                                <th>...</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr>
                                <th>...</th>
                            </tr>
                        </tbody>
                    </table>
                </div><!--swiper-slide-->
            </div><!--swiper-wrapper-->
            <!-- Add Scroll Bar -->
            <div class="swiper-scrollbar"></div>
        </div><!--swiper container-->

   </div><!--end ys-table-main-->
</div><!--end amp-table-wrapper-swiper-->
```

> js

```
var amp_main_swiper;
amp_main_swiper = new Swiper('#amp-floor-main-table', {
            scrollbar: '.swiper-scrollbar-a',
            direction: 'horizontal',
            slidesPerView: 'auto',
            //mousewheelControl: true,
            freeMode: true,
            scrollbarHide:false,
            preventClicksPropagation:false
        });
```

> 页面销毁时，回收处理

```
 $scope.$on("$destroy", function() {
       //清除配置,不然swiper会重复监听
       amp_main_swiper.destroy(true,true);
       });
```

> **表头随页面滚动，固定至页面顶部写法，用到了pin.js**

```
<div class="amp-table-wrapper-swiper" id="noi-main-table-wrapper">

    <!-- ys-table-fixed-top -->
     <div class="ys-table-fixed-top" style="padding-left:160px;">
          <div class="ys-table-static ys-table-static-left" style="width:160px;">
               <table class="table table-no-bordered amp-table table-hover table-header-fixed" style="width:100%;">
                    <thead>
                        <tr>
                            <th>...</th>
                        </tr>
                    </thead>
               </table>
           </div>

           <div class="swiper-container" style="width:100%;" id="noi-main-table-head">
                <div class="swiper-wrapper">
                    <div class="swiper-slide">
                        <table class="table table-no-bordered amp-table table-hover table-header-fixed" style="width:1500px;" >
                             <thead>
                                    <tr>
                                        <th>...</th>
                                    </tr>
                                </thead>
                            </table>
                        </div><!--swiper-slide-->
                    </div><!--swiper-wrapper-->
                </div><!--swiper container-->
     </div>               
    <!--end ys-table-fixed-top -->
    <!--ys-table-main-->
    <div class="ys-table-main" style="padding-left:160px;">
        <!--ys-table-static-left-->
        <div class="ys-table-static ys-table-static-left" style="width:160px;">
            <table class="table table-no-bordered amp-table table-hover" style="width:100%;">
                <thead>
                   <tr>
                       <th>...</th>
                   </tr>
                </thead>
                <tbody>
                    <tr>
                        <th>...</th>
                    </tr>

                </tbody>
           </table>
       </div><!--end ys-table-static-left-->

       <!--swiper-container-->
       <div class="swiper-container"  style="width:100%;" id="noi-main-table">
            <div class="swiper-wrapper">
                <div class="swiper-slide">
                    <table class="table table-no-bordered amp-table table-hover" style="width:1800px;">
                        <thead>
                            <tr>
                                <th>...</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr>
                                <th>...</th>
                            </tr>
                        </tbody>
                    </table>
                </div><!--swiper-slide-->
            </div><!--swiper-wrapper-->
            <!-- Add Scroll Bar -->
            <div class="swiper-scrollbar"></div>
        </div><!--swiper container-->

   </div><!--end ys-table-main-->
</div><!--end amp-table-wrapper-swiper-->
```

> js

```
        /*swiper */
        var pin;
        var noi_head_swiper,noi_main_swiper;
        var swiper_init=function(){
            noi_head_swiper = new Swiper('#noi-main-table-head', {
                //scrollbar: '.swiper-scrollbar',
                direction: 'horizontal',
                slidesPerView: 'auto',
                //mousewheelControl: true,
                freeMode: true,
                scrollbarHide:true,
                //watchSlidesProgress:true,
            });


            noi_main_swiper = new Swiper('#noi-main-table', {
                scrollbar: '.swiper-scrollbar',
                direction: 'horizontal',
                slidesPerView: 'auto',
                //mousewheelControl: true,
                freeMode: true,
                scrollbarHide:false,
                //watchSlidesProgress:true,
            });

            noi_head_swiper.params.control = noi_main_swiper;
            noi_main_swiper.params.control = noi_head_swiper;

            pin=$(".ys-table-fixed-top").pin({
                containerSelector: "#noi-main-table-wrapper",
                padding: {top: 44, bottom: 50}
            });
        };
```

> 页面销毁时，回收处理

```
$scope.$on("$destroy", function() {
            //清除配置,不然swiper会重复请求
            noi_head_swiper.destroy(true,true);
            noi_main_swiper.destroy(true,true);
        });
```

> css

```
/*fixed table*/
.ys-table-wrapper-swiper{overflow: hidden;position: relative;}
.ys-table-wrapper .table, .ys-table-wrapper-swiper .table {
    table-layout: fixed;
    margin-bottom:0;
}
.ys-table-wrapper .table{margin-bottom:20px;}
.ys-table-fixed-top .table{margin-bottom:0;}
.ys-table-wrapper-swiper .ys-table-main .table, .ys-table-wrapper-swiper .ys-table-main .table{
    margin-bottom:20px;
}

table.ys-table thead {
    background-color: #f3f4f8;
    color: #8592a3;
}
/*
.table-no-bordered thead{background-color:transparent;}
*/

.ys-table tr>th, .ys-table tr>td {
    height: 40px;
    overflow: hidden;
    vertical-align: middle;
}

.ys-table>thead>tr>th{
    padding:0;
    padding-left:15px;padding-right:15px;
    height:28px;
    color: #8592a3;
    font-size: 13px;
    text-align: center;
    vertical-align: middle;
    border-bottom:0;
    font-weight:normal;
    border-bottom: 1px solid #d9dde0 ;
}

.ys-table>thead>tr>th.text-left{text-align: left;}
.ys-table>thead>tr>th.text-right{text-align: right;}
.ys-table>thead>tr.thead-tr-sub>th{font-size: 12px;}
.ys-table>thead>tr>th.fake-th:before{display: block;content:"/";opacity: 0;color:#fff;}

.ys-table tr>th.td-fake,.ys-table tr>th.th-fake{ border: 0; padding: 0; width: 0; margin: 0; }

.ys-table>tbody>tr>th,.ys-table>tbody>tr>td,
.ys-table>tfoot>tr>th,.ys-table>tfoot>tr>td{
    padding:7px 15px;height:40px;line-height:24px;vertical-align: middle;font-size: 14px;color:#373c42;font-weight:normal;border-bottom:solid 1px #f3f4f8;}

.table-no-bordered>tbody>tr>th, .table-no-bordered>tbody>tr>td,
.ys-table-wrapper-swiper .table-no-bordered tr>th, .ys-table-wrapper-swiper .table-no-bordered tr>td {
    border: 0;
}
.ys-table-wrapper .table-no-bordered tr>th, .ys-table-wrapper .table-no-bordered tr>td,
.ys-table-wrapper-swiper .table-no-bordered tr>th, .ys-table-wrapper-swiper .table-no-bordered tr>td {
    border: 0;
}

.ys-table-wrapper .table-no-bordered tr>th.t-split, .ys-table-wrapper .table-no-bordered tr>td.t-split,
.ys-table-wrapper-swiper .table-no-bordered tr>th.t-split, .ys-table-wrapper-swiper .table-no-bordered tr>td.t-split{
    border-right: solid 1px #dae1e7;
}

.ys-table-wrapper-swiper table.ys-table thead>tr.thead-tr-sub{background-color:#fff;}

/*.table-hover>tbody>tr:hover,.table-hover>tbody>tr.hover,
.table-hover>tfoot>tr:hover,.table-hover>tfoot>tr.hover{background-color:#f3f4f8;}*/

/*
.table>tbody>tr>td, .table>tbody>tr>th, .table>tfoot>tr>td, .table>tfoot>tr>th, .table>thead>tr>td, .table>thead>tr>th{
    font-weight:normal;border-bottom:solid 1px #dae1e7;border-top:0; }
.table>thead>tr>th{border-bottom:solid 2px #dae1e7;}
*/

/* table static */
.ys-table-wrapper-swiper {
    position: relative;
    width:100%;
    padding-bottom:20px;
    /*padding-left: 160px;*/
   /* padding-right: 220px;*/
}
.ys-table-wrapper-swiper .ys-table-fixed-top{ position: relative;  padding-left: 160px;width:100%;z-index:99;}
.ys-table-wrapper .ys-table-fixed-top{padding-left:0;}
.ys-table-wrapper-swiper  .ys-table-main{ position: relative;  padding-left: 160px;width:100%;}
.ys-table-wrapper .ys-table-main{padding-left:0;}
.ys-table-main.scroll-wrapper{padding-left:0;}
.ys-table-main.scroll-wrapper .scroll{padding-left:160px;position: relative;width:100%;}
.ys-table-wrapper-swiper .swiper-container {
    width: 100%;
    height: 100%;
}
.ys-table-wrapper-swiper .swiper-slide {
    font-size: 14px;
    width: auto;
    -webkit-box-sizing: border-box;
    box-sizing: border-box;
    padding: 0;
}

.ys-table-wrapper-swiper .ys-table-static {
    position: absolute;
    top: 0;
    left: 0;
    border-right:solid 1px #dae1e7;
}

/*stick part*/
.isStuck{margin-top:43px;border-bottom:solid 1px #eee;
    -webkit-box-shadow:  0 2px 3px rgba(33,33,33,0.1);
    -moz-box-shadow:  0 2px 3px rgba(33,33,33,0.1);
    box-shadow:  0 2px 3px rgba(33,33,33,0.1);}
.pin-wrapper .ys-table-fixed-top{
    -webkit-box-shadow:  0 1px 3px rgba(33,33,33,0.1);
    -moz-box-shadow:  0 1px 3px rgba(33,33,33,0.1);
    box-shadow:  0 1px 3px rgba(33,33,33,0.1);}

/*em element,notify element*/
.ys-table em{display: inline-block;margin-left:5px;margin-right:5px;}
.ys-table>tbody>tr>th.notify,.ys-table>tbody>tr>td.notify,
.ys-table>tfoot>tr>th.notify,.ys-table>tfoot>tr>td.notify{color:#ff0000;}

.ys-table>tbody>tr.tr-main{}
.ys-table>tbody>tr.tr-main.tr-collapse{}
.ys-table>tbody>tr.tr-collapsed{display: none;}

.table-bordered>tbody>tr>td, .table-bordered>tbody>tr>th, .table-bordered>tfoot>tr>td, .table-bordered>tfoot>tr>th, .table-bordered>thead>tr>td, .table-bordered>thead>tr>th{
    border:solid 1px #dfe5e9;
}
.table-bordered>thead>tr>td, .table-bordered>thead>tr>th{border-bottom-width: 1px;}

/*right-bordered*/
.ys-table.table-right-bordered{margin-bottom: 0;}
.ys-table.table-right-bordered thead{background-color:#fff;}
.ys-table.table-right-bordered thead>tr>th{padding:0 30px; padding-right:15px;font-size: 14px;text-align: left; vertical-align: top; border:0;border-right:solid 1px #dfe5e9;border-top:0;border-bottom:0;}
.ys-table.table-right-bordered tbody>tr>th,
.ys-table.table-right-bordered tbody>tr>td{padding-left:30px;padding-right:15px;padding-bottom:0;text-align:left;vertical-align: top;border:0; border-right:solid 1px #dfe5e9;border-top:0;border-bottom:0; }
.ys-table.table-right-bordered thead>tr>th:first-child,
.ys-table.table-right-bordered tbody>tr>td:first-child{padding-left:15px;}
.ys-table.table-right-bordered thead>tr>th:nth-last-child(1),
.ys-table.table-right-bordered tbody>tr>td:nth-last-child(1){border-right:0;}


/*td active reset*/
.table>tbody>tr.active>td, .table>tbody>tr.active>th, .table>tbody>tr>td.active, .table>tbody>tr>th.active, .table>tfoot>tr.active>td, .table>tfoot>tr.active>th, .table>tfoot>tr>td.active, .table>tfoot>tr>th.active, .table>thead>tr.active>td, .table>thead>tr.active>th, .table>thead>tr>td.active, .table>thead>tr>th.active {
    background-color: inherit;
}
.ys-table tr>td.required{border-left:solid 2px #ff3030;}
.ystable tr>td.edit{}
```



