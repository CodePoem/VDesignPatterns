# 单一职责原则

## 定义（what）

- 单一职责原则（Single Responsibility Principle）缩写 SRP 。
- 类应该是一组相关性很高的函数、数据的封装，它的职责是单一的。

## 缘由（why）

为什么要确保职责是单一呢？

这很好理解，如果一个类承担过多的职责，那么代码的耦合性就越高，就越不易维护，牵一发而动全身。举个例子，图片裁剪和图片选择的功能，如果都放一个类里完成，那么当我需要修改他们两个其中一个功能而不希望另外一个功能受影响的时候就捉襟见肘了。

## 实践（how）

职责单一的界定可能不是很清晰，往往依赖个人经验和具体的业务逻辑。通常我们依据个人经验和具体的业务逻辑来判断一个类是否承载了过多的职责，而对类进行功能划分，拆分更多出职责单一的类来。