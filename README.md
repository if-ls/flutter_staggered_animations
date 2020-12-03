# Flutter Staggered Animations

适用于Row、Column、List、Grid的展示动画。

## 动图

| ListView                  | GridView                   | Column                       |
| ---                       | ---                        | ---                          |
|![](https://github.com/mobiten/flutter_staggered_animations/blob/master/assets/card_list.gif?raw=true)  | ![](https://github.com/mobiten/flutter_staggered_animations/blob/master/assets/card_grid.gif?raw=true)  | ![](https://github.com/mobiten/flutter_staggered_animations/blob/master/assets/card_column.gif?raw=true)  |


## 安装

### 依赖
```yaml
dependencies:
  flutter_staggered_animations: "^0.0.1"
```

### Import
```dart
import 'package:flutter_staggered_animations/flutter_staggered_animations.dart';
```

## AnimationConfiguration构造方法

- `AnimationConfiguration.staggeredList` 

  > 适用于`ListView`的动画

- `AnimationConfiguration.staggeredGrid`

  > 适用于`GridView`的动画

- `AnimationConfiguration.toStaggeredList`

  > 适用于`Row`、`Column`的动画

## Animations

- `FadeInAnimation`：Opacity显示隐藏动画
- `SlideAnimation`：水平或垂直方向的平移动画
- `ScaleAnimation`：放大、缩小动画
- `FlipAnimation`：X轴、Y轴旋转动画


##  样例 

### ListView

```dart
@override
Widget build(BuildContext context) {
  return Scaffold(
    body: AnimationLimiter(
      child: ListView.builder(
        itemCount: 100,
        itemBuilder: (BuildContext context, int index) {
          return AnimationConfiguration.staggeredList(
            position: index,
            duration: const Duration(milliseconds: 375),
            child: SlideAnimation(
              verticalOffset: 50.0,
              child: FadeInAnimation(
                child: YourListChild(),
              ),
            ),
          );
        },
      ),
    ),
  );
}
```

### GridView

```dart
@override
Widget build(BuildContext context) {
  int columnCount = 3;

  return Scaffold(
    body: AnimationLimiter(
      child: GridView.count(
        crossAxisCount: columnCount,
        children: List.generate(
          100,
          (int index) {
            return AnimationConfiguration.staggeredGrid(
              position: index,
              duration: const Duration(milliseconds: 375),
              columnCount: columnCount,
              child: ScaleAnimation(
                child: FadeInAnimation(
                  child: YourListChild(),
                ),
              ),
            );
          },
        ),
      ),
    ),
  );
}
```

### Column

```dart
@override
  Widget build(BuildContext context) {
    return Scaffold(
      body: SingleChildScrollView(
        child: AnimationLimiter(
          child: Column(
            children: AnimationConfiguration.toStaggeredList(
              duration: const Duration(milliseconds: 375),
              childAnimationBuilder: (widget) => SlideAnimation(
                horizontalOffset: 50.0,
                child: FadeInAnimation(
                  child: widget,
                ),
              ),
              children: YourColumnChildren(),
            ),
          ),
        ),
      ),
    );
  }
```
