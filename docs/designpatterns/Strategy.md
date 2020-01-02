# 策略模式（Strategy）

![策略模式](https://raw.githubusercontent.com/CodePoem/VDesignPatterns/master/docs/drawio/Strategy.png)

<a href = "https://www.draw.io/?lightbox=1#Uhttps://raw.githubusercontent.com/CodePoem/VDesignPatterns/master/docs/drawio/Strategy.png">全屏</a> |
<a href = "https://www.draw.io/#Uhttps://raw.githubusercontent.com/CodePoem/VDesignPatterns/master/docs/drawio/Strategy.png">作为模板编辑为新图</a> |
<a href = "https://www.draw.io/#HCodePoem/VDesignPatterns/master/docs/drawio/Strategy.drawio">编辑原图（需登录）</a>

## 定义（what）

- 定义一系列的算法，分别封装起来，并使它们可以互相替换。

## 缘由（why）

为什么需要策略模式？

让算法的变化独立于调用者。策略模式符合开闭原则，可以灵活地注入算法实现，从而达到很好的可扩展性。

## 实践（how）

```java
public Interface Strategy {
    public void algorithm();
}

public class ConcreteStrategyA implements Strategy {
    @Overrite
    public void algorithm() {
        // Do somthing
    }
}

public class ConcreteStrategyB implements Strategy {
    @Overrite
    public void algorithm() {
        // Do somthing
    }
}

public class Context {

    private Strategy mStrategy;

    public void setStrategy(Strategy strategy) {
        this.mStrategy = strategy;
    }

    public void algorithm() {
        mStrategy.algorithm();
    }
}
```

PS：
与状态模式容易混淆，但实际上策略模式更关注的是算法（算法往往是独立的），而状态模式更关注的是状态对行为的影响（状态有时候可能会有依赖）。
