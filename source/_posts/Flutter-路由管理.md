---
title: Flutter 路由管理
copyright: true
date: 2019-09-07 10:48:47
tags:
categories: Flutter
---

> 之前两篇文章，我们在新建的Flutter项目中初步接触了Flutter，并进行了简单的分析，接下来，是对Flutter中的路由管理，进行简单的学习

## 路由管理
简单的来说，Flutter中的路由，相当于Android中的Activity，这里的路由管理，就是Android中，不同的Activity之间进行跳转。在Android中，打开关闭Activity都会有一个堆栈进行管理，而在Flutter中，也有一个路由栈，对Route进行入栈(push)，出栈(pop)的管理。

## 简单举例
新建一个Route，可以在main.dart文件下新建，也可以另外新建一个dart文件，不过不要忘记导包。这里我是重新建了一个dart文件，并新建了一个Route

```Dart
import 'package:flutter/material.dart';

class NewRoute extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("This is a new Route"),
      ),
      body: Center(
        child: FlatButton(
          child: Text("This is a new Route body"),
          textColor: Colors.blue,
          onPressed: (){
            Navigator.pop(context);
          },
        ),
      ),
    );
  }
}
```

### 分析
`NewRoute`继承了无状态的Widget，返回了一个带导航栏的Widget，内容是居中显示的一个FlatButton，显示的文字是“This is a new Route body”,颜色是蓝色，点击事件的话，这里是`Navigator.pop(context)`,这里不具体的分析这个方法，只是说明一下作用，是让Route从路由栈中出栈。那么一个新的Route就完成了。

接下来是在之前的main.dart文件中进行一下修改，添加一个路由管理的按钮

```Dart
class _MyHomePageState extends State<MyHomePage> {
  ...
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(...),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            
            ...
            //添加的代码
            FlatButton(
              child: Text("open new route"),
              textColor: Colors.blue,
              onPressed: () {
                Navigator.push(context, MaterialPageRoute(builder: (context) {
                  return NewRoute();
                }));
              },
            ),
          ],
        ),
      ),
     ...
    );
  }
```

### 分析
简单说就是在body的子Widget下面，添加了一个FlatButton，文字是“open new route”，颜色是蓝色，点击方法是
```Dart
Navigator.push(context, MaterialPageRoute(builder: (context) {
    return NewRoute();
}));
```
作用是将一个Route入栈。

## MaterialPageRoute
`MaterialPageRoute`继承自`PageRoute`类，`PageRoute`类是一个抽象类，表示占有整个屏幕空间的一个模态路由页面，它还定义了路由构建及切换时过渡动画的相关接口及属性。`MaterialPageRoute` 是`Material`组件库提供的组件，它可以针对不同平台，实现与平台页面切换动画风格一致的路由切换动画：
    
- 对于Android，当打开新页面时，新的页面会从屏幕底部滑动到屏幕顶部；当关闭页面时，当前页面会从屏幕顶部滑动到屏幕底部后消失，同时上一个页面会显示到屏幕上。
- 对于iOS，当打开页面时，新的页面会从屏幕右侧边缘一致滑动到屏幕左边，直到新页面全部显示到屏幕上，而上一个页面则会从当前屏幕滑动到屏幕左侧而消失；当关闭页面时，正好相反，当前页面会从屏幕右侧滑出，同时上一个页面会从屏幕左侧滑入。

简单说一下`MaterialPageRoute`类的构造函数
```Dart
MaterialPageRoute({
    WidgetBuilder builder,
    RouteSettings settings,
    bool maintainState = true,
    bool fullscreenDialog = false,
})
```

`builder` 是一个WidgetBuilder类型的回调函数，它的作用是构建路由页面的具体内容，返回值是一个widget。我们通常要实现此回调，返回新路由的实例。
`settings`包含路由的配置信息，如路由名称、是否初始路由（首页）。
`maintainState`默认情况下，当入栈一个新路由时，原来的路由仍然会被保存在内存中，如果想在路由没用的时候释放其所占用的所有资源，可以设置maintainState为false。
`fullscreenDialog`表示新的路由页面是否是一个全屏的模态对话框，在iOS中，如果fullscreenDialog为true，新页面将会从屏幕底部滑入（而不是水平方向）。

## Navigator
上面的入栈和出栈中，都有用到Navigator类，那么现在我们就来稍微分析一下这个类
是一个路由管理的组件，它提供了打开和退出路由页方法。Navigator通过一个栈来管理活动路由集合。通常当前屏幕显示的页面就是栈顶的路由。Navigator提供了一系列方法来管理路由栈，在此我们只介绍其最常用的两个方法：
### Future push(BuildContext context, Route route)
将给定的路由入栈（即打开新的页面），返回值是一个Future对象，用以接收新路由出栈（即关闭）时的返回数据。
### bool pop(BuildContext context, [ result ])
将栈顶路由出栈，result为页面关闭时返回给上一个页面的数据。

## 实例方法

`Navigator`类中第一个参数为context的静态方法都对应一个Navigator的实例方法， 比如`Navigator.push(BuildContext context, Route route)`等价于`Navigator.of(context).push(Route route)` ，下面命名路由相关的方法也是一样的。

## 总结
Flutter中的路由管理，大致可以看作Android中的Activity堆栈的管理，后续类似Activity跳转动画和Activity间的传值，我想Flutter中应该也有相对应的实现。