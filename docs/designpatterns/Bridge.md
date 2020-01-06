# 桥接模式（Bridge）

![桥接模式](https://raw.githubusercontent.com/CodePoem/VDesignPatterns/master/docs/drawio/Bridge.png)

<a href = "https://www.draw.io/?lightbox=1#Uhttps://raw.githubusercontent.com/CodePoem/VDesignPatterns/master/docs/drawio/Bridge.png">全屏</a> |
<a href = "https://www.draw.io/#Uhttps://raw.githubusercontent.com/CodePoem/VDesignPatterns/master/docs/drawio/Bridge.png">作为模板编辑为新图</a> |
<a href = "https://www.draw.io/#HCodePoem/VDesignPatterns/master/docs/drawio/Bridge.drawio">编辑原图（需登录）</a>

## 定义（what）

- 将抽象部分和实现部分分离，使得它们都可以独立变化。

## 缘由（why）

为什么需要桥接模式？

在构件的抽象化角色和具体化角色之间增加更多的灵活性。

## 实践（how）

```java
public interface Implementor {
    void methodImpl();
}

public class ConcreteImplementorA implements Implementor {
    @Overrite
    public void methodImpl() {
        // ConcreteImplementorA methodImpl
    }
}

public class ConcreteImplementorB implements Implementor {
    @Overrite
    public void methodImpl() {
        // ConcreteImplementorB methodImpl
    }
}

public abstract class Abstraction {
    protected Implementor implementor;

    public Abstraction() {
    }

    public Abstraction(Implementor implementor) {
        this.implementor = implementor;
    }

    public void setImplementor(Implementor implementor) {
        this.implementor = implementor;
    }

    public abstract void method();
}

public class RefineedAbstraction extends Abstraction {
    public RefineedAbstraction() {
        super();
    }

    public RefineedAbstraction(Implementorimplementor ) {
        super(implementor);
    }

    @Overrite
    public void method() {
        implementor.methodImpl();
    }
}

public class Client {
    public static void main(String[] args) {
        Abstraction abstraction = new RefineedAbstraction();
        abstract.setImplementor(new ConcreteImplementorA()):
        abstract.method();
        abstract.setImplementor(new ConcreteImplementorB()):
        abstract.method();
    }
}
```

### Android中的例子

#### Window 和 WindowManager
