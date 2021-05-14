# 组合模式（Composite）

![组合模式](https://raw.githubusercontents.com/CodePoem/VDesignPatterns/master/docs/drawio/Composite.png)

<a href = "https://www.draw.io/?lightbox=1#Uhttps://raw.githubusercontents.com/CodePoem/VDesignPatterns/master/docs/drawio/Composite.png">全屏</a> |
<a href = "https://www.draw.io/#Uhttps://raw.githubusercontents.com/CodePoem/VDesignPatterns/master/docs/drawio/Composite.png">作为模板编辑为新图</a> |
<a href = "https://www.draw.io/#HCodePoem/VDesignPatterns/master/docs/drawio/Composite.drawio">编辑原图（需登录）</a>

## 定义（what）

- 将对象组合成树形结构以表示“部分-整体”的层次结构。

## 缘由（why）

为什么需要组合模式？

确保用户对单个对象和组合对象的使用具有一致性。

## 实践（how）

```java
public abstract class Component {
    public abstract void method();
}

public class Leaf extends Component {
    @Overrite
    public void method() {
        // Leaf do something
    }
}

public class Composite extends Component {
    private List<Component> components = new ArrayList<>();

    @Overrite
    public void method() {
        if (components != null) {
            for (Component tempComponent : components) {
                tempComponent.method();
            }
        }
    }

    public void add(Component component) {
        components.add(component);
    }

    public void reomve(Component component) {
        components.reomve(component);
    }
}

public class Client {
    public static void main(String[] args) {
        Composite root = new Composite();
        Composite branch1 = new Composite();
        Composite branch2 = new Composite();
        Leaf leaf1 = new Leaf();
        Leaf leaf2 = new Leaf();
        branch1.add(leaf1);
        branch2.add(leaf2);
        root.add(branch1);
        root.add(branch2);
        root.method();
    }
}
```

### Android 中的例子

#### View 和 ViewGroup
