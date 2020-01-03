# 观察者模式（Observer）

![观察者模式](https://raw.githubusercontent.com/CodePoem/VDesignPatterns/master/docs/drawio/Observer.png)

<a href = "https://www.draw.io/?lightbox=1#Uhttps://raw.githubusercontent.com/CodePoem/VDesignPatterns/master/docs/drawio/Observer.png">全屏</a> |
<a href = "https://www.draw.io/#Uhttps://raw.githubusercontent.com/CodePoem/VDesignPatterns/master/docs/drawio/Observer.png">作为模板编辑为新图</a> |
<a href = "https://www.draw.io/#HCodePoem/VDesignPatterns/master/docs/drawio/Observer.drawio">编辑原图（需登录）</a>

## 定义（what）

- 定义对象间一种一对多的依赖关系，使得每当一个对象改变状态，则所有依赖于它的对象都会得到通知并被自动更新。

## 缘由（why）

为什么需要观察者模式？

将观察者与被观察者解耦。可以实现一对多的订阅关系。

## 实践（how）

```java
public interface Observer {
   void update(Object object);
}

public class ConcreteObserver implements  Observer{
    @Overrite
    public void update(Object object){
        // Do something
    }
}

public abstract class Subject {
    private List<Observer> observers = new ArrayList();

    public void attach(Observer observer) {
        observers.add(observer);
    }

    public void detach(Observer observer) {
        observers.remove(observer);
    }

    public void notify(Object object) {
        for(observer in observers) {
            observer.update(object);
        }
    }
}

public class ConcreteSubject extends Subject {
    @Overrite
    public void notify(Object object) {
        for(observer in observers) {
            boolean matched = false;
            // jude matched
            if(matched) {
                observer.update(object);
            }
        }
    }
}

public class Client {
    public static void main(String[] args) {
        Subject subject = new ConcreteSubject();
        Observer observer1 = new ConcreteObserver();
        Observer observer2 = new ConcreteObserver();
        subject.attach(observer1);
        subject.attach(observer2)
        subject.notify("update");
    }
}
```
