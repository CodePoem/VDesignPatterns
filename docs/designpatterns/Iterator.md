# 迭代器模式（Iterator）

![迭代器模式](https://raw.githubusercontent.com/CodePoem/VDesignPatterns/master/docs/drawio/Iterator.png)

<a href = "https://www.draw.io/?lightbox=1#Uhttps://raw.githubusercontent.com/CodePoem/VDesignPatterns/master/docs/drawio/Iterator.png">全屏</a> |
<a href = "https://www.draw.io/#Uhttps://raw.githubusercontent.com/CodePoem/VDesignPatterns/master/docs/drawio/Iterator.png">作为模板编辑为新图</a> |
<a href = "https://www.draw.io/#HCodePoem/VDesignPatterns/master/docs/drawio/Iterator.drawio">编辑原图（需登录）</a>

## 定义（what）

- 提供一种方法顺序访问一个聚合对象中的各个元素，而又不暴露该对象的内部表示。

## 缘由（why）

为什么需要迭代器模式？

为遍历不同的聚集结构提供访问的统一的接口。

## 实践（how）

```java
public Interface Iterator<T> {
    boolean hasNext();
    T next();
}

public class ConcreteIterator<T> implements Iterator<T> {
    private List<T> list = new ArrayList();
    private int cursor = 0;

    public ConcreteIterator(List<T> list) {
        thi.list = list;
    }

    @Overrite
    public boolean hasNext() {
        return cursor != list.size();
    }

    @Overrite
    public T next() {
        T object = null;
        if (hasNext()) {
            object = list.get(cursor++);
        }
        return object;
    }
}

public Interface Aggregate<T> {
    void add(T object);
    void remove(T object);
    Iterator<T> iterator();
}

public class ConcreteAggregate<T> implements Aggregate<T> {
    private List<T> list = new ArrayList();

    @Overrite
    public void add(T object) {
        list.add(object);
    }
    @Overrite
    public void remove(T object) {
        list.remove(object);
    }
    @Overrite
    public Iterator<T> iterator() {
        return new ConcreteIterator<T>(list);
    }
}

public class Client {
    public static void main(String[] args) {
        Aggregate<String> aggregate = new ConcreteAggregate<>();
        aggregate.add("A");
        aggregate.add("B");
        aggregate.add("C");
        aggregate.add("D");
        Iterator<String> iterator = aggregate.iterator();
        while (iterator.hasNext()) {
            String next = iterator.next();
        }
    }
}
```

### Android中的例子

用于 ContentProvider 查询的游标对象 Cursor 本质就是一个具体的迭代器。
