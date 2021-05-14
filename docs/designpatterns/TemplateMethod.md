# 模板方法模式（TemplateMethod）

![模板方法模式](https://raw.githubusercontents.com/CodePoem/VDesignPatterns/master/docs/drawio/TemplateMethod.png)

<a href = "https://www.draw.io/?lightbox=1#Uhttps://raw.githubusercontents.com/CodePoem/VDesignPatterns/master/docs/drawio/TemplateMethod.png">全屏</a> |
<a href = "https://www.draw.io/#Uhttps://raw.githubusercontents.com/CodePoem/VDesignPatterns/master/docs/drawio/TemplateMethod.png">作为模板编辑为新图</a> |
<a href = "https://www.draw.io/#HCodePoem/VDesignPatterns/master/docs/drawio/TemplateMethod.drawio">编辑原图（需登录）</a>

## 定义（what）

- 定义一个操作中的算法的骨架，而将一些步骤延迟到子类中。

## 缘由（why）

为什么需要模板方法模式？

模板方法使得子类可以不改变一个算法的结构即可重定义该算法的某些特定步骤。

## 实践（how）

```java
public abstract class AbstractTemplate {
    public void templateMethod() {
        stepOne();
        stepTwo();
    }
    public abstract void stepOne();
    public abstract void stepTwo();
}

public class ConcreteImpleA extends AbstractTemplate {
    @Overrite
    public void stepOne() {
        // stepOne
    }
    @Overrite
    public void stepTwo() {
        // stepTwo
    }
}


public class ConcreteImpleB extends AbstractTemplate {
    @Overrite
    public void stepOne() {
        // stepOne
    }
    @Overrite
    public void stepTwo() {
        // stepTwo
    }
}

public class Client {
    public static void main(String[] args) {
        // ConcreteImpleA
        AbstractTemplate abstractTemplateA = new ConcreteImpleA();
        abstractTemplate.templateMethod();
        // ConcreteImpleB
        AbstractTemplate abstractTemplateB = new ConcreteImpleA();
        abstractTemplateB.templateMethod();
    }
}
```

### Android 中的例子

#### AsyncTask

excute() -> onPreExecute() -> doInBackground() -> onPostExcute()

#### Activity 生命周期

onCreate() -> onStart() -> onResume() -> onPause() -> onStop() -> onDestroy()
