---
title: Flutter路由传值
copyright: true
date: 2019-09-08 10:54:24
tags:
categories: Flutter
---

> 上篇文章简单介绍了下Flutter的路由管理，那么自然想到，单单是入栈出栈是不够的，就像Android中Activity的传值一样，Flutter肯定也要这种情况，那么就引出了本篇文章，Route的传值

## 代码示例
让我们新建一个代码示例，来简单的描述下路由传值如何操作及处理

我们创建一个路由，需要接受上一个Route传过来的值并显示，然后点击返回按键会销毁页面，并将返回值返回上一个Route，
```Dart
class TipRoute extends StatelessWidget {
  TipRoute({Key key, @required this.text}) : super(key: key);
  final String text;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("提示"),
      ),
      body: Padding(
        padding: EdgeInsets.all(18),
        child: Center(
          child: Column(
            children: <Widget>[
              Text(text),
              RaisedButton(
                onPressed: () => Navigator.pop(context, "我是返回值"),
                child: Text("返回"),
              )
            ],
          ),
        ),
      ),
    );
  }
}
```

我们创建一个Route，按键打开上面我们创建的需要传入参数的Route，并且打开的Route销毁的时候，打印返回值
```Dart
class RouteTestRoute extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Center(
      child: RaisedButton(
        onPressed: () async {
          var result = await Navigator.push(
            context,
            MaterialPageRoute(builder: (context) {
              return TipRoute(text: "我是提示xxxx");
            }),
          );
          print("路由返回值：$result");
        },
        child: Text("打开提示页"),
      ),
    );
  }
}
```

提示文案，我是提示xxx是通过`TipRoute`的`text`参数传递过来的。我们可以通过等待`Navigator.push(...)`返回的`Future`来获取新路由的返回数据

在TipRoute中有两种返回方式，

    1. 导航栏左边的返回箭头，不会有返回值
    2. 中间的返回按钮，会走逻辑中传递的返回值

`var result = await Navigator.push(...)` 打开新的Route，并等待返回结果

## 总结
通过简单的两个Route，涉及到了Route间参数的传递及返回值的接收，这是普通的Route操作，那么在Flutter中还有一个更直观的方式对Route进行管理，就是命名Route，那么下一篇文章，我们就来看一下这种简单便捷的Route操作方式。