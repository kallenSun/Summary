#### 1、HashMap和HashTable的区别
- 1、线程安全两者最主要的区别在于Hashtable是线程安全，而HashMap则非线程安全。Hashtable的实现方法里面都添加了synchronized关键字来确保线程同步，因此相对而言HashMap性能会高一些，我们平时使用时若无特殊需求建议使用HashMap，在多线程环境下若使用HashMap需要使用Collections.synchronizedMap()方法来获取一个线程安全的集合。Note：Collections.synchronizedMap()实现原理是Collections定义了一个SynchronizedMap的内部类，这个类实现了Map接口，在调用方法时使用synchronized来保证线程同步,当然了实际上操作的还是我们传入的HashMap实例，简单的说就是Collections.synchronizedMap()方法帮我们在操作HashMap时自动添加了synchronized来实现线程同步，类似的其它Collections.synchronizedXX方法也是类似原理。
- 2、针对null的不同HashMap可以使用null作为key，而Hashtable则不允许null作为key虽说HashMap支持null值作为key，不过建议还是尽量避免这样使用，因为一旦不小心使用了，若因此引发一些问题，排查起来很是费事。Note：HashMap以null作为key时，总是存储在table数组的第一个节点上。
- 3、继承结构HashMap是对Map接口的实现，HashTable实现了Map接口和Dictionary抽象类。
- 4、初始容量与扩容HashMap的初始容量为16，Hashtable初始容量为11，两者的填充因子默认都是0.75。HashMap扩容时是当前容量翻倍即:capacity*2，Hashtable扩容时是容量翻倍+1即:capacity*2+1。
- 5、两者计算hash的方法不同Hashtable计算hash是直接使用key的hashcode对table数组的长度直接进行取模int hash = key.hashCode();
int index = (hash & 0x7FFFFFFF) % tab.length;HashMap计算hash对key的hashcode进行了二次hash，以获得更好的散列值，然后对table数组长度取摸。

#### 获取Class类的三种方式
- 使用Class.forName()静态方法
- 使用类的class属性
- 使用实例对象的getClass()方法
### SSM
#### 1、Spring
#### 1.1 请问声明是IOC和DI？并简要说明一下DI是如何实现的
IOC叫控制反转，DI叫依赖注入。控制反转是把传统上由程序代码直接操控的对象的调用权交给容器，通过容器来实现对象组件的装配和管理。"控制反转"就是对组件对象控制权的转移，从程序代码本身转移到了外部容器，由容器来创建对象并管理对象之间的依赖关系。依赖注入的基本原则是应用组件不应该负责查找资源或者其他依赖的协作对象。配置对象的工作应该由容器负责，查找资源的逻辑应该从应用组件的代码中抽取出来，交给容器来完成。DI是对IoC更准确的描述，即组件之间的依赖关系由容器在运行期决定，即由容器动态的将某种依赖关系注入到组件之中。
依赖注入可以通过setter方法注入（设值注入）、构造器注入和接口注入三种方式来实现，Spring支持setter注入和构造器注入，通常使用构造器注入来注入必须的依赖关系，对于可选的依赖关系，则setter注入是更好的选择，setter注入需要类提供无参构造器或者无参的静态工厂方法来创建对象。
- 依赖注入是从应用程序的角度在描述：应用程序依赖容器创建并注入它所需要的外部资源；
- 控制反转是从容器的角度在描述：容器控制应用程序，由容器反向的向应用程序注入应用程序所需要的外部资源。
#### 1.2 请问AOP的原理是什么？
AOP指面向切面编程，用于处理系统中分布于各个模块的横切关注点，比如事务管理、日志、缓存等等。AOP实现的关键在于AOP框架自动创建的AOP代理，AOP代理主要分为静态代理和动态代理，静态代理的代表为AspectJ；而动态代理则以Spring AOP为代表。通常使用AspectJ的编译时增强实现AOP，AspectJ是静态代理的增强，所谓的静态代理就是AOP框架会在编译阶段生成AOP代理类，因此也称为编译时增强。
Spring AOP中的动态代理主要有两种方式，JDK动态代理和CGLIB动态代理。
- JDK动态代理通过反射来接收被代理的类，并且要求被代理的类必须实现一个接口。核心是InvocationHandler接口和Proxy类。如果目标类没有实现接口，那么Spring AOP会选择使用CGLIB来动态代理目标类。
- CGLIB（Code Generation Library），是一个代码生成的类库，可以在运行时动态的生成某个类的子类



