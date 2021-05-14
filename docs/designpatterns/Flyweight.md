# 享元模式（Flyweight）

![享元模式](https://raw.githubusercontents.com/CodePoem/VDesignPatterns/master/docs/drawio/Flyweight.png)

<a href = "https://www.draw.io/?lightbox=1#Uhttps://raw.githubusercontents.com/CodePoem/VDesignPatterns/master/docs/drawio/Flyweight.png">全屏</a> |
<a href = "https://www.draw.io/#Uhttps://raw.githubusercontents.com/CodePoem/VDesignPatterns/master/docs/drawio/Flyweight.png">作为模板编辑为新图</a> |
<a href = "https://www.draw.io/#HCodePoem/VDesignPatterns/master/docs/drawio/Flyweight.drawio">编辑原图（需登录）</a>

## 定义（what）

- 运用共享技术有效地支持大量细粒度的对象。

## 缘由（why）

为什么需要享元模式？

缓存共享对象，达到对象共享，避免创建过多对象，提升性能。

## 实践（how）

```java
public abstract class Flyweight {
    public abstract void method();
}

public class ConcreteFlyweight extends Flyweight {
    @Overrite
    public void method() {
        // ConcreteFlyweight method
    }
}

public class FlyweightFactory {
    private HashMap map = new HashMap();

    public FlyweightFactory() {
        map.put("A", new ConcreteFlyweight());
        map.put("B", new ConcreteFlyweight());
        map.put("C", new ConcreteFlyweight());
    }

    @Overrite
    public Flyweight getFlyweight(String key) {
        return (Flyweight)(map.get(key));
    }
}

public class Client {
    public static void main(String[] args) {
        FlyweightFactory flyweightFactory = new FlyweightFactory();
        Flyweight flyweightA = flyweightFactory.get("A");
        flyweightA.method();
        Flyweight flyweightB = flyweightFactory.get("B");
        flyweightB.method();
        Flyweight flyweightC = flyweightFactory.get("C");
        flyweightC.method();
    }
}
```

### Android 中的例子

#### Message obtain()
