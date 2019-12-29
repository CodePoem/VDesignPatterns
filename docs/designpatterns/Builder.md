# 建造者模式（Builder）

![建造者模式](https://raw.githubusercontent.com/CodePoem/VDesignPatterns/master/docs/drawio/Builder.png)

<a href = "https://www.draw.io/?lightbox=1#Uhttps://raw.githubusercontent.com/CodePoem/VDesignPatterns/master/docs/drawio/Builder.png">全屏</a> |
<a href = "https://www.draw.io/#Uhttps://raw.githubusercontent.com/CodePoem/VDesignPatterns/master/docs/drawio/Builder.png">作为模板编辑为新图</a> |
<a href = "https://www.draw.io/#HCodePoem/VDesignPatterns/master/docs/drawio/Builder.drawio">编辑原图（需登录）</a>

## 定义（what）

- 将一个复杂对象的构建过程与其构建的表示分离，使得同样的构建过程可以创建不同的表示。

## 缘由（why）

为什么需要建造者模式？

为了将复杂对象的构建过程和构建部件的表示解耦。

## 实践（how）

在实际使用中，通常会去除UML图中Director角色，直接使用Builder的链式调用来进行对象的组装。多用于配置项的配置场景。

