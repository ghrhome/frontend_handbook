# 版本碎片化统一策略：

1. 目前公司技术状况：jQuery, angular。 vue

   jQuery:商业系统----印力，南国，中建。

   angular：成本，amp， 万科产城， 昌发展办公

   vue:美术馆，其他小型项目。

   未来重构一套：vue, react, angular4+中做技术选型。

2. jQuery版后续统一直印力版的组件及UI，

   jQuery版本的外框架统一成目前印力的这一套

   ---各区要统一路由和用户验证及权限管理。

   angular---成本改版UI以印力为标准修改。

   ```
    ---产城待确人。
   ```

3. 现有项目维护，对页面样式的折行，空白，间距，字符过长的问题统一处理方式。

4. jQuery后做项目，统一用印力版本， 业务重构时不要擅自引用旧项目的样式，js,和页面。\(印力版本里面有少量这个问题\)

   angular版本成本和产城业务完全分开，如果要在任何一个版本里面集成另一个业务，新做，不要copy.

   严格避免项目冗余。

   后续版本规划：数据交互统一成api形式， 各区项目要统一用户验证及权限管理接口，统一api格式。


