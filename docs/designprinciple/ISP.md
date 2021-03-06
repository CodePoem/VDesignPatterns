# 接口隔离原则

## 定义（what）

- 接口隔离原则（Interface Segregation Principle）缩写 ISP 。
- 客户端不应该依赖它不需要的接口。
- 类间的依赖关系应该建立在最小的接口上。

## 缘由（why）

为什么要细化接口粒度？

减低接口的使用难度，隐藏不必要、客户端根本不关心的接口信息。

## 实践（how）

根据客户端实际关心的接口信息，将庞大的接口拆分为多个更细粒度的接口。例如图片加载框架只需知道图片缓存接口有存、取的接口信息即可，其他的一概不关心，这就使得缓存功能的具体实现对于图片加载框架来说是隐藏的。
