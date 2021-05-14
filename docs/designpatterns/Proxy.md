# 代理模式（Proxy）

![代理模式](https://raw.githubusercontents.com/CodePoem/VDesignPatterns/master/docs/drawio/Proxy.png)

<a href = "https://www.draw.io/?lightbox=1#Uhttps://raw.githubusercontents.com/CodePoem/VDesignPatterns/master/docs/drawio/Proxy.png">全屏</a> |
<a href = "https://www.draw.io/#Uhttps://raw.githubusercontents.com/CodePoem/VDesignPatterns/master/docs/drawio/Proxy.png">作为模板编辑为新图</a> |
<a href = "https://www.draw.io/#HCodePoem/VDesignPatterns/master/docs/drawio/Proxy.drawio">编辑原图（需登录）</a>

## 定义（what）

- 为其他对象提供一种代理以控制对整个对象的访问。

## 缘由（why）

为什么需要代理模式？

当无法或者不想直接访问某个对象或访问某个对象存在困难时。

## 实践（how）

代理模式主要可以分为两大类，静态代理和动态代理。

- 静态代理

编译时代理，对性能几乎无影响。

- 动态代理

运行时（Runtime）代理，对性能有些影响。

```java
public abstract class Subject {
    public abstract void visit();
}

public class RealSubject extends Subject {
    @Overrite
    public void visit() {
        // RealSubject visit
    }
}

public class ProxySubject extends Subject {
    private RealSubject realSubject;

    @Overrite
    public void visit() {
        if (realSubject != null) {
            realSubject = new RealSubject();
        }
        realSubject.visit();
    }
}

public class Client {
    public static void main(String[] args) {
       ProxySubject proxySubject = new ProxySubject();
       proxySubject.visit();
    }
}
```

### Android 中的例子

#### 埋点/AOP

静态代理：

- JavaCode -> .java (IDE Processor) : APT / AST
- .java -> .class (Java Compiler) : AspectJ
- .class -> .dex (GradlePlugin) : ASM / Javassist

动态代理：

#### Binder 机制
