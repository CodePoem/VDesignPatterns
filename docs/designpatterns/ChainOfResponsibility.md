# 责任链模式（ChainOfResponsibility）

![责任链模式](https://raw.githubusercontents.com/CodePoem/VDesignPatterns/master/docs/drawio/ChainOfResponsibility.png)

<a href = "https://www.draw.io/?lightbox=1#Uhttps://raw.githubusercontents.com/CodePoem/VDesignPatterns/master/docs/drawio/ChainOfResponsibility.png">全屏</a> |
<a href = "https://www.draw.io/#Uhttps://raw.githubusercontents.com/CodePoem/VDesignPatterns/master/docs/drawio/ChainOfResponsibility.png">作为模板编辑为新图</a> |
<a href = "https://www.draw.io/#HCodePoem/VDesignPatterns/master/docs/drawio/ChainOfResponsibility.drawio">编辑原图（需登录）</a>

## 定义（what）

- 使多个对象都有机会处理请求，从而避免请求的发送者和接受者之间的耦合关系。将这些对象连成一条链，并沿着这条链传递该请求，直到有对象处理它为止。

## 缘由（why）

为什么需要责任链模式？

多个对象可以处理同一请求，可以在运行时动态决定处理请求的对象。

## 实践（how）

```java
public abstract Class Handler {

    protected Handler successor;

    public void setSuccessor(Handler successor) {
        this.successor = successor;
    }

    public abstract void handleRequest(String request);
}

public class ConcreteHandlerA extend Handler {
    @Overrite
    public void handleRequest(String request) {
        boolean matched = false;
        // jude matcher
        if (matched) {
            // Do somthing
        } else {
            successor.handleRequest(request);
        }
    }
}

public class ConcreteHandlerB extend Handler {
    @Overrite
    public void handleRequest(String request) {
        boolean matched = false;
        // jude matcher
        if (matched) {
            // Do somthing
        } else {
            successor.handleRequest(request);
        }
    }
}

public class Client {
    publica static void main(String[] args) {
        ConcreteHandlerA concreteHandlerA = new ConcreteHandlerA();
        ConcreteHandlerB concreteHandlerB = new ConcreteHandlerB();
        concreteHandlerA.setSuccessor(concreteHandlerB);
        concreteHandlerB.setSuccessor(concreteHandlerA);
        concreteHandlerA.handleRequst("request");
    }
}
```
