# 代理模式（Proxy）

![代理模式](https://raw.githubusercontents.com/CodePoem/VDesignPatterns/master/docs/drawio/Proxy.png)

<a href = "https://www.draw.io/?lightbox=1#Uhttps://raw.githubusercontents.com/CodePoem/VDesignPatterns/master/docs/drawio/Proxy.png">全屏</a> |
<a href = "https://www.draw.io/#Uhttps://raw.githubusercontents.com/CodePoem/VDesignPatterns/master/docs/drawio/Proxy.png">作为模板编辑为新图</a> |
<a href = "https://www.draw.io/#HCodePoem/VDesignPatterns/master/docs/drawio/Proxy.drawio">编辑原图（需登录）</a>

## 定义（what）

- 为其他对象提供一种代理以控制对整个对象的访问。

## 缘由（why）

为什么需要代理模式？

当无法或者不想直接访问某个对象或访问某个对象存在困难时。

## 实践（how）

代理模式主要可以分为两大类，静态代理和动态代理。

- 静态代理

编译时代理，对性能几乎无影响。

- 动态代理

运行时（Runtime）代理，对性能有些影响。

动态代理实现方式：

1. 基于 JDK 实现动态代理
2. 基于 CGlib 实现动态代理模式
3. 基于 Aspectj 实现动态代理 (在程序编译的时候修改目标类的字节，织入代理的字节，不会生成全新的 Class)
4. 基于 instrumentation 实现动态代理（在类装载动态拦截去修改目标类的字节码，不会生成全新的 Class）

### 静态代理

```java
public abstract class Subject {
    public abstract void visit();
}

public class RealSubject extends Subject {
    @Overrite
    public void visit() {
        // RealSubject visit
    }
}

public class ProxySubject extends Subject {
    private RealSubject realSubject;

    @Overrite
    public void visit() {
        if (realSubject != null) {
            realSubject = new RealSubject();
        }
        realSubject.visit();
    }
}

public class Client {
    public static void main(String[] args) {
       ProxySubject proxySubject = new ProxySubject();
       proxySubject.visit();
    }
}
```

### 基于 Java 动态代理

```java
public interface Person {
    /**
     * visit
     */
    public abstract String visit(String visitString);
}
```

```java
public class RealPerson implements Person {

    @Override
    public String visit(String visitString) {
        System.out.println("RealPerson visit");
        return "Hello visitString";
    }
}
```

```java
public class PersonInvocationHandler<T> implements InvocationHandler {
    T target;

    public PersonInvocationHandler(T target) {
        this.target = target;
    }

    /**
     * 当一个代理实例的方法被调用时，代理方法将被编码并分发到 InvocationHandler接口的invoke方法执行
     *
     * @param proxy  代表动态生成的 动态代理 对象实例
     * @param method 代表被调用委托类的接口方法，和生成的代理类实例调用的接口方法是一致的，对应的 Method 实例
     * @param args   代表调用接口方法对应的 Object 参数数组，如果接口是无参，则为 null； 对于原始数据类型返回其包装类型
     * @return 返回调用结果
     * @throws Throwable 抛出异常
     */
    @Override
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        System.out.println("PersonInvocationHandler before, proxyClass =" + proxy.getClass() + " " +
                "methodName: " + method.getName() + " methodReturnType：" + method.getReturnType()
                + " methodArgs: " + (args == null ? "null" : Arrays.toString(args)));
        TimeMonitor.start();
        Object result = method.invoke(target, args);
        TimeMonitor.finish(method.getName());
        System.out.println("PersonInvocationHandler after, result = " + result);
        return result;
    }
}
```

```java
public class TimeMonitor {

    private static final ThreadLocal<Long> tl = new ThreadLocal<>();

    public static void start() {
        tl.set(System.currentTimeMillis());
    }

    /**
     * 结束时打印耗时
     *
     * @param methodName 方法名
     */
    public static void finish(String methodName) {
        long finishTime = System.currentTimeMillis();
        System.out.println(methodName + " method cost time: " + (finishTime - tl.get()) + "ms");
    }
}
```

```java
public class PersonInvocationHandlerTest {
    public static void main(String[] args) {
        try {
            saveGeneratedJdkProxyFiles();
        } catch (Exception e) {
            e.printStackTrace();
        }

        // 第一种方案：
        // 1. 创建一个与代理对象相关联的 InvocationHandler，以及真实的委托类实例
        // 2. Proxy 类 getProxyClass 静态方法生成一个动态代理类 proxyClass，该类继承 Proxy 类，实现 Person.java接口；
        // JDK 动态代理的特点是代理类必须继承 Proxy 类
        // 3. 通过代理类 proxyClass 获得其 InvocationHandler 接口的构造函数 ProxyConstructor
        // 4. 通过 构造函数实例 ProxyConstructor 实例化一个代理对象，并将  InvocationHandler 接口实例传递给代理类
        Person personNew = new RealPerson();
        InvocationHandler handlerNew = new PersonInvocationHandler<>(personNew);
        Class<?> proxyClass = Proxy.getProxyClass(Person.class.getClassLoader(),
                new Class<?>[]{Person.class});
        System.out.println("package = " + proxyClass.getPackage() +
                " SimpleName = " + proxyClass.getSimpleName() +
                " name =" + proxyClass.getName() +
                " CanonicalName = " + "" + proxyClass.getCanonicalName() +
                " Interfaces = " + Arrays.toString(proxyClass.getInterfaces()) +
                " superClass = " + proxyClass.getSuperclass() +
                " methods =" + Arrays.toString(proxyClass.getMethods()));
        try {
            Constructor<?> proxyConstructor = proxyClass.getConstructor(InvocationHandler.class);
            Person proxyPerson = (Person) proxyConstructor.newInstance(handlerNew);
            System.out.println("proxyPerson isProxy " + Proxy.isProxyClass(proxyPerson.getClass()));
            InvocationHandler handlerObject = Proxy.getInvocationHandler(proxyPerson);
            System.out.println(handlerObject.getClass().getName());
            proxyPerson.visit("Girl");
        } catch (NoSuchMethodException | IllegalAccessException | InstantiationException | InvocationTargetException e) {
            e.printStackTrace();
        }

        // 第二种方案：通过 Proxy.newProxyInstance 方法 获取代理对象
        Person person = new RealPerson();
        InvocationHandler handler = new PersonInvocationHandler<>(person);
        Person personProxy = (Person) Proxy.newProxyInstance(Person.class.getClassLoader(),
                new Class<?>[]{Person.class}, handler);
        System.out.println("package = " + personProxy.getClass().getPackage() +
                " SimpleName = " + personProxy.getClass().getSimpleName() +
                " name =" + personProxy.getClass().getName() +
                " CanonicalName = " + "" + personProxy.getClass().getCanonicalName() +
                " Interfaces = " + Arrays.toString(personProxy.getClass().getInterfaces()) +
                " superClass = " + personProxy.getClass().getSuperclass() +
                " methods =" + Arrays.toString(personProxy.getClass().getMethods()));
        // 通过 代理类 执行 委托类
        personProxy.visit("Boy");
    }

    /**
     * 设置保存 Java 动态代理生成的类文件
     * 会在项目根目录下 com.sun.proxy
     *
     * @throws Exception
     */
    public static void saveGeneratedJdkProxyFiles() throws Exception {
        Field field = System.class.getDeclaredField("props");
        field.setAccessible(true);
        Properties props = (Properties) field.get(null);
        props.put("sun.misc.ProxyGenerator.saveGeneratedFiles", "true");
    }
}
```

基于 JDK 动态代理创建对象过程可分为以下四个步骤：

1. 通过实现 InvocationHandler 接口创建自己的调用处理器。
2. 通过为 Proxy 类 指定 ClassLoade r 对象和一组 interface 代理类需要实现的接口，创建动态代理类类文件。
3. 通过新建的代理 clazz 的反射机制获取动态代理类的一个构造函数。
4. 通过构造函数实例创建代理类实例，将调用处理器对象作为参数被传入。

注：Java 为了简化动态对象创建过程，Proxy 类中的 newInstance 工具方法封装了步骤 2~4，只需两步即可完成代理对象的创建。

其他：

- 会默认代理 Object 中 equals、toString、hashCode
- 不足：Java 动态代理只能对接口产生代理，不能对类产生代理。由于 Java 动态代理原理是继承 Proxy 来实现，Java 没有多继承机制，因此不能对类产生代理。

### 基于 CGlib 技术动态代理

原理：

- 对接口进行代理的情况，最后生成的源码是实现了该接口和 Factory 接口
- 对类进行代理的情况，最后生成的源码是继承了类并实现了 Factory 接口

```java
public interface Flower {
    String grow();
}
```

```java
public class SunFlower implements Flower{
    @Override
    public String grow() {
        System.out.println("SunFlower grow");
        return "return SunFlower grow";
    }
}
```

```java
class MoonFlower {
    public String withered() {
        System.out.println("MoonFlower withered");
        return "return MoonFlower withered";
    }
}
```

```java
public class FlowerMethodInterceptor implements MethodInterceptor {

    Class targetClass;

    private FlowerMethodInterceptor() {
        super();
    }

    public FlowerMethodInterceptor(Class targetClass) {
        this();
        this.targetClass = targetClass;
    }

    public Object getProxyClass() {
        // 创建cglib 代理类
        // 创建加强器，用来创建动态代理类
        Enhancer enhancer = new Enhancer();
        // 为代理类指定需要代理的类
        enhancer.setSuperclass(targetClass);
        // 获取动态代理类对象并返回
        enhancer.setCallback(this);
        return enhancer.create();
    }

    /**
     * 功能主要是在调用业务类方法之前 之后添加统计时间的方法逻辑.
     * intercept 因为  具有 MethodProxy proxy 参数的原因 不再需要代理类的引用对象了,直接通过 proxy 对象访问被代理对象的方法(这种方式更快)。
     * 当然 也可以通过反射机制，通过 method 引用实例    Object result = method.invoke(target, args); 形式反射调用被代理类方法，
     * target 实例代表被代理类对象引用, 初始化 MethodInterceptor 时候被赋值 。但是 CGlib 不推荐使用这种方式
     *
     * @param obj    代表 CGlib 生成的动态代理类 对象本身
     * @param method 代理类中被拦截的接口方法 Method 实例
     * @param args   接口方法参数
     * @param proxy  用于调用父类真正的业务类方法。可以直接调用被代理类接口方法
     * @return 返回调用结果
     * @throws Throwable 异常
     */
    @Override
    public Object intercept(Object obj, Method method, Object[] args, MethodProxy proxy) throws Throwable {
        System.out.println("before");
        TimeMonitor.start();
        Object result = null;
        System.out.println("proxy Class = " + proxy.getClass()
                + "，proxy SuperName = " + proxy.getSuperName()
                + "，proxy Signature = " + proxy.getSignature()
                + "，proxy SuperIndex = " + proxy.getSuperIndex());
        // 如果是代理接口不能调用
        if (!targetClass.isInterface()) {
            result = proxy.invokeSuper(obj, args);
        }
        System.out.println("after");
        TimeMonitor.finish(method.getName());
        return result;
    }
}
```

```java
public class FlowerMethodInterceptTest {
    public static void main(String[] args) {
        try {
            saveGeneratedJdkProxyFiles("cglib-proxy");
        } catch (Exception e) {
            e.printStackTrace();
        }

        // 代理接口
        FlowerMethodInterceptor flowerMethodInterceptor =
                new FlowerMethodInterceptor(Flower.class);
        Flower proxyFlower = (Flower) flowerMethodInterceptor.getProxyClass();
        System.out.println(proxyFlower.grow());

        // 代理类
        FlowerMethodInterceptor moonFlowerMethodInterceptor =
                new FlowerMethodInterceptor(MoonFlower.class);
        MoonFlower proxyMoonFlower = (MoonFlower) moonFlowerMethodInterceptor.getProxyClass();
        System.out.println(proxyMoonFlower.withered());
    }

    /**
     * 设置保存 Cglib 动态代理生成的类文件
     * 会在指定目录下生成
     *
     * @throws Exception 异常
     */
    public static void saveGeneratedJdkProxyFiles(String dir) throws Exception {
        Field field = System.class.getDeclaredField("props");
        field.setAccessible(true);
        Properties props = (Properties) field.get(null);
        System.setProperty(DebuggingClassWriter.DEBUG_LOCATION_PROPERTY, dir);
        props.put("net.sf.cglib.core.DebuggingClassWriter.traceEnabled", "true");
    }
}
```

其他：

- 会默认代理 Object 中 equals、toString、hashCode、clone
- 不足：不能对 final 修饰的类进行代理。由于 CGlib 针对类的代理采用的是继承其方式实现，而 final 修饰的类不可继承。同样的 static 方法、private 方法也不能被代理。
- 做了方法访问优化，使用建立方法索引的方式避免了传统 JDK 动态代理需要通过 Method 方法反射调用。

### Android 中的例子

#### 埋点/AOP

静态代理：

- JavaCode -> .java (IDE Processor) : APT / AST
- .java -> .class (Java Compiler) : AspectJ
- .class -> .dex (GradlePlugin) : ASM / Javassist

动态代理：

#### Binder 机制
