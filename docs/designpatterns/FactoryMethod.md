# 工厂方法模式（FactoryMethod）

![工厂方法模式](https://raw.githubusercontents.com/CodePoem/VDesignPatterns/master/docs/drawio/FactoryMethod.png)

<a href = "https://www.draw.io/?lightbox=1#Uhttps://raw.githubusercontents.com/CodePoem/VDesignPatterns/master/docs/drawio/FactoryMethod.png">全屏</a> |
<a href = "https://www.draw.io/#Uhttps://raw.githubusercontents.com/CodePoem/VDesignPatterns/master/docs/drawio/FactoryMethod.png">作为模板编辑为新图</a> |
<a href = "https://www.draw.io/#HCodePoem/VDesignPatterns/master/docs/drawio/FactoryMethod.drawio">编辑原图（需登录）</a>

## 定义（what）

- 定义一个用于创建对象的接口，让子类决定实例化哪个类。

## 缘由（why）

为什么需要工厂方法模式？

对于复杂对象的创建，希望不暴露创建的细节，只暴露创建的接口，符合依赖倒置原则(面向接口编程)。

## 实践（how）

### 工厂方法

抽象产品类、具体产品类、抽象工厂类、具体工厂类。
其中抽象工厂类是工厂方法模式的核心，具体工厂类来实现具体的创建业务逻辑。

```java
public abstract class Product {
}

public class ConcreteProductA extends Product {
}

public class ConcreteProductB extends Product {
}
```

```java
public abstract class Factory {
    public abstract Product creteProduct();
}

public class ConcreteFactory extends Factory {
    @Override
    public Product creteProduct() {
        // 具体工厂类决定创建出什么具体产品
        return new ConcreteProductA();
        // return ConcreteProductB();
    }
}
```

```java
public class Client {
    public static void main(String[] args) {
        Fatctory factory = new ConcreteFactory();
        Product product = factory.creteProduct();
    }
}
```

另外，具体工厂类可以用反射来简洁、灵活地创建具体产品（编译时转为运行时）。

```java
public abstract class Factory {
    public abstract <T extends Product> T creteProduct(Class<T> clz);
}

public class ConcreteFactory extends Factory {
    @Override
    public <T extends Product> T  creteProduct(Class<T> clz) {
        Product product = null;
        try {
            product = (Product) Class.forName(clz.getName()).newInstance();
        } catch (Exception e) {
            e.printStackTrace();
        }
        return (T) product;
    }
}
```

```java
public class Client {
    public static void main(String[] args) {
        Fatctory factory = new ConcreteFactory();
        Class clz =  ConcreteProductB.class;
        Product product = factory.creteProduct(clz);
    }
}
```

### 多工厂方法

为每一种产品定义一个具体的工厂，各司其职。

```java
public abstract class Factory {
    public abstract Product creteProduct();
}

public class ConcreteFactoryA extends Factory {
    @Override
    public Product creteProduct() {
        return ConcreteProductA();
    }
}

public class ConcreteFactoryB extends Factory {
    @Override
    public Product creteProduct() {
        return ConcreteProductB();
    }
}
```

```java
public class Client {
    public static void main(String[] args) {
        Fatctory factoryA = new ConcreteFactoryA();
        Product productA = factoryA.creteProduct();
        Fatctory factoryB = new ConcreteFactoryB();
        Product productB = factoryB.creteProduct();
    }
}
```

### 简单工厂（静态工厂模式）

工厂方法模式的弱化版。如果确定只有一个工厂类，那么可以简化掉抽象类，将对应的工厂方法改为静态方法即可。

```java
public abstract class Product {
}

public class ConcreteProduct extends Product {
}

public class Factory {
    public static Product createProduct() {
         // 决定创建出什么具体产品
        return new ConcreteProductA();
        // return ConcreteProductB();
    }
}
```
