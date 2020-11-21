# Flutter Widget | 18 | ScaleTransition

## Here is the video tutorial

[![YouTube](https://img.youtube.com/vi/WuXus0RlWrU/0.jpg)](https://youtu.be/WuXus0RlWrU "ScaleTransition | Animation,Tween, FloatingActionButton")

### Code
#### main.dart

```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      title: 'Flutter Demo',
      theme: ThemeData(
        primaryColor: Color(0xFF832685),
        primaryColorLight: Color(0xFFC81379),
        accentColor: Colors.black,
      ),
      home: MyHomePage(),
    );
  }
}

class MyHomePage extends StatefulWidget {
  @override
  _MyHomePageState createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage>
    with SingleTickerProviderStateMixin {
  String title = 'Scale Transition';

  bool _isPlaying = false;
  AnimationController _animationController;
  Animation<double> _animation;

  void animate() {
    if (_isPlaying)
      _animationController.stop();
    else
      _animationController.forward();

    setState(() {
      _isPlaying = !_isPlaying;
    });
  }

  @override
  void initState() {
    super.initState();
    _animationController =
        AnimationController(vsync: this, duration: Duration(seconds: 2));

    _animation = Tween<double>(begin: 1.5, end: 2.5).animate(
        CurvedAnimation(parent: _animationController, curve: Curves.easeIn));

    _animation.addStatusListener((status) {
      if (status == AnimationStatus.completed)
        _animationController.reverse();
      else if (status == AnimationStatus.dismissed)
        _animationController.forward();
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(title),
        centerTitle: true,
      ),
      body: Material(
        child: Center(
          child: Column(
            mainAxisSize: MainAxisSize.min,
            children: <Widget>[
              Padding(
                padding: const EdgeInsets.all(32.0),
                child: Text(
                  'Press Play Button',
                  style: TextStyle(fontSize: 22),
                ),
              ),
              ScaleTransition(
                scale: _animation,
                child: Container(
                  child: Icon(
                    Icons.favorite,
                    color: Colors.red,
                  ),
                ),
              ),
              Padding(
                padding: const EdgeInsets.all(32.0),
                child: FloatingActionButton(
                    child: _isPlaying
                        ? Icon(
                            Icons.pause,
                            color: Colors.white,
                            size: 32,
                          )
                        : Icon(
                            Icons.play_arrow,
                            color: Colors.white,
                            size: 32,
                          ),
                    tooltip: 'Play',
                    backgroundColor: Color(0xFF832685),
                    onPressed: animate),
              )
            ],
          ),
        ),
      ),
    );
  }
}
```

[Link to blog post](https://thetechdesigner7363.blogspot.com/2020/05/flutter-widgets-18-scaletransition.html)

[![The Tech Designer's blog](https://3.bp.blogspot.com/-4GCVha8IzrQ/XrphAY6Rw6I/AAAAAAAAAKg/bcNnWC7dYy8y-zW7c0xEYvwmFUChE9zIQCK4BGAYYCw/s113/logo1.png)](https://www.thetechdesigner7363.blogspot.com/ "The Tech Designer's blog")

