# 单例模式（Singleton）

![单例模式](https://raw.githubusercontent.com/CodePoem/VDesignPatterns/master/docs/drawio/Singleton.png)

<a href = "https://www.draw.io/?lightbox=1#Uhttps://raw.githubusercontent.com/CodePoem/VDesignPatterns/master/docs/drawio/Singleton.png">全屏</a> |
<a href = "https://www.draw.io/#Uhttps://raw.githubusercontent.com/CodePoem/VDesignPatterns/master/docs/drawio/Singleton.png">作为模板编辑为新图</a> |
<a href = "https://www.draw.io/#HCodePoem/VDesignPatterns/master/docs/drawio/Singleton.drawio">编辑原图（需登录）</a>

## 定义（what）

- 确保某一个类只有一个实例，并提供一个访问它的全局访问点。

## 缘由（why）

为什么需要单例模式？

实现对唯一实例的受控访问。某种类型的对象应该只需要一个，创建过多的该类型的对象就是浪费资源。

## 实践（how）

在使用单例模式时特别需要注意是否是在多线程的使用场景下，多线程场景下需要考虑线程安全。

### 七种单例写法

#### 1.静态变量（懒汉，线程不安全）

```java
public class Singleton {
    private static Singleton instance;

    private Singleton() {
    }`

    public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}
```

```kotlin
class Singleton private constructor(private val param: String) {

    companion object {

       private var instance: Singleton? = null

        fun getInstance(param: String) =
                instance ?: Singleton(param).also { instance = it }
    }
}
```

- 满足单线程场景下的单例需求且采用了懒加载。
- 多线程场景下不能正确保证单例。

#### 2.静态变量+同步 （懒汉，线程安全）

```java
public class Singleton {
    private static Singleton instance;

    private Singleton() {
    }

    public static synchronized Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}
```

```kotlin
class Singleton private constructor(private val param: String) {

    companion object {

        private var instance: Singleton? = null

        @Synchronized
        fun getInstance(param: String) =
            instance ?: Singleton(param).also { instance = it }
    }
}
```

- 基于静态变量的单例在获取单例的方法上加上了同步关键字 synchronized，能确保多线程场景下的单例。
- 效率较低，存在不必要的同步（instance 已创建的情况下不需要同步）。

#### 3. DCL(double checked locking)双重校验锁（懒汉，线程安全）

```java
public class Singleton {
    private volatile static Singleton instance;

    private Singleton() {
    }

    public static Singleton getInstance() {
        if (instance == null) {
            // 类锁
            synchronized (Singleton.class) {
                if (instance == null) {
                    instance = new Singleton();
                }
            }
        }
        return instance;
    }
}
```

```kotlin
class Singleton private constructor(private val param: String) {

    companion object {

        @Volatile private var instance: Singleton? = null

        fun getInstance(param: String) =
                instance ?: synchronized(this) {
                    instance ?: Singleton(param).also { instance = it }
                }
    }
}
```

- 基于静态变量+同步，增加一层 instance 的 null 判断，避免不必要的同步（ instance 已创建的情况下不需要同步）。
- 对静态变量 instance 加 volatile 关键字，保证可见性和禁止指令重排序（通过内存屏障实现），但不能保证原子性。

第二个 null 判断是为了避免多个线程通过第一个 null 判断，而造成多次实例化。

instance = new Singleton()语句看起来是一句代码，实际上并不是一个原子操作，它会被编译成多条汇编指令。大致做了三件事：

1. 给 Singleton 实例分配内存。
2. 调用 Singleton 的构造函数，初始化成员变量。
3. 将 instance 对象指向分配的内存空间。

由于指令重排序优化（在保证单线程执行结果正确的情况下优化指令执行执行速度），上述（2）（3）的执行顺序是不能够保证的。

volatile 通过禁止指令重排序的方式，避免多个线程在第一个 null 判断时判断已实例化（实际因为指令重排序 instance 尚未指向分配的内存空间）。

#### 4.静态变量初始化（饿汉，线程安全）

```java
public class Singleton {
    private static Singleton instance = new Singleton();

    private Singleton() {

    }
    public static Singleton getInstance() {
        return instance;
    }
}
```

- Singleton 中的静态变量 instance 基于 classloder 机制避免了多线程的同步问题。

- 没有懒加载效果，instance 在 Singleton 装载的时候就实例化。

#### 5.静态代码块初始化（饿汉，线程安全）

```java
public class Singleton {
    private static Singleton instance  = null;

    static {
        instance = new Singleton();
    }

    private Singleton() {

    }
    public static Singleton getInstance() {
        return instance;
    }
}
```

- 同静态变量初始化的单例实现方式差不多。

### 6.静态内部类（懒汉，线程安全）

```java
public class Singleton {
    private Singleton(){}

    private static class SingletonHolder {
        private static final Singleton INSTANCE = new Singleton();
    }

    public static Singleton getInstance() {
        return SingletonHolder.INSTANCE;
    }
}
```

- 静态内部类中的静态变量 INSTANCE 基于 classloder 机制避免了多线程的同步问题。

ClassLoader 的 loadClass 方法在加载类的时候使用了 synchronized 关键字。也正是因为这样， 除非被重写，这个方法默认在整个装载过程中都是同步的，也就是保证了线程安全。

所以，以上各种方法，虽然并没有显示的使用 synchronized，但是还是其底层实现原理还是用到了 synchronized。

- 懒加载，Singleton 装载的时候 INSTANCE 不一定被初始化，只有显示调用 getInstance() SingletonHolder 才会被装载从而 INSTANCE 才会初始化。

#### 7.枚举

```java
public enum Singleton {
    INSTANCE;

    public void whateverMethod() {
    }
}
```

```kotlin
enum class Singleton(val param: String) {
    INSTANCE("instance");

    fun whateverMethod() {}
}
```

- 避免多线程同步问题
- 防止反序列化重新创建新的对象
- 避免反射调用

### 防御攻击

由于类的创建不止通过 new 关键字一种方式，还有克隆、序列化、反射等方式。

#### 防御克隆攻击

```java
public class Singleton implements Cloneable{
    ···
    @Override
    protected Object clone() throws CloneNotSupportedException {
        return getInstance();
    }
}
```

#### 防御序列化攻击

```java
public class Singleton {
    ···
    private Object readResolve() {
        return getInstance();
    }
}
```

#### 防御反射攻击

枚举法实现单例模式。

### 无锁单例

使用 CAS

```java
public class Singleton {
    private static final AtomicReference<Singleton> INSTANCE = new AtomicReference<Singleton>();

    private Singleton() {}

    public static Singleton getInstance() {
        for (;;) {
            Singleton singleton = INSTANCE.get();
            if (null != singleton) {
                return singleton;
            }

            singleton = new Singleton();
            if (INSTANCE.compareAndSet(null, singleton)) {
                return singleton;
            }
        }
    }
}
```

- 不需要使用传统的锁机制来保证线程安全,CAS 是一种基于忙等待的算法,依赖底层硬件的实现,相对于锁它没有线程切换和阻塞的额外消耗,可以支持较大的并行度。

- 忙等待可能一直执行不成功(一直在死循环中),会对 CPU 造成较大的执行开销。

- N 个线程同时执行到 singleton = new Singleton();的时候，会有大量对象创建，很可能导致内存溢出。
