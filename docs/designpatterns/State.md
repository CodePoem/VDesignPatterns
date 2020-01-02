# 状态模式（State）

![状态模式](https://raw.githubusercontent.com/CodePoem/VDesignPatterns/master/docs/drawio/State.png)

<a href = "https://www.draw.io/?lightbox=1#Uhttps://raw.githubusercontent.com/CodePoem/VDesignPatterns/master/docs/drawio/State.png">全屏</a> |
<a href = "https://www.draw.io/#Uhttps://raw.githubusercontent.com/CodePoem/VDesignPatterns/master/docs/drawio/State.png">作为模板编辑为新图</a> |
<a href = "https://www.draw.io/#HCodePoem/VDesignPatterns/master/docs/drawio/State.drawio">编辑原图（需登录）</a>

## 定义（what）

- 当一个对象的内存状态改变的时允许改变其行为，使得这个对象看起来像是改变了其类。

## 缘由（why）

为什么需要状态模式模式？

当需要运行时改变对象的状态，使得对象的行为改变，但同时对象的状态转换逻辑过于复杂，就需要将状态模式来分割不同状态，将特定的状态相关行为都封装起来。

## 实践（how）

```java
public Interface State {
    public void doSomething();
}

public class ConcreteStateA implements State {
    @Overrite
    public void doSomething() {
        // Do somthing
    }
}

public class ConcreteStateB implements State {
    @Overrite
    public void doSomething() {
        // Do somthing
    }
}

public class Context {

    private State mState;

    public void setState(State state) {
        this.mState = state;
    }

    public void doSomething() {
        mState.doSomething();
    }
}
```

PS：
与策略容易混淆，但实际上状态模式更关注的是状态对行为的影响（状态有时候可能会有依赖），而策略模式更关注的是算法（算法往往是独立的）。
