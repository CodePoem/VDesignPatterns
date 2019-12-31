# 策略模式（Strategy）

![策略模式](https://raw.githubusercontent.com/CodePoem/VDesignPatterns/master/docs/drawio/Strategy.png)

<a href = "https://www.draw.io/?lightbox=1#Uhttps://raw.githubusercontent.com/CodePoem/VDesignPatterns/master/docs/drawio/Strategy.png">全屏</a> |
<a href = "https://www.draw.io/#Uhttps://raw.githubusercontent.com/CodePoem/VDesignPatterns/master/docs/drawio/Strategy.png">作为模板编辑为新图</a> |
<a href = "https://www.draw.io/#HCodePoem/VDesignPatterns/master/docs/drawio/Strategy.drawio">编辑原图（需登录）</a>

## 定义（what）

- 定义一系列的算法，分别封装起来，并使它们可以互相替换。

## 缘由（why）

为什么需要策略模式？

让算法的变化独立于调用者。

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

    public void setStrategy(Strategy mStrategy) {
        this.mStrategy = mStrategy;
    }

    public void algorithm() {
        mStrategy.algorithm();
    }
}
```
