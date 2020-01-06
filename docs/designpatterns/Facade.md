# 外观模式（Facade）

![外观模式](https://raw.githubusercontent.com/CodePoem/VDesignPatterns/master/docs/drawio/Facade.png)

<a href = "https://www.draw.io/?lightbox=1#Uhttps://raw.githubusercontent.com/CodePoem/VDesignPatterns/master/docs/drawio/Facade.png">全屏</a> |
<a href = "https://www.draw.io/#Uhttps://raw.githubusercontent.com/CodePoem/VDesignPatterns/master/docs/drawio/Facade.png">作为模板编辑为新图</a> |
<a href = "https://www.draw.io/#HCodePoem/VDesignPatterns/master/docs/drawio/Facade.drawio">编辑原图（需登录）</a>

## 定义（what）

- 子系统外部与内部通过一个统一的接口通信。

## 缘由（why）

为什么需要外观模式？

为子系统提供一个高层接口，使子系统更加容易使用。

## 实践（how）

```java
public class SubSystemA {
    public void method() {
        // SubSystemA method
    }
}

public class SubSystemB {
    public void method() {
        // SubSystemB method
    }
}

public class SubSystemC {
    public void method() {
        // SubSystemC method
    }
}

public class Facade {
    private SubSystemA subSystemA;
    private SubSystemB subSystemB;
    private SubSystemC subSystemC;

    public Facade() {
        subSystemA = new SubSystemA();
        subSystemB = new SubSystemB();
        subSystemC = new SubSystemC();
    }

    public void methodA() {
        // Facade methodA
        subSystemA.method();
        subSystemB.method();
    }

    public void methodB() {
        // Facade methodB
        subSystemB.method();
        subSystemC.method();
    }
}

public class Client {
    public static void main(String[] args) {
        Facade facade = new Facade();
        facade.methodA();
        facade.methodB();
    }
}
```

### Android中的例子

#### ContextImpl

ContextImpl 内部封装了很多不同子系统的操作，例如 Activity的跳转、发送广播、启动服务、设置壁纸等。
