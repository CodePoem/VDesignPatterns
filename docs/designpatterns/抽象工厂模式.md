# 抽象工厂模式（AbstractFactory）

![抽象工厂模式](https://raw.githubusercontent.com/CodePoem/VDesignPatterns/master/docs/drawio/AbstractFactory.png)

<a href = "https://www.draw.io/?lightbox=1#Uhttps://raw.githubusercontent.com/CodePoem/VDesignPatterns/master/docs/drawio/AbstractFactory.png">全屏</a> |
<a href = "https://www.draw.io/#Uhttps://raw.githubusercontent.com/CodePoem/VDesignPatterns/master/docs/drawio/AbstractFactory.png">作为模板编辑为新图</a> |
<a href = "https://www.draw.io/#HCodePoem/VDesignPatterns/master/docs/drawio/AbstractFactory.drawio">编辑原图（需登录）</a>

## 定义（what）

- 提供一个创建一些列相关或者相互依赖的对象的接口，而不需要指定它们的具体类。

## 缘由（why）

为什么需要抽象工厂模式？

当一个产品族中的多个对象被设计成一起工作时，需要确保始终只使用同一个产品族中的对象。（例如不同操作系统平台下的各种软件）

什么是产品族？
位于不同产品等级结构中，功能相关联的产品组成的家族。

## 实践（how）

```java
public abstract class AbstractProductA {
}

public abstract class AbstractProductB {
}

public class ConcreteProductA1 extends Product {
}

public class ConcreteProductA2 extends Product {
}

public class ConcreteProductB1 extends Product {
}

public class ConcreteProductB2 extends Product {
}
```

```java
public abstract class AbstractFactory {
    public abstract AbstractProductA creteProductA();
    public abstract AbstractProductB creteProductB();
}

public class ConcreteFactory1 extends Factory {
    @Override
    public AbstractProductA creteProductA() {
        return ConcreteProductA1();
    }

    @Override
    public AbstractProductB creteProductB() {
        return ConcreteProductB1();
    }
}

public class ConcreteFactory2 extends Factory {
    @Override
    public AbstractProductA creteProductA() {
        return ConcreteProductA2();
    }

    @Override
    public AbstractProductB creteProductB() {
        return ConcreteProductB2();
    }
}
```

```java
public class Client {
    public static void main(String[] args) {
        AbstractFactory factory1 = new ConcreteFactory1();
        AbstractProductA productA1 = factory1.creteProductA();
        AbstractProductB productB1 = factory1.creteProductB();
        AbstractFactory factory2 = new ConcreteFactory2();
        AbstractProductA productA2 = factory2.creteProductA();
        AbstractProductB productB2 = factory2.creteProductB();
    }
}
```
