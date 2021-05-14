# 访问者模式（Visitor）

![访问者模式](https://raw.githubusercontents.com/CodePoem/VDesignPatterns/master/docs/drawio/Visitor.png)

<a href = "https://www.draw.io/?lightbox=1#Uhttps://raw.githubusercontents.com/CodePoem/VDesignPatterns/master/docs/drawio/Visitor.png">全屏</a> |
<a href = "https://www.draw.io/#Uhttps://raw.githubusercontents.com/CodePoem/VDesignPatterns/master/docs/drawio/Visitor.png">作为模板编辑为新图</a> |
<a href = "https://www.draw.io/#HCodePoem/VDesignPatterns/master/docs/drawio/Visitor.drawio">编辑原图（需登录）</a>

## 定义（what）

最复杂的设计模式，大多数情况下不会使用；但你一旦需要使用它，就真正需要它。

- 表示一个作用于某对象结构中的各元素的操作。在不改变元素的类的前提下定义作用于这些元素的新操作。

## 缘由（why）

为什么需要访问者模式？

将数据结构和作用于结构上的操作解耦，使得操作集合可以相对自由地演化。当数据结构比较稳定，但经常需要在此数据结构上定义新的操作，希望添加这些新操作时不去修改这些数据结构的类。

## 实践（how）

```java
public abstract class Element {
    public abstract void accept(Visitor visitor);
}

public class ConcreteElementA extends Element {
    @Overrite
    public void accept(Visitor visitor) {
        visitor.visitorElementA(this);
    }

    public void operatorA() {
        // operatorA
    }
}

public class ConcreteElementB extends Element {
    @Overrite
    public void accept(Visitor visitor) {
        visitor.visitorElementB(this);
    }

    public void operatorB() {
        // operatorA
    }
}

public abstract class Visitor {
    public abstract void visitorElementA(ConcreteElementA concreteElementA);
    public abstract void visitorElementA(ConcreteElementB concreteElementB);
}

public class ConcreteVisitorA extends Visitor {
    @Overrite
    public void visitorElementA(ConcreteElementA concreteElementA) {
        // visitorElementA
    }

    @Overrite
    public void visitorElementB(ConcreteElementB concreteElementB) {
        // visitorElementB
    }
}

public class ConcreteVisitorB extends Visitor {
    @Overrite
    public void visitorElementA(ConcreteElementA concreteElementA) {
        // visitorElementA
    }

    @Overrite
    public void visitorElementB(ConcreteElementB concreteElementB) {
        // visitorElementB
    }
}

public class ObjectStructure {
    private List<Element> elements = new ArrayList<Element>();

    public void attach(Element element) {
        elements.add(element);
    }

    public void detach(Element element) {
        elements.remove(element);
    }

    public void accept(Visitor visitor) {
        for (Element element : elements) {
            element.accept();
        }
    }
}

public class Client {
    public static void main(String[] args) {
       ObjectStructure objectStructure = new ObjectStructure();
       // attach element
       objectStructure.attach(new ConcreteElementA());
       objectStructure.attach(new ConcreteElementB());
       // visitor accept
       objectStructure.accept(new ConcreteVisitorA());
       objectStructure.accept(new ConcreteVisitorB());
    }
}
```

### Android 中的例子

#### APT（Annotation Processing Tools）编译时注解

核心类：

- AbstractProcessor：注解处理器
- AnnotationProcessorFactory：为某些注解类型创建注解处理器的工厂

编辑器会检查 AbstractProcessor 的子类，并将所有添加了对应注解的元素传递到 process()方法参数中进行调用。

对于编译器来说，代码中的元素结构基本是不变的。

- PackageElement：包元素
- TypeElement：类型元素，例如字段属于某种类型
- ExcutableElement：可执行元素，代表函数类型元素
- VariableElement；变量元素
- TypeParameterElement：类型参数元素
