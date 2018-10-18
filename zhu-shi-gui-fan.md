### 注释规范

注释是**你自己**与你的小伙伴们了解代码写法和目的的唯一途径。特别是在写一些看似琐碎的无关紧要的代码时，由于记忆点不深刻，注释就变得尤为重要了。

编写自解释代码只是一个**传说**，没有任何代码是可以完全自解释的。而代码注释，则是永远也不嫌多。

当你写注释时一定要注意：不要写你的代码都干了些什么，而要写你的代码为什么要这么写，背后的考量是什么。当然也可以加入所思考问题或是解决方案的链接地址。

**不推荐**

```
var offset = 0;

if(includeLabels) {
  // Add offset of 20
  offset = 20;
}
```

**推荐**

```
var offset = 0;

if(includeLabels) {
  // If the labels are included we need to have a minimum offset of 20 pixels
  // We need to set it explicitly because of the following bug: http://somebrowservendor.com/issue-tracker/ISSUE-1
  offset = 20;
}
```

下面格式可以帮助我们写出更好的注释。

`JAVASCRIPT`、`CSS`文件注释需要标明作者、文件版本、创建/修改时间、重大版本修改记录、函数描述、文件版本、创建或者修改时间、功能、作者等信息

/\* \* 注释块 \*/

中间可添加如下信息

```
    @file 文件名
    @addon 把一个函数标记为另一个函数的扩张，另一个函数的定义不在源文件中
    @argument 用大括号中的自变量类型描述一个自变量
    @author 函数/类作者的姓名
    @base 如果类是继承得来，定义提供的类名称
    @class 用来给一个类提供描述，不能用于构造器的文档中
    @constructor 描述一个类的构造器
    @deprecated 表示函数/类已被忽略
    @exception 描述函数/类产生的一个错误
    @exec @extends 表示派生出当前类的另一个类
    @fileoverview 表示文档块将用于描述当前文件，这个标签应该放在其它任何标签之前
    @final 指出函数/类
    @ignore 让jsdoc忽视随后的代码
    @link 类似于@link标签，用于连接许多其它页面
    @member 定义随后的函数为提供的类名称的一个成员
    @param 用大括号中的参数类型描述一个参数
    @private 表示函数/类为私有，不应包含在生成的文档中
    @requires 表示需要另一个函数/类
    @return 描述一个函数的返回值
    @see 连接到另一个函数/类
    @throws 描述函数/类可能产生的错误
    @type 指定函数/成员的返回类型
    @version 函数/类的版本号
```



