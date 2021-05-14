# 备忘录模式（Memento）

![备忘录模式](https://raw.githubusercontents.com/CodePoem/VDesignPatterns/master/docs/drawio/Memento.png)

<a href = "https://www.draw.io/?lightbox=1#Uhttps://raw.githubusercontents.com/CodePoem/VDesignPatterns/master/docs/drawio/Memento.png">全屏</a> |
<a href = "https://www.draw.io/#Uhttps://raw.githubusercontents.com/CodePoem/VDesignPatterns/master/docs/drawio/Memento.png">作为模板编辑为新图</a> |
<a href = "https://www.draw.io/#HCodePoem/VDesignPatterns/master/docs/drawio/Memento.drawio">编辑原图（需登录）</a>

## 定义（what）

- 在不破坏封装性的前提下，捕获一个对象的内部状态，并在改对象之外保存这个状态。这样以后就可将对象恢复到原先保存的状态。

## 缘由（why）

为什么需要备忘录模式？

需要保存一个对象在某一时刻的部分状态，同时又不希望是通过暴露接口等破坏封装性的方式，而是通过中间对象来访问其部分状态。

## 实践（how）

```java
public class Memoto {
    private Object state;

    Memoto(){
    }

    Memoto(Object state){
        this.state = state;
    }

    public Object getState(){
        return state;
    }

    public void setState(Object state){
        this.state = state;
    }
}
public class Originator {
    private Object state;

    public Object getState(){
        return state;
    }

    public void setState(Object state){
        this.state = state;
    }

    public void setMemoto(Memoto memoto){
        this.state = memoto.state;
    }

    public Memoto createMemoto(){
        return new Memoto(state);
    }
}

public class Caretaker {
    private Memoto memoto;

    public Memoto getMemoto(){
        return memoto;
    }

    public void setMemoto(Memoto memoto){
        this.memoto = memoto;
    }
}

public class Client {
    public static void main(String[] args) {
        // 原始状态
        Originator originator = new Originator();
        originator.setState("stateA");
        // 备忘
        Caretaker caretaker = new Caretaker();
        caretaker.setMemoto(originator.createMemoto());
        // 改变状态
        originator.setState("stateB");
        // 恢复状态
        originator.setMemoto(caretaker.getMemoto());
    }
}
```

### Android 中的例子

Activity 的 onSaveInstanceState 机制。
