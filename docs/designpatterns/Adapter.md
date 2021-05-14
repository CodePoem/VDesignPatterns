# 适配器模式（Adapter）

![适配器模式](https://raw.githubusercontents.com/CodePoem/VDesignPatterns/master/docs/drawio/Adapter.png)

<a href = "https://www.draw.io/?lightbox=1#Uhttps://raw.githubusercontents.com/CodePoem/VDesignPatterns/master/docs/drawio/Adapter.png">全屏</a> |
<a href = "https://www.draw.io/#Uhttps://raw.githubusercontents.com/CodePoem/VDesignPatterns/master/docs/drawio/Adapter.png">作为模板编辑为新图</a> |
<a href = "https://www.draw.io/#HCodePoem/VDesignPatterns/master/docs/drawio/Adapter.drawio">编辑原图（需登录）</a>

## 定义（what）

- 将一个类的接口转换成客户希望的另外一个接口。

## 缘由（why）

为什么需要适配器模式？

使那些接口不兼容的类可以一起工作。

## 实践（how）

```java
public class Target {
    public void method() {
        // Target do something
    }
}

public class Adaptee {
    public void otherMethod() {
        // Adaptee do something
    }
}

public class Adapter {
    private Adaptee adaptee;

    public Adapter(Adaptee adaptee) {
        this.adaptee = adaptee;
    }

    public void method() {
        adaptee.otherMethod();
    }
}

public class Client {
    public static void main(String[] args) {
        Adapter adapter = new Adapter(new Adaptee());
        adapter.method();
    }
}
```

### Android 中的例子

#### ListView / RecyclerView 的 Adapter
