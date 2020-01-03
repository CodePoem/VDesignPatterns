# 命令模式（Command）

![命令模式](https://raw.githubusercontent.com/CodePoem/VDesignPatterns/master/docs/drawio/Command.png)

<a href = "https://www.draw.io/?lightbox=1#Uhttps://raw.githubusercontent.com/CodePoem/VDesignPatterns/master/docs/drawio/Command.png">全屏</a> |
<a href = "https://www.draw.io/#Uhttps://raw.githubusercontent.com/CodePoem/VDesignPatterns/master/docs/drawio/Command.png">作为模板编辑为新图</a> |
<a href = "https://www.draw.io/#HCodePoem/VDesignPatterns/master/docs/drawio/Command.drawio">编辑原图（需登录）</a>

## 定义（what）

- 将一个请求封装为一个对象，从而让用户使用不同的请求对客户进行参数化。
- 对请求排队或记录请求日志，以及支持可撤销的操作

## 缘由（why）

为什么需要命令模式？

将行为调用者和实现者解耦。

## 实践（how）

```java
public class Receiver {
    public void action() {
        // action
    }
}

public interface Command {
   void excute();
}

public class ConcreteCommand implements Command {
    private Receiver receiver;

    public ConcreteCommand(Receiver receiver) {
        this.receiver = receiver;
    }
    @Overrite
    public void excute() {
        // action
        receiver.action();
    }
}

public class Invoker {
    private Command command;

    public Invoker(Command command) {
        this.command = command;
    }

    public void action() {
       command.excute();
    }
}

public class Client {
    public static void main(String[] args) {
        Receiver receiver = new Receiver();
        Command command = new ConcreteCommand(receiver);

        Invoker invoker = new Invoker(command);
        invoker.action();
    }
}
```
