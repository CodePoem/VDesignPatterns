# 解释器模式（Interpreter）

![解释器模式](https://raw.githubusercontent.com/CodePoem/VDesignPatterns/master/docs/drawio/Interpreter.png)

<a href = "https://www.draw.io/?lightbox=1#Uhttps://raw.githubusercontent.com/CodePoem/VDesignPatterns/master/docs/drawio/Interpreter.png">全屏</a> |
<a href = "https://www.draw.io/#Uhttps://raw.githubusercontent.com/CodePoem/VDesignPatterns/master/docs/drawio/Interpreter.png">作为模板编辑为新图</a> |
<a href = "https://www.draw.io/#HCodePoem/VDesignPatterns/master/docs/drawio/Interpreter.drawio">编辑原图（需登录）</a>

## 定义（what）

- 给定一种语言，定义它的文法（语法）的一种表示，并定义一个解释器，这个解释器使用该表示来解释语言中的句子。
- 正则表达式就是解释器模式的一种应用。

## 缘由（why）

为什么需要解释器模式？

能够支持某种简单的语言（或简单语法）的解释执行（该语言的语句可以表示为抽象语法树）,且容易改变和扩展文法。

## 实践（how）

```java
public class Context {

}

public abstract Class AbstractExpression {

    public abstract void interpret(Context context);
}

public class TerminalExpression extend AbstractExpression {
    @Overrite
    public void interpret(Context context) {
        // Do something
    }
}

public class NormalExpression extend AbstractExpression {
    @Overrite
    public void interpret(Context context) {
        // Do something
    }
}
```
