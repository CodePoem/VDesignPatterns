# 中介者模式（Mediator）

![中介者模式](https://raw.githubusercontent.com/CodePoem/VDesignPatterns/master/docs/drawio/Mediator.png)

<a href = "https://www.draw.io/?lightbox=1#Uhttps://raw.githubusercontent.com/CodePoem/VDesignPatterns/master/docs/drawio/Mediator.png">全屏</a> |
<a href = "https://www.draw.io/#Uhttps://raw.githubusercontent.com/CodePoem/VDesignPatterns/master/docs/drawio/Mediator.png">作为模板编辑为新图</a> |
<a href = "https://www.draw.io/#HCodePoem/VDesignPatterns/master/docs/drawio/Mediator.drawio">编辑原图（需登录）</a>

## 定义（what）

- 用一个中介对象来封装一系列的对象交互。

## 缘由（why）

为什么需要中介者模式？

中介者模式使得各个对象不需要显式地相互引用，从而使其耦合松散，而且可以独立地改变它们之间的交互。
中介者模式将多对多的相互作用转化为一对多的相互作用。

## 实践（how）

```java
public abstract class Mediator {
    protected ConcreteColleagueA colleagueA;
    protected ConcreteColleagueB colleagueB;

    public abstract void method();
}

public class ConcreteMediator extends Mediator {
    @Overrite
    public void method() {
        colleagueA.action();
        colleagueB.action();
    }
}

public abstract class Colleague {
    protected Mediator mediator;

    public Colleague(Mediator mediator) {
        this.mediator = mediator;
    }

    public abstract void action();
}

public class ConcreetColleagueA extends Colleague {
    public ConcreetColleagueA(Mediatormediator) {
        super(mediator);
    }
    @Overrite
    public void action() {
        // ConcreetColleagueA action
    }
}

public class ConcreetColleagueB extends Colleague {
    public ConcreetColleagueB(Mediatormediator) {
        super(mediator);
    }
    @Overrite
    public void action() {
        // ConcreetColleagueB action
    }
}
```

### Android中的例子

#### Keyguard锁屏

KeyguardViewMediator管理协调各种Manager(AlarmManager、AudioManager等)。

#### Binder机制
