---
title: 新建Flutter项目并分析
copyright: true
date: 2019-09-06 22:44:17
tags:
categories: Flutter
---



[TOC]

使用AndroidStudio创建一个新的Flutter项目，我们来对它进行分析
## 代码
`main.dart`代码如下:
```Dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      theme: ThemeData(
        // This is the theme of your application.
        //
        // Try running your application with "flutter run". You'll see the
        // application has a blue toolbar. Then, without quitting the app, try
        // changing the primarySwatch below to Colors.green and then invoke
        // "hot reload" (press "r" in the console where you ran "flutter run",
        // or simply save your changes to "hot reload" in a Flutter IDE).
        // Notice that the counter didn't reset back to zero; the application
        // is not restarted.
        primarySwatch: Colors.blue,
      ),
      home: MyHomePage(title: 'Flutter Demo Home Page'),
    );
  }
}

class MyHomePage extends StatefulWidget {
  MyHomePage({Key key, this.title}) : super(key: key);

  // This widget is the home page of your application. It is stateful, meaning
  // that it has a State object (defined below) that contains fields that affect
  // how it looks.

  // This class is the configuration for the state. It holds the values (in this
  // case the title) provided by the parent (in this case the App widget) and
  // used by the build method of the State. Fields in a Widget subclass are
  // always marked "final".

  final String title;

  @override
  _MyHomePageState createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  int _counter = 0;

  void _incrementCounter() {
    setState(() {
      // This call to setState tells the Flutter framework that something has
      // changed in this State, which causes it to rerun the build method below
      // so that the display can reflect the updated values. If we changed
      // _counter without calling setState(), then the build method would not be
      // called again, and so nothing would appear to happen.
      _counter++;
    });
  }

  @override
  Widget build(BuildContext context) {
    // This method is rerun every time setState is called, for instance as done
    // by the _incrementCounter method above.
    //
    // The Flutter framework has been optimized to make rerunning build methods
    // fast, so that you can just rebuild anything that needs updating rather
    // than having to individually change instances of widgets.
    return Scaffold(
      appBar: AppBar(
        // Here we take the value from the MyHomePage object that was created by
        // the App.build method, and use it to set our appbar title.
        title: Text(widget.title),
      ),
      body: Center(
        // Center is a layout widget. It takes a single child and positions it
        // in the middle of the parent.
        child: Column(
          // Column is also a layout widget. It takes a list of children and
          // arranges them vertically. By default, it sizes itself to fit its
          // children horizontally, and tries to be as tall as its parent.
          //
          // Invoke "debug painting" (press "p" in the console, choose the
          // "Toggle Debug Paint" action from the Flutter Inspector in Android
          // Studio, or the "Toggle Debug Paint" command in Visual Studio Code)
          // to see the wireframe for each widget.
          //
          // Column has various properties to control how it sizes itself and
          // how it positions its children. Here we use mainAxisAlignment to
          // center the children vertically; the main axis here is the vertical
          // axis because Columns are vertical (the cross axis would be
          // horizontal).
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            Text(
              'You have pushed the button this many times:',
            ),
            Text(
              '$_counter',
              style: Theme.of(context).textTheme.display1,
            ),
          ],
        ),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: _incrementCounter,
        tooltip: 'Increment',
        child: Icon(Icons.add),
      ), // This trailing comma makes auto-formatting nicer for build methods.
    );
  }
}
```

## 分析

### 导入包
`import 'package:flutter/material.dart';` 这是一套标准的UI设计语言，是Google所大力推行的，包括原生Android都有Material风格的设计
### 应用入口
`void main() => runApp(MyApp());` dart语言跟java语言一样，都有一个执行的入口方法，main()方法就是该入口。
该方法中的 => 符号，是Dart中当行函数或者方法的简写，所以，该方法也可以写为
```Dart
void main(){
  runApp(MyApp());
}
```

在Main方法中，运行了runApp方法，该方法的功能是启动Flutter应用。它接受一个Widget作为参数。
MyApp()是Flutter应用的根组件

### 应用结构
为了方便阅读，去掉了注释
```Dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: MyHomePage(title: 'Flutter Demo Home Page'),
    );
  }
}
```

该类继承了`StatelessWidget`类而通过源码，可以看到`StatelessWidget`类又继承了`Widget`，所以，MyApp是一个`Widget`

Flutter在构建页面的时候会调用`Widget`的build方法，在该方法中返回一个`Widget`

当前方法中返回了一个`MaterialApp`的Widget。`MateruakApp`是Material库中提供的Flutter APP框架，通过它可以设置应用的名称、主题、语言、首页及路由列表等。

`title`应用的名称
`theme`应用的主题
`home`应用的首页，是一个Widget，代码中返回的是`MyHomePage`

### 首页
为了方便阅读，去掉了注释
```Dart
class MyHomePage extends StatefulWidget {
  MyHomePage({Key key, this.title}) : super(key: key);

  final String title;

  @override
  _MyHomePageState createState() => _MyHomePageState();
}
```
`MyHomePage`继承了`StatefulWidget`表示是一个有状态的`Widget`，也是一个`Widget`

#### 有状态的Widget和无状态的Widget
- `StatelessWidget`表示无状态的Widget，状态不可变
- `StatefulWidget`表示有状态的Widget，状态在Widget的生命周期中是可变化的
- `Stateful Widget`至少有两个类来构成
    1. 一个StatefulWidget类。
    2. 一个 State类； StatefulWidget类本身是不变的，但是State类中持有的状态在widget生命周期中可能会发生变化。

在`MyHomePage`中创建并返回了一个`_MyHomePageState`类
`_MyHomePageState`类是`MyHomePage`类对应的状态类。

### State类
为了便于阅读，去掉了注释
```Dart
class _MyHomePageState extends State<MyHomePage> {
  int _counter = 0;

  void _incrementCounter() {
    setState(() {
      _counter++;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(widget.title),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            Text(
              'You have pushed the button this many times:',
            ),
            Text(
              '$_counter',
              style: Theme.of(context).textTheme.display1,
            ),
          ],
        ),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: _incrementCounter,
        tooltip: 'Increment',
        child: Icon(Icons.add),
      ), 
    );
  }
}
```

在该Widget中的build方法中返回了一个`Scaffold`，
`Scaffold`是 Material组件库中提供的一个组件，它提供了默认的导航栏、标题和包含主屏幕widget树（后同“组件树”或“部件树”）的body属性。组件树可以很复杂。
`appBar`是导航栏部分，下面的title，是应用的名称
`body`是主要显示的内容部分，里面的是显示的Widget
`floatingActionButton`是右下角浮动的按钮

该方法中，body是一个`Center`的组件，表示widget位置居中，它的子Widget是一个`Column`

`Column`的作用是将其所有子组件沿屏幕垂直方向依次排列

此例中Column子组件是两个 Text，第一个Text 显示固定文本 “You have pushed the button this many times:”，第二个Text 显示_counter状态的数值。

当点击`floatingActionButton`,会执行`_incrementCounter`方法，该方法会使的`_counter`值自增加，然后刷新状态重新构建UI。

## 总结
到此，第一个Flutter项目的分析就结束了。可以看出来，虽然是刚刚开始接触，但是其实还是有迹可寻的。只不过前期因为不熟练，可能会比较吃力，等会面熟悉了，应该会好很多。