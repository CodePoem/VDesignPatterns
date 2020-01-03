# 开闭原则

## 定义（what）

- 开闭原则（Open Close Principle）缩写 OCP 。
- 软件中的对象（类、模块、函数等）应该对扩展开放，对修改关闭。

## 缘由（why）

为什么要对扩展开放，对修改关闭？

在软件的生命周期中，因为各种原因需要对原有软件进行修改时，可能会将错误异常引入到原本已经过测试的旧代码中去。

## 实践（how）

在实际中不可能完全做到对扩展开放，对修改关闭。往往修改原代码和扩展代码是同时存在的。在软件变化时，尽量通过扩展来实现变化，而不是修改已有代码来实现。