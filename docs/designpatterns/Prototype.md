# 原型模式（Prototype）

![原型模式](https://raw.githubusercontent.com/CodePoem/VDesignPatterns/master/docs/drawio/Prototype.png)

<a href = "https://www.draw.io/?lightbox=1#Uhttps://raw.githubusercontent.com/CodePoem/VDesignPatterns/master/docs/drawio/Prototype.png">全屏</a> |
<a href = "https://www.draw.io/#Uhttps://raw.githubusercontent.com/CodePoem/VDesignPatterns/master/docs/drawio/Prototype.png">作为模板编辑为新图</a> |
<a href = "https://www.draw.io/#HCodePoem/VDesignPatterns/master/docs/drawio/Prototype.drawio">编辑原图（需登录）</a>

## 定义（what）

- 用原型实例指定创建对象的种类，并通过复制这些原型创建新的对象。

## 缘由（why）

为什么需要原型模式？

- 避免那些初始化需要消耗较多资源的类的资源消耗。
- 保护性拷贝。在需要原型实例，但又不希望被其他调用者修改的时候，就需要拷贝一份给其他调用者。

## 实践（how）

使用原型模式比较多的场景就是克隆，实现Cloneable接口。

克隆需要特别注意区分浅拷贝（只会克隆基本类型，其他类型只是拷贝了引用）和深拷贝，尽量使用深拷贝。

### 浅拷贝

```java
public class Prototype implements Cloneable {
    private String fieldString;
    private ArrayList<String> fieldArratString;

    @Overrive
    protected Prototype clone() {
        try {
            Prototype clonePrototype = (Prototype) super.clone();
            clonePrototype.filedString = this.filedString;
            clonePrototype.fieldArratString = this.fieldArratString;
            return clonePrototype;
        } catch(Exception e){

        }
        return null;
    }
}
```

其中fieldArratString只是拷贝了引用。

### 深拷贝

```java
public class Prototype implements Cloneable {
    private String fieldString;
    private ArrayList<String> fieldArratString;

    @Overrive
    protected Prototype clone() {
        try {
            Prototype clonePrototype = (Prototype) super.clone();
            clonePrototype.filedString = this.filedString;
            // 对fieldArratString深拷贝
            clonePrototype.fieldArratString = (ArrayList<String>) this.fieldArratString.clone();
            return clonePrototype;
        } catch(Exception e){

        }
        return null;
    }
}
