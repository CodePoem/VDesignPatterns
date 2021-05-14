# 装饰模式（Decorator）

![装饰模式](https://raw.githubusercontents.com/CodePoem/VDesignPatterns/master/docs/drawio/Decorator.png)

<a href = "https://www.draw.io/?lightbox=1#Uhttps://raw.githubusercontents.com/CodePoem/VDesignPatterns/master/docs/drawio/Decorator.png">全屏</a> |
<a href = "https://www.draw.io/#Uhttps://raw.githubusercontents.com/CodePoem/VDesignPatterns/master/docs/drawio/Decorator.png">作为模板编辑为新图</a> |
<a href = "https://www.draw.io/#HCodePoem/VDesignPatterns/master/docs/drawio/Decorator.drawio">编辑原图（需登录）</a>

## 定义（what）

- 动态地给一个对象添加一些额外的职责。

## 缘由（why）

为什么需要装饰模式？

透明且动态地扩展类的功能。

## 实践（how）

```java
public abstract class Component {
    public abstract void operation();
}

public class ConcreteComponent extends Component {
    @Overrite
    public void operation() {
        // ConcreteComponent operation
    }
}

public abstract class Decorator extends Component{
    protected Component component;

    public Decorator(Component component) {
        this.component = component;
    }

    @Overrite
    public void operation() {
        component.operation();
    }
}

public class ConcreteDecoratorA extends Decorator {
    private Object addField;

    public ConcreteDecoratorA(Component component) {
        super(component);
    }

    public ConcreteDecoratorA(Component component, Object addField) {
        super(component);
        this.addField = addField;
    }

   @Overrite
    public void operation() {
        super.operation();
    }
}

public class ConcreteDecoratorB extends Decorator {
    public ConcreteDecoratorA(Component component) {
        super(component);
    }

   @Overrite
    public void operation() {
        super.operation();
        addMethond();
    }

    public void addMethond() {
        // ConcreteDecoratorB addMethond
    }
}

public class Client {
    public static void main(String[] args) {
        Component component = new ConcreteComponent();

        Decorator decoratorA = new Decorator(component, "addField");
        decoratorA.operation();

        Decorator decoratorB = new Decorator(component);
        decoratorB.operation();
        decoratorB.addMethond();
    }
}
```

### Android 中的例子

#### ContextWrapper
