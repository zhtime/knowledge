# JAVA知识总结

## 面向对象和面向过程的区别

面向过程：

优点：

直观上来说面向对象生成对象实例过程消耗的资源较大。

从根本上来说面向过程语言大多数是直接编译成机械码在计算机中运行，而面向对象语言(Java)是半编译语言，通过编译器将源文件编译成JVM可识别的字节码文件，通过解释器将字节码文件解释成计算机可以识别的机械码文件。

缺点：相比面向对象语言，它不利于维护、复用以及扩展。



面向对象：

优先：面向对象语言能够实现代码易维护、易复用以及易扩展的特点，具有封装、继承、多态等特性，设计出低耦合系统、是系统更加灵活。

缺点：相比于面向过程语言，面向对象语言的性能较低.	



- [ ] 补充

[ [图解高内聚与低耦合 - 大道方圆 - 博客园 (cnblogs.com)](https://www.cnblogs.com/xdecode/p/9393885.html) ]()

高内聚和低耦合 ------->基于模块

模块： 从逻辑上将系统分解为更细微的部分, 分而治之, 复杂问题拆解为若干简单问题, 逐个解决 

耦合:主要是模块与模块之间的联系,关系越密切,耦合性越强,模块的独立性越差.

内聚 :是指模块内部的元素,比如:方法,变量,对象等等.



低耦合

如果模块与模块之间的关系型越密切,耦合性越强,改变一个模块中的数据可能会导致其他模块中的数据跟着改变,

模块的独立性越差,不利于维护.因此设计出低耦合的关系模块.

比如:给出两个模块,模块1和模块2, 如果我想要和模块2做数据的交互,低耦合的设计应该是通过模块1数据与模块2进行交互,而不是模块1直接操作模块2上的数据.

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210709093116623.png" alt="image-20210709093116623" style="zoom: 80%;" />![image-20210816104154566](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210816104154566.png)



高内聚

模块内部的元素,相互之间关系越好,内聚就越强,模块的单一性更强.一个模块能够独立完成某个功能.

低内聚的模块代码,不利于维护和重构,不够健壮.

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210709093440360.png" alt="image-20210709093440360" style="zoom:80%;" />

​																					低内聚

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210709093552180.png" alt="image-20210709093552180" style="zoom: 67%;" />

​																					高内聚

------

##  类和对象的区别 

 　　1，类是一个抽象的概念，它不存在于现实中的时间/空间里，类只是为所有的对象定义了抽象的属性与行为。就好像“Person（人）”这个类，它虽然可以包含很多个体，但它本身不存在于现实世界上。
　　2，对象是类的一个具体。它是一个实实在在存在的东西。
　　3，类是一个静态的概念，类本身不携带任何数据。当没有为类创建任何对象时，类本身不存在于内存空间中。
　　4，对象是一个动态的概念。每一个对象都存在着有别于其它对象的属于自己的独特的属性和行为。对象的属性可以随着它自己的行为而发生改变。 

------

[java中类与类之间的几种关系 - 简书 (jianshu.com)](https://www.jianshu.com/p/eda2cbe51961)

补充：java类之间的关系





## 接口和抽象类的区别

抽象类:在java中被abstract关键字修饰的类.

抽象方法: 被abstract关键字修饰的方法,抽象方法只有方法的声明没有方法体.

特点:

- 抽象类不能被实列化只能被继承
- 抽象类可以包含属性,方法,构造方法,但是构造方法不能被用于实例化,只是为子类实例化做服务.
- 抽象类中抽象方法的修饰符只能为:public和protect,默认为public
- 包含抽象方法的类一定是抽象类,但抽象类不一定有抽象方法.
- 一个子类继承一个抽象类,则子类必须实现父类抽象方法,否则该子类只能是一个抽象类.



接口:使用interface关键字修饰

特点:

- 包含变量,方法. 变量默认为:public static final .   方法默认为: public abstract  (jdk1.8之前)

- 支持多继承,即一个接口可以extends多个接口

- 一个类可以实现多个接口

- jdk1.8中对接口增加新的特性:

  - 默认方法(default method):允许接口添加非抽象的方法实现,但必须使用default关键字修饰,定义了default的方法可以不被实现子类所实现,但只能被实现子类的对象调用.
  - 静态方法(static method):允许使用static关键字修饰一个方法,并提供实现,称为:接口静态方法.接口静态方法只能通过接口调用(接口名.静态方法名)

  注意:jkd1.9是允许接口中出现private修饰的默认方法和静态方法.



## 重载和重写(覆盖)区别

|            | 重载                     | 重写                                                   |
| ---------- | ------------------------ | ------------------------------------------------------ |
| 发生范围   | 同一类                   | 子类                                                   |
| 发生阶段   | 编译时期                 | 运行时期                                               |
| 参数列表   | 修改参数(个数,类型,位置) | 必须相同                                               |
| 返回类型   | 可修改                   | 子类方法返回值类型 <= 父类(**必须在继承关系的前提下**) |
| 异常       | 可修改                   | 子类方法声明抛出异常类型 <= 父类异常                   |
| 访问修饰符 | 可修改                   | 子类访问修饰符 >= 父类访问权限                         |

补充:

**重写返回值类型**:如果方法的返回类型是void和基本数据类型,则返回值重写时不可修改,但是如果返回类型时引用类型,重写时可以返回该引用类型的子类.

------





## Java语言特点

1. 简单易学
2. 面向对象
3. 平台无关性
4. 可靠性
5. 安全性
6. 支持多线程
7. 支持网络编程
8. 编译与解释并存



面向对象三大特点

封装:将对象的属性私有化,外界不能够直接访问对象的属性,对象提供了方法供外界访问,很安全,易维护.



继承:已经存在的类作为基础类(父类),在此基础上建立的新类,新类又称为子类或派生类. 提高代码的复用率和扩展.

- 子类拥有父类中所有的属性和方法,但子类只能访问非私有属性和方法.
- 子类可用拥有自己的属性和方法,对本身进行扩展
- 子类可以对父类方法进行重写(**子类不能覆写父类中的静态方法.在子类中定义与父类完全相同的静态方法,父类的会被隐藏)**

补充：子类不可以**继承父类的构造方法**，子类实例化之前都需要调用父类的构造方法，一般子类构造方法中，首行是super关键字调用父类构造方法，若没有显示调用父类构造方法，子类就会去调用父类的无参构造方法，若父类不存在无参构造方法(**父类中定义了有参构造方法，默认的无参构造方法就不存在了，需要自己在父类中定义无参构造**)，抛出异常。



多态:允许不同子类型对象对同一消息做出不同的响应.父类类型的引用指向子类型对象.

实现多态的形式:继承(多个子类对同一方法(**非静态方法**)进行重写)和接口(实现接口并覆盖接口中同一方法)

**注意:多态是一种运行期行为,不是编译行为,不要将函数重载理解为多态**

[多态实现的方式](https://www.cnblogs.com/ymym/p/12495922.html)

编译时多态性(前绑定):方法重载(overLoad)

运行时多态性(后绑定):方法重写(override)

特点:

- 当使用多态方式调用方法时,**首先检查父类中是否有该方法,如果没有,则编译错误.如果有,再去调用子类的同名方法**.
- **静态方法特殊,静态方法只能继承,不能覆盖**,如果子类和父类有相同的静态方法,只能起到**隐藏**父类方法的作用,**这时候,谁的引用就调用谁的方法.**

```java
public class Father {


    public void say(){
        System.out.println("father");
    }


    public static void action(){
        System.out.println("爸爸打儿子！");
    }
}


public class Son extends Father{

    public void say() {
        System.out.println("son");
    }

   public static void action(){
        System.out.println("打打！");
    }


    public static void main(String[] args) {
        Father f=new Son();
        f.say();
        f.action();

    }
}

输出：son
          
爸爸打儿子！
```



平台无关性:

java是半编译语言,也叫解释型语言和跨平台语言,这都是java语言的特性.

java的跨平台不是源文件的跨平台,而是字节码文件跨平台.将源文件通过编译器(javac)编译成jvm可以识别的字节码文件,字节码文件与平台无关,因此编译好的字节码文件通过对应平台的jvm解释成平台可以是识别执行的机器码文件.



java和c++区别

- 都是面向对象语言,都支持封装,继承,多态
- java不提供指针访问内存,程序内存更加安全
- java类是单继承,接口可以多继承,c++支持多重继承
- java有自动内存管理机制,无需手动释放无用内存
- 在c语言中,字符串和字符数组最后都会有一个额外的字符'\0'表示结束,但java没有这一概念.

```
在C语言中字符串和字符数组基本上没有区别，都需要结束符；如：char s[4]={'a'，'b'，'c'，'d'}；此字符数组的定义编译可以通过，但却没有关闭数组，若其后需要申请内存，那么以后的数据均会放入其中，尽管它的长度不够，但若为 char s[5]={'a'，'b'，'c'，'d'}；则系统会自动在字符串的最后存放一个结束符，并关闭数组，说明字符数组是有结束符的；

java中无需结束符的原因

Java里面一切都是对象，是对象的话，字符串肯定就有长度，即然有长度，编译器就可以确定要输出的字符个数，当然也就没有必要去浪费那1字节的空间用以标明字符串的结束了。比如，数组对象里有一个属性length,就是数组的长度，String类里面有方法length()可以确定字符串的长度，因此对于输出函数来说，有直接的大小可以判断字符串的边界，编译器就没必要再去浪费一个空间标识字符串的结束。
```



## 字符串常量和字符型常量的区别

形式上: 

字符常量是单引号引起的⼀个字符; 字符串常量是双引号引起的若⼲个字符 

含义上: 

字符常量相当于⼀个整型值( ASCII 值),可以参加表达式运算; 字符串常量代表⼀个地 

址值(该字符串在内存中存放位置) 

 占内存大小:

字符常量只占 2 个字节; 字符串常量占若⼲个字节 (**注意：** **char** **在** **Java** **中占两** 

**个字节**)

![image-20210709104049032](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210709104049032.png)



------







## String为什么不可变,String,StringBuffer,StringBuilder区别

String类实现用**字符数组(char value[])存储字符串**,**字符数组是被final修饰的,因此无法修改**，所以String类不可以改变

(java9之后,String类改用byte数组存储字符串)



StringBuilder 与 StringBuffer 都继承⾃ AbstractStringBuilder 类.

AbstractStringBuilder 中使用**字符数组(char value[])保存字符串,数组没有用final关键字修饰**,因此StringBuffer和StringBuilder都是可变的.

| AbstractStringBuilder                                        | StringBuilder                                                | StringBuffer                                                 |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![image-20210709121133846](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210709121133846.png) | ![image-20210709121205147](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210709121205147.png) | ![image-20210709121056095](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210709121056095.png) |

补充：**String、StringBuilder、StringBuffer类都是被final修饰的，都是限制他们所存储的引用地址不可以修改，同时还表示该类无法被继承**。而StringBuilder、StringBuffer的字符数组可以被修改。也就是内容可以被修改



线程安全

String类中的对象是不可变的,线程安全

StringBuilder中并没有对方法加同步锁,线程不安全

StringBuffer中对方法或调用方法加同步锁,线程安全



性能

对String类型进行更改时,都会生成一个新的String对象,将指针指向新的String对象.

String对象的两种创建方式

1. String   str 1 ="aa"; 

   这种方式声明的String对象，在编译时期就已**字面量**的形式存在字节码（class）文件常量池中，到来运行期间，字节码（class）文件常量池会被加载到“运行时常量池中”，包括String的字面量，但同时会将“**aa**”的一个引用存放到字符串常量池中，“**aa**”本体还是和所有对象一样在堆上创建。若进行比较会先在字符串常量池中寻找引用。

2. String  str 2 =new String("aa"),调用的是String的构造函数，在类型加载完成后，进行对象加载在运行期间才能够确定，此"aa"是位于堆内存中。



StringBuffer和StringBuilder每次更改时都是对自身进行操作,比如方法append.而不是生成新的对象.



使用:

操作少量数据:String

单线程操作字符串缓冲区下大量数据:StringBuilder

多线程操作字符串缓冲区下大量数据:StringBuffer

------



## ==与equals

==:如果比较的是基本数据类型,判断的是两个数值是否相等,如果比较的是引用数据类型,判断是否指向同一内存地址.

equals:Object类中的equals方法与"=="作用相同,如果重写了equals方法,比较两个对象是否相等,通过equals比较两个对象中内容是否相同.

------





## 自动装箱和拆箱

[自动装箱和拆箱](https://www.cnblogs.com/dolphin0520/p/3780005.html)

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210709124851690.png" alt="image-20210709124851690" style="zoom:67%;" />

装箱:自动将基本数据类型转换为包装类型

装箱的时候自动调用的是Integer的valueOf(int)方法



拆箱:自动将包装类型转换为基本数据类型

在拆箱的时候自动调用的是Integer的intValue方法。 



面试中相关问题:

```java
public class Main {
    public static void main(String[] args) {
         
        Integer i1 = 100;
        Integer i2 = 100;
        Integer i3 = 200;
        Integer i4 = 200;
         
        System.out.println(i1==i2);
        System.out.println(i3==i4);
    }
}

输出:
true
false
```

查阅Integer的源码:

```java
public static Integer valueOf(int i) {
    //IntegerCache类型的缓存
        if(i >= -128 && i <= IntegerCache.high)
            return IntegerCache.cache[i + 128];
        else
            return new Integer(i);
    }
    
  
private static class IntegerCache {
        static final int high;
        static final Integer cache[];

        static {
            final int low = -128;

            // high value may be configured by property
            int h = 127;
            if (integerCacheHighPropValue != null) {
                // Use Long.decode here to avoid invoking methods that
                // require Integer's autoboxing cache to be initialized
                int i = Long.decode(integerCacheHighPropValue).intValue();
                i = Math.max(i, 127);
                // Maximum array size is Integer.MAX_VALUE
                h = Math.min(i, Integer.MAX_VALUE - -low);
            }
            high = h;

            cache = new Integer[(high - low) + 1];
            int j = low;
            for(int k = 0; k < cache.length; k++)
                cache[k] = new Integer(j++);
        }

        private IntegerCache() {}
    }
```

 在通过valueOf方法创建Integer对象的时候，如果数值在[-128,127]之间，便返回指向IntegerCache.cache中已经存在的对象的引用；否则创建一个新的Integer对象。 

因此,200已经超越了[-128,127],生成是两个不同对象,因此是false.



```java
public class Main {
    public static void main(String[] args) {
         
        Double i1 = 100.0;
        Double i2 = 100.0;
        Double i3 = 200.0;
        Double i4 = 200.0;
         
        System.out.println(i1==i2);
        System.out.println(i3==i4);
    }
}

输出:
false
false
```

 在某个范围内的整型数值的个数是有限的，而浮点数却不是,因此这四个变量都是不同的对象.

Integer、Short、Byte、Character、Long这几个类的valueOf方法的实现是类似的。

　　　　　Double、Float的valueOf方法的实现是类似的。





```java
public class Main {
    public static void main(String[] args) {
         
        Boolean i1 = false;
        Boolean i2 = false;
        Boolean i3 = true;
        Boolean i4 = true;
         
        System.out.println(i1==i2);
        System.out.println(i3==i4);
    }
}

输出:
true
true
```

```java
public static final Boolean TRUE = new Boolean(true);

    /** 
     * The <code>Boolean</code> object corresponding to the primitive 
     * value <code>false</code>. 
     */
public static final Boolean FALSE = new Boolean(false);
```

Boolean类中定义了两个静态不可改变的变量





```java
		Integer a = 6 ;
		Integer a1 = new Integer(6);
        Integer b = new Integer(1);
        Integer c = new Integer(2);
        Integer e = 3 ;
        Integer f = 3 ;
        Integer d = new Integer(1);
		Integer g = 6 ;

        System.out.println(e.equals(b+c));
        System.out.println(b.equals(d));
        System.out.println(a.equals(e+f));
 		System.out.println(a == a1);
		System.out.println(a == g);
/*
true
true
true
false
true

Integer包装类重写了equals方法，因此比较的是值，==若都是包装类比较的是地址，若是基本数据类型，包装类会进行自动拆箱转换成基本类型，比较的是值。

Integer g = 6 ;能够自动装箱相当于 Integer g = Integer.ValueOf(6);在Integer常量池中寻找6的引用
*/
```



 Integer i = new Integer(xxx)和Integer i =xxx;这两种方式的区别。 

1.  第一种方式不会触发自动装箱的过程；而第二种方式会触发自动装箱(**java编译时会自动调用Integer.valueOf(xxx)**)； 
2.  在执行效率和资源占用上的区别。第二种方式的执行效率和资源占用在一般性情况下要优于第一种情况（注意这并不是绝对的）。 





```java
public class Main {
    public static void main(String[] args) {
         
        Integer a = 1;
        Integer b = 2;
        Integer c = 3;
        Integer d = 3;
        Integer e = 321;
        Integer f = 321;
        Long g = 3L;
        Long h = 2L;
         
        System.out.println(c==d);
        System.out.println(e==f);
        System.out.println(c==(a+b));
        System.out.println(c.equals(a+b));
        System.out.println(g==(a+b));
        System.out.println(g.equals(a+b));
        System.out.println(g.equals(a+h));
    }
}

输出:
true
false
true  先进行a+b运算的拆箱,转换成基本数据类型,最后比较的是数值是否相等
true  先进行a+b的拆箱(intValue),比较的是值是否相等
true  拆箱后基本数据转换成long类型(向上类型转换)
false a+b拆箱(intValue),g进行拆箱，equals不会进行类型转换，因此long和int类型不符合
true a+h拆箱进行运算，a为int、h为long a+h结果为long类型，最后比较的是值类型
```

 当 "=="运算符的两个操作数都是 包装器类型的引用，则是比较指向的是否是同一个对象，而如果其中有一个操作数是表达式（即包含算术运算）则比较的是数值（即会触发自动拆箱的过程） ，对于包装器类型，**equals方法并不会进行类型转换 .**

[java基本数据类型转换](https://www.cnblogs.com/fanweisheng/p/11130515.html)

**向上转换：**

整型，字符型，浮点型的数据在混合运算中相互转换，转换时遵循以下原则：

容量小的类型可自动转换为容量大的数据类型；

byte,short,char → int → long → float → double

byte，short，char之间不会相互转换，他们在计算时首先会转换为int类型。

boolean 类型是不可以转换为其他基本数据类型。

补充：**当long类型转换为float类型时 不需要进行强制类型转换，虽然long类型占8个字节，float占4个字节，float是浮点类型表示的范围比long类型要大。**



**向下转换**：

整型，字符型，浮点型的数据在混合运算中相互转换，转换时遵循以下原则：

容量大的类型向容量小的类型转换时需要进行 **强制类型转换，例如：long l = 123L; int i = (int) l;//必须强转**

byte,short,char <-----int <----- long <----- float <--- double

byte，short，char之间不会相互转换，他们在计算时首先会转换为int类型。

boolean 类型是不可以转换为其他基本数据类型。

**类型转化**

**小转大，自动！自动类型转换（也叫隐式类型转换）** 

**大转小，强转！强制类型转换（也叫显式类型转换）**

------







## 静态方法调用一个非静态方法是非法的

静态方法属于类而不属于对象,通过类去调用静态方法,静态方法不可以调用和访问非静态变量.

一个类实例化之前,首先加载其静态变量和静态代码块,其次加载普通变量和代码块,最后调用构造函数.**因为加载顺序的原因，所以静态方法无法访问非静态方法合变量**

------



## java中无参构造函数作用

如果一个类实例化时,没有定义构造函数,会默认提供一个无参构造函数.

如果子类实列化,子类构造函数中没有用super关键字调用父类特定的构造函数(先有父亲后有儿子),那么会去调用父类中的无参构造函数(此无参构造函数是自己定义的),如果父类中没有定义无参构造函数,则会发生编译错误.

------





## 成员变量与局部变量区别

从语法形式上:成员变量属于类,局部变量属于方法内部或方法的参数,成员变量可以被public,protect,private,static等修饰,而局部变量只能被final关键字修饰.

从存储形式上:成员变量被static修饰,那么它属于类,否则它是属于对象实例,对象被存放在堆内存中.局部变量如果是基本数据类型,它被存储在栈内存中,如果是引用数据类型,存放的是指向堆中的对象引用或着是常量池中的地址.

从生存时间上:成员变量是对象的一部分,随着对象的创建而创建,局部变量随着方法调用而调用.

赋值:成员变量在没有赋值的情况下会自动赋予默认值,而局部变量不会自动赋值.



------



## java中创建对象的几种方式

1.  new 关键字(调用构造函数)
2. Class类的 newInstance方法(调用构造函数) ,java反射机制
3. Constructor类newInstance方法(调用构造函数),java反射机制
4. clone方法 (不调用构造函数,通过jvm创建新的对象,将对象的内容进行拷贝)
5. 反序列化



## hashCode() 与 equals

hashCode()方法作用:获取对象的哈希码,哈希码又称为(散列码).

hashCode()和equals一样,都定义在Object类中(Object是所有类的父类),因此每个类中都继承了hashCode().



散列码:用来确定对象在散列表中的位置.

实质:将对象的内存地址转换成int类型返回,这个int整数(散列码)确定了对象在散列表中的索引位置.



散列表(哈希表):本质上是通过数组实现的.

存储的是键值对(key-value)通过键快速找到对应值.

键是通过对应散列码计算得到的



为什么要有hashCode()

以Set接口以及其实现类HashSet为例说明,Set集合特点是不允许重复元素,向Set集合中加入一个新的对象,

通过获取该对象的散列码计算该对象存放的位置,同时会和其他已经加入到集合的对象的位置作比较,如果hashCode值不相等,那么会认为没有重复对象,如果hashCode值出现相同的情况,会通过调用equals判断相同hashCode值的对象是否是相等的,如果相等那么就不允许加入,如果不相等,允许加入,重新将其散列到其他位置,减少了equals判定的次数,大大提高了执行速率.

例如:向HashSet集合中加入第101个元素,只需要对新加入的对象的散列码计算其位置加入到散列表中,不需要进行大量的equals比较.    由
             



**hashCode() 和 equals()的关系**

第一种:不会创建"类对应的散列表"

 **这里所说的“不会创建类对应的散列表”是说：我们不会在HashSet, Hashtable, HashMap等等这些本质是散列表的数据结构中，用到该类。例如，不会创建该类的HashSet集合。** (说白了就是创建了对象之后,不使用HashSet,HashTable等等,单纯的比较它们的hashcode())

这种情况下:hashCode()和equals没有关系，equals() 用来比较该类的两个对象是否相等。而hashCode() 则根本没有任何作用，所以，不用理会hashCode()。

比如:定义两个相同的对象它们的hashCode()值也不相同.

[引用](https://www.cnblogs.com/skywang12345/p/3324958.html)

```java
10 public class NormalHashCodeTest{
11 
12     public static void main(String[] args) {
13         // 新建2个相同内容的Person对象，
14         // 再用equals比较它们是否相等
15         Person p1 = new Person("eee", 100);
16         Person p2 = new Person("eee", 100);
17         Person p3 = new Person("aaa", 200);
18         System.out.printf("p1.equals(p2) : %s; p1(%d) p2(%d)\n", p1.equals(p2), p1.hashCode(), p2.hashCode());
19         System.out.printf("p1.equals(p3) : %s; p1(%d) p3(%d)\n", p1.equals(p3), p1.hashCode(), p3.hashCode());
20     }
21 
22     /**
23      * @desc Person类。
24      */
25     private static class Person {
26         int age;
27         String name;
28 
29         public Person(String name, int age) {
30             this.name = name;
31             this.age = age;
32         }
33 
34         public String toString() {
35             return name + " - " +age;
36         }
37 
38         /** 
39          * @desc 覆盖equals方法 
40          */  
41         public boolean equals(Object obj){  
42             if(obj == null){  
43                 return false;  
44             }  
45               
46             //如果是同一个对象返回true，反之返回false  
47             if(this == obj){  
48                 return true;  
49             }  
50               
51             //判断是否类型相同  
52             if(this.getClass() != obj.getClass()){  
53                 return false;  
54             }  
55               
56             Person person = (Person)obj;  
57             return name.equals(person.name) && age==person.age;  
58         } 
59     
60 }
结果:
p1.equals(p2) : true; p1(1169863946) p2(1901116749)
p1.equals(p3) : false; p1(1169863946) p3(2131949076)
```



第二种:会创建“类对应的散列表”

 这里所说的“会创建类对应的散列表”是说：我们会在HashSet, Hashtable, HashMap等等这些本质是散列表的数据结构中，用到该类。例如，会创建该类的HashSet集合。 

  在这种情况下，该类的“hashCode() 和 equals() ”是有关系的：
    1)、如果两个对象相等，那么它们的hashCode()值一定相同。
       这里的相等是指，通过equals()比较两个对象时返回true。
    2)、如果两个对象hashCode()相等，它们并不一定相等。 



比如:创建两个对象,将他们加入到HashSet集合中,如果只是重写了equals方法而不重写hashCode方法,两个相等的对象的hashCode是不同的,它们位于HashSet散列表中的位置不同,最后两个都加入了HashSet集合中,这与不允许重复元素的Set集合的规则相违背,因此重写了equals方法之后也必须重写hashCode(),保证两个相同对象的hashCode值一定相同.

```java
 public class ConflictHashCodeTest2{
11 
12     public static void main(String[] args) {
13         // 新建Person对象，
14         Person p1 = new Person("eee", 100);
15         Person p2 = new Person("eee", 100);
16         Person p3 = new Person("aaa", 200);
17         Person p4 = new Person("EEE", 100);
18 
19         // 新建HashSet对象 
20         HashSet set = new HashSet();
21         set.add(p1);
22         set.add(p2);
23         set.add(p3);
24 
25         // 比较p1 和 p2， 并打印它们的hashCode()
26         System.out.printf("p1.equals(p2) : %s; p1(%d) p2(%d)\n", p1.equals(p2), p1.hashCode(), p2.hashCode());
27         // 比较p1 和 p4， 并打印它们的hashCode()
28         System.out.printf("p1.equals(p4) : %s; p1(%d) p4(%d)\n", p1.equals(p4), p1.hashCode(), p4.hashCode());
29         // 打印set
30         System.out.printf("set:%s\n", set);
31     }
32 
33     /**
34      * @desc Person类。
35      */
36     private static class Person {
37         int age;
38         String name;
39 
40         public Person(String name, int age) {
41             this.name = name;
42             this.age = age;
43         }
44 
45         public String toString() {
46             return name + " - " +age;
47         }
48 
49         /** 
50          * @desc重写hashCode 
51          */  
52         @Override
53         public int hashCode(){  
54             int nameHash =  name.toUpperCase().hashCode();
55             return nameHash ^ age;
56         }
57 
58         /** 
59          * @desc 覆盖equals方法 
60          */  
61         @Override
62         public boolean equals(Object obj){  
63             if(obj == null){  
64                 return false;  
65             }  
66               
67             //如果是同一个对象返回true，反之返回false  
68             if(this == obj){  
69                 return true;  
70             }  
71               
72             //判断是否类型相同  
73             if(this.getClass() != obj.getClass()){  
74                 return false;  
75             }  
76               
77             Person person = (Person)obj;  
78             return name.equals(person.name) && age==person.age;  
79         } 
80     }
81 }

结果:
p1.equals(p2) : true; p1(68545) p2(68545)
p1.equals(p4) : false; p1(68545) p4(68545)
set:[aaa - 200, eee - 100]
```

这下，equals()生效了，HashSet中没有重复元素。
    比较p1和p2，我们发现：它们的hashCode()相等，通过equals()比较它们也返回true。所以，p1和p2被视为相等。
    比较p1和p4，我们发现：虽然它们的hashCode()相等；但是，通过equals()比较它们返回false。所以，p1和p4被视为不相等。

------





## Java为什么只有值传递

**按值调用(call by value)**表示方法接收的是调⽤者提供的值，⽽按引用调用（**call by reference)**表示⽅法**接收的是调用者提供的变量地址。**

 java中只有值传递，只不过引用类型的变量里的值是个内存地址罢了，都是复制一份做赋值操作 。

```java
public static void main(String[] args) {
 int num1 = 10;
 int num2 = 20;
 swap(num1, num2);
 System.out.println("num1 = " + num1);
 System.out.println("num2 = " + num2);
}
public static void swap(int a, int b) {
 int temp = a;
 a = b;
 b = temp;
 System.out.println("a = " + a);
 System.out.println("b = " + b);
}

结果：
a = 20
b = 10
num1 = 10
num2 = 20
```

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210710093547068.png" alt="image-20210710093547068" style="zoom:50%;" />

num1和num2都是基本数据类型，而传入swap方法中的参数，只是num1和num2的拷贝，因此无论swap方法中参数如何变化，都不会影响num1和num2的数据。



```java
 public static void main(String[] args) {
 int[] arr = { 1, 2, 3, 4, 5 };
 System.out.println(arr[0]);
 change(arr);
 System.out.println(arr[0]);
 }
 public static void change(int[] array) {
 // 将数组的第⼀个元素变为0
 array[0] = 0;
 }
 
 结果：
 1
 0
```

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210710093933633.png" alt="image-20210710093933633" style="zoom:67%;" />

arr指向堆中的数组对象，change方法中array是数组对象引用的拷贝，它们指向的都是同一个数组对象，因此方法中通过array[0] = 0 ,指向的就是堆中数据，因此外部对对象引用的改变反映到所对应的对象上。



Java 程序设计语⾔对对象采⽤的不是引⽤调⽤，实际上，对象引⽤是按值传递的。 

下⾯再总结⼀下 Java 中⽅法参数的使⽤情况： 

⼀个⽅法不能修改⼀个基本数据类型的参数（即数值型或布尔型）。 

⼀个⽅法可以改变⼀个对象参数的状态。 

⼀个⽅法不能让对象参数引⽤⼀个新的对象。

------





## final关键字

主要引用范围：变量，方法，类

变量：被修饰的基本类型，如果没有被赋值（final  number）,一旦被赋值之后就不能重新赋值(final number 	= 1)

​			被修饰的引用类型，保证了引用类型变量所指向的地址不改变，而不能保证所引用的对象不改变。

补充：

```java
byte b1 = 1, b2 = 2, b3 ,b4
final byte b5 =4,b6=6;

//试问,下面哪里编译错误？
1. b3 = b5 + b6;
2. b4 = b1 + b2;

//答案：2编译错误
/*原因：基本数据类型:byte、char、short在做运算时，都会自动进行转换成int、b1 + b2最后的结果时int， b4确是byte类型，类型不匹配。而b3 = b5 + b6;编译成功，b3 = 10,因为final关键字修饰后，b5和b6都是常量类型byte，最后10也是btye类型因此编译成功。
*/
```

方法：不可以被继承的子类所重写（覆盖）。

​			效率原因，早期final方法为内嵌调用，如果方法过于庞大，并不能得到提升。

类：不能被继承，类中所有成员方法都被隐式指定为final。

------





## Java异常

![image-20210710095851862](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210710095851862.png)

​			

在 Java 中，所有的异常都有⼀个共同的祖先 java.lang 包中的 Throwable 类。 Throwable 类 有两个重要的⼦类 Exception （异常）和 Error （错误）。 Exception 能被程序本身处理( try-catch )， Error 是⽆法处理的(只能尽量避免)。

**Error** 

1. Error 类是指 java 运行时系统的内部错误和资源耗尽错误。应用程序不会抛出该类对象。如果 出现了这样的错误，除了告知用户，剩下的就是尽力使程序安全的终止。 

**Exception**（RuntimeException、CheckedException）

2. Exception 又 有 两 个 分 支 ， 一 个 是 运 行 时 异 常 RuntimeException ， 一 个 是 CheckedException。 

**RuntimeException** 如 ： NullPointerException 、 ClassCastException ； 一 个 是 检 查 异 常 CheckedException，如 I/O 错误导致的 IOException、SQLException。 RuntimeException 是 那些可能在 Java 虚拟机正常运行期间抛出的异常的超类。 如果出现 RuntimeException，那么一 定是程序员的错误（想想空指针问题、数组越界的问题）.



**检查异常 CheckedException**：一般是外部错误，这种异常都发生在编译阶段，Java 编译器会强制程序去捕获此类异常，即会出现要求你把这段可能出现异常的程序进行 try catch。**所以编译时的异常必须显示处理，运行时异常交给虚拟机处理。**



异常处理方式

throws，throw

try-catch-finally

系统自动抛出异常



```java
try{
    return  						//finally块前（try/catch）中有return,会先执行return语句，
        							//并保存下来，再执行finally块，最后return
}
catch(){
    
}finally{}
```

```java
try{
return  							//finally块前（try/catch）中有return,finally块中也有
									//return会先执行前面return语句
        							//并保存下来，再执行finally块中的return，覆盖掉之前的结果，返回。
}
catch(){
    
}finally{
	return
}
```

补充：在tyr、catch语句中，catch语句块允许有多个，若出现父子类型的异常，需要把子类型的异常放在前面，父类型的异常放在后面。

比如：Exception是所有异常的父类，若将它放在首位，那么就没有办法定位到具体的异常类型，不知道具体的异常，只知道有异常，不好检查。



finally不会被执行情况

```
try或finally块中有system.exit(0)(推出虚拟机)
关闭cpu
程序所在线程死亡
```



throw和throws区别

- throws位于函数上，可以定义多个异常类

  throw位于函数内部，定义异常对象

- throws声明异常，表示函数中可能发生的异常，给出预先处理方式

  throw抛出异常，抛出具体问题对象，此时功能到此已经结束了

- 两者都是消极处理异常方式，只是抛出异常，但是不会由函数处理异常，真正处理异常由函数上层调用处理。

------







## Java反射

特点：

动态语言

在程序运行期间可以改变其结构，引入新的函数，也可以改变已有函数结构。例如：JavaScript

从反射角度来看：java属于半动态语言。c++、c不是动态语言。



反射机制概念（运行状态中知道类的所有属性和方法）

在java的反射机制中处于运行状态时，对于任意一个类都能够知道它所有的属性和方法，并且对于任意一个对象，都能够调用它的任意一个方法。动态获取信息以及动态调用对象方法的功能。

本质上：从字节码中查找，动态获取类的结构，包括属性、构造器、动态调用对象方法，**注意并不是修改类**。



反射应用场景

编译时类型和运行时类型

编译时类型由声明的类型决定，运行时类型由实际赋予的对象类型决定。

```java
Person p=new Student();
编译类型：Person   运行类型:Student
//引用类型Person是定义的，new Student()是在运行时创建的对象    
```



当程序处于运行时从外部传入新的对象，该对象的编译时类型为Object，但程序运行时需要调用该对象的运行时类型方法，在编译时无法获取对象属于哪些类时，为了在运行时获取该对象的具体类型的方法，此时就要用到反射。

 <img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/2019042011494188.png" alt="img" style="zoom: 200%;" /> 

 反射API

- Class 类：位于java.lang包下，反射的核心类，可以获取类的属性，方法、构造方法等信息。 
- Field 类：Java.lang.reflec 包中的类，表示类的成员变量，可以用来获取和设置类之中的属性值。 
- Method 类： Java.lang.reflec 包中的类，表示类的方法，它可以用来获取类中的方法信息或者执行方法。
- Constructor 类： Java.lang.reflec 包中的类，表示类的构造方法。



反射的核心操作：获取想要操作的Class对象，用来调用类方法。

获取Class对象方式

- 调用Object类的getClass方法

```
Person p=new Person();
Class clazz=p.getClass();
```

- 通过类名获取：类名.class(字节码文件)

```
Class clazz=Person.class;
```

- 使用Class.forName("完整的类名")方法**（最安全、性能最好）**

```
Class clazz=Class.forName("类的全路径"); (最常用)
```



创建对象的两种方法

**Class对象的newInstance()**

使用Class对象的newInstance()方法创建该Class对象对应类的实列，这种方法要求该Class对象对应的类有默认的空构造器。

**调用Constructor对象的newInstance()**

先通过获取Class对象中对应类指定的Constructor对象，调用Constructor对象的newInstance()方法创建Class对象对应类的实例。

```
//获取 Person 类的 Class 对象
 Class clazz=Class.forName("reflection.Person"); 
 //使用.newInstane 方法创建对象
 Person p=(Person) clazz.newInstance();
//获取构造方法并创建对象
 Constructor c=clazz.getDeclaredConstructor(String.class,String.class,int.class);
 //创建对象并设置属性
 Person p1=(Person) c.newInstance("李四","男",20);
```

------







## JAVA注解

 [(7条消息) java注解-最通俗易懂的讲解_Tanyboye的博客-CSDN博客_java 注解](https://blog.csdn.net/qq1404510094/article/details/80577555) 

在正真对注解进行理论上的学习之前，可以对注解进行形象化方便理解。

可以把注解想象成标签，标签是干什么的呢，表明名称、属性、作用的，类似一种说明，反映事物的特性的。

标签是对事物行为的评价与解释，注解的作用类似于标签。



概念：

Annotation（注解）是一个接口，程序可以通过反射来获取指定程序中元素的 Annotation对象，然后通过该 Annotation 对象来获取注解中的元数据信息。 

注解定义：

```java
public @interface TestAnnotation {
}// 注解通过 @interface 关键字进行定义。 
```

定义了一个名为TestAnnotation的注解（标签）。

注解应用：

```java
@TestAnnotation
public class Test {
}
//将TestAnnotation注解贴在Test类上
```



元注解：

负责注解其他注解， 作用在注解中，方便我们使用注解实现想要的功能。元注解分别有@Retention、 @Target、 @Document、 @Inherited和@Repeatable（JDK1.8加入）五种。 

元注解负责**解释定义**注解的属性、范围、功能的。



**@Retention**

Retention 的英文意为保留期的意思。当 @Retention 应用到一个注解上的时候，它解释说明了这个注解的的存活时间。

它的取值如下：

- RetentionPolicy.SOURCE 注解只在源码阶段保留，在编译器进行编译时它将被丢弃忽视。
- RetentionPolicy.CLASS 注解只被保留到编译进行的时候，它并不会被加载到 JVM 中。
- RetentionPolicy.RUNTIME 注解可以保留到程序运行的时候，它会被加载进入到 JVM 中，所以在程序运行时可以获取到它们。

```java
//元注解
@Retention(RetentionPolicy.RUNTIME)
public @interface TestAnnotation {
}
//指定TestAnnotation可以在运行期间被获取到
```



@**Documented**

- Document的英文意思是文档。它的作用是能够将注解中的元素包含到 Javadoc 中去。



**@Target**

- Target的英文意思是目标，这也很容易理解，使用@Target元注解表示我们的注解作用的范围就比较具体了，可以是类，方法，方法参数变量等，同样也是通过枚举类ElementType表达作用类型
- @Target(ElementType.TYPE) 作用接口、类、枚举、注解
- @Target(ElementType.FIELD) 作用属性字段、枚举的常量
- @Target(ElementType.METHOD) 作用方法
- @Target(ElementType.PARAMETER) 作用方法参数
- @Target(ElementType.CONSTRUCTOR) 作用构造函数
- @Target(ElementType.LOCAL_VARIABLE)作用局部变量
- @Target(ElementType.ANNOTATION_TYPE)作用于注解（@Retention注解中就使用该属性）
- @Target(ElementType.PACKAGE) 作用于包
- @Target(ElementType.TYPE_PARAMETER) 作用于类型泛型，即泛型方法、泛型类、泛型接口 （jdk1.8加入）
- @Target(ElementType.TYPE_USE) 类型使用.可以用于标注任意类型除了 class （jdk1.8加入）
- 一般比较常用的是ElementType.TYPE类型

```java
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.TYPE)
public @interface MyTestAnnotation {

}
```

**@Inherited**

Inherited 是继承的意思，但是它并不是说注解本身可以继承，而是说如果一个超类被 @Inherited 注解过的注解进行注解的话，那么如果它的子类没有被任何注解应用的话，那么这个子类就继承了超类的注解。
说的比较抽象。代码来解释。

```java
@Inherited
@Retention(RetentionPolicy.RUNTIME)
@interface Test {}
@Test
public class A {}
public class B extends A {}
```

注解Test被@Inherited修饰，之后A类被Test注解修饰，B类是A类的子类，因此B类也拥有Test这个注解。



**@Repeatable**

Repeatable 自然是可重复的意思。@Repeatable 是 Java 1.8 才加进来的，所以算是一个新的特性。

什么样的注解会多次应用呢？通常是注解的值可以同时取多个。

```java
//一个人他既是程序员又是产品经理,同时他还是个画家。
@interface Persons {
    Person[]  value();
}

@Repeatable(Persons.class)
@interface Person{
    String role default "";
}

@Person(role="artist")
@Person(role="coder")
@Person(role="PM")
public class SuperMan{
}
```

 @Repeatable 注解了 Person。而 @Repeatable 后面括号中的类相当于一个容器注解。 

```java
//容器注解
@interface Persons {
    Person[]  value();
}
```



注解的属性

```java
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
public @interface TestAnnotation {
    int id();
    String msg();
}

//属性又叫成员变量
//属性：id 和msg
//返回类型： int、String 
```

赋值

```java
//赋值的方式是在注解的括号内以 value=”” 形式，多个属性之前用 ，隔开。
@TestAnnotation(id=3,msg="hello annotation")
public class Test {
}
```

```java
//注解中属性可以有默认值，默认值需要用 default 关键值指定。
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
public @interface TestAnnotation {
    public int id() default -1;
    public String msg() default "Hi";
}
```



java中其他三个标准注解

**@Deprecated**

这个元素是用来标记过时的元素，想必大家在日常开发中经常碰到。编译器在编译阶段遇到这个注解时会发出提醒警告，告诉开发者正在调用一个过时的元素比如过时的方法、过时的类、过时的成员变量。

```java
public class Hero {
    @Deprecated
    public void say(){
        System.out.println("Noting has to say!");
    }
    public void speak(){
        System.out.println("I have a dream!");
    }
}
//say()方法被标注为过时
```

@**SuppressWarnings**

阻止警告的意思。之前说过调用被 @Deprecated 注解的方法后，编译器会警告提醒，而有时候开发者会忽略这种警告，他们可以在调用的地方通过 @SuppressWarnings 达到目的。

```java
@SuppressWarnings("deprecation")
public void test1(){
    Hero hero = new Hero();
    hero.say();
    hero.speak();
}
//编辑器不会发出say()的过时警告
```

@**Override**

 子类要复写父类中被 @Override 修饰的方法 



**注解与反射。**

 注解通过反射获取。首先可以通过 Class 对象的 isAnnotationPresent() 方法判断它是否应用了某个注解 

```java
public boolean isAnnotationPresent(Class<? extends Annotation> annotationClass) {}
```

 然后通过 getAnnotation() 方法来获取 Annotation 对象。 

```java
 public <A extends Annotation> A getAnnotation(Class<A> annotationClass) {}
```

 或者是 getAnnotations() 方法。 

```java
public Annotation[] getAnnotations() {}
```

测试：

```java
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
public @interface TestAnnotation {
    public int id() default -1;
    public String msg() default "Hi";
}

@TestAnnotation()
public class Test {
    public static void main(String[] args) {
        // 注解通过反射获取。
        boolean hasAnnotation = Test.class.isAnnotationPresent(TestAnnotation.class);
        if ( hasAnnotation ) {
            //通过 getAnnotation() 方法来获取 Annotation 对象。 
            TestAnnotation testAnnotation = Test.class.getAnnotation(TestAnnotation.class);
            System.out.println("id:"+testAnnotation.id());
            System.out.println("msg:"+testAnnotation.msg());
        }
    }
}
//id:-1
//msg:Hi
```



注解同样无法改变代码本身，注解只是某些工具的的工具。

**注解的应用实例**

JUnit 这个是一个测试框架，典型使用方法如下：

```java
public class ExampleUnitTest {
    @Test
    public void addition_isCorrect() throws Exception {
        assertEquals(4, 2 + 2);
    }
}
```

自定义的注解为了实现某个目的而定义注解，比如要实现单元测试，可以自定义一个类似于@Test的注解，来完成单元测试达到目的。



注解有许多用处，主要如下：

- 提供信息给编译器： 编译器可以利用注解来探测错误和警告信息
- 编译阶段时的处理： 软件工具可以用来利用注解信息来生成代码、Html文档或者做其它相应处理。
- 运行时的处理： 某些注解可以在程序运行的时候接受代码的提取
  值得注意的是，注解不是代码本身的一部分。





总结

- 如果注解难于理解，你就把它类同于标签，标签为了**解释事物**，注解为了**解释代码**。
- 注解的基本语法，创建如同接口，但是多了个 @ 符号。
- 注解的元注解。
- 注解的属性。
- 注解主要给**编译器**及工具类型的软件用的。
- 注解的提取需要借助于 Java 的反射技术，反射比较慢，所以注解使用时也需要谨慎计较时间成本

------





## Java内部类

Java 类中不仅可以定义变量和方法，还可以定义类，这样定义在类内部的类就被称为内部类。根 

据定义的方式不同，内部类分为**静态内部类，成员内部类，局部内部类，匿名内部类**四种。



**静态内部类**

定义在类内部的被static关键字修饰的类

```java
public class innerClass {
    private static  int a  = 1;
    private int b = 2;
    public static class staticClass{
        private int n =3;
        private static  int c = 6;
        int b = innerClass.a;

        public static void main(String[] args) {
            innerClass.print1();
        }

    }
    public void print(){
        System.out.println(1);
    }

    public  static void print1(){
        System.out.println(1);
    }
}
/*
1. 静态内部类可以访问外部类所有的静态变量和方法，即使是 private 的也一样。不能访问非静态变量和方法
2. 静态内部类和一般类一致，可以定义静态变量和非静态变量、方法，构造方法等。
3. 其它类使用静态内部类需要使用“外部类.静态内部类”方式，如下所示：
Out.Inner inner = new Out.Inner();
inner.print();
*/
```



**成员内部类**

定义在类内部的非静态类，就是成员内部类。成员内部类**不能定义静态方法和变量**（final 修饰的 

除外）。这是因为成员内部类是非静态的，**类初始化的时候先初始化静态成员，如果允许成员内** 

**部类定义静态变量，那么成员内部类的静态变量初始化顺序是有歧义的。** 

补充：成员内部类本身可以访问外围类的所有资源。ee

```java
public class innerClass {
    private static  int a  = 1;
    private int b = 2;
    public  class staticClass{
        private int n =3;
        //不能定义静态变量和方法
//        private static  int c = 6;
        int b = innerClass.a;

//        public static void main(String[] args) {
//            innerClass.print1();
//        }

    }
    public void print(){
        System.out.println(1);
    }

    public  static void print1(){
        System.out.println(1);
    }
}
```



**局部内部类（定义在方法中的类）**

定义在方法中的类，就是局部类。如果一个类只在某个方法中使用，则可以考虑使用局部类。 

```java
public class innerClass {
    private static  int a  = 1;
    private int b = 2;

    public void test(){
        int o = 1;
        class constClass{
            //不允许定义静态变量和方法
//            private static int  j = 0;
//            public static  void print(){
//                System.out.println(1);
//            }
            public  int i = 0;
            public  void print(){
                System.out.println(2);
            }
        }
        System.out.println(1);
    }

}
```



**匿名内部类（要继承一个父类或者实现一个接口、直接使用new** **来生成一个对象的引用）** 

匿名内部类我们必须要继承一个父类或者实现一个接口，当然也仅能只继承一个父类或者实现一 

个接口。同时它也是没有 class 关键字，这是因为匿名内部类是直接使用 new 来生成一个对象的引 

用。 



补充:**由于构造器的名字必须与类名相同，而匿名内部类没有类名**

 

```java
public abstract class Bird {
    private String name;
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    public abstract int fly();
}
public class Test {
    public void test(Bird bird){
        System.out.println(bird.getName() + "能够飞 " + bird.fly() + "米");
    }
    public static void main(String[] args) {
        Test test = new Test();
        //new关键字实现抽象类Bird的fly方法
        test.test(new Bird() {
            public int fly() {
                return 10000;
            }
            public String getName() {
                return "大雁";
            }
        });
    } 
}
```

------





## Java泛型

 [Java泛型详解，通俗易懂只需5分钟 - 会偷袭的猫 - 博客园 (cnblogs.com)](https://www.cnblogs.com/cat520/p/9353291.html) 

一般情况下，我们在使用变量时会先进行定义，确定变量具体的类型，定义方法时也需要给定具体的类型的参数。

当遇到同一个变量需要不同类型或者方法的参数类型多样时，一般不是定义多个变量就是重载方法，这样做的话会让代码显得臃肿。虽然java中有一个顶级父类，任何一个类的实例都可以向上转型成Object，但是具体到某个数据时又需要将Object类强制转换，当中可能存在着风险，因此使用java通过的泛型就可以很好的解决这样的问题。



所谓泛型：就是宽泛的数据类型，它可以接受任意的数据类型。

应用：

**泛型类**

```java
public class Demo {
    public static void main(String[] args){
        // 实例化泛型类
        Point<Integer, Integer> p1 = new Point<Integer, Integer>();
        p1.setX(10);
        p1.setY(20);
        int x = p1.getX();
        int y = p1.getY();
        System.out.println("This point is：" + x + ", " + y);

        Point<Double, String> p2 = new Point<Double, String>();
        p2.setX(25.4);
        p2.setY("东京180度");
        double m = p2.getX();
        String n = p2.getY();
        System.out.println("This point is：" + m + ", " + n);
    }
}

// 定义泛型类
class Point<T1, T2>{
    T1 x;
    T2 y;
    public T1 getX() {
        return x;
    }
    public void setX(T1 x) {
        this.x = x;
    }
    public T2 getY() {
        return y;
    }
    public void setY(T2 y) {
        this.y = y;
    }
}
```

特点：与普通类相比，泛型类的类名后多了<T1, T2>， T1, T2 是自定义的标识符，也是参数，用来传递数据的类型，而不是数据的值，我们称之为**类型参数**。 

类型参数（泛型参数）由尖括号包围，多个参数由逗号分隔，如<T1, T2>。 

```
T 代表一般的任何类。
E 代表 Element 的意思，或者 Exception 异常的意思。
K 代表 Key 的意思。
V 代表 Value 的意思，通常与 K 一起配合使用。
S 代表 Subtype 的意思，文章后面部分会讲解示意。
```

在真正运用泛型类时，要指出它具体的类型：

```
Point<Integer, Integer> p1 = new Point<Integer, Integer>();
```

和我们经常用到的Map，List接口非常的相似，它们是泛型接口罢了。



**泛型方法**

```java
public class Demo {
    public static void main(String[] args){
        // 实例化泛型类
        Point<Integer, Integer> p1 = new Point<Integer, Integer>();
        p1.setX(10);
        p1.setY(20);
        p1.printPoint(p1.getX(), p1.getY());

        Point<Double, String> p2 = new Point<Double, String>();
        p2.setX(25.4);
        p2.setY("东京180度");
        p2.printPoint(p2.getX(), p2.getY());
    }
}

// 定义泛型类
class Point<T1, T2>{
    T1 x;
    T2 y;
    public T1 getX() {
        return x;
    }
    public void setX(T1 x) {
        this.x = x;
    }
    public T2 getY() {
        return y;
    }
    public void setY(T2 y) {
        this.y = y;
    }

    // 定义泛型方法
    public <T1, T2> void printPoint(T1 x, T2 y){
        T1 m = x;
        T2 n = y;
        System.out.println("This point is：" + m + ", " + n);
    }
}
```

 定义了一个泛型方法 printPoint()，既有普通参数，也有类型参数，类型参数需要放在修饰符后面、返回值类型前面。一旦定义了类型参数，就可以在参数列表、方法体和返回值类型中使用了。 

和泛型类相比，泛型方法在调用时不需要指出明确的参数类型，会根据输入的参数编译器自动识别，和普通方法调用是一致的。



**泛型接口**

```java
public class Demo {
    public static void main(String arsg[]) {
        Info<String> obj = new InfoImp<String>("www.weixueyuan.net");
        System.out.println("Length Of String: " + obj.getVar().length());
    }
}

//定义泛型接口
interface Info<T> {
    public T getVar();
}

//实现接口
class InfoImp<T> implements Info<T> {
    private T var;

    // 定义泛型构造方法
    public InfoImp(T var) {
        this.setVar(var);
    }

    public void setVar(T var) {
        this.var = var;
    }

    public T getVar() {
        return this.var;
    }
}
```







通配符 **？**

 **通配符的出现是为了指定泛型中的类型范围**。 

- <?>被称作无限定的通配符。
- <? extends T>表示该通配符所代表的类型是 T 类型及其子类。 
- <? super T>表示该通配符所代表的类型是 T 类型及其父类。 



**类型擦除**

 Java中的泛型基本上都是在编译器这个层次来实现的。在生成的Java字节码中是不包含泛型中的类型信息的。使用泛型的时候加上的类型参数，会在编译器在编译的时候去掉。这个过程就称为类型擦除。 

 [(7条消息) Java 泛型，你了解类型擦除吗？_frank 的专栏-CSDN博客_java 泛型擦除](https://blog.csdn.net/briblue/article/details/76736356) 

```java
例如： 
List<String> l1 = new ArrayList<String>();
List<Integer> l2 = new ArrayList<Integer>();
		
System.out.println(l1.getClass() == l2.getClass());

结果:true List.class
```

​	List<String>和List<Integer>在编译阶段 泛型类型String和Integer都被擦除掉，但是到了JVM中字节码文件中它们都变成了原始类型List，通过反射获取运行时期的信息时，它们是一样的因此是true。

**补充**：JVM并不知道泛型，所有 泛型在编译阶段就已经被处理成了普通类和方法，JVM中没有泛型，只有普通类和方法。

JVM如何获取具体的类型呢？

答案就是强大 **反射机制**。



**String和Integer怎么办？**

答案：**泛型转义**

```java
public class Erasure <T>{
	T object;

	public Erasure(T object) {
		this.object = object;
	}
	
}
```

定义一个Erasure泛型类，同反射看看它在运行时信息

```java
Erasure<String> erasure = new Erasure<String>("hello");
Class eclz = erasure.getClass();
System.out.println("erasure class is:"+eclz.getName());

//结果：erasure class is: com.frank.test.Erasure
```

通过Class对象发现并不是**Erasure<T>**的泛型类，只是普通类Erasure



```java
Field[] fs = eclz.getDeclaredFields();
for ( Field f:fs) {
	System.out.println("Field name "+f.getName()+" type:"+f.getType().getName());
}
//结果：Field name object type:java.lang.Object
```

原本定义的类型参数T被擦除后，对应类型变成了Object类型（顶级父类），**是不是所有类型参数都会转换成Object类型呢？**

**答案是否定的**

配上通配符，指定类型参数的范围

```java
//String类型的子类
public class Erasure <T extends String>{
//	public class Erasure <T>{
	T object;

	public Erasure(T object) {
		this.object = object;
	}
	
}

```

再来看看对应T擦除后的类型

```java
Field name object type:java.lang.String
```

**结论**：在泛型类被类型擦除的时候，之前泛型类中的类型参数部分如果没有指定上限，如 `<T>`则会被转译成普通的 Object 类型，如果指定了上限如 `<T extends String>`则类型参数就被替换成类型上限。



增加一个add()泛型方法

```java
public class Erasure <T>{
	T object;

	public Erasure(T object) {
		this.object = object;
	}
	
	public void add(T object){
		
	}
	
}
```

add方法中类型参数没有指定具体类型，最后应该是被转义成Object类型。

```java
Erasure<String> erasure = new Erasure<String>("hello");
Class eclz = erasure.getClass();
System.out.println("erasure class is:"+eclz.getName());

Method[] methods = eclz.getDeclaredMethods();
for ( Method m:methods ){
	System.out.println(" method:"+m.toString());
}
// method:public void com.frank.test.Erasure.add(java.lang.Object)
```

如果通过反射来获取add方法，应该调用 `getDeclaredMethod("add",Object.class)`，在泛型类中类型参数T被擦除后，转义成了Object类型。



```java
public class Test2{  
    public static void main(String[] args) {  
        /*
        Number类是java.lang包下的一个抽象类，提供了将包装类型拆箱成基本类型的方法，所有基本类型（数据类型）的包装类型都继承了该抽象类，并且是final声明不可继承改变
        */
        /**不指定泛型的时候*/  
        int i=Test2.add(1, 2); //这两个参数都是Integer，所以T为Integer类型  
        Number f=Test2.add(1, 1.2);//这两个参数一个是Integer，以风格是Float，所以取同一父类的最小级，为Number  
        Object o=Test2.add(1, "asd");//这两个参数一个是Integer，以风格是String，所以取同一父类的最小级，为Object  
  
                /**指定泛型的时候*/  
        int a=Test2.<Integer>add(1, 2);//指定了Integer，所以只能为Integer类型或者其子类  
        int b=Test2.<Integer>add(1, 2.2);//编译错误，指定了Integer，不能为Float  
        Number c=Test2.<Number>add(1, 2.2); //指定为Number，所以可以为Integer和Float  
    }  
      
    //这是一个简单的泛型方法  
    public static <T> T add(T x,T y){  
        return y;  
    }  
}  
```

类型擦除的基本过程也比较简单，首先是找到用来替换类型参数的具体类。这个具体类一般是 Object。如果指定了类型参数的上界的话，则使用这个上界。把代码中的类型参数都替换成具体的类。





**类型擦除的局限性**

泛型擦除，是泛型能够与之前的java版本代码兼容共存原因，但也因此抹除了很多继承相关的特性。

通过泛型擦除的原理可以结合反射技术绕过被限制的操作。

例如：List<E>接口，实现类ArrayList

```java
public interface List<E> extends Collection<E>{
	
	 boolean add(E e);
}
```

通过反射调用add方法查看，会发现add方法中类型参数E已经转义成了Object类型

```java
boolean add(Object obj);
```

绕过编译器，利用反射，非正常操作

```java
public class ToolTest {


	public static void main(String[] args) {
		List<Integer> ls = new ArrayList<>();
		ls.add(23);
//		ls.add("text");
		try {
			Method method = ls.getClass().getDeclaredMethod("add",Object.class);
			
			
			method.invoke(ls,"test");
			method.invoke(ls,42.9f);
		} catch (NoSuchMethodException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} catch (SecurityException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} catch (IllegalAccessException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} catch (IllegalArgumentException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} catch (InvocationTargetException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
		
		for ( Object o: ls){
			System.out.println(o);
		}
	
	}

}

/*
23
test
42.9
*/
```

发现可以在数组中添加字符，不可思议，正常情况下不允许的。

------



## Java序列化

**保存对象及其状态到内存或磁盘中**

java平台允许在内存中创建可复用的对象，一般情况下，JVM在运行时对象才可能存在，对象的声明周期 <= JVM的生命周期。希望在JVM生命周期结束后，对象也能够存在，并且能够在未来被重新使用。



**序列化的对象以Byte数组保存**（**类中静态成员不会被序列化**）

java对象序列化，将其状态保存为一组字节，在未来，将这一组字节组装成对象(反序列化)，**对象序列化保存的是对象的状态，即它的成员变量。**



**序列化用户远程对象传输**

除了在持久化对象时会用到对象序列化之外，当使用 RMI(远程方法调用)，或在网络中传递对象时， 

都会用到对象序列化。



**Serializable接口实现对象序列化**

java中一个类实现java.io.Serializable 接口，那么它就可以被序列化。 



**ObjectOutputStream** **和** **ObjectInputStream** **对对象进行序列化及反序列化**



**序列化** **ID（private static final long serialVersionUID)**

情境：两个客户端 A 和 B 试图通过网络传递对象数据，A 端将对象 C 序列化为二进制数据再传给 B，B 反序列化得到 C。

问题：C 对象的全类路径假设为 com.inout.Test，在 A 和 B 端都有这么一个类文件，功能代码完全一致。也都实现了 Serializable 接口，但是反序列化时总是提示不成功。

虚拟机是否允许反序列化，不仅取决于类路径和功能代码是否一致，非常重要的一点是两个类的序列化 ID 是否一致。



**序列化并不保存静态变量** 

**序列化子父类说明** 

要想将父类对象也序列化，就需要让父类也实现 Serializable 接口。 



**Transient** **关键字阻止该变量被序列化到文件中**

- 在变量声明前加上 Transient 关键字，可以阻止该变量被序列化到文件中，在被反序列化后，transient 变量的值被设为初始值，如 int 型的是 0，对象型的是 null。 

- 一定程度保证序列化对象的数据安全。 

  服务器端给客户端发送序列化对象数据，对象中有一些数据是敏感的，比如密码字符串等，希望对该密码字段在序列化时，进行加密，而客户端如果拥有解密的密钥，只有在客户端进行反序列化时，才可以对密码进行读取。

------





## Java复制

将一个对象的引用复制给另一个对象，一共有三种方式。

- 直接赋值
- 浅拷贝
- 深拷贝



**直接赋值**

在 Java 中，A a1 = a2，A为对象，我们需要理解的是这实际上把a2所指向的对象的引用的拷贝赋值给a1，也就是说 a1 和 a2 指向的是同一个对象。因此，当 a1 变化的时候，a2 里面的成员变量也会跟着变化。



**浅拷贝（复制引用但不复制引用的对象）**

对基本数据类型进⾏值传递，对引⽤类型进⾏引⽤类型的拷⻉。



**深拷贝（复制对象和其应用对象）**

对基本数据类型进⾏值传递，对引⽤数据类型，创建⼀个新的对象，并复制其内容

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210711135323031.png" alt="image-20210711135323031" style="zoom:67%;" />

**序列化（深 clone 一中实现）** 

在 Java 语言里深复制一个对象，常常可以先使对象实现 Serializable 接口，然后把对象（实际上只是对象的一个拷贝）写到一个流里，再从流里读出来，便可以重建对象。

------





## Java集合

集合类存放于 Java.util 包中，主要有 3 种：**set(集）**、**list(列表包含 Queue）和 map(映射)**。

- Collection：Collection 是集合 List、Set、Queue 的最基本的接口。 
- Iterator：迭代器，可以通过迭代器遍历集合中的数据 
- Map：是映射表的基础接口

![image-20210711141733071](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210711141733071.png)

------

先来说说Collection接口中的集合

### **List**（对付顺序的好帮手）

Java 的 List 是非常常用的数据类型。List 是有序的 Collection。Java List 最常见的实现类： 

分别是 ArrayList、Vector 和 LinkedList。 

特点：存储的元素是有序的、可重复的。



**ArrayList（数组）**

ArrayList是最常用的List实现类。

- **线程安全**：ArrayList是不同步的，因此线程不安全。

- **底层数据结构**：使用**Object**数组实现。

- **插入和删除是否受元素位置影响**：ArrayList采用数组存储数据，做插入和删除元素操作时受元素位置的影响。

  例如：数组长度为n,如果在数组i的位置做插入或删除操作时，需要将插入i位置之后的元素都向后位移一位，或者将删除的元素i之后的元素都向前位移一位。

- **随机访问**：支持对元素进行快速随机访问。

- **内存占用**： ArrayList 的空 间浪费主要体现在在 list 列表的结尾会预留⼀定的容量空间。



**ArrayList的扩容机制**



了解一下ArrayList的内部构成

```java
//举出一部分扩容的重点
public class ArrayList<E> extends AbstractList<E>
        implements List<E>, RandomAccess, Cloneable, java.io.Serializable
{
    //默认容量位10
    private static final int DEFAULT_CAPACITY = 10;
    //定义一个空数组
    private static final Object[] EMPTY_ELEMENTDATA = {};
    //默认实例化一个空数组
    private static final Object[] DEFAULTCAPACITY_EMPTY_ELEMENTDATA = {};
    //存放在数组中的元素，不参与序列化
    transient Object[] elementData; 
    //数组的长度，此参数是数组中实际的参数，区别于elementData.length
	private int size;
    
    
    //ArrayList中一共有三个构造函数
    //默认无参构造函数，定义出的数组是一个空数组
    public ArrayList() {
        this.elementData = DEFAULTCAPACITY_EMPTY_ELEMENTDATA;
    }
    
    //用户指定数组大小的构造函数
    public ArrayList(int initialCapacity) {
        if (initialCapacity > 0) {
            //创建数组大小为initialCapacity的数组
            this.elementData = new Object[initialCapacity];
        } else if (initialCapacity == 0) {
            //创建一个空数组
            this.elementData = EMPTY_ELEMENTDATA;
        } else {
            throw new IllegalArgumentException("Illegal Capacity: "+
                                               initialCapacity);
        }
    }
    
    //包含特定集合元素的构造函数
    public ArrayList(Collection<? extends E> c) {
        elementData = c.toArray();
        if ((size = elementData.length) != 0) {
            // c.toArray might (incorrectly) not return Object[] (see 6260652)
            if (elementData.getClass() != Object[].class)
                //传入的集合转换为数组，然后通过Arrays.copyOf方法把集合中的元素拷贝到elementData中
                elementData = Arrays.copyOf(elementData, size, Object[].class);
        } else {
            // 创建空数组
            this.elementData = EMPTY_ELEMENTDATA;
        }
    }
}
```



从创建一个ArrayList数组开始

```java
    List<Integer> integers = new ArrayList<>();
    //此时创建的数组的长度为0，也就是一个空数组
    integers.add(1);
	//当向integers数组中加入第一个元素时，此时ArrayList的扩容就已经开始了。
```

机制：

```java
//ArrayList中调用add方法的源码 
public boolean add(E e) {
    //在向数组中加入新元素时，先判断这个数组的容量够不够装下下一个，因此调用ensureCapacityInternal方法
        ensureCapacityInternal(size + 1);  // Increments modCount!!
        elementData[size++] = e;
        return true;
}

//此时加入第一个元素1到数组中，此时size = 0 ，size+1 =1 ，也就是minCapacity = 1.
private void ensureCapacityInternal(int minCapacity) {
    ensureExplicitCapacity(calculateCapacity(elementData, minCapacity));
}


//此时minCapacity = 1，而DEFAULT_CAPACITY =10，因此最后minCapacity = 10
private static int calculateCapacity(Object[] elementData, int minCapacity) {
    //此时elementData 为空
    if (elementData == DEFAULTCAPACITY_EMPTY_ELEMENTDATA) {
        //通过比较默认容量(10)和最小扩容量，选取较大的一方，作为扩容的标准
        return Math.max(DEFAULT_CAPACITY, minCapacity);
    }
    return minCapacity;
}

//判断是否需要扩容
//此时，minCapacity = 10，数组还是空数组，因此elementData.length = 0，需要进行扩容
private void ensureExplicitCapacity(int minCapacity) {
    modCount++;

    //判断是否需要进行扩容
    if (minCapacity - elementData.length > 0)
        //扩容的方法(核心)
        grow(minCapacity);
}

//扩容方法
private void grow(int minCapacity) {
    //oldCapacity :旧容量
    int oldCapacity = elementData.length;
    //newCapacity：新容量
    //oldCapacity >> 1：算数右移，右移一位相当于除2操作，右移n位相当于除2的n次方,(如果该数为正，则高位补0，若为负数，则高位补1；)
    //十进制转成二进制进行位运算要比普通十进制除法运算要快的多.
    //这也是为什么ArrayList每次都是扩容1.5倍的关键。
    int newCapacity = oldCapacity + (oldCapacity >> 1);
    //如果新的扩容容量比最小需求容量还要小
    if (newCapacity - minCapacity < 0)
        //就把最小需求容量赋给新容量
        newCapacity = minCapacity;
    //判断新容量是否大于集合的最大容量（一般大不了）
    if (newCapacity - MAX_ARRAY_SIZE > 0)
        newCapacity = hugeCapacity(minCapacity);
    // 将扩容好的数组重新赋值
    elementData = Arrays.copyOf(elementData, newCapacity);
}

//此时，minCapacity = 10 ，oldCapacity =elementData.length = 0
//因此newCapacity = 0 ，所以 newCapacity = minCapacity = 10；
//完成了ArrayList的一次扩容，从0扩容到10 。

//一值不断向数组加入新的元素，当加入第11个元素时，ArrayList就需要进行扩容，
//minCapacity = 11 ，oldCapacity =elementData.length = 10，
//newCapacity = 10 +（10 >> 1） = 10 + 5 = 15;
//最后完成扩容的数组的容量从10变成了15，满足了下一次的新数组的加入
```



**LinkList（链表）**

- **线程安全**：LinkList是不同步的，因此线程不安全。

- **底层数据结构**：使用**双向链表** 数据结构实现。（JDK1.6 之前为循环链表，JDK1.7 取消了循环)

- **插入和删除是否受元素位置影响**：**对于** **add(E e)** **⽅法的插⼊，删除元素时间复杂度不受元素** 

  **位置的影响，近似** **O(1)**

- **随机访问**：很适合数据的动态插入和删除，随机访问和遍历速度比较慢。

- **内存占用**： LinkedList 的空间花费则体现在它的每⼀个元素都需要消耗⽐ ArrayList 更多的空间。

**双向链表和双向循环链表**

**双向链表：** 包含两个指针，⼀个 prev 指向前⼀个节点，⼀个 next 指向后⼀个节点。

![image-20210711155214913](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210711155214913.png)

![image-20210711155242130](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210711155242130.png)

**双向循环链表：** 最后⼀个节点的 next 指向 head，⽽ head 的 prev 指向最后⼀个节点，构成⼀ 

个环。

![image-20210711155314551](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210711155314551.png)



补充：**LinkedList插入和删除的效率一定比ArrayList高吗**

[面经手册 · 第8篇《LinkedList插入速度比ArrayList快？你确定吗？》 - bugstack虫洞栈](https://bugstack.cn/interview/2020/08/30/面经手册-第8篇-LinkedList插入速度比ArrayList快-你确定吗.html)

答案：**不一定**

**插入**

先从插入的方面来看

LinkedList中有很多插入的方法，这里就用**头插入**、**尾插入**、**中间插入**这三个方法来对比一下ArrayList和LinkedList

的插入效率。

![image-20210917102144692](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210917102144692.png)

**头插**

通过下面一张图清楚看到头插的过程

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210917102331620.png" alt="image-20210917102331620" style="zoom:67%;" />

1. ArrayList在进行头部插入时，需要把之后的元素都往后位移，如果遇到容量不够时还需要进行扩容
2. LinkedList在头插时，只需要把元素加入到头部即可，不需要考虑位移和扩容的因素

LinkedList中的头插的源码

```java
    public void addFirst(E e) {
        linkFirst(e);
    }

    /**
     * Pointer to first node.
     * Invariant: (first == null && last == null) ||
     *            (first.prev == null && first.item != null)
     */
    transient Node<E> first;
    /**
     * Pointer to last node.
     * Invariant: (first == null && last == null) ||
     *            (last.next == null && last.item != null)
     */
    transient Node<E> last;
    
        /**
     * Links e as first element.
     */
    private void linkFirst(E e) {
        //原链表的头节点
        final Node<E> f = first;
        //需要插入的新元素：x
        final Node<E> newNode = new Node<>(null, e, f);
        //把新元素作为新节点
        first = newNode;
        if (f == null)
            //不存在则把头插节点作为最后一个节点
            last = newNode;
        else
            //f不为空,将新的头节点和原头节点相连
            f.prev = newNode;
        //大小+1
        size++;
        //元素数量
        modCount++;
    }
```



测试：

```java
    @Test
    public void testAddFirstLinkedList(){
        System.out.println("LinkedList");
        LinkedList<Integer> linkedList = new LinkedList<>();
        long startTime = System.currentTimeMillis();

        //这里测试一百万和一千万的数据，对比消耗时间
        for (int i = 0; i < 1000000 ; i++) {
            linkedList.addFirst(i);
        }

        System.out.println(String.format("100万消耗时间:" + (System.currentTimeMillis() - startTime), TimeUnit.SECONDS));

        LinkedList<Integer> linkedList1 = new LinkedList<>();
        long startTime1 = System.currentTimeMillis();

        //这里测试一百万和一千万的数据，对比消耗时间
        for (int i = 0; i < 10000000 ; i++) {
            linkedList1.addFirst(i);
        }

        System.out.println(String.format("1000万消耗时间:" + (System.currentTimeMillis() - startTime1), TimeUnit.SECONDS));

    }

```

```java
    @Test
    public void testAddFirstArrayList(){
        System.out.println("ArrayList");
        ArrayList<Integer> list = new ArrayList<>();
        long startTime = System.currentTimeMillis();

		//ArrayList这里只测100万，1000万数据太大，效率太慢
        for (int i = 0; i < 1000000 ; i++) {
            list.add(0,i);
        }

        System.out.println(String.format("100万消耗时间:" + (System.currentTimeMillis() - startTime), TimeUnit.SECONDS));
    }


ArrayList
100万消耗时间:172858  (单位：毫秒)
LinkedList
100万消耗时间:47
1000万消耗时间:10299
```

结论：**从上面两个数据测试就可以看出，头插情况下，LinkedList效率远远高于ArrayList效率。**





**尾插**

上图

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210917104556149.png" alt="image-20210917104556149" style="zoom:67%;" />

1. ArrayList中尾插不需要在移动数据，耗时点在于扩容，需要拷贝迁移
2. LinkedList中尾插时，耗时点在于对象的创建上

源码：

```java
    /**
     * Links e as last element.
     */
    void linkLast(E e) {
        final Node<E> l = last;
        final Node<E> newNode = new Node<>(l, e, null);
        last = newNode;
        if (l == null)
            first = newNode;
        else
            l.next = newNode;
        size++;
        modCount++;
    }
```

测试：

```java
    @Test
    public void testAddFirstLinkedList(){
        System.out.println("LinkedList");
        LinkedList<Integer> linkedList = new LinkedList<>();
        long startTime = System.currentTimeMillis();

        //这里测试一百万和一千万的数据，对比消耗时间
        for (int i = 0; i < 1000000 ; i++) {
            linkedList.addLast(i);
        }

        System.out.println(String.format("100万消耗时间:" + (System.currentTimeMillis() - startTime), TimeUnit.SECONDS));

        LinkedList<Integer> linkedList1 = new LinkedList<>();
        long startTime1 = System.currentTimeMillis();

        //这里测试一百万和一千万的数据，对比消耗时间
        for (int i = 0; i < 10000000 ; i++) {
            linkedList1.addLast(i);
        }

        System.out.println(String.format("1000万消耗时间:" + (System.currentTimeMillis() - startTime1), TimeUnit.SECONDS));

    }

```

```java
    @Test
    public void testAddFirstArrayList(){
        System.out.println("ArrayList");
        ArrayList<Integer> list = new ArrayList<>();
        long startTime = System.currentTimeMillis();

        //这里测试一百万和一千万的数据，对比消耗时间
        for (int i = 0; i < 1000000 ; i++) {
            list.add(i);
        }

        System.out.println(String.format("100万消耗时间:" + (System.currentTimeMillis() - startTime), TimeUnit.SECONDS));

        ArrayList<Integer> list1 = new ArrayList<>();
        long startTime1 = System.currentTimeMillis();

        //这里测试一百万和一千万的数据，对比消耗时间
        for (int i = 0; i < 10000000 ; i++) {
            list1.add(i);
        }

        System.out.println(String.format("1000万消耗时间:" + (System.currentTimeMillis() - startTime1), TimeUnit.SECONDS));

    }

LinkedList
100万消耗时间:41 (单位：毫秒)
1000万消耗时间:9950
    
ArrayList
100万消耗时间:34
1000万消耗时间:4886
```

结论：**在数据比较庞大的情况下，尾插中ArrayList的效率就比LinkedList效率高，因为LinkedList每次都要创建一个新的对象**



**中间插入**

上图

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210917105816944.png" alt="image-20210917105816944" style="zoom:67%;" />

1. ArrayList中的中间插入操作，当知道要插入的位置时定位的时间复杂度为O(1),比较耗时的点在于数据位移和扩容
2. LinkedList的中间插入操作，耗时点在于定位需要插入的位置时间复杂度O(n)



测试：

```java
    @Test
    public void testAddFirstArrayList(){
        System.out.println("ArrayList");
        ArrayList<Integer> list = new ArrayList<>();
        long startTime = System.currentTimeMillis();

        //中间插入：1000000
        for (int i = 0; i < 1000000 ; i++) {
            list.add(list.size() >> 1 , i);
        }

        System.out.println(String.format("100万消耗时间:" + (System.currentTimeMillis() - startTime), TimeUnit.SECONDS));


    }
    
    ArrayList
100万消耗时间:60460
    
    LinkedList
100万消耗时间:1527501
```

```
    @Test
    public void testAddFirstLinkedList(){
        System.out.println("LinkedList");
        LinkedList<Integer> linkedList = new LinkedList<>();
        long startTime = System.currentTimeMillis();

        //中间插入：10万
        for (int i = 0; i < 100000 ; i++) {
            linkedList.add(linkedList.size(),i);
        }

        System.out.println(String.format("10万消耗时间:" + (System.currentTimeMillis() - startTime), TimeUnit.SECONDS));
    }
```

结论：**在进行中间插入时，ArrayList的效率要高于LinkedList的效率**



**总结：**

ArrayList和LinkedList都有自己的应用场景，要根据具体的场景选择合适的集合。如果是在集合的首部插入和删除元素，可以选择LinkedList，因为它的效率高于ArrayList，它提供了addFirst、addLast、removeFirst等等这些方法的时间复杂度都是O(1)。

因此不是LinkedList插入和删除的效率就一定比ArrayList高，具体还是要看数据量的大小。



RandomAccess接口

```java
public interface RandomAccess {
}
// RandomAccess 接⼝中什么都没有定义。所以，在我看来
//RandomAccess 接⼝不过是⼀个标识罢了。标识什么？ 标识实现这个接⼝的类具有随机访问功能
/*
ArrayList 实现了 RandomAccess 接⼝， ⽽ LinkedList 没有实现。为什么呢？我觉得还是
和底层数据结构有关！ ArrayList 底层是数组，⽽ LinkedList 底层是链表。数组天然⽀持随机
访问，时间复杂度为 O（1），所以称为快速随机访问。链表需要遍历到特定位置才能访问特定位置的
元素，时间复杂度为 O（n），所以不⽀持快速随机访问。 ArrayList 实现了 RandomAccess 接
⼝，就表明了他具有快速随机访问功能。
*/
```

**总结⼀下** **list** **的遍历方式选择：**

实现了 RandomAccess 接⼝的list，优先选择普通 for 循环 ，其次 foreach

未实现 RandomAccess 接⼝的list，优先选择iterator遍历（foreach遍历底层也是通过iterator实现的,），⼤size的数据，千万不要使⽤普通for循环





**Vector（数组实现、线程同步）** 

Vector 与 ArrayList 一样，也是通过数组实现的，不同的是它支持线程的同步，即某一时刻只有一 

个线程能够写 Vector，避免多线程同时写而引起的不一致性，但实现同步需要很高的花费，因此， 

访问它比访问 ArrayList 慢。

补充：Stack是Vector的子类，它同样是线程安全的

------



### **Set(注重独一无二的性质)**

集合用于存储无序(存入和取出的顺序不一定相同)元素，值不能重复。对象的相等性本质是对象 hashCode 值（java 是依据对象的内存地址计算出的此序号）判断的**，如果想要让两个不同的对象视为相等的，就必须覆盖 Object 的 hashCode 方法和 equals 方法。**



**HashSet（Hash表无序，唯⼀）**

哈希表中存放的是哈希值。HashSet 存储元素的顺序并不是按照存入时的顺序（和 List 显然不 

同） 而是按照哈希值来存的所以取数据也是按照哈希值取得。元素的哈希值是通过元素的 

hashcode 方法来获取的, HashSet 首先判断两个元素的哈希值，如果哈希值一样，接着会比较 

equals 方法 如果 equls 结果为 true ，HashSet 就视为同一个元素。如果 equals 为 false 就不是 

同一个元素。

哈希值相同 equals 为 false 的元素是怎么存储呢,就是在同样的哈希值下顺延（可以认为哈希值相 

同的元素放在一个哈希桶中）。也就是哈希一样的存一列。下图表示 hashCode 值不相同的情 

况；表示 hashCode 值相同，但 equals 不相同的情况。

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210711161502112.png" alt="image-20210711161502112" style="zoom:67%;" />

HashSet 通过 hashCode 值来确定元素在内存中的位置。一个 hashCode 位置上可以存放多个元 

素。 



**TreeSet（二叉树）（有序，唯⼀）**

TreeSet()是使用**红黑树**的原理对新 add()的对象按照指定的顺序排序（升序、降序），每增加一个对象都会进行排序，将对象插入的二叉树指定的位置。 

Integer 和 String 对象都可以进行默认的 TreeSet 排序(**Integer，String类都实现了Compareable接口**)，而自定义类的对象是不可以的，自己定义的类必须实现 Comparable 接口，并且覆写相应的 compareTo()函数，才可以正常使用。

在覆写 compare()函数时，要返回相应的值才能使 TreeSet 按照一定的规则来排序 

比较此对象与指定对象的顺序。如果该对象小于、等于或大于指定对象，则分别返回负整数、零或正整数。 





**Compareable和Comparetor的区别**

 [(7条消息) 详解Java中Comparable和Comparator接口的区别_牵着蜗牛_去散步-CSDN博客](https://blog.csdn.net/u010859650/article/details/85009595?utm_medium=distribute.pc_relevant.none-task-blog-2~default~BlogCommendFromMachineLearnPai2~default-4.control&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2~default~BlogCommendFromMachineLearnPai2~default-4.control) 

**Compareable**：是排序接口

若定义的类实现了Compareable接口，也就意味着该类支持排序， 此外，“实现Comparable接口的类的对象”可以用作“有序映射(如TreeMap)”中的键或“有序集合(TreeSet)”中的元素 。

Compareable接口方法： **x.compareTo(y)** 

规则：x > y ,返回正整数，x < y,返回负数，x=y ，返回 0。



**Comparetor**：是比较器接口。

若定义的某个类需要进行排序，而该类本身不支持排序(没有实现Compareable接口)，那么就需要通过建议该类的比较器来实现排序。

Comparetor接口方法：  **compare(T o1, T o2)** 

规则：如：01 > 02 , 返回正整数； 01 < 02 ,返回负数； 01 = 02，返回0。 **返回正数，零和负数分别代表大于，等于和小于。** 



例子：

```java
/*
这里自定义的类实现了Comparable接口并重写了compareTo方法
*/
public class Student implements Comparable<Student>{

    private int age ;
    private int name ;

    public Student(int age, int name) {
        this.age = age;
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public int getName() {
        return name;
    }

    public void setName(int name) {
        this.name = name;
    }



    @Override
    public int compareTo(Student s) {
        if (this.age > s.getAge()){
            return 1;
        }else if (this.age < s.getAge()){
            return -1;
        }
        return 0;
    }
}


public class StudentTest {

    public static void main(String[] args) {
        List<Student> students = new ArrayList();
        Student student = new Student("张三",80);
        Student student1 = new Student("张二",15);
        Student student2 = new Student("张一",20);
        Student student3 = new Student("张四",33);
        students.add(student);
        students.add(student1);
        students.add(student2);
        students.add(student3);
        comparable(students);
        comparator(students);
    }

    private static void comparator(List<Student> students) {
        System.out.printf("未排序前的顺序,%s\n", students);
        /*
        lemd表达式：Collections.sort(students, (Comparator<Student>)(o1,o2)-> {
        	 if (o1.getAge() > o2.getAge()){
                    return 1;
                }else if (o1.getAge() < o2.getAge()){
                    return -1;
                }
                return 0;
        }
        */
        Collections.sort(students, new Comparator<Student>() {
            @Override
            public int compare(Student o1, Student o2) {
                if (o1.getAge() > o2.getAge()){
                    return 1;
                }else if (o1.getAge() < o2.getAge()){
                    return -1;
                }
                return 0;
            }
        });
        System.out.printf("按单价大小排序后的顺序,%s\n", students);
    }

    private static void comparable(List<Student> students) {
        System.out.printf("未排序前的顺序,%s\n", students);
        Collections.sort(students);
        System.out.printf("按年龄大小排序后的顺序,%s\n", students);
    }
}

结果：
/*
未排序前的顺序,[姓名张三   年龄80, 姓名张二   年龄15, 姓名张一   年龄20, 姓名张四   年龄33]
按年龄大小排序后的顺序,[姓名张三   年龄80, 姓名张四   年龄33, 姓名张一   年龄20, 姓名张二   年龄15]
未排序前的顺序,[姓名张三   年龄80, 姓名张四   年龄33, 姓名张一   年龄20, 姓名张二   年龄15]
按单价大小排序后的顺序,[姓名张二   年龄15, 姓名张一   年龄20, 姓名张四   年龄33, 姓名张三   年龄80]
*/
```



**LinkHashSet（HashSet+LinkedHashMap）**

对于 LinkedHashSet 而言，它继承与 HashSet、又基于 LinkedHashMap 来实现的。 

LinkedHashSet 底层使用 LinkedHashMap 来保存所有元素，它继承与 HashSet，其所有的方法 

操作上又与 HashSet 相同。



------



### **Map(⽤Key来搜索的专家)**

形式：key-value  键值对

key是唯一的，不可重复的，无序的。

value是可重复的，无序的。



**HashMap（数组+链表+红黑树）** 

HashMap根据键的hashCode值存储数据，通过键可以快速找到对应的值，因此查询的速度非常快。

HashMap允许键的值为null，但最多只能允许一条，而允许多条记录的值为null。

HashMap是非线程安全的，在多个线程操作同一个HashMap时会导致数据错乱。



[红黑树)](https://juejin.cn/post/6844903519632228365#comment)

**红黑树**：简单说一下自己的理解，说实话

了解红黑树之前需要先了解一下**二叉搜索树**。



二叉搜索树：

左子树上所有的节点的值均小于根节点的值。

右子树上所有节点的值均大于根节点的值。

左、右子树又分别为二叉搜索树。



二叉搜索树有缺点：

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210821191952651.png" alt="image-20210821191952651" style="zoom:67%;" />

上面是一个二叉搜索树，我要加入3、4、5、6、7这四个结点，会变成如下情况

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210821192031866.png" alt="image-20210821192031866" style="zoom:67%;" />

这样的结构导致查找的性能大大折扣，递归的过程变成的冗长。

红黑树就是在这里情况诞生出来的，解决这样的问题。



红黑树是一种**自平衡**的二叉搜索树。

红黑树是在二叉搜索树的基础上，多了一些特性：（有黑色和红色节点）

1. 根节点是黑色节点
2. 所有的叶子节点是黑色节点（NULL空节点）
3. 节点是黑色或红色节点
4. 若节点是红色节点那么，它的子节点都为黑色节点(不存在连续的红色节点)
5. 任意一节点到它每个叶子节点的路径上的黑色节点的数目相同

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210821192115360.png" alt="image-20210821192115360" style="zoom:67%;" />

不满足上面的特性都会导致红黑树失衡。



保持红黑树的平衡方法：**变色或旋转**

**变色**

以上面的那个图为例子，去当中的一部分来说明一下变色

加入一个新的节点21，此节点是红色，不满足红黑树条件，下面通过变色

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/1602b60192dd75db~tplv-t2oaga2asx-watermark.awebp" alt="img" style="zoom: 67%;" />



将节点22变成黑色，虽然满足了不连续为红色节点的条件，这样的变色还不能满足红黑树的条件，破坏了最后一个条件，黑色节点数目不一致。

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210821192144835.png" alt="image-20210821192144835" style="zoom:67%;" />



将25节点变成红色节点，条件4无法满足

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210821192202495.png" alt="image-20210821192202495" style="zoom:67%;" />

接着将27节点变成黑色节点



<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210821192230765.png" alt="image-20210821192230765" style="zoom:67%;" />







**旋转**

**左旋转**

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210818144322447.png" alt="image-20210818144322447" style="zoom: 67%;" />

**右旋转**

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210818145238345.png" alt="image-20210818145238345" style="zoom: 67%;" />

了解完旋转后，根据上面变色后的内容接着说，整个红黑树如何保证平衡的。

变色后，如下图，发现17和25节点破坏了**条件4**，先想想使用变色？

把17变成黑色？好像不太行，破坏了**条件5**。

把17变成黑色，把13变成红色？也不行，破坏了条件2。

到这里说明相通过变色来保持平衡已经行不通，接下来就轮到旋转登场，大展身手。

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210821192253226.png" alt="image-20210821192253226" style="zoom:67%;" />



注意了：这里以17为中心节点，和13节点做**左旋转运行**，想想上面的左旋，

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210821192722043.png" alt="image-20210821192722043" style="zoom:67%;" />

结果如下：17成为了根节点，13成为了17的左子节点，15成为了13的右子节点，其他保持不变。

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210821192750840.png" alt="image-20210821192750840" style="zoom:67%;" />

把17节点变色成黑色

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210821192819800.png" alt="image-20210821192819800" style="zoom:67%;" />

观察是否平衡，发现 17 -> 8 -> 6 ->比其他的要多一个节点，不行，变色能解决吗？好像不行，还是通过旋转来吧。

接下来通过右旋转，想想右旋转：以8为中心，和13做**右旋**运动

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/1602b602bcfa03b3~tplv-t2oaga2asx-watermark.awebp" alt="img" style="zoom:67%;" />

结果如下：13成为了8的右节点，8成为了13的根节点，11节点成为了13节点的左子节

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210821192849408.png" alt="image-20210821192849408" style="zoom:67%;" />

再进行一次变色，11节点变成黑色。

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/1602b602b45e1d3c~tplv-t2oaga2asx-watermark.awebp" alt="img" style="zoom:67%;" />

观察是否平衡？

终于平衡，几经波折，最终平衡。

这里把红黑树搞懂了，下面说hashMap岂不是游刃有余。





**HashMap底层实现**

存储结构：

在java1.8之前，HashMap采用的是**数组+链表**的形式存储键值对，而在java1.8之后，HashMap中增加了红黑树，变成了**数组+链表+红黑树**的数据结构。

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210712133612262.png" alt="image-20210712133612262" style="zoom:67%;" />

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210712133622884.png" alt="image-20210712133622884" style="zoom: 67%;" />

先从HashMap的源码开始

```java
// 序列化自动生成的一个码，用来在正反序列化中验证版本一致性。
private static final long serialVersionUID = 362498820763181265L;   

// 默认的初始容量 1 * 2^4 = 16
//算数左移4位，相当于 * 2的四次方，这也是HashMap默认初始大小为16的原因
static final int DEFAULT_INITIAL_CAPACITY = 1 << 4;

// 最大容量 1 * 2^30
static final int MAXIMUM_CAPACITY = 1 << 30;

// 默认的加载因子 0.75
static final float DEFAULT_LOAD_FACTOR = 0.75f;

// 桶的树化阈值，当桶(bucket)上的结点数大于这个值时会转成红黑树，
// 也就是上面提到的长度大于阈值（默认为8）时，将链表转化为红黑树
static final int TREEIFY_THRESHOLD = 8;

// 桶的链表还原阈值，当桶(bucket)上的结点数小于这个值时树转链表
// 一个道理
static final int UNTREEIFY_THRESHOLD = 6;

// 最小树形化容量阈值，当哈希表中的容量 > 该值时，才允许树形化链表 
// 否则，若桶内元素太多时，则直接扩容，而不是树形化
// 为了避免进行扩容和树形化选择的冲突，这个值不能小于 4 * TREEIFY_THRESHOLD
static final int MIN_TREEIFY_CAPACITY = 64;

// 存储元素的数组，总是2的幂次倍
transient Node<k,v>[] table; 

// 存放具体元素的集
transient Set<map.entry<k,v>> entrySet;

// 存放元素的个数（不是数组的长度）
transient int size;

// 扩容和修改的计数变量
transient int modCount;   

// 临界值 当实际大小(容量*填充因子)超过临界值时，会进行扩容
int threshold;

// 加载因子
final float loadFactor;
```



Node<k,v>[] table字段，是HashMap最主体的部分，它就是哈希表数组。

```java
static class Node<K,V> implements Map.Entry<K,V> {
        final int hash;    //用来定位数组索引位置
        final K key;
        V value;
        Node<K,V> next;   //链表的下一个node

        Node(int hash, K key, V value, Node<K,V> next) { ... }
        public final K getKey(){ ... }
        public final V getValue() { ... }
        public final String toString() { ... }
        public final int hashCode() { ... }
        public final V setValue(V newValue) { ... }
        public final boolean equals(Object o) { ... }
}
//Node是HashMap的一个内部类，实现了 Map.Entry<K,V>，存储键值对。
```



HashMap使用哈希表来存储数据，这样的存储结构也会因为多个数据存放在同一位置而产生冲突，这就是哈希冲突。

通常解决冲突办法有：**拉链法和开放地址发**

拉链法：

在哈希表中每个数组的后面加上一个链表结构，这样不同的数据存放在相同的位置，只要加入到链表中就可以了，

这也是为什么HashMap是数组+链表的数据结构。

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210712140136065.png" alt="image-20210712140136065" style="zoom:50%;" />

开放地址法（线性探测法）：

一定要保证哈希表的大小远大于数据量。 我们需要依靠哈希表中的空位来解决碰撞问题。

例如冲突的位置，放了小李，那么就向下找一个空位放置小王的信息。所以要求tableSize一定要大于dataSize ，要不然哈希表上就没有空置的位置来存放 冲突的数据了。

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210712140310392.png" alt="image-20210712140310392" style="zoom:50%;" />



举例说明：新元素加入HashMap中的过程。

```java
    Map<String,String> map = new HashMap<>();
    map.put("华为","小美");

//程序将通过'华为'这个key的hashCode()方法(之前介绍过hashCode方法)得到hashCode值，通过Hash函数(扰动函数)以及后续运算（高位运算和取模运算）来定位该数据存放在哈希表中的位置。
//如果说该数据的存放位置已经被其他数据存放了，那就产生了之前所说的冲突。通过拉链法或开放地址法解决
```



如果想要哈希冲突发生的概率降低，一般通过扩容机制和提升Hash函数的功能。



[参考](https://zhuanlan.zhihu.com/p/21673805)

先说一说Hash函数（扰动函数）

**确定哈希表数组索引位置**

对HashMap做添加、删除、查询操作时候，首先第一步就是查询位置，而HashMap查询位置的步骤分为三部。

- 通过数据的key的hashCode（）**获取该对象的hashCode值**
- 通过Hash函数（扰动函数）计算出hash值(**高位运算+异或操作**)
- 通过**取模运算**得出该数据位于哈希桶数组的位置

尽可能的让哈希表中的数据分布的均匀，这样哈希冲突的概率就会降低，尽量不要将数据加入到链表中，因为会增加查询的负担。

先来看看**Hash函数（扰动函数）**

```java
static final int hash(Object key) {   //jdk1.8 & jdk1.7
     int h;
     // h = key.hashCode() 为第一步 取hashCode值
     // h ^ (h >>> 16)  为第二步 高位参与运算，异或操作
    // 无符号右移，高位补0
     return (key == null) ? 0 : (h = key.hashCode()) ^ (h >>> 16);
}
static int indexFor(int h, int length) {  //jdk1.7的源码，jdk1.8没有这个方法，但是实现原理一样的
     return h & (length-1);  //第三步 取模运算
}
```

举例说明运算的过程：

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210712150456316.png" alt="image-20210712150456316" style="zoom:67%;" />

重点说明一下：

```java
 //length:数组的长度 , hash :hash值 
//计算位于数组的索引的位置
 hash & (length-1) 和 hash % length
```

HashMap底层数组长度总是保持2的幂次(后面介绍原因)，取余（%）等价于（length-1）&的操作前提是**length是2的幂次**，其次是&比%具有更高的效率。



**HashMap长度为什么一定是2的幂次**

 [(7条消息) 面试官：为什么HashMap的长度一定是2的次幂？_ju_362204801的博客-CSDN博客](https://caoju.blog.csdn.net/article/details/116293664) 

HashMap长度为2的幂次作用主要体现在：确定数据在哈希表中的位置和HashMap的扩容

现在说说**确定数据在哈希表中的位置**中所产生的作用

四步确定位置：获取hashCode、 \>>>无符号右移、^异或、&与 

**Hash函数中高位运算和取模运算不仅仅是为了找出数据在哈希桶数组中的位置，更为了让数据在哈希桶数组中分布的更加均匀，减少哈希冲突，提高效率，数组长度为2的幂次更是起到了推波助澜的作用。**

下面举一个例子来说明：

如果length长度不是2的次幂，比如是奇数，调用取模方法（hash & (length-1)），最后得到二进制结果最后一位一定是0，

```java
 length = 5;
 length - 1 = 4 ;                       
  1111
 &0100  = 0100 =4 
 
  length = 7;
 length - 1 = 6 ;
  1111
 &0110  = 0110 =6
```

那么对于十进制来说，只能定位到偶数，而奇数无法定位到。数组中可能有一半的空间别浪费掉。

如果length长度是偶数，调用取模方法（hash & (length-1)），取一个length = 6的树， 那参与&运算的就是5
的二进制  00000000 00000000 00000000 00000101 ，和5与二进制第二位始终为0，对应到数组索引2或3取不到。虽然2的幂次可能取不到所有的位置，但是相比于奇数来说，2的幂次范围更广，更适合。

```java
/**
 * 返回一个大于输入参数，且最接近的，2的整数次幂的数
 * 只是一个初始化内容，创建哈希表时，会再重新赋值
 保证了length长度为2的幂次
 */
static final int tableSizeFor(int cap) {
    int n = cap - 1;
    n |= n >>> 1;
    n |= n >>> 2;
    n |= n >>> 4;
    n |= n >>> 8;
    n |= n >>> 16;
    return (n < 0) ? 1 : (n >= MAXIMUM_CAPACITY) ? MAXIMUM_CAPACITY : n + 1;
}
```



**HashMap的长度一定是2的次幂，还有另外一个原因，那就是在扩容迁移的时候不需要再重新通过哈希
定位新的位置了。扩容后，元素新的位置，要么在原脚标位，要么在原脚标位+扩容长度这么一个位置。**



```java
比如扩容前长度是8，扩容后长度是16
 
第一种情况：
扩容前：
 00000000 00000000 00000000 00000101
&00000000 00000000 00000000 00000111     8-1=7
-------------------------------------
                                 101   ===== 5 原来脚标位是5
 
扩容后：                       
 00000000 00000000 00000000 00000101
&00000000 00000000 00000000 00001111    16-1=15
-------------------------------------
                                 101   ===== 5 扩容后脚标位是5（原脚标位）java
第二种情况：
扩容前：
 00000000 00000000 00000000 00001101
&00000000 00000000 00000000 00000111     8-1=7
-------------------------------------
                                 101   ===== 5 原来脚标位是5
                            
扩容后：                            
 00000000 00000000 00000000 00001101
&00000000 00000000 00000000 00001111    16-1=15
-------------------------------------
                                1101   ===== 13 扩容后脚标位是13（原脚标位+扩容长度）
```





HashMap中put方法

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/58e67eae921e4b431782c07444af824e_r.jpg" style="zoom: 50%;" />

1. 加入新的数据判断table是否为空或者为null，为空执行**resize()**进行扩容
2. 根据键值key计算hash值位于哈希桶数组的位置，如果当前table[i]为空，直接建立新节点条件，跳转到步骤6，如果table[i]不为空，跳转到步骤3
3. 判断table[i]的首位key是否和传入的key一致，若一致(hashCode和equals)直接覆盖value，否则跳转到步骤4，
4. 判断table[i]是否为treeNode(**红黑树**)，若是则将键值对插入到红黑树中，若不是则跳转步骤5
5. 遍历table[i],判断当前链表的长度，若长度**大于8，还要HashMap中的数组长度大于64，将链表树化成红黑树。也就是如果HashMap长度小于64，链表长度大于8是不会转化为红黑树的，而是直接扩容。**（**补充：避免单条链表过长而影响查询效率，提高查询效率**）在红黑树中插入键值对，否则在链表中插入键值对，判断链表中是否存在和key一致的数据，有就直接覆盖value。
6. 插入成功后，判断size(键值对数目)是否大于**阈值(threshold)**,若大于进行扩容

```java
 1 public V put(K key, V value) {
 2     // 对key的hashCode()做hash
 3     return putVal(hash(key), key, value, false, true);
 4 }
 5 
 6 final V putVal(int hash, K key, V value, boolean onlyIfAbsent,
 7                boolean evict) {
 8     Node<K,V>[] tab; Node<K,V> p; int n, i;
 9     // 步骤①：tab为空则创建
10     if ((tab = table) == null || (n = tab.length) == 0)
11         n = (tab = resize()).length;
12     // 步骤②：计算index，并对null做处理 
13     if ((p = tab[i = (n - 1) & hash]) == null) 
14         tab[i] = newNode(hash, key, value, null);
15     else {
16         Node<K,V> e; K k;
17         // 步骤③：节点key存在，直接覆盖value
18         if (p.hash == hash &&
19             ((k = p.key) == key || (key != null && key.equals(k))))
20             e = p;
21         // 步骤④：判断该链为红黑树
22         else if (p instanceof TreeNode)
23             e = ((TreeNode<K,V>)p).putTreeVal(this, tab, hash, key, value);
24         // 步骤⑤：该链为链表
25         else {
26             for (int binCount = 0; ; ++binCount) {
27                 if ((e = p.next) == null) {
28                     p.next = newNode(hash, key,value,null);
                        //链表长度大于8转换为红黑树进行处理
29                     if (binCount >= TREEIFY_THRESHOLD - 1) // -1 for 1st  
30                         treeifyBin(tab, hash);
31                     break;
32                 }
                    // key已经存在直接覆盖value
33                 if (e.hash == hash &&
34                     ((k = e.key) == key || (key != null && key.equals(k))))                                          break;
36                 p = e;
37             }
38         }
39         
40         if (e != null) { // existing mapping for key
41             V oldValue = e.value;
42             if (!onlyIfAbsent || oldValue == null)
43                 e.value = value;
44             afterNodeAccess(e);
45             return oldValue;
46         }
47     }

48     ++modCount;
49     // 步骤⑥：超过最大容量 就扩容
50     if (++size > threshold)
51         resize();
52     afterNodeInsertion(evict);
53     return null;
54 }
```



**扩容机制**

- 当put时发现table未初始化时，进行初始化扩容
- 当put加入节点后，发现size（键值对数量）>threshold时，进行扩容

在说扩容之前，说一说一些重要的参数。

```java
  	int threshold;             // 所能容纳的key-value对极限 
     final float loadFactor;    // 负载因子
     int modCount;  
     int size;

/*
threshold:临界值（阈值）
当数组实际大小（容量 * 加载因子，即：threshold = capacity * loadFactor）超过临界值时，会进行扩容。
也是HashMap进行扩容的一个重要的判断依据

loadFactor：加载因子（默认为0.75）
如果加载因子过高，空间利用率提高，但是会使得哈希冲突的概率增加；如果加载因子过低，会频繁扩容，哈希冲突概率降低，但是会使得空间利用率变低


size：是HashMap中实际存在的键值对数量

modCount：记录HashMap内部结构发生变化的次数，主要用于迭代的快速失败
*/
```



```java
 1 //jdk1.7
     
     void resize(int newCapacity) {   //传入新的容量
 2     Entry[] oldTable = table;    //引用扩容前的Entry数组
 3     int oldCapacity = oldTable.length;         
 4     if (oldCapacity == MAXIMUM_CAPACITY) {  //扩容前的数组大小如果已经达到最大(2^30)了
 5         threshold = Integer.MAX_VALUE; //修改阈值为int的最大值(2^31-1)，这样以后就不会扩容了
 6         return;
 7     }
 8  
 9     Entry[] newTable = new Entry[newCapacity];  //初始化一个新的Entry数组
10     transfer(newTable);                         //！！将数据转移到新的Entry数组里
11     table = newTable;                           //HashMap的table属性引用新的Entry数组
12     threshold = (int)(newCapacity * loadFactor);//修改阈值
13 }

//将原有Entry数组的元素拷贝到新的Entry数组里。
 1 void transfer(Entry[] newTable) {
 2     Entry[] src = table;                   //src引用了旧的Entry数组
 3     int newCapacity = newTable.length;
 4     for (int j = 0; j < src.length; j++) { //遍历旧的Entry数组
 5         Entry<K,V> e = src[j];             //取得旧Entry数组的每个元素
 6         if (e != null) {
 7             src[j] = null;//释放旧Entry数组的对象引用（for循环后，旧的Entry数组不再引用任何对象）
     			//获取当前哈希桶数组中位于同一链表中的元素，
 8             do {
     				//拿到下一个元素
 9                 Entry<K,V> next = e.next;
10                 int i = indexFor(e.hash, newCapacity); //！！重新计算每个元素在新数组中的位置
11                 e.next = newTable[i]; //标记[1]
12                 newTable[i] = e;      //将元素放在数组上
13                 e = next;             //访问下一个Entry链上的元素
14             } while (e != null);
15         }
16     }
17 }
```

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210712163350709.png" alt="image-20210712163350709" style="zoom: 80%;" />

jdk1.7每次扩容，都是将原数组中的数据放入到扩容后的新数组中，每次都要重新计算数据在新数组中的位置Hash函数(扰动函数)，jdk1.8的优势就是在于**扩容后不需要再重新计算数据在新数组中的位置**，节省了时间，数据在新数组的位置只有两种情况：**一种原来的位置，另一种是在原来位置的基础上+扩容后的大小**。这也是为什么在jdk1.8后HashMap的扩展都是2的幂次方的原因之一。

在没有指定初始容量时，HashMap默认16，每次扩容成原来的2倍。

如果指定了初始容量，HashMap会扩充为2的幂次方大小。





**ConcurrentHashMap**

ConcurrentHashMap和HashMap结构差不多，存放数据的方式也是类似，只不过HashMap无法保证线程安全，因此多线程多用ConcurrentHashMap。

java7中，

- ConcurrentHashMap是由一个个Segment数组组成的，每个Segment中包含一个HashEntry数组，每个HashEntry本质上是一个链表。
- Segment 实现了 ReentrantLock,所以 Segment 是⼀种**可重入锁**，扮演锁的⻆⾊。HashEntry ⽤于存储键值对数据。
- 每个Segment 守护着⼀个HashEntry数组⾥的元素，当对 HashEntry 数组的数据进⾏修改时，必须⾸先获得 对应的 Segment的锁。
- 每次加锁操作都是锁定一个Segment，这样只要保证每个 Segment 是线程安全的，也就实现了全局的线程安全。

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210712203423167.png" alt="image-20210712203423167" style="zoom:67%;" />

**并行度(默认16)**

concurrencyLevel：并行级别、并发数、Segment 数，默认16，初始化后不能进行扩容。

理论上，最多同时可以支持16个线程并发访问，只要它们操作在不同的Segment上，就可以保证线程的安全，每个Segment上拥有自己的一把锁。



java8

ConcurrentHashMap取消了Segment分段锁，采⽤**CAS和synchronized**来保证并发安全。数据结构跟 

HashMap1.8的结构类似，**数组+链表/红黑二叉树**。

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210712203919062.png" alt="image-20210712203919062" style="zoom:67%;" />

**HashTable线程安全**

- 使用它加入对象时，不允许键值对为null，不然直接抛出直接NullPointerException。

- 创建时如果不指定容量初始值，Hashtable 默认的初始⼤⼩为11，之后每次扩充，容量变为原来的2n+1。
- 创建时如果给定了容量初始值，那么 Hashtable 会直接使⽤你给定的大小
- Hashtable 和 JDK1.8 之前的HashMap 的底层数据结构类似都是采⽤ **数组+链表** 的形式，数组是 HashMap 的主体，链表则是主要为了解决哈希冲突⽽存在的。
- 线程安全，使⽤ synchronized 来保证线程安全（同一把锁），效率⾮常低下。当⼀个线程访问同步⽅法时，其他线程也访问同步⽅法，可能会进⼊阻塞或轮询状态

**多线程建议是使用ConcurrentHashMap**！！

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210712204711594.png" alt="image-20210712204711594" style="zoom:67%;" />



**TreeMap（可排序）**

TreeMap 实现 SortedMap 接口，能够把它保存的记录根据键排序，默认是按键值的升序排序， 

也可以指定排序的比较器，当用 Iterator 遍历 TreeMap 时，得到的记录是排过序的。 

如果使用排序的映射，建议使用 TreeMap。 

在使用 TreeMap 时，key 必须实现 Comparable 接口或者在构造 TreeMap 

传入自定义的Comparator，否则会在运行时抛出 java.lang.ClassCastException 类型的异常。 



**LinkHashMap（记录插入顺序）**

LinkedHashMap 继承⾃ HashMap ，所以它的底层仍然是基于拉链式散列结构即由数组和链表或红⿊树组成。

另外， LinkedHashMap 在上⾯结构的基础上，增加了⼀条双向链表，使得上⾯的结构可以保持键值对的插⼊顺序。同时通过对链表进⾏相应的操作，实现了访问顺序相关逻辑。

------



## JVM

基本概念

运行java字节码文件的虚拟进程(假象计算机)。它运行在**操作系统**之上，与硬件没有直接的交互。

组成：垃圾回收，栈，堆，方法域，寄存器，一套字节码指令集。

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210713151204665.png" alt="image-20210713151204665" style="zoom:80%;" />

运行的过程：

java语言是半编译语言，因为java的源文件通过编译器(javac)编译成字节码文件(.class)，通过JVM的解释器将字节码文件解释成对应平台的机器码。

1. Java 源文件—->编译器—->字节码文件 
2.  字节码文件—->JVM—->机器码 

java语言也是跨平台语言，跨平台语言指的是字节码文件跨平台，而不是java源文件，不同的平台上的JVM的实现是相同的，因此通过JVM将字节码文件解释成平台的机器码文件运行。



JVM的结构图

![](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/21744606-a155004ed63c2a86.png) )



### **JVM内存区域(运行时数据区）** 

运行时：线程在JVM中执行的过程。

![image-20210713152558456](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210713152558456.png)

 <img src="https://gimg2.baidu.com/image_search/src=http%3A%2F%2Foscimg.oschina.net%2Foscnet%2F466efdc217868409df4da3de2905f70e85b.jpg&refer=http%3A%2F%2Foscimg.oschina.net&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1628753072&t=f32e6255c86a86777263f3b9dbd7d87f" alt="img" style="zoom: 50%;" /> 

线程：

这里的线程指的是程序执行过程中的一个线程实体，JVM允许一个程序并发执行多个线程。

JVM内存区域主要分为**线程私有区域**、**线程共享区域**、**直接内存**。

线程私有区域：程序计数器、虚拟机栈、本地方法栈

线程共享区域：Java堆和方法区。

直接内存：直接内存并不是 JVM 运行时数据区的一部分, 但也会被频繁的使用



**线程私有数据区域**生命周期与线程相同, 依赖用户线程的启动/结束 而 创建/销毁(在 Hotspot  JVM 内, 每个线程都与操作系统的本地线程直接映射, 因此这部分内存区域的存/否跟随本地线程的生/死对应)。

**线程共享区域**随虚拟机的启动/关闭而创建/销毁



 ![img](https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fwww.west.cn%2Finfo%2Fupload%2F20191201%2Fy3nueqzuoxl.jpg&refer=http%3A%2F%2Fwww.west.cn&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1628753072&t=c87fb2b4ff8818bc975153fd0e80c5fb) 

- 线程私有域

  - **程序计数器**

    一块较小的内存空间, 是当**前线程所执行的字节码的信号指示器**，每条线程都拥有一个。

    JVM通过解释器解释字节码文件，通过改变程序计数器的值来选取下一条需要执行的字节码指令，实现代码流程的控制。

    在进行线程之间的切换后，记录当前线程执行的位置，方便下一次运行时能够知道指定的位置。

    **tip:**  程序计数器是唯一一个不会出现内存溢出（**OutOfMemoryError**）的区域,它生命周期随着线程的创建而创建，随着线程的结束而结束。

  - **虚拟机栈**

    用来描述**Java方法执行**的内存模型，每个方法在执行的同时都会伴随着一个**栈帧(Stack Frame)**的创建,这个栈帧用来存储：**局部变量表**、**操作数栈、动态链接、方法出口等信息**。每一个方法从调用到执行再到结束，就对应着一个栈帧的创建到入栈再到出栈的过程。

    **栈帧**：是用来存储数据和部分过程结果的数据结构，同时也被用来处理动态链接 (Dynamic Linking)、 方法返回值和异常分派（ Dispatch Exception）。

    **动态链接**： **常量池**中会存储**方法的符号引用**，而每个**栈帧**中都会存储**一个引用**，用于**指向常量池中该方法对应的符号引用**，字节码指令中方法的调用就以方法对应的符号引用为参数来进行，在类加载阶段的解析步骤中，部分符号引用会被解析为直接引用，称为静态解析，在方法的运行过程中，另一部分符号引用会被实时的解析为直接引用，称为**动态连接**。

    **tip:   **

    **出现的错误**

    1.栈溢出(**典型：递归方法**) :虚拟机栈内存不允许动态扩展，因此当调用方法的数量超过了栈的最大深度时。

    2.内存溢出：虚拟机栈没有更多的内存，垃圾回收也没法提供更多的内存。

  - **本地方法栈**

    和虚拟机栈很类似，也是描述方法执行，不过本地方法栈是用来描述**JVM**使用的Native方法的执行过程，也是栈帧的创建从入栈再到出栈。在 HotSpot 虚拟机中和 Java虚拟机栈合⼆为⼀。 

    **tip:**

    **出现的错误**:栈溢出和内存溢出。

- 线程共享域

  - **堆**

    创建的对象和数组都保存在堆中，这里同时也是垃圾收集器进行垃圾回收最重要的内存区域。现在VM采用**分代收集算法**，从GC（garbage-Collection）角度来看可以将堆细分为：**新生代（Eden 区、From Survivor 区和 To Survivor 区）**和**老年代**。

  - **方法区(永久代)**

    用来存储**被JVM加载的类的结构信息：运行时常量池、字段和方法数据、构造函数和普通方法的字节码内容，还包含类、实例、接口初始化时用到的特殊方法**。

    方法区在**java虚拟机规范中**被定义为堆的一部分(**逻辑上的**)，本身并不是堆的一部分。

    

    方法区又被成为**永久代**。**永久代与方法区的关系**？

    在JAVA虚拟机规范中仅仅只定义方法区的概念和作用，并没有真正实现它，**⽽永久代就是HotSpot 虚拟机对虚拟机规范中方法区的⼀种实现方式**。相当于：方法区是接口，而永久代是接口的实现类。**其他的虚拟机实现并没有永久代这⼀说法。**

    

    [彻底弄懂java中的常量池 - 云+社区 - 腾讯云 (tencent.com)](https://cloud.tencent.com/developer/article/1450501)

    **Class文件常量池**

    Class文件是以字节为单位的二级制数据流，将java源代码通过编译器生成.class文件。

    Class文件常量池就是其中的一部分。
  
    编写一个JavaBean类

    ```java
    class JavaBean{
        private int value = 1;
        public String s = "abc";
        public final static int f = 0x101;
    
        public void setValue(int v){
            final int temp = 3;
            this.value = temp + v;
        }
    
        public int getValue(){
            return value;
        }
    }
    ```
  
    这里就不把字节码文件放出来了，感兴趣看上文链接。我选了一些我认为重要的部分，用来描述下面**字面量和符号引用的知识**
  
    Class文件中包含类的**版本号**、**常量池**、**其他的信息**。
  
    Class文件常量池中存放两大常量：**字面量和符号引用**
  
    
  
    **字面量：**
  
    - **文本字符串**
  
      上面类中定义的
  
      ```java
      public String s = "abc";
      ```
  
      这就是一个典型的字面量。
  
      ```java
       #9 = Utf8               s
       #3 = String             #31            // abc
       #31 = Utf8              abc
      ```
  
      在字节码文件中可以看到字符串“**abc**”
  
    - **用final修饰的成员变量**，包含：**静态变量、实例变量和局部变量**
  
      再来看看
  
      ```java
      public final static int f = 0x101;
      ```
  
      对应字节码
  
      ```java
      #11 = Utf8               f
       #12 = Utf8               ConstantValue
       #13 = Integer            257
      ```
  
       这里有一点需要注意：**所谓的常量池中的字面量，指的是数据的值，就如上面所说的字符串s = "abc", f = 0x101,都能在字节码中找到对应的值**。
  
      **对应的基本数据类型，也就是上面的private int value = 1;常量池中只保留了他的的字段描述符I和字段的名称value，他们的字面量不会存在于class文件常量池。**
  
      
  
    **符号引用**
  
    - **类和接口的完全限定名**
  
      例如：String类，在java源码中它表示如下：
  
      ```java
      import java.lang.String;
      ```
  
       在字节码文件中
  
      ```java
        #10 = Utf8               Ljava/lang/String;
      ```
  
      主要用于在运行时解析得到类的直接引用
  
      
  
    - **字段的名称和描述符**
  
      表示类或接口中定义变量
  
      ```java
          private int value = 1;
          public String s = "abc";
          public final static int f = 0x101;
      ```
  
       对应字节码文件中
  
      ```java
       #7 = Utf8               value
         #8 = Utf8               I
         #9 = Utf8               s
        #10 = Utf8               Ljava/lang/String;
        #11 = Utf8               f
      ```
  
    - **方法中的名称和描述符**
  
      表示类中定义的方法名和方法中的参数、返回值以及局部变量
  
      ```java
      public void setValue(int v){
          final int temp = 3;
          this.value = temp + v;
      }
      
      public int getValue(){
          return value;
      }
      ```
  
       对应字节码文件
  
      ```java
        #21 = Utf8               setValue
        #22 = Utf8               (I)V
            
            //v和temp是方法setvalue中局部变量只是在常量池中保存了它们的符号引用，它们真正的字面量不在常量池中
        #23 = Utf8               v
        #24 = Utf8               temp
        #25 = Utf8               getValue
        #26 = Utf8               ()I
      ```
  
      
  
      **class字节流代表的静态存储结构转化为方法区的运行时数据结构，其中就包含了class文件常量池进入运行时常量池的过程**
  
    - **运行时常量池**
  
      是方法区的一部分，Class ⽂件中除了有类的版本、字段、⽅法、接⼝等描述信息外，还有(**Class文件常量池**)常量池表（⽤于存放**编译期**⽣成的各种**字面量和符号引用**）上面已经解释过了
  
      ![image-20210713165250106](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210713165250106.png)
  
      运行时常量池的**作用**是存储java **class文件常量池**中的**符号信息**，运行时常量池中保存着一些class文件中描述的**符号引用**，同时在**类的解析阶**段还会将这些**符号引用翻译出直接引用**（直接指向实例对象的指针，内存地址），翻译出来的直接引用也是存储在运行时常量池中。
  
      
      
      **随着jdk的更新，常量池的位置也发生了改变。**
      
      - JDK1.7之前，**运行时常量池**包含**字符串常量池**位于方法区
      
      - JDK1.7，原本位于永久代的**字符串常量池和静态变量**被移出，放入到了java堆中，
      
      - JDK1.8，永久代被移除，取而代之是**元空间**，元空间位于直接内存中。方法区的实现虽然改变了，但是方法区并没有改变，变动的只是实现存放内容的物理地址。**字符串常量池和运行时常量池**被放到了堆中。无论物理存放上如何变化，在逻辑上它们永远都属于方法区。
      
        
  
  - **直接内存**
  
    **直接内存并不是虚拟机运行时数据区的⼀部分，也不是虚拟机规范中定义的内存区域，但是这部分内存也被频繁地使⽤。而且也可能导致** **OutOfMemoryError** **错误出现。**
  
    ------





### JVM运行时内存

java堆从GC的角度，将堆分为：**新生代和老年代**。

![image-20210715094813893](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210715094813893.png)

补充：

| -Xms              | 初始堆大小。如：-Xms256m                                     |
| ----------------- | ------------------------------------------------------------ |
| -Xmx              | 最大堆大小。如：-Xmx512m                                     |
| -Xmn              | 新生代大小。通常为 Xmx 的 1/3 或 1/4。新生代 = Eden + 2 个 Survivor 空间。 |
| -XX:SurvivorRatio | 新生代中 Eden 与 Survivor 的比值。默认值为 8。即 Eden 占新生代空间的 8/10，另外两个 Survivor 各占 1/10 |

```
对于JVM内存配置参数：
-Xmx 10240m -Xms 10240m -Xmn 5120m -XXSurvivorRatio=3,其最小内存值和Survivor区总大小分别是（）

最小内存:Xms= 10240
最大堆：Xmx = 10240
新生代大小: Xmn = 5120
SurvivorRatio=3 新生代中 Eden 与 Survivor 的比值
3x+x+x = 5120  x = 1024
```



**新生代**

用来存放新创建的对象，占整个堆的1/3，由于对象创建频繁，所以新生代会频繁出发GC,而新生代中使用MinorGC进行垃圾回收。

新生代分为：Eden区、SurvivorFrom区、SurvivorTo区。

- **Eden区**

  java新生对象存储的地方（如果新生的对象的内存大于Eden区的内存(**大对象**)，就将该对象分配到老年代--->**分配担保机制**）。

  **分配担保机制**：这里的担保人是老年代，老年代为新生代做担保，如果新的对象在新生代没有位置 ，就将其放入老年代中。

  当Eden区的内存不够时，就会触发MinorGC进行垃圾回收。

- **SurvivorFrom区**

  通过上一次在Eden区MinorGC回收后，存活下来的对象，作为下一次被GC的目标

- **SurvivorTo区**

  保存一次MinorGC过程中的存活对象

**MinorGC**

采用复制算法**(复制->清空->互换**)

- **eden、survicorFrom复制到 SurvicorTo，年龄+1**

  在进行MinorGC后，将存活的对象复制到SurvicorTo区域中(**如果存活的对象中有年龄达到了老年代的标准（默认15），就将该对象放入到老年代中**)，把SurvicorTo区域中的对象年龄+1（如果SurvicorTo区的内存不够，就将对象加入到老年代中）。

- **清空eden、survivorFrom区**

  将存活的对象复制到 SurvicorTo区后，将eden、survivorFrom区的对象都清除，用来存放新的对象

- **将survivorFrom和survivorTo区进行互换**

  原survivorTo成了下一次GC的survivorFrom区，原survivorFrom成了存储GC对象的survivorTo



**老年代**

主要存放应用程序中生命周期长的对象

老年代采用的时**MajorGC**算法

老年代比较稳定，不会进行频繁的MajorGC。在新生代晋升为老年代（年龄到达15）时会先在新生代中进行MinorGC将年龄+1，到达老年代标准晋升为老年代，老年代中的内存不足时进行MajorGC算法。或者当新生代中的对象为大对象时加入到老年代来，导致老年代中内存不足时，触发MajorGC。



**MajorGC**

采用**标记清除**算法

将对象分为：存活对象和可回收对象，标记可回收对象，回收标记的对象。这种GC算法相比与MinorGC的耗时要更长一些，因为需要进行扫描标记回收，而且这种回收机制会导致产生内存碎片(**不连续的内存空间**)。为了减少内存损耗，需要进行内存的标记或合并方便下次使用。



**永久代（PermGen)**

主要存放 **Class** 和 **Meta（元数据）**的信息,类在被加载的时候被放入永久区域，它和存放实例的java堆不同,GC 不会在主程序运行期对永久区域进行清理。**是方法区的实现**

**永久代溢出:** 动态**加载了大量java类**而导致溢出。



**java8中的元数据**

在jdk1.8之后，永久代被移除，取而代之的是元空间。元空间与永久代本质上相似，它们之间最大的区别在于：永久代是位于JVM中，而元空间是放在了直接内存中（**本地内存**）。

- 永久代的大小是受JVM控制的，无法进行调整，元空间使用直接内存，受本地内存大小控制，而本地内存的大小肯定是远远大于JVM的，因此可能产生的内存溢出的概率就大大减小了。
- 元空间中存放的是**类的元数据**，**字符串池和类的静态变量**放入 java 堆中，这样加载多少类的元数据不再由MaxPermSize 控制，由系统的实际可用空间来控制。
- 永久代对于GC会带来不必要的复杂性，并且回收效率偏低，在永久代中每进行一次GC当中元数据的位置就会发生变化， hotspot虚拟机每种类型的垃圾回收器都要特殊处理永久代中的元数据。 使用元空间替代了永久代时，简化了整个**Full GC**过程。



### 垃圾回收与算法

![image-20210715110149559](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210715110149559.png)



**哪些内存需要回收？**

GC主要关注的在**堆和方法区**

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210716102147217.png" alt="image-20210716102147217" style="zoom: 80%;" />

**什么时候回收？**

**判断对象是否需要回收（确定垃圾）**

- 引用计数法
- 可达性分析算法



**引用计数法**

对象的操作都有引用与之关联，给对象添加一个引用计数器，如果该对象被引用了，那么计数器+1，当引用失效时 ，计数器-1，如果对象的引用计数器变成了0，说明该对象没有被引用，该对象需要被回收。



**可达性分析算法**

引用计数存在着缺陷，它很难解决循环引用的问题，对象之间相互循环引用，导致对象永远无法回收。

因此采用了可达性分析的方法。

通过**GC roots**作为对象的起点搜索，搜索走过的路径称为**引用链**。如果一个对象到GC roots没有任何引用链与之相连接，那么这个对象称为**不可达对象**。

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210716161456801.png" alt="image-20210716161456801" style="zoom:67%;" />

**注意**：不可达对象并不代表是可回收对象。不可达对象成为可回收对象至少经过两次标记过程。如果标记后是可回收对象，方可回收。

**补充:**

Object类中**finalize**方法

判断一个对象A是否可回收，两次标记过程。

1. 如果对象A没有任何引用链与GC roots相关联，那么就对对象A做第一次标记，标记为：不可达对象。

2. 判断对象A是否有必要执行**finalize方法**

   - 如果对象A没有重写**finalize方法**或者该方法已经被虚拟机调用过，那么该方法被JVM视为：没有必要执行。该对象被认定为不可达对象，**可以进行回收的对象**。

   - 如果对象A重写了**finalize方法**并且该方法没有被虚拟机调用过，那么该对象A会被放入到**F-Queue**队列中，该队列是**由JVM自动创建的、低优先级**的Finalizer线程触发**finalize方法的执行**。

     **finalize方法**是对象A逃脱GC的最后的机会，换而言之就是：救命稻草。GC会对**F-Queue**队列中的对象进行**第二次标记**，如果对象A在**finalize方法**中与引用链中任何一个对象建立起联系之后，在第二次标记之后，对象A就会被移出**即将回收的集合**。如果这之后该对象成为不可达对象时，它没有方法再次拜托GC,只能被回收。每个重写**finalize方法**的对象只能被使用一次。





**Java中四种引用**

- 强引用（Strong Reference）

  java中最常见的引用就是强引用，例如：一个对象的引用就是一个强引用，此时的对象是可达性对象，只要引用不为null，该对象就会被一直引用，因此它永远可达，永远不会被GC，因此会造成**内存溢出**。

- 软引用（SoftReference）

  需要引用（SoftReference）类来实现。如果对象只有软引用时，当系统内存足够时，该对象不会被回收，一旦系统的内存不足时，它就会被回收。它通常**应用于内存敏感的程序**。

- 弱引用（Weak Reference）

  弱引用相比于软引用，它的生命周期更短。如果对象只有弱引用，无论系统内存是否充足，它都会被GC。

  **垃圾回收机制(垃圾回收器是一个优先级很低的线程)**

- 虚引用（Phantom Reference）

  它不会决定对象的生命周期，如果对象只有虚引用，任何时刻该对象都可能会被回收。**虚引用一般和引用队列联合使用**。**主要作用是跟踪对象被垃圾回收的状态。** 

  

**怎么回收？**

- **标记清楚算法 （Mark-Sweep）**

  最基础的GC算法，分为两个阶段。标记阶段和清除阶段。

  标记阶段：标记出需要回收的对象

  清除阶段：回收标记的对象

  <img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210716165012149.png" alt="image-20210716165012149" style="zoom:67%;" />

  此算法会产生大量的内存碎片，影响后续内存的利用率

- **复制算法（copying）**

  为了解决内存碎片化的问题，提出了复制算法。

  将内存空间分为大小相等的两块，其中一块用来存储对象，另一块用来存放GC后存活的对象，然后将原来存放对象的内存清空。

  <img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210716165402538.png" alt="image-20210716165402538" style="zoom:67%;" />

  虽然解决了内存碎片化的问题，但是最大的问题在于不能够存放大量的对象，如果数据量过多可能导致该算法的效率低下。

- **标记整理算法（Mark-Compact)**

  为了解决上面两个方法带来的弊端，提出了标记整理算法。

  标记阶段：将内存中的对象分别标

  整理阶段：不是将标记的可回收对象直接进行回收，而是将存活的对象都整理到内存的一端，将端边界以外的内存全部清空。

  ![image-20210716170120456](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210716170120456.png)

- **分代收集算法**

  **该方法是当前大部分JVM所采用的方法。**

  核心思想：根据**对象生命周期的不同**，将内存(堆)划分为**新生代和老年代域**。新生代的特点：每次都需要回收大量的对象，只有少部分对象存活，当年龄到达一直阈值时，晋升为老年代。

  老年代特点:比较稳定，每次只回收少量对象。根据不同区域选择对应的算法。



**新生代与复制算法(MinorGC)**

目前大部分JVM对于新生代都(MinorGC)采用复制算法,复制算法的特点：**实现简单、内存效率高、不易产生碎片**。

因为新生代中每次都要回收大量的对象，只有少量的对象存活下来，因此使用复制算法非常符合新生代的特点。这里复制算法并不是将新生代的内存按照**1：1**划分，而是将**Eden区**占据整个内存的绝大部分，将剩下的一小部分划分成**SurvivorFrom区**和**SurvivorTo区**。在进行回收时，将Eden区和SurviviorFrom区中存活的对象放入To区。

![image-20210717094721080](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210717094721080.png)

**老年代与标记整理算法**

老年代每次只需要回收少量的对象，采用**标记整理**或**标记清除**算法。

- 对象的内存分配主要位于新生代的Eden、SurviviorFrom和SurvivorTo区。少数情况会分配到老年代中（大对象或对象的年龄达到了阈值）。



上面说的是对JVM内存中线程共享区中java堆GC的过程，对于线程共享区另一个区域，垃圾回收对于方法区中的永久代回收主要包括：**废弃常量**和**无用的类**。



**如何判断一个常量是废弃常量**

运行时常量池位于方法区中，主要是回收常量池中的废弃常量。

如果字符串常量池中字符串‘abc’没有被任何String类型的引用所引用，该字符串‘abc’会被判定为废弃常量， 在进行GC时，将会被回收。



**如何判断一个类时无用的类**

满足三个条件

- 该类对应的java.lang.Class中Class对象没有被引用在任何地方，无法通过反射Class对象获取对应该类的属性和方法。

- 该类对应的实例都已经被回收，java堆中找不带任何该类对应的实例
- 加载该类的ClassLoader已经被回收



**采用分代回收算法堆中内存对对象分配的基本策略**

- 新生对象优先在eden区分配
- 大对象直接进入老年代
- 长期存活的对象将进入老年代



**GC 分代垃圾回收  VS 分区垃圾回收**

**分代垃圾回收**

大多数JVM都采用分代垃圾回收，根据对象生命周期不同，将堆的内存划分为新生代和老年代，根据不同区域的特点采用适合的收集算法，更好地回收内存，更好地分配内存。

**分区垃圾回收**

将整个堆内存划分为连续的不同小区间，每个小区间独立使用，独立回收。





**补充：**GC分为两大类

- **部分收集(Partial GC）**

  - 新生代收集(Minor GC / Young GC)
  - 老年代收集(Major GC/ Old GC)（只有**CMS垃圾收集器**有这个模式）**注意：在某些语境中 Major GC也指代整个堆的收集**
  - 混合收集(Mixed GC):收集整个新生代和部分老年代(只有**G1垃圾收集器**有这个模式)

- **整堆收集（Full GC）**

  收集整个堆和方法区





### GC垃圾收集器

**收集算法是内存回收的方法论，那么垃圾收集器就是内存回收的具体实现**

**是根据具体应用场景选择适合的垃圾收集器**

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210717103948570.png" alt="image-20210717103948570" style="zoom:67%;" />

**Serial（单线程、复制算法）新生代**

serial（连续）垃圾收集器是**最基本的垃圾收集器**，采用**单线程**模型的收集器。

它只会使用一个cpu或一个线程去完成垃圾回收，并且在垃圾回收的过程中，其他所有的线程都必须停止(**STW-stop the world**),直到它完成了垃圾回收的工作。

优点：简单而高效，在单个cup环境中，不存在线程交互的开销，可以获取很高效的单线程垃圾回收效率。

应用于：java 虚拟机运行在 **Client 模式**下默认的**新生代**垃圾收集器。 

**ParNew（Serial+多线程）新生代**

是Serial收集器的多线程版本，也使用复制算法。在进行垃圾回收的过程中也是（STW）。

默认开启和cpu数目相同的线程数，可以用：XX:ParallelGCThreads来设置线程数。

应用于：java虚拟机运行在 **Server 模式**下**新生代**的默认垃圾收集器。



**并行和并发概念**

 [( 并发与并行的区别是什么？ - 知乎 (zhihu.com)](https://www.zhihu.com/question/33515481) 

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210717155507985.png" alt="image-20210717155507985" style="zoom:67%;" />

如上图所示，可以很清楚解释并发和并行。

**并发（Concurrent）：**两个队列交替使用一台咖啡机

**并行（Parallel）：**一个队列使用一台咖啡机，另一个队列使用另一个咖啡机。

并发和并行都可以是多个线程，关键是看能否被（多个）cpu同时执行。

如果多个线程被多个cpu同时执行，那么就是并行

如果只由一个cpu交替执行多线程任务，那么就是并发

**Parallel Scavenge（多线程复制算法、高效）新生代**

**自适应调节策略**是它的一个重要的特点。

和ParNew收集器相比，Parallel Scavenge收集器更加注重的是**吞吐量(Thoughout)**。

**吞吐量：**CPU运行用户线程时间 / (CPU运行用户线程时间+**垃圾回收时间**）

当垃圾回收时间越小，cpu总的消耗时间越小，吞吐量就越大 。

高吞吐量可以最高效率利用cpu时间，尽快的完成程序的运算任务。

应用：后台运算而不需要太多交互的任务。

**Serial Old（单线程、标记整理算法）老年代**

该收集器是Serial 的老年代版本，采用了标记整理算法

应用于：

在 **Client 默认**的 java 虚拟机默认的**年老代**垃圾收集器。 

在**Server**模式下

在jkd1.5以前与Parallel Scavenge搭配使用

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210717161757921.png" alt="image-20210717161757921" style="zoom:67%;" />

这样的搭配**只能保证新生代的高吞吐量，而老年代无法保证**



新生代 Serial 与年老代 Serial Old 搭配垃圾收集过程图： 

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210717161857301.png" alt="image-20210717161857301" style="zoom:67%;" />

**Parallel Old（多线程、标记整理算法）老年代**

在jdk1.6之后出现该收集器，是Parallel Scavenge的老年代版本。采用标记整理算法。

该收集器保证了老年代的高吞吐量，Parallel Old和Parallel Scavenge搭配能够保证新生代和老年代都保持高吞吐量。

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210717162434704.png" alt="image-20210717162434704" style="zoom:67%;" />

**CMS(多线程、标记清除算法)**

Concurrent mark sweep(CMS)收集器是一种年老代垃圾收集器,它使用的是**多线程 + 标记清除算法**。

最主要的目标是**获取最短垃圾回收停顿时间**。

最短垃圾回收集停顿时间能够让交互频繁程序提升速度，提高用户体验性。

CMS工作的阶段分为4个：（**三个标记一个清除**）

- **初始标记**

  标记与GC ROOTS直接相连的对象，速度很快，但是任然需要**STW**

- **并发标记**

  用户线程和GC是同时进行的，这时进行GC ROOTS跟踪，记录可达性对象，因为用户线程同时进行的原因，可能导致对象的引用发生了改变，对象的可达性就受到了影响。**不需要暂停工作线程**。

- **重新标记**

  为了修复在并发标记阶段用户线程运行导致标记产生变动的那部分对象记录。此过程需要**STW**

- **并发清除**

  清除GC ROOTS不可达对象，和用户线程一起工作，不需要停止线程。

这4个阶段中耗时最长的是**并发标记和并发清除**阶段，这两个阶段中用户线程可以一起工作，**总体上来说CMS收集器的内存回收和用户线程是一起并发执行的。**

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210717164557404.png" alt="image-20210717164557404" style="zoom:67%;" />

优点：并发收集、低停顿

缺点：采用标记清除算法会产生内存碎片化的问题，导致内存的利用率降低。无法处理浮动垃圾，对cpu资源敏感。

**G1(Grabage-first)**

面向服务器的垃圾收集器，Hotspot 虚拟机在 **jdk** 8 之后正式（java7处于试验阶段）推出的

G1除了追求**低停顿垃圾回收时间**之外，还实现了可以**精确控制停顿时间**，可以设定⼀个⻓度为 M 毫秒的时间⽚段。**低停顿时间的同时保持高吞吐量**。

G1采用了**标记整理**算法，因此内存碎片化问题就得到了解决。

G1可以独立掌管整个GC堆(新生代和老年代)，还是采用了分代的概念

G1的**运行阶段**

- **初始标记** 
- **并发标记** 
- **最终标记** 
- **筛选回收**

G1避免进行全域的垃圾回收，将堆分为几个大小固定的独立区域，跟踪这些区域中垃圾回收的进度，同时在后台维护一个优先级列表，每次根据所允许的时间，优先回收垃圾最多的区域。

区域的划分和优先级收集机制，确保G1在有限的时间内获得最高的垃圾回收效率。

------



## JAVA BIO/NIO

**同步**

发起一个请求或任务，被调用者在未完成请求或任务前，不会返回结果。

需要一直等待该请求返回或任务完成反馈的结果，在这期间不能够去做其他的事情。

比如：你打电话给书店老板询问书籍，老板帮你去找书，你需要一直等待，等待书店老板给你回复。



**异步**

发起一个请求或任务之后，被调用者会理刻返回表示已经接受请求或任务，但是并没有返回结果，就接着去做别的事情，发出的请求或任务完成时，被调用者会返回结果。

比如：你打电话给书店老板询问书籍，你让他查到了再打电话给你，然后你挂断电话，期间你可以干其他事情，等到老本找到了书籍然后给你打电话。



**阻塞**

发起请求后，调用者需要一直等待结果返回，也就是当前的线程会被挂起，无法去做其他请求。



**非阻塞**

发起请求后，调用者不需要等待结果返回，可以去做别的事情。



**BIO(Blocking I/O)（最传统的同步阻塞IO模型）**

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210718153538501.png" alt="image-20210718153538501" style="zoom:50%;" />

典型的同步阻塞IO模型：data = socket.read();

当应用程序发出请求时，先去判断内核中的数据是否准备完成，如果没有准备完成，该应用程序就会被阻塞(**让出cpu资源**)，等到内核数据准备完成，将数据拷贝给应用程序，应用程序解除**block状态**。



基于**字节流和字符流**操作，数据流的特点是**单向性**，要么只读、要么只写。

server端要为每一个连接建立一个线程，这样的好处是每个线程可以专注自身的I/O操作并且编程简单。但是这种模型并不适合连接数过多情况。





**NIO(Non - Blocking  I/O)(同步非阻塞IO模型)**

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210718154121553.png" alt="image-20210718154121553" style="zoom: 50%;" />

当应用程序发出read请求后，不需要等待，它会马上得到来自内核的返回，如果返回的结果是**error(数据没有准备好)**,那么应用程序就继续向内核发出请求，再次去确认，这样不停做循环，一旦内核准好数据同时应用程序发来请求，那么就将数据拷贝给应用程序，返回。

这样带来的问题：线程没有进入阻塞状态，它就不会让出cpu资源，导致cpu的占用率很高。



NIO的组成包括：**Channel(通道)、 Buffer(缓冲区)、Selector**。

**Channel**

- Channel和Stream（**流**）是同一个级别的，区别在于：Stream是单向的，而Channel是双向的，既可以用来读也可以用来写操作。

- Channel的主要实现：

  1. FileChannel
  2. DatagramChannel
  3. SocketChannel
  4. ServerSocketChannel

  1对应文件IO、2对应文件UDP、3、4对应文件TCP（Server和 Client）

- **Buffer**

  是一个容器，连续的数组用来存储数据。

  Channel提供从文件、网络读取数据的渠道，但是读写操作都必须由Buffer来操作。

  <img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210719154353391.png" alt="image-20210719154353391" style="zoom: 67%;" />

  <img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210719155137722.png" alt="image-20210719155137722" style="zoom:67%;" />

  上面是一个从客户端向服务器端发送数据的过程。

  客户端发出数据经过Buffer写入传给Channel，读入数据经过Channel将数据读入Buffer传给服务端。

- **Selector**

  是NIO的核心类，通过Selector去检测多个Channel中是否有数据的发生(**读或写请求**)，如果对应的Channel上有真正的请求发生，那么就去处理该Channel上的请求。Selector本身也是一个线程，设定一个线程专门去管理多个Channel的请求任务，而不需要为每一个Channel去建立对应的线程，避免了多个线程之间的上下文切换，大大减少了系统的开销。

  <img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210719160209617.png" alt="image-20210719160209617" style="zoom: 67%;" />

  

**多路复用IO模型**

此模型的本质还是NIO模型，在NIO中的通过Selector实现在一个线程轮询多个通道的数据，需要先将用户线程中需要轮询的socket注册到Selector中，用Selector去轮询多个socketChannel是否有请求到达，一旦请求到达，Selector.select返回，最后完成I/O数据的传输这个过程用户线程是处于阻塞状态的。注意：socket配置也是非阻塞的。

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210719164029022.png" alt="image-20210719164029022" style="zoom:50%;" />



相比于NIO，多路复用IO用户线程首先需要在Reactor中注册一个事件处理器，然后Reactor（相当于上文提到的selector）负责轮询各个通道是否有新的数据到来，当有新的数据到来时，Reactor通过先前注册的事件处理器通知用户线程有数据可读，此时用户线程向内核发起读取IO数据的请求，用户线程阻塞直至数据读取完成。

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210719164038684.png" alt="image-20210719164038684" style="zoom:50%;" />

多路复用IO模型效率高于NIO模型原因在于：NIO中socket轮询是在用户线程中的，而多路复用是在内核中。



**信号驱动IO模型**

当用户线程发起一个I/O请求时，给对应的**socket**注册一个**信号函数**，用户不会立刻得到结果(**内核中数据还没有准备好**)，而是继续去做别的事情，当内核中数据准备号时，给用户发送一个信号给用户线程，用户线程通过在信号函数中调用I/O操作进行实际的读写操作。



**异步IO模型**

该模型是最理想模型。它实现的流程：当用户线程发起read操作之后，就去做它自己的事情了，内核接收到用户线程的请求后，立刻返回，表明该请求已经受理，这个过程不会对用户线程造成任何阻塞。因为内核在完成数据准备后就将数据拷贝给用户线程，返回用户线程信息表明数据已经传输完毕，read操作已经完成，不需要用户线程再去调用IO操作。**只需要先发起一个请求，当接收内核返回的成功信号时表示 IO 操作已经完成，可以直接去使用数据了。**

和信号驱动模型的差别就在这里，信号驱动模型在内核完成数据准备之后，告诉用户线程数据已经准备完毕，需要你自己来调用IO操作拿到数据。

------





## **Java IO**

![img](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/20140814122633546)

**IO分类**

- 按照流的流向分，可以分为输⼊流和输出流；
- 按照操作单元划分，可以划分为字节流和字符流；
- 按照流的⻆⾊划分为节点流和处理流。

**InputStream**/**Reader**: 所有的输⼊流的基类，前者是字节输⼊流，后者是字符输⼊流。

**OutputStream**/**Writer**: 所有输出流的基类，前者是字节输出流，后者是字符输出流。



**不管是文件读写还是网络发送接收，信息的最小存储单元都是字节，那为什么I/O流操作要分为字节流操作和字符流操作呢？**

字符流是由 Java 虚拟机将字节转换得到的，问题就出在这个过程还算是⾮常耗时，并且，如果我们不知道编码类型就很容易出现乱码问题。所以， I/O 流就⼲脆提供了⼀个直接操作字符的接⼝⽅便我们平时对字符进⾏流操作。

------



## JVM类加载机制

Java程序运行时，必须经过编译和运行两个步骤。首先将后缀名为.java的源文件进行编译，最终生成后缀名为.class的字节码文件。然后Java虚拟机将编译好的字节码文件加载到内存（这个过程被称为类加载，是由加载器完成的），然后虚拟机针对加载到内存的java类进行解释执行，显示结果。


JVM类加载大致分为三个过程：**加载、连接、初始化**。

#### **类加载器**

在类加载的过程中，只有加载阶段可以自定义类加载器，而其他阶段由JVM主导。

因此加载的阶段被放到了JVM外部实现，便于让应用程序决定如何获取所需的类。

JVM中提供了三种类加载器：

- **启动类加载器(Bootstrap ClassLoader)**

  最顶层的类加载器，由c++实现。

  负责加载：JAVA_HOME\lib 目录中的jar包或被 -Xbootclasspath 参数指定的路径中的所有类

- **扩展类加载器(Extension ClassLoader)**

  继承自：java.lang.ClassLoader

  负责加载 JAVA_HOME\lib\ext 目录中的，或通过 java.ext.dirs 系统变量指定路径中的类库。

- **应用程序类加载器(Application ClassLoader/ System Class Loader )：**

  (这里的Application ClassLoader 和System Class Loader 是同一个类加载器，只是叫法不同)

  继承自：java.lang.ClassLoader

  ⾯向我们⽤户的加载器，负责加载当前应⽤classpath下的所有jar包和类。

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210720104224453.png" alt="image-20210720104224453" style="zoom:67%;" />

可以通过继承 java.lang.ClassLoader实现自定义的类加载器，重写findClass方法加载指定路径上的class。

------



#### 双亲委派模型

每一个类都有对应的类加载器。当类收到一个加载请求时，先去判断这个类是否已经被加载，被加载过的类会直接返回，否则尝试加载。

**加载过程：类本身不会主动去加载，它会将请求委派给父类加载器loadClass（）处理，父类则会委派给父类的父类，因此所有的请求都会传到顶层的类加载器中（Bootstrap ClassLoader），只有当父类中的加载器无法进行加载时，自己才会来处理类加载**。

![image-20210720105501358](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210720105501358.png)

注意：类加载器之间的“**⽗⼦**”关系也**不是通过继承**来体现的，是由“**优先级”来决定**

```java
   //源码
    private final ClassLoader parent;
    protected Class<?> loadClass(String name, boolean resolve)
            throws ClassNotFoundException
    {
        synchronized (getClassLoadingLock(name)) {
            // ⾸先，检查请求的类是否已经被加载过
            Class<?> c = findLoadedClass(name);
            if (c == null) {
                long t0 = System.nanoTime();
                try {
                    if (parent != null) {//⽗加载器不为空，调⽤⽗加载loadClass()⽅法处理
                                c = parent.loadClass(name, false);
                    } else {//⽗加载器为空，使⽤启动类加载器BootstrapClassLoader 加载
                        c = findBootstrapClassOrNull(name);
                    }
                } catch (ClassNotFoundException e) {
                    //抛出异常说明⽗类加载器⽆法完成加载请求
                }

                if (c == null) {
                    long t1 = System.nanoTime();
                    //⾃⼰尝试加载
                    c = findClass(name);
                    // this is the defining class loader; record the
                    stats

                    sun.misc.PerfCounter.getParentDelegationTime().addTime(t1 - t0);

                    sun.misc.PerfCounter.getFindClassTime().addElapsedTimeFrom(t1);
                    sun.misc.PerfCounter.getFindClasses().increment();
                }
            }
            if (resolve) {
                resolveClass(c);
            }
            return c;
        }
    }
```



**好处：避免类的重复加载（JVM 区分不同类的方式不仅仅根据类名，相同的类文件被不同的类加载器加载产生的是两个不同的类）**

比如：加载rs.jar包中的类java.lang.Object,无论加载器加载那个类，最终委派给启动类加载器进行类的加载，保证了不同的类加载器最终得到的是同一个Ojbect对象。





**连接**的过程在细分为：**验证、准备、解析**

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210720092329414.png" alt="image-20210720092329414" style="zoom:67%;" />

- **加载**

  这个阶段会在内存中生成代表该类的**java.lang.Class对象**(**类对象**)，作为方法区这个类的各种数据的入口。

  注意：获取类的过程并不一定要从Class文件中，也可以从jar包或war包中获取，也可以运行时计算生成(**动态代理**)。

- **连接**

  - **验证**

    确保class文件的字节流中的信息符合JVM的要求，不会危害JVM的安全

  - **准备**

    正式为类中的变量分配内存以及为其设置初始值阶段（**在方法区中为这些类变量分配内存**）。

    举例：

    ```java
    public static int v = 8080;
    /*
    定义的静态变量 v
    这里初始化值的过程并不是直接将 8080 赋值给 v ，v 变量在准备阶段的初始化值是 0 ，
    将其赋值为 8080 的是put static 指令，该指令被编译后存放在类构造器<client>方法中。
    */
    
    public final static int v = 8080;
    /*
    如果声明静态变量被final关键字所修饰，在编译阶段生成的v 的ConstantValue属性，在准备阶段中v被赋值为 8080
    */
    ```

    

  - **解析**

    JVM将常量池中符号引用替换直接引用的过程。

    - **符号引用**

      一组符号所描述的引用目标，符号的形式是字面量。

      如：在Class文件中它以CONSTANT_Class_info、CONSTANT_Field_info、CONSTANT_Method_info等类型的常量出现。

      在Java中，一个java类将会编译成一个class文件。在编译时，**java类并不知道所引用的变量（基本数据类型、局部变量、方法等等）实际地址**，**因此只能使用符号引用来代替**。比如org.simple.People类引用了org.simple.Language类，在编译时People类并不知道Language类的实际内存地址，因此只能使用符号org.simple.Language。

      各种JVM实现内存的布局可能不同，但是它们识别符号引用是一致的。

    - **直接引用**

      指向目标的指针，相对偏移量(指向实例变量、实例方法的直接引用都是偏移量),间接定位到目标的句柄。

      直接引用与JVM布局有关，同一个符号引用在不同的虚拟机实例上翻译出来的直接引用一般不会相同。

      如果有了直接引用，那目标必定存在于内存中。

- **初始化**

  类加载的最后一个阶段，除了在类加载阶段可以自定义类加载器，其他的阶段都是由JVM主导控制。

  这个阶段才是正真的执行字节码文件，根据字节码文件的内容对类的各个字段进行赋值。



**类构造器<client>**

初始化阶段是类构造器<client>方法执行的过程,<client>方法是由编译器收集类中的类变量赋值操作和静态代码块合成的，JVM会保证<client>方法执行前其父类的<client>方法已经执行完毕。**如果一个类中没有静态变量、静态语句块，那么编译器可以不为这个类生成<client>方法**。

------



## Java对象创建的过程

对象的创建分为五个过程

- **类加载检查**

  当JVM接收到new指令时，首先会先去检查该指令能否在常量池中找到对应该类的符号引用，并检查该类是否已经被加载、连接，初始化过。如果没有先进行类的加载。

- **分配内存**

  在类加载检查完成后，在java堆中为新生的对象分配内存。

  分配内存方式有两种：**指针碰撞**、**空闲列表**。

  分配方式选择根据：**java堆内存是否规整**

  **指针碰撞**：

  - 适用场景：java堆内存规整(没有内存碎片化)
  - GC收集器：Serial (单线程、复制算法)和 PerNew(多线程、复制算法)。
  - 原理：将内存分为两块，中间有一个分界值指针，用过的内存放一边，没有用过的内存放一边，将对象放入到没有用过的内存中

  **空闲列表：**

  - 适用场景：Java堆内存碎片化
  - GC收集器：CMS（多线程+标记清除算法）
  - 原理：将列表中没有用过的内存标记下来，找到适合新生对象大小的位置放入即可，更新列表。

  **分配内存需要考虑到线程安全的问题：**

  对象的创建很频繁，因此JVM需要保证线程的安全：

  - **TLAB**:为每个线程预先在Eden区分配一块内存，JVM给对象分配内存时先在TLAB中分配，当TLAB中内存不够或者使用完之后，就采用**CAS+失败重试**的方法。
  - **CAS+失败重试**:CAS 是乐观锁的一种实现方式。乐观锁：每次不加锁而是假设没有冲突去完成某个操作，如果因为冲突失败就重试，直到成功为止。**此方法保证更新操作的原子性**。

- **初始化零值**

  内存分配完成后，JVM将分配到的内存空间初始化零值(**不包含对象头**)，这一操作保证了对象中的成员变量在不赋初值就可以使用。

- **设置对象头**

  对象头中的信息包含：

  <img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/20170419212953720" style="zoom: 80%;" />

  **markword（标记字段）**

  - 对象的哈希码
  - 对象对应的**GC分代年龄**
  - **锁状态标志**、线程持有的锁、

  **klass（Class对象指针）**

  - 对象指向它的类元数据的指针，虚拟机通过这个指针来确定这个对象是哪个类的实例

  **数组长度（只有数组对象有）**
  如果对象是一个数组, 那在对象头中还必须有一块数据用于记录数组长度(例如:int)。

- **执行构造方法**

  从JVM角度来看一个对象已经产生，从java程序角度来看，创建对象才开始，执行构造方法，按照意愿将对象初始化数据之后这个对象才能够真正得到使用。

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210720160753504.png" alt="image-20210720160753504" style="zoom:150%;" />

图上有点小错误:**分配内存中：采用指针碰撞是复制算法，不是标记整理**



**牛客上做到的题目：**

```java
(单选题)以下代码的输出结果是?
    public class B
    {
        public static B t1 = new B();
        public static B t2 = new B();
        {
            System. out.println( "构造块");
        }
        
        static{
            System.out.println("静态块");
        }
        public static void main( String[] args){
            B t = new B( );
        }
    }

//正确答案:构造块、构造块、静态块、构造块
//现从主函数Main中入手，执行 B t = new B( );也就是创建对象，创建对象之前需要先进行类加载过程，而类加载的过程需要检查类是否进行加载，现在进行类的加载过程。
/*类中定义了静态域：静态变量，静态代码块，静态方法。
静态域执行的过程：按照其定义的变量、代码块、方法的顺序来。
因此这里先执行public static B t1 = new B();这个代码，而这也是创建对象的语句，创建对象之前也是需要进行类加载检查，而B类在前就已经加载过了，注意：类中的静态域只在类第一次加载的过程中执行，因此这里不会再在进行静态域的加载，跳过静态域到构造块和构造方法的执行过程，完成t1对象创建,因此控制台输出：构造块。
接着回到 public static B t2 = new B();的过程，继续创建对象t2，这个过程和t1是一样的因此，输出:构造块。

当两个静态变量都完成时，接下来执行静态代码块，输出：静态块。
执行构造块和构造方法，最后创建对象t，输出：构造块。
*/
```





**对象访问定位的两种方式**

建立对象之后就是要调用对象干事，java中通过栈上的reference数据来操作堆上的具体对象。

- 句柄

  在java堆中开辟一块内存用作句柄池，句柄本身是指向对象的实例数据和类型数据，引用是指向句柄。

  <img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210720161837763.png" alt="image-20210720161837763" style="zoom:67%;" />

- 直接指针

通过指针直接指向java堆中对象的地址，堆中对象的布局有所改变，在对象的实例数据中存放指向对象类型数据的地址。

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210720162258288.png" alt="image-20210720162258288" style="zoom:67%;" />

句柄访问对象的好处就是：当对象的地址改变时，引用的地址不要改变，需要改变的是指向对象的句柄。

缺点：通过句柄这个间接访问对象开销要高一些。

直接指针：访问的速度快于句柄，对象地址发生改变时，引用也要发生改变。

------



## Java多线程并发

### **什么是线程和进程**

进程

是程序执行的一次过程，即进程从创建到运行再到消亡的过程。

**是系统进行资源分配的独立单位**

进程之间是相互独立的，因此很难进行进程间的通信。



线程

是比进程更小的执行单位，通常一个进程可以包含多个进程。

**是进行资源调度和保护的基本单位**

进程拥有独立的内存单元，线程拥有自己独立的程序计数器、虚拟机栈、本地方法栈，多个线程之间共享进程的堆和方法区。



### **多线程**

多线程是多个线程的集合。一个程序（进程）中同时执行一个以上的线程，一个线程不必等待另一个线程执行完毕之后才执行，所有的线程在同一时刻发生。

多线程程序中，多个线程共享内存，带来好处就是提高程序的运行效率。







### 线程的实现和创建

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210815182704130.png" alt="image-20210815182704130" style="zoom:80%;" />



**继承Thread类**

Thread类实际是Runnable接口的实现类，继承此类的类或子类的对象都是一个线程对象。继承Thread类需要重写run方法。

启动线程的方法：通过Thread类的start（）实例方法。

线程启动后会自行调用run方法中的业务。

```java
public class MyThread extends Thread { 
 public void run() { 
 System.out.println("MyThread.run()"); 
 } 
} 
MyThread myThread1 = new MyThread(); 
myThread1.start();
```



**实现Runnable接口**

Runnable接口提供唯一的run方法，如何实现该接口的类都需要重写run方法。

多个线程共同处理数据

```java
//如果一个类继承父类，不能够使用Thread类来实现线程，那么可以同实现Runnable接口来完成。
public class MyThread extends OtherClass implements Runnable { 
 public void run() { 
 System.out.println("MyThread.run()"); 
 } 
}

//实现Runnable接口如何启动线程。
    public static void main(String[] args) {
        /*使用同一个Runnable实现对象构建Thread线程对象*/
        MyRunnable myRunnable = new MyRunnable();


        /**
         * 多个线程使用同一个run方法
         */
        Thread thread = new Thread(myRunnable,"第一个线程");
        Thread thread1 = new Thread(myRunnable,"第二个线程");


        thread.start();
        thread1.start();
    }

public class MyRunnable implements Runnable {
    @Override
    public void run() {
        //获取当前正在执行的线程对象
        Thread current = Thread.currentThread();
        System.out.println("当前线程名字:"+current.getName());
    }
}
```





### 线程的生命周期

线程的生命周期分为：**新建(New)**、**就绪(Runnable)**、**运行(Running)**、**阻塞(Block)**、**死亡(Death)**

当一个线程被创建后并不是立刻开始运行，在运行之前，它处于就绪状态，通过调用启动线程方法，获得cpu后进入运行态，当然线程也不是一直处于运行状态，因为多个线程之间的切换，线程让出CPU资源，让线程从运行态进入阻塞态，所有的线程都逃脱不了死亡。



- **新建态**

  同**new**关键字创建一个线程，JVM为线程分配内存，初始化成员变量。

- **就绪态**

  线程调用**start()**进入就绪态，等待获取cpu资源，JVM为其创建方法调用**栈和程序计数器**。

- **运行态**

  获得cpu资源，执行**run()**方法中的任务。

- **阻塞态**

  因为某些原因让出cpu资源，从运行态进入暂时的阻塞状态，当再次获取cpu时，又从阻塞态进入就绪态。

  **阻塞情况**

  - **等待阻塞（执行wait()）**

    运行态的线程执行了wait()，线程被放入**等待队列(waiting queue)**

  - **同步阻塞**

    运行态的线程在获取对象的**同步锁**时，发现该对象的同步锁已经被其他线程占用，因此该线程进入阻塞状态。

    该线程被放入**锁池(lock pool)**

  - **其他阻塞**

    运行态的线程执行了**sleep方法或join方法**，或者发出**IO请求**

- **死亡态**

  - **正常结束**

    run()或call()结束

  - **异常结束**

    线程抛出**异常(Exception)或错误(Error)**

  - **调用stop方法**

    线程调用stop方法(**容易产生死锁**)

![image-20210722162006343](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210722162006343.png)

-   就绪状态--->运行状态：获得处理机资源（分派处理机的时间片） 
-   运行状态--->就绪状态：1）处于运行状态的进程时间片用完  2）当有更高优先级的进程就绪时 
-   运行状态--->阻塞状态：1）进程请求资源（外设）使用和分配 2）等待某一事件的发生（IO操作完成） 
-   阻塞状态--->就绪状态：当进程等待事件到来（IO操作结束或者中断的结束）



### 终止线程的方式

- **正常结束**

  程序正常结果，线程自动销毁

- **自定义标志控制**

  正常情况下run方法执行完毕，线程就会终止，**有些特殊情况下，线程需要很长的运行时间，只有在满足外部某些条件下，才能结束进程。**

  可以通过自定义变量来控制执行的时间。

  例如：设定一个boolean类型的变量，执行while（）语句，控制循环。

  ```java
  public class ThreadSafe extends Thread {
   public volatile boolean exit = false; 
   public void run() { 
   //设定变量exit来控制run（）
   while (!exit){
   //需要执行的业务
   }
   } 
  }
  //当exit为true时，while语句不成立，run（）方法结束，线程结束。
  //exit被volatile关键字修饰，实现同步代码，保护线程的安全。
  ```

- **Interrupt()方法结束线程**

  - **线程处于阻塞状态时**

    使用sleep()、同步方法wait（）等方法，进入阻塞状态。

    当调用线程的Interrupt()方法时，会抛出异常(**InterruptException**),通过在代码块中catch捕获异常，通过**break关键字**跳出循环状态。**(调用Interrupt方法一定要捕获异常通过break跳出循环，才能正常结束run方法)**

  - **线程处于运行状态时**

    通过**isInterrupted**()方法判断线程是否处于阻塞状态，如果进入阻塞状态，用阻塞状态的方法来完成线程终止。

    ```java
    public class ThreadSafe extends Thread {
     public void run() { 
     	while (!isInterrupted()){ //非阻塞过程中通过判断中断标志来退出
     		try{
     			Thread.sleep(5*1000);//阻塞过程捕获中断异常来退出
    		    }catch(InterruptedException e){
    				 e.printStackTrace();
    				 break;//捕获到异常之后，执行 break 跳出循环
     			}
     		}
     	} 
    }
    ```

- **stop方法**

  前面也说了stop方法**虽然可以终止线程但是会让线程不安全**。

  stop方法是强制线程终止，就像把计算机的电源断了，而不是正常关机，很可能产生数据上的异常。

  比如一个线程中有其n个子线程，子线程被同步锁绑定，为了保证数据的安全性，如果执行stop方法，停止该线程，那么其子线程会**释放所有的同步锁**，**同时抛出TheadDeatherror的错误，**可能导致子线程中数据的不一致。



**start（）和run（）区别**

**start()**

是用来启动线程，new Thread通过调用start方法让线程处于**就绪状态**，等待获取cpu。

它不需要等待run方法结果就可以去执行其他任务，实现了多线程的过程。

```java
		Thread thread = new Thread(myRunnable,"第一个线程");
        Thread thread1 = new Thread(myRunnable,"第二个线程");


        thread.start();
        thread1.start();
//两个线程争夺cpu，在控制台你可以看到两个线程交替输出
```

补充：**如果同一个线程同时调用两次start()方法会怎么样**

```java
public class TestMain {

    public static void main(String[] args) throws Exception {
        Thread thread = new Thread(new Runnable() {
            @Override
            public void run() {
                System.out.println("开始运行");
            }
        });
        System.out.println("线程当前的状态为" + thread.getState());
        thread.start();
        System.out.println("start后线程当前的状态为" + thread.getState());
        thread.start();
    }
}
/*结果
第一次调用start()方法能够有结果，而第二次则报了IllegalThreadStateException异常
*/
```

来看一下start()方法的源码

```java
	//volatile关键字修饰的threadStatus，保证多线程下该变量的可见性，默认为0 表示处于NEW状态
 private volatile int threadStatus = 0;
 
 public synchronized void start() {
       //如果线程状态不等于0，说明线程状态已经不是NEW了，不是NEW说明至少已经开始运行了，再走start()方法就没意义了，所以会抛出IllegalThreadStateException异常
        if (threadStatus != 0)
            throw new IllegalThreadStateException();
}
```



**run()**

当线程获取cpu时，线程进入运行态，执行run方法中内容，run方法是线程需要完成的工作内容。run方法结束，线程终止。





### **线程的基本方法**

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210730102649764.png" alt="image-20210730102649764" style="zoom:67%;" />

**线程等待(wait)**

当前拥有**对象监视器**的线程调用wait方法，会释放对象监视器的所有权，进入等待队列。

只能等待其他**拥有该对象监视器的线程唤醒或者被中断**，该线程重新获取对象监视器的所有权后才开始执行。

**wait方法一般用在同步方法或同步代码中**

补充：**调用wait方法会释放cpu资源和锁资源，这两个资源。**



**线程睡眠(Sleep)**

线程调用sleep方法进入睡眠状态，与wait方法不同之处在于sleep方法**不会让线程释放所占有的对象锁**，线程进入**Time_Waiting状态**，

wait方法让线程进入**Waiting状态**。

补充：**sleep方法会让当前线程释放cpu资源，但是不会释放当前线程所占有的锁资源(重要)**

锁是用来同步的，保证线程的安全，如果当前线程调用sleep方法后，其他的线程如果需要锁才能够运行，那么它们只能继续等待，如果说某些线程只需要cpu的资源就可以运行，一旦得到cpu资源它们就会立刻执行。



**线程让步(yield)**

yield让线程让出当前所持有的cpu资源，和其他线程一起重新争取cpu资源。一般情况下，优先级高的线程有更大的概率获取到cpu资源，但这不是绝对的，不同操作系统对线程优先级有着不同的敏感度。



**线程中断(interrupt)**

中断一个线程，但是**interrupt方法本身并不是改变线程的状态**，而是给对应**线程设置一个中断标志位**，通过这个中断标志位来判断是否需要中断线程。

**runnable状态**

如果一个线程处于运行状态，使用方法Thread.interrupt()只是将这个线程的中断标志位设置为**true**，此时线程还是处于runnable状态，

具体在线程的run方法中合使的位置检查中断标志位，若为true，说明需要进行中断响应处理，若为false，说明不需要进行中断处理。

例如：

```java
public class InterruptRunnableDemo extends Thread {
    @Override
    public void run() {
        //若为true，进行中断，若为false，执行while()循环体
        while (!Thread.currentThread().isInterrupted()) {
            // ... 单次循环代码
        }
        System.out.println("done ");
    }
    public static void main(String[] args) throws InterruptedException {
        Thread thread = new InterruptRunnableDemo();
        thread.start();
        Thread.sleep(1000);
        thread.interrupt();//true
    }
}
/*
interrupt()设置thread线程的中断标志位为true
isInterrupted()方法判断当前线程的中断标志为是否为true，
*/
```



**Waiting(等待) / Timed-Waiting(超时等待)状态**

使用sleep、同步wait、join进入等待状态，当线程处于这种状态时，调用Thread.interrupt()，会抛出对应的InterruptedException异常。注意：**异常抛出后进行处理，此时线程的中断标志位会被清空(true -> false)**，线程结果提前Waiting / Timed-Waiting状态。

例如：

```java
Thread t = new Thread (){
    @Override
    public void run() {
        try {
            Thread.sleep(1000);
        } catch (InterruptedException e) {
        //exception被捕获，但是为输出为false 因为标志位会被清空
            //此时线程的中断标志为false
            System.out.println(isInterrupted());
        }
    }        
};
t.start();
try {
    Thread.sleep(100);
} catch (InterruptedException e) {
}
t.interrupt();//置为true
```



**Join等待其他线程终止**

join()方法：调用join方法的线程获取cpu资源，其他线程被迫阻塞，只有等当前调用join方法的线程结束释放cpu资源后，其他线程才可以运行。

若在当前线程中的子线程调用join方法，当前线程需要等待子线程运行完后，才可以运行，因此join方法也称为：**等待其他线程终止**。

很典型的主线程中有子线程，子线程调用join方法，主线程就需要等待调用join的线程运行终。

```java
public static void main(String[] args){
    System.out.println(Thread.currentThread().getName() + "线程运行开始!");
     Thread6 thread1 = new Thread6();
     thread1.setName("线程 B");
     thread1.join();
    System.out.println("这时 thread1 执行完毕之后才能执行主线程");
}
```



**线程唤醒(notify)**

和wait方法配套使用，应用与同步场景。

持有锁资源的线程使用wait方法释放锁资源，进入Waiting状态等待唤醒，只能是**拥有当前对象锁**的线程调用notify方法唤醒等待获取当前对象锁的线程，**notify()只能唤醒单个线程并且是随机的**，被唤醒的线程并不能立刻执行，需要等待唤醒它的线程将当前对象锁释放之后，它获取到对象锁之后才继续运行。**notifyAll()**唤醒等待同一个对象锁上的所有的线程。





### Java后台线程(守护线程)

- **定义**

  守护线程又叫做服务线程，它是运行在后台的一个特殊线程。

  主要为用户线程(普通线程)提供服务，当JVM中只剩下守护线程时，JVM将自动退出。

- **优先级**

  守护线程的优先级较低，用于为JVM中其他的对象和线程服务(**垃圾回收就是一个守护线程**)

- **设置**

  通过 setDaemon(true)来设置线程为“守护线程”；可以将一个用户线程设置为守护线程，守护线程中产生的新线程也是守护线程。

- **Example**

  垃圾回收就是一个经典的守护线程，它是一个优先级较低的线程，JVM中运行的普通线程产生的垃圾就由它来回收，当JVM中不再运行用户线程时，垃圾回收线程就会自动退出。



### 线程上下文切换

**利用时间片轮转的方式**，实现了一个CPU可以为多个线程服务。

CPU为每个线程设置一定的服务时间，当前服务的线程时间到了，就将当前线程的状态保存下来，接着去为下一个线程服务，多个线程轮巡，当下次再遇到这个线程时，加载上一次状态继续服务。这就是**上下文切换过程**。

![img](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/v2-b93776903a775f5265862124654b6a8e_720w.jpg)

**进程**

是程序执行的一次过程，即进程从创建到运行再到消亡的过程。

**是系统进行资源分配的独立单位**

进程之间是相互独立的，因此很难进行进程间的通信。



**上下文**

某一时间点上**cpu寄存器和程序计数器内容**



**寄存器**

CPU 寄存器是 CPU 内置的容量小、但速度极快的内存。



**程序计数器**

专用寄存器，**专门用来表明正在执行的cpu指令序列，用于存储cpu正在执行的指令位置或下一次执行的指令。**



**PCB-"切换帧"**

**进程是由内核来管理和调度，进程的切换只能发生在内核中。**线程的上下文的切换也是在内核(**操作系统的核心**)中，上下文切换中信息内容是保存在**进程控制块中**(**PCB**)的。当再次用到时直接从这里调用。



**上下文切换的活动**

- 挂起一个线程，将挂起的线程在CPU中的状态(上下文)存储在内存中
- 在内存中检索下一个线程的上下文并将在CPU的寄存器中恢复
- 在程序计数器中找寻上一次执行指令位置，用来进行这次运行的开头。



**线程上下文切换的原因**

1. 在当前线程的cpu时间片用完之后，cpu正常去调用下一个线程。
2. 多个线程抢占锁资源，获取锁的线程执行，其他线程挂起。
3. 当前线程遭遇**IO阻塞**，调度器将当前线程挂起，继续执行下一个。
4. 用户代码挂起当前任务，让出cpu时间片
5. 硬件中断





### Java锁

[不可不说的Java“锁”事 - 美团技术团队 (meituan.com)](https://tech.meituan.com/2018/11/15/java-lock.html)

![img](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/20181122101753671.png)

#### **乐观锁**

对同一数据进行并发操作，乐观锁在进行操作数据时总是乐观认为不会有别的线程修改数据，因此它不会对资源加锁。当自己在进行数据修改之前它会先进行判断有没有其他线程修改了数据，如果数据没有修改，就写入数据。如果数据被修改了，则根据不同的实现方式执行不同的操作（例如报错或者自动重试）。

java中乐观锁基本上通过**CAS（Compare And Swap（比较与交换），是一种无锁算法）**操作实现的，，CAS 是一种更新的原子操作，比较当前值跟传入值是否一样，一样则更新，否则失败。

​		**应用场景：适合读操作多的场景，不加锁的特性让读操作的性能得到很大的提升**

#### **悲观锁**

对同一数据进行并发操作，悲观锁总认为别的线程会改写数据，因此在获取资源前它会对资源加锁，确保数据不会被更改。

Java中，**synchronized**关键字和**Lock**的实现类都是**悲观锁**。

**应用场景：适合写操作多的场景，加锁的特性确保数据的准确性**

#### **自旋锁**

多个线程并发操作同一个资源，发现该资源已经被占用，一般的情况是需要等待该资源的锁被释放之后，其他线程去争夺锁，获得锁的线程执行，其他线程等待(上下文的切换)，从**运行态转变为阻塞态**，**这个状态转换的过程需要耗费时间**，**如果说当前占用资源的线程运行的时长比其他线程状态转换时长还要短，那么可以考虑不需要进入阻塞状态，而是让线程等待一会(自旋一会)，如果自旋之后资源已经被释放，那么就不必阻塞直接获取同步资源即可**

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/452a3363.png" alt="img" style="zoom: 50%;" />

注意：线程自旋的过程也是要消耗cpu的，因此需要设定一个自旋的时间（**默认是10次，可以使用-XX:PreBlockSpin来更改**），来确保资源能否在规定时间内获取到，如果获取不到，那么线程就从自旋转为阻塞。

**优缺点：**

- 自旋锁适合在对于资源竞争不激烈的情况下，尽量减少线程阻塞再到唤醒的过程，线程自旋的时间小于线程状态切换的时间，能够大幅度提升性能。
- 在资源竞争激烈或者持有同步锁的线程执行耗时很长，这个时候自旋锁就不适用。因为让线程一直占着cpu，但是线程又没有做事，纯属浪费资源和时间，并且此时其他需要cpu的线程无法得到，导致性能大大下降。

**自旋锁开启**

JDK1.4.2中引入，使用-XX:+UseSpinning来开启,-XX:PreBlockSpin 为自旋次数。

JDK1. 6中变为默认开启，并且引入了自适应的自旋锁（**适应性自旋锁**）。

**适应性自旋锁**

1.6之前的自旋锁的次数一定程度是写死的，之后的自适应锁次数不在固定，是**由上一次在同一个锁上的自旋时间以及锁的拥有者的状态来决定的**。

如果对于同一个锁对象，自旋等待并且成功在自选周期内获得了锁资源，线程成功执行，那么JVM认为下一次这个自旋的过程很可能成功，因此会把自旋的周期持续相对更长的时间。反之，自旋过程很少获取锁资源，JVM认为这个自旋执行效率可能不高，可能考虑取消自旋进入阻塞状态，避免资源的浪费。



#### **公平锁**

多个线程**按照顺序**获取锁，需要获取锁的线程进入队列中等待，队列中最先发起请求锁的线程，也就是队列中的第一个线程能够最先获得锁，这就是公平锁。

**好处：队列中等待锁资源的线程都能够获得锁，不会出现有些线程一直得不到锁的情况**

**缺点：整体吞吐量降低，因为每个没有获得锁的线程都要去队列中排队等待，cpu每次都要进行线程状态的转换，增加了开销**

排队按顺序打水

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210725104704513.png" alt="image-20210725104704513" style="zoom: 50%;" />



#### **非公平锁**

如果当前资源有其他线程正在时候，这个时候又来其他线程也需要这个资源，它并不会马上进入队列中等待，其他线程会尝试去等待锁资源的释放，如果获得了锁直接使用，不会去队列中等待(**插队**)，如果没有获取到锁，它才会去队列中等待。

**好处：减少了线程阻塞到唤醒的过程中的开销，整体吞吐效率提升**

**缺点：位于等待队列中的线程可能要等待很长时间才能获取到锁，甚至可能永远都获取不到**

插队打水

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/4499559e.png" alt="img" style="zoom: 50%;" />

**非公平锁实际执行的效率要远远超出公平锁，除非程序有特殊需要，否则最常用非公平锁的分配机制。**



#### **可重入锁（递归锁）**

当一个线程调用同步方法时获取对象锁，执行方法内部的代码，方法内部中又有同步方法，他会自动获取锁（**前提是锁的对象一定是同一个对象或者类**），该线程不会因为已经得到的锁没有释放而阻塞。**Sychronized和ReentrantLock**都是可重入锁。

例如：

```java
public class Widget {
    public synchronized void doSomething() {
        System.out.println("方法1执行...");
        doOthers();
    }

    public synchronized void doOthers() {
        System.out.println("方法2执行...");
    }
}
/*
线程获取Widget的对象锁调用doSomething方法，调用doOthers方法，synchronized是可重入锁，线程继续获取锁调用doOthers方法
*/
```

n还是打水问题

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/58fc5bc9.png" alt="img" style="zoom: 50%;" />

村民(线程)需要获取锁才能打水，现在管理员规定，一个锁可以和同一个村民多个水桶绑定，因此第一个水桶和锁绑定后打水，接着将锁和第二个水桶绑定打水，所有的水桶中都装满了水，将锁还给管理员，村民能够完成整个打水的流程。



#### **非可重入锁**

非重入锁修饰的方法，在线程获取对象锁调用doSomething方法需要线程释放当前的锁，重新获取doOthers方法的锁才能执行，然而这两个方法的锁是同一个，锁已经被当前线程所持有，无法释放也无法获取，会造成死锁。

打水问题

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/ea597a0c.png" alt="img" style="zoom: 50%;" />

村民（线程）需要获得锁才能打水，管理规定一个锁只能锁定村民的一个水桶，村民将水桶a和锁锁定打水，这个锁无法释放，村民的水桶b没有锁无法打水，导致线程死锁。

#### **独享锁**

独享锁又叫排它锁，该锁只能被一个线程锁持有，若数据A被某个线程加了独享锁，该数据A不能再被加任何锁。获得独享锁的线程既能够读数据也能够修改数据，其他的线程只能等待。Synchronized和ReentrantLock以独占方式实现的互斥锁。

#### **共享锁**

允许多个线程同时获取锁，并发访问，共享资源。若数据B被线程加了共享锁，其他线程只能对B加共享锁，不能加排它锁。获得共享锁的线程只能够读数据，不能修改数据。



#### **Synchronized同步锁**

同步锁可以将任意一个不为null的对象当作锁。它属于**独占式的悲观锁**，同时属于**可重入锁**、**非公平锁**



**作用范围**

[(9条消息) Java中synchronized同步锁用法及作用范围_在梅边的专栏-CSDN博客_java 同步锁](https://blog.csdn.net/yx0628/article/details/79086511)

java中的**对象锁和类锁**：

对象锁作用于：对象实例方法或者对象实例上。

类锁作用于：类的静态方法和类对应的Class对象。

一个类可以对应多个对象实列，一个对象拥有一个对象锁，多个对象对应多把锁，因此各个对象实例之间的对象锁互不干扰。

每个类只有一个，对应一把类锁。

**注意：类锁只是概念上的，并不是真实存在的，这里是用来理解同步锁作用在静态方法中。**

- 非静态方法

  使用Synchronized修饰非静态方法，**锁定的是调用当前方法的对象实例**。

  ```java
      public synchronized void test(){
          // TODO
      }
  ```

  - 创建两个线程，同时调用同一个对象中的同步方法test()，那么同一时间只能是获得对象锁的线程执行，另一个被挂起，等待获取对象锁。
  - 创建两个线程，同时调用同一个对象中的同步方法test()、同步方法test1（），那么同一时间只能是获得对象锁的线程执行，另一个被挂起，等待获取对象锁。**只要是调用同一个对象中的同步方法，只要对象锁被线程获取占用了，其他线程必须等待**
  - 创建两个线程，同时调用同一个对象中的同步方法test()、**非同步**方法test1（），那么两个线程交替进行，说明**获取对象锁只能确保被Synchronized修饰的方法或代码块同步，非同步方法不受影响，其他的线程可以访问同一对象中的非同步方法**.。

- 静态方法

  使用**Synchronized关键字**修饰静态方法，修饰静态代码块

  ```java
      public static synchronized void test(){
          // TODO
      }
  ```

  ```java
  	//需要引用当前的类
  public static void test(){
          synchronized (TestSynchronized.class) {
              // TODO
          }
      }
  ```

  - 创建两个线程，同时调用同一类中的同步静态方法test(),同一时间只能由一个线程执行test方法，另一个线程挂起等待。

    一个类可以创建很多对象，这些对象同属于一个类，静态方法是属于类，同步后的静态方法也是唯一的。

  - 创建两个线程，同时调用类中的同步静态方法test（），同步非静态方法test1（），发现两个线程交替，并没有产生阻塞，

    **同步静态方法和同步非静态方法所需要的锁并非同一把锁，对象锁和类锁两个是相互独立的**

- 代码块

  使用Synchronized修饰代码块，根据传入的参数，来决定锁定的哪个。

  ```java
      public void test(){
          synchronized (this) {
              // TODO
          }
      }
      //如果传入的参数是 this，那么锁定的也是当前的对象：
  ```



**Synchronized底层实现**

```java
package com.paddx.test.concurrent;

public class SynchronizedDemo {
    public void method() {
        synchronized (this) {
            System.out.println("Method 1 start");
        }
    }
}
```

Synchronized**同步代码块的语义底层是基于对象内部的监视器锁(monitor)**，分别使用**monitorenter**和**monitorexit**两条指令实现。

**monitorenter：**指令在编译为字节码后插入到同步代码块的开始位置。

每个对象都有一个监视器锁（monitor），当monitor被线程占用时当前就处于锁定的状态，线程执行monitorenter执行尝试获取monitor的控制权，尝试获取对象锁。过程：

- 如果monitor当前的进入数为0，表示没有线程占用，线程可以进入monitor，之后将数值设置为1，成为该monitor的所有者。
- 如果monitor已经被其他线程所占用，当前线程进入阻塞的状态，等待monitor的进入值为0时，尝试重新获取monitor的所有权。
- 如果当前线程已经占用monitor，只是重新进入，则进入monitor的进入数加1



**monitorexit：**指令在编译为字节码后插入到同步代码块的结束位置

执行这个指令的线程必须是 objectref 所对应的 monitor 的所有者。执行指令，monitor的进入数减一，如果进入数变为0，则线程退出monitor，不再是monitor的所有者，其他被阻塞的线程尝试获取monitor的所有权。



每个monitorenter指令的执行都要对应monitorexit指令。



Synchronized同步方法中是用**ACC_SYNCHRONIZED标识符来实现同步的**

反编译：

![img](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/820406-20160418202553429-1642545018.png)

相比于普通方法常量池中多了**ACC_SYNCHRONIZED**标识符来实现同步，如果该常量被设置了，**执行线程将先获取monitor**，获取monitor之后才可以执行方法体，执行完后释放monitor。它是一种隐式的同步的实现。





**Synchronized核心组件**

1. **Wait Set** ：调用wait方法被阻塞放入的地方
2. **Contention List(竞争队列)**：多个线程竞争请求锁。
3. **Entry List**：竞争队列中多个线程中有资格成为候选资源的线程被放入Entry List中。
4. **OnDeck**：只有一个线程能够获得锁的线程。
5. **Owner**：已经获取锁资源的线程
6. **!Owner**：已经释放了锁资源的线程



<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/20200304230629833.png" alt="在这里插入图片描述" style="zoom:80%;" />

多个线程请求同一资源，如果资源被占用那么，线程被放入**Contention List(竞争队列)**中，在竞争队列中将具有成为候选资源的线程放入到**Entry List**中，在Entry List选取能够成为OnDeck的线程(**能够获取monitor的线程**)，onDeck线程尝试获取资源的monitor，获取到monitor的所有权后进入到Owner，同时将monitor的进入数加1，线程运行。如果在线程运行的时候执行了wait方法，进入阻塞的状态，该线程会释放monitor并将其进入数减一，放入**Wait Set（阻塞队列中）**。阻塞队列中的线程和等待队列中的线程一同争夺锁定资源。

 如果线程式正常运行完毕，也会释放monitor，其他线程争夺monitor的所有权。





在 JDK1.6 之后，出现了各种锁优化技术，如轻量级锁、偏向锁、适应性自旋、锁粗化、锁消除等，这些技术都是为了在线程间更高效的解决竞争问题，从而提升程序的执行效率。



[Java并发编程：Synchronized底层优化（偏向锁、轻量级锁） - liuxiaopeng - 博客园 (cnblogs.com)](https://www.cnblogs.com/paddix/p/5405678.html)

**Java对象头**

Hotspot虚拟机，java对象头主要包含：**Mark Word(标记字段)、  Klass Pointer(类指针)**

Mark Word：主要存储**对象的HashCode、GC分代年龄、锁状态以及锁标志位**

Klass Poniter：对象指向类的**元数据的指针**，表明**该对象对应类的实例**。

**Monitor**

Synchronized通过给同步资源加锁实现同步操作，这个锁存在于Java对象头中，每个对象有都有一把锁，这把锁指得就是Monitor(监视器锁/内部锁)。

Monitor是**线程私有的数据结构**，每一个线程都有一个**monitor record列表**和一个**全局列表**。monitor中有一个**Owner字段**，若锁没有被线程占用，字段为**NULL**,若被线程占用，存放拥有该锁线程唯一标识。

Monitor是**依赖底层操作系统的Mutex Lock(互斥锁)来实现线程的同步**。操作系统**实现线程之间的切换**，也就是线程的阻塞和唤醒之间状态的转换，这种状态的转换需要耗费的时间和资源都是很多的。这也是**起初Synchronized实现同步的方式，也是其效率低的原因**。

将依赖于底层操作系统Mutex Lock实现的锁称之为"**重量级锁**"。

为了减少重量级锁带来的时间和资源上的消耗，引入了“**偏向锁**”和"轻量级锁" ，JKD1.6中对Synchronized做出的优化。



锁的状态有四种：无锁、偏向锁、轻量级锁、 重量级锁，级别从低到高依次是：无锁、偏向锁、轻量级锁和重量级锁。**锁状态只能升级不能降级。**

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210728135419630.png" alt="image-20210728135419630" style="zoom: 67%;" />

#### **无锁、偏向锁、轻量级锁、重量级锁**

- 无锁

  无锁表示对资源没有进行锁定，允许多个线程同时访问并修改同一资源，但是最终只能是一个线程对其修改成功。

  **存放内容**：对象hashCode，GC分代年龄，锁标志位:**01**，是否为偏向锁

- 偏向锁

  偏向锁表示一段同步代码一直被一个线程所访问，该线程会**自动获取锁，降低获取锁的代价**。实现在只有一个线程执行同步代码时进一步提高性能。

  引入偏向锁是为了在无多线程竞争的情况下尽量减少不必要的轻量级锁执行路径。因为轻量级锁的获取以及释放需要执行多次的CAS原子指令，而偏向锁只在设置线程ID时执行一次CAS操作。

  **存放内容：**线程id、GC分代年龄、是否为偏向锁、锁标志位：**01**

  **获取偏向锁的过程：**

  - **可偏向状态**：检查Mark Word中偏向锁的表示是否为：1，锁标志位为：01
  - **检测线程ID**：线程ID是否为当前线程，如果是，执行同步代码，如果不是，执行CAS操作。
  - **执行CAS操作**：若线程ID不是当前线程，通过CAS操作竞争锁。若竞争成功，将线程ID设为当线程。若竞争失败，撤销偏向锁。
  - **撤销偏向锁**：CAS操作无法获取锁，说明有多个线程在竞争同一把锁，当前无法再使用偏向锁，需要将偏向锁撤销转换成其他锁。

  **偏向锁撤销：**

  当偏向锁遇到其他线程尝试竞争时，持有偏向锁的线程才会主动释放锁，线程不会主动去释放偏向锁。偏向锁的撤销，需要等待全局安全点（在这个时间点上没有字节码正在执行），它会首先**挂起**拥有偏向锁的线程，判断锁对象是否处于被锁定状态，撤销偏向锁后恢复到未锁定（标志位为“01”）或轻量级锁（标志位为“00”）的状态。**之后在安全点被阻塞的线程继续往下执行同步代码**

  **禁用偏向锁（-XX:-UseBiasedLocking）**

- 轻量级锁

  当锁是偏向锁时，有其他的线程尝试争取偏向锁，那么这个偏向锁就会升级为轻量级锁。轻量级锁适用于交替执行同步块的情况，减少线程之间切换带来的性能消耗，通过**自旋的方式**获取锁，不会产生**阻塞**，提升性能。注意：**轻量级锁的出现并不是替代重量级锁，在一定条件下，轻量级锁会升级为重量级锁**。

  **存放内容：**指向栈中锁记录的指针。

  **轻量级锁加锁过程：**

  1. 在进入同步块时，如果同步对象锁状态为：**无锁(锁标志：01，偏向锁为：0)**，JVM会在当前线程中的栈帧中建立一个**锁记录(Lock Record)**,该空间是用来**存储对象头中Mark Word的拷贝**。

     <img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210728144857021.png" alt="image-20210728144857021" style="zoom:50%;" />

     ​																	 轻量级锁CAS操作之前堆栈与对象的状态

  2. 拷贝对象头中Mark Word复制到锁记录中

  3. 拷贝成功后，JVM使用CAS(Compare And Swap)操作尝试将对象头中的Mark Word指向锁记录，让锁记录中的**Owner（存放拥有该锁线程唯一标识）**指向对象头中的Mark Word。若更新成功，执行步骤4，若失败，执行步骤5

  4. 更新成功，该线程拥有的该对象的锁，对象头中锁标志:00。

     <img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/820406-20160424105540163-1019388398.png" alt="img" style="zoom: 33%;" />

     ​																	轻量级锁CAS操作之后堆栈与对象的状态

  5. 更新失败，JVM会先去检查对象头中Mark Word 是否指向当前线程的栈帧，如果有说明当前线程已经拥有了该对象锁，可以直接进入同步块继续执行，如果没有，说明有多个线程竞争锁，这时轻量级锁就要晋升为重量级锁，锁标志：10，Mark Word中存储的就是**指向重量级锁的指针**，后面等待的线程也要进入阻塞状态了。

  **轻量级锁解锁过程：**

  1. 通过CAS操作尝试把线程中复制的Displaced Mark Word对象替换成当前的Mark Word

     <img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210823142051828.png" alt="image-20210823142051828" style="zoom: 50%;" />

  2. 若替换成功，表明当前线程释放锁的过程，没有其他线程请求该锁资源，没有竞争发生。

  3. 若替换失败，说明有其他线程尝试获取该锁(此时锁已经膨胀)，存在着竞争，将轻量级锁升级为重量级锁。

- 重量级锁

  依赖于底层操作系统Mutex Lock实现的锁称之为"**重量级锁**"。

  操作系统**实现线程之间的切换**，也就是线程的阻塞和唤醒之间状态的转换，这种状态的转换需要耗费的时间和资源都是很多的。

**重量级锁、轻量级锁和偏向锁之间转换**

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/820406-20160424163618101-624122079.png" alt="img" style="zoom:67%;" />

#### **分段锁**

ConcurrentHashMap在java7中就采用分段锁的思想，给每一段分别加上对应的一把锁，保证线程安全。

**减少锁持有的时间**

只用在有线程安全要求的程序上加锁

**减少颗粒度**

将大对象(**会被很多线程访问**)，拆分成小对象，大大增加并行度，降低锁的竞争，锁的竞争度降低了，偏向锁、轻量级锁成功率才能得到提升。最经典的减小颗粒度案例:**ConcurrentHashMap**。



#### **锁粗化**

为了保证并发的有效性，会要求每个线程持有锁的时间尽可能的短，即在使用完资源后，立刻释放锁资源。

凡是有度，若有一系列操作是针对同一个对象（操作的是同一把锁），每次操作都要加锁和解锁，就会觉得繁琐并且耗费了额外的资源，因此就对锁进行了粗化，在第一次操作时加锁，中间其他一系列的操作不再进行解锁、加锁，而是在最后一次操作时解锁，保证了效率的同时也减少了资源的消耗。

例如：StringBuffer中append方法。

```java
package com.paddx.test.string;

public class StringBufferTest {
    StringBuffer stringBuffer = new StringBuffer();

    public void append(){
        stringBuffer.append("a");
        stringBuffer.append("b");
        stringBuffer.append("c");
        //一系列的操作进行锁的粗化，整个过程只进行一次加锁和解锁
    }
}
/* 
单单调用一次要进行加锁和解锁stringBuffer.append("a");
*/
```



#### 锁销除

如果发现不可能被共享的对象，则可以消除这些对象的锁操作，删除不必要的加锁操作，发生在**编译器级别**。

java的编译体系公有两次编译阶段，第一次将java源代码通过编译器编译为.class字节码文件。第二次通过JVM解释器转换成二进制机器码。

第二阶段JVM通过解释器将字节码文件解释成对应操作系统的二进制机器码，**传统的解释器功能是逐行读入，逐行解释**，这样执行的效率不高，为了解决这个问题，引入了**JIT（即时编译技术）**。

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210903144507676.png" alt="image-20210903144507676" style="zoom: 80%;" />

引入即使编译技术，通过解释器解释，当JVM发现某个方法或代码块运行特别频繁时，就将其认定为**热点代码，JIT**会把部分“热点代码”翻译成本地机器相关的机器码，并进行优化，然后再把翻译后的机器码缓存起来，以备下次使用。

JIT优化中最重要的一个就是**逃逸分析**。

逃逸分析：当一个对象被定义在方法中时，该对象是一个局部变量，若它作为参数传递到了其他的方法中时(**被外部方法所引用**)，就称为**方法逃逸**。



append方法被synchronized锁修饰

```java
 @Override
    public synchronized StringBuffer append(String str) {
        toStringCache = null;
        super.append(str);
        return this;
    }
```



```java
public static StringBuffer craeteStringBuffer(String s1, String s2) {
    StringBuffer sh = new StringBuffer();
    sh.append(s1);
    sh.append(s2);
    return sh;
}//sh作为局部参数被外界引用了，因此sh是方法逃逸，可能造成线程不安全。
```





```java
public class SynchronizedTest02 {

    public static void main(String[] args) {
        SynchronizedTest02 test02 = new SynchronizedTest02();
        //启动预热
        for (int i = 0; i < 10000; i++) {
            i++;
        }
        long start = System.currentTimeMillis();
        for (int i = 0; i < 100000000; i++) {
            test02.append("abc", "def");
        }
        System.out.println("Time=" + (System.currentTimeMillis() - start));
    }

    public void append(String str1, String str2) {
        StringBuffer sb = new StringBuffer();
        sb.append(str1).append(str2);
    }
}
/*
 StringBuffer sb = new StringBuffer();作为append方法中的局部参数，它并没有被其他方法所以引用，因此无法逃逸，所以这个过程是线程安全的，没有必要进行加锁操作，就可以将锁消除
*/
```





#### **ReentrantLock**

ReentrantLock实现了**Lock接口**中的方法，它是一把**独占锁、悲伤锁、可重入锁、即可以实现公平锁也可以实现非公平锁**



**ReentrantLock** **与** **synchronized**

- 两者都保证了**可见性和互斥性**

- synchronized是独占锁，synchronized会被**JVM**自动加锁和解锁，方便但不够灵活

  ReentrantLock也是独占锁，它是通过**手动lock() 和unlock()**来进行加锁和解锁操作，操作不易但是灵活。

- synchronized与ReentrantLock都是**可重入锁**，区别还是在加锁的过程上，synchronized是自动加解锁，ReentrantLock是手动加解锁，考虑程序安全性会在finally语句块中加入unlock()。（**可能造成死锁**）

  补充：synchronized**在发生异常时，自动释放占用的锁**，而ReentrantLock需要手动释放锁，**不然会造成死锁**

- ReentrantLock相比于synchronized，最大优势在于它可以实现**公平锁**和**非公平锁**，synchronized无法实现公平锁。

  其次是ReentrantLock能够**响应中断**，synchronized无法做到。

JDK1.6之前，ReentrantLock的性能优于Synchronized的，在JDK1.6中优化了Synchronized(**引入了轻量级锁、偏向锁、适应性自旋、锁粗化、锁消除等**)，使得Synchronized性能得到很大提升。



**ReentrankLock实现**

```java
    public class MyService {
        //构造函数中参数若不指定，默认为非公平锁
        private Lock lock = new ReentrantLock();
        //Lock lock=new ReentrantLock(true);//公平锁
        //Lock lock=new ReentrantLock(false);//非公平锁
        private Condition condition=lock.newCondition();//创建 Condition
        public void testMethod() {
            try {
                //手动加锁
                lock.lock();//lock 加锁
                //1：wait 方法等待：
                //System.out.println("开始 wait");
                condition.await();
       		 //通过创建 Condition 对象来使线程 wait，必须先执行 lock.lock 方法获得锁
            //:2：signal 方法唤醒
                condition.signal();//condition 对象的 signal 方法可以唤醒 wait 线程
                for (int i = 0; i < 5; i++) {
                    System.out.println("ThreadName=" + Thread.currentThread().getName()+ (" " + (i + 1)));
                }
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            finally
            {
                //手动解锁
                //解锁
                lock.unlock();
            }
        } 
    }

//void lock():若需要的获取的锁处于空闲状态，那么当前线程获得锁资源。如果锁被其他线程占用，那么就禁用当前线程，直到获取锁为止，
//获取不到锁就不罢休，不可被打断。
//void unlock():当前线程执行完后，释放锁资源
//boolean tryLock():若当前锁可用，立刻返回true，否则立刻返回false。
//boolean tryLock(long timeout TimeUnit unit):设置超时时间，如果在规定时间内没有获取到锁资源，返回false，如果获取到锁，返回true。

//lock()和tryLock()区别：两者都是获取锁的过程，区别在于lock方法如果获取不到锁，当前线程就会被阻塞，直到能够得到锁，再继续执行。tryLock方法如果获取到锁，继续往下执行，如果得不到锁，会立刻返回false，并不会阻塞线程，而是继续往下执行。
```



**ReentrantLock的中断响应机制**

与Synchronized不同，ReentrantLock有中断响应的机制。

中断响应就是一个线程若获取不到锁，并不会一直在那里等待，ReentrantLock会给予一个中断的响应。而Synchronized修饰的资源，若线程尝试去获取锁，得不到锁就会一直等待。



**lock()**:若资源中的加锁方式使用了这种方法，那么在线程获取不到锁时，线程被阻塞，直到获取锁资源。

**若发出中断指令，该方法接受中断指令中断了持有锁的线程，但是它并不能立刻unlock解锁，而是机械式执行完所有的操作，在释放锁。**

**lockInterruptibly()**:优先响应中断，也就是若收到中断指令，它会中断持有锁的线程，立刻释放锁资源。

这个方法适合于tryLock()配合使用，中断优先级低的线程，将资源让给优先级高的线程来。



```java
public class ThreadDemo extends Thread {
    ReentrantLock  firstLock;
    ReentrantLock  secondLock;

    int lock;

    public ThreadDemo( int lock ,ReentrantLock  firstLock, ReentrantLock  secondLock){
        this.firstLock = firstLock;
        this.secondLock = secondLock;
        this.lock = lock;
    }

    @Override
    public void run(){
        try {
            if (lock ==1){
                firstLock.lock();
                System.out.println("线程"+Thread.currentThread().getName()+" 如果执行中断操作，lock方法还在工作");
                TimeUnit.MILLISECONDS.sleep(600);
                secondLock.lock();
            }else{
                firstLock.lockInterruptibly();
                System.out.println("线程"+Thread.currentThread().getName()+" 没有被中断,lockInterruptibly正常工作");
                TimeUnit.MILLISECONDS.sleep(600);
                secondLock.lockInterruptibly();
            }
        } catch (InterruptedException e) {
            e.printStackTrace();
        }finally {
            firstLock.unlock();
            secondLock.unlock();
            System.out.println(Thread.currentThread().getName()+"获得锁资源执行后释放资源");
        }
    }


    public static void main(String[] args) {
        ReentrantLock first = new ReentrantLock();
        ReentrantLock second = new ReentrantLock();
        ThreadDemo thread1 = new ThreadDemo(1,first,second);
        ThreadDemo thread2 = new ThreadDemo(1,first,second);
//        ThreadDemo thread1 = new ThreadDemo(2,first,second);
//        ThreadDemo thread2 = new ThreadDemo(2,first,second);
        thread1.start();
        thread2.start();
        thread1.interrupt();
    }

}
/*
创建了两组线程thread1、thread2,它们参数分别给1、2
1:对应使用lock方法
2:使用lockInterruptibly方法
执行参数1的线程时，中断thread1线程
lock中的方法体
结果：线程Thread-0 如果执行中断操作，lock方法还在工作。该方法在接受中断后，并没有立刻unlock

执行参数2的线程时，中断thread1线程
结果：thread1线程的lockInterruptibly在接受到中断时立刻释放资源，控制台中没有输出thread1。
*/
```



**ReentrantLock中的Condition**

在JDK1.5中加入，**用来替代传统Object类的wait()、notify()方法实现线程间的通讯协作更加安全和高效**，

Condition**是一个接口**，基本的方法是**await()和signal()**,阻塞和唤醒。

Condition的实现

```java
private Lock lock = new ReentrantLock();
Condition condition=lock.newCondition();//创建 Condition
Condition condition1=lock.newCondition();//创建 Condition
```

可以创建多个Condition对应绑定多个线程，每个线程调用所绑定的方法，condition实现阻塞和唤醒就可以控制线程的状态，进而让多个线程之间来回切换，实现多线程的通讯协作功能。

**注意**：调用Condition的await()和signal()方法，都必须在lock保护之内，就是说必须在lock.lock()和lock.unlock之间才可以使用。

[Java多线程之ReentrantLock与Condition - 平凡希 - 博客园 (cnblogs.com)](https://www.cnblogs.com/xiaoxi/p/7651360.html)

```java
public class ThreadReentrantLockCondition {

    //实现Condition来控制线程之间的切换
    //定义
    public ReentrantLock lock = new ReentrantLock();

    //线程a绑定一个Condition
    public Condition conditionA = lock.newCondition();

    //线程b绑定一个Condition
    public Condition conditionB = lock.newCondition();

    public void awaitA(){
        try {
            lock.lock();
            System.out.println("线程:"+Thread.currentThread().getName()+"进入了awaitA方法中");
            long startTime = System.currentTimeMillis();
            //执行conditionA的等待,必须先执行 lock.lock 方法获得锁
            conditionA.await();
            //唤醒了线程了
            long endTime = System.currentTimeMillis();
            System.out.println("线程"+Thread.currentThread().getName()+"被唤醒了");
            System.out.println("该线程睡眠了"+( endTime- startTime));
        } catch (InterruptedException e) {
            e.printStackTrace();
        }finally {
            lock.unlock();
        }
    }


    public void awaitB(){
        try {
            lock.lock();
            System.out.println("线程:"+Thread.currentThread().getName()+"进入了awaitB方法中");
            long startTime = System.currentTimeMillis();
            //执行conditionB的等待,必须先执行 lock.lock 方法获得锁
            conditionB.await();
            //唤醒了线程了
            long endTime = System.currentTimeMillis();
            System.out.println("线程"+Thread.currentThread().getName()+"被唤醒了");
            System.out.println("该线程睡眠了"+( endTime- startTime));
        } catch (InterruptedException e) {
            e.printStackTrace();
        }finally {
            lock.unlock();
        }
    }


    public void signAllA(){
        try{
            lock.lock();
            System.out.println("唤起线程A");
            conditionA.signalAll();
        } finally {
            lock.unlock();
        }
    }


    public void signAllB(){
        try{
            lock.lock();
            System.out.println("唤起线程B");
            conditionB.signalAll();
        } finally {
            lock.unlock();
        }
    }


}

class Service extends Thread{
    ThreadReentrantLockCondition threadReentrantLockCondition ;

    public Service(ThreadReentrantLockCondition threadReentrantLockCondition ){
        this.threadReentrantLockCondition = threadReentrantLockCondition;
    }
    @Override
    public void run(){
        threadReentrantLockCondition.awaitA();
    }
}

class Service1 extends Thread{
    ThreadReentrantLockCondition threadReentrantLockCondition ;

    public Service1(ThreadReentrantLockCondition threadReentrantLockCondition ){
        this.threadReentrantLockCondition = threadReentrantLockCondition;
    }

    @Override
    public void run(){
        threadReentrantLockCondition.awaitB();
    }
}


    public static void main(String[] args) throws InterruptedException {
        ThreadReentrantLockCondition threadReentrantLockCondition = new ThreadReentrantLockCondition();
        Service service = new Service(threadReentrantLockCondition);
        Service1 service1 = new Service1(threadReentrantLockCondition);

        Thread A = new Thread(service);
        Thread B = new Thread(service1);

        //开启线程
        A.start();
        B.start();


        //唤醒线程A
        Thread.sleep(2000);
        threadReentrantLockCondition.signAllA();


        //唤醒线程B
        Thread.sleep(2000);
        threadReentrantLockCondition.signAllB();

    }
/*
线程:Thread-3进入了awaitB方法中
线程:Thread-2进入了awaitA方法中
唤起线程A
线程Thread-2被唤醒了
该线程睡眠了1999
唤起线程B
线程Thread-3被唤醒了
该线程睡眠了4000

线程A和线程B启动运行后，通过Condition分别进入阻塞的状态，之后通过Condition中signall方法来唤醒，这样可以控制线程的执行顺序。
*/
```



**经典的生产者消费者模式**

```java
/**
 * 生产者消费者问题(同步与互斥)
 */
public class ThreadProAndCon {
    public Lock lock = new ReentrantLock();
    public Condition condition = lock.newCondition();
    public int num = 0 ;
    public boolean flag = false;


    public void produce(){

        try {
            lock.lock();
            //判断当前是否该该生产产品
            while (flag  == true){
                //不需要生产产品，停止生产
                condition.await();
            }
            num++;
            System.out.println("生产者生产"+ num+"个产品");
            //生产者要进入阻塞状态
            flag = true;
            //叫醒消费者起来消费
            condition.signalAll();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }finally {
            lock.unlock();
        }

    }
    public void consume(){

        try {
            lock.lock();
            //判断当前是否该消费产品
            while (flag  == false){
                //没有产品，停止消费
                condition.await();
            }
            num--;
            System.out.println("消费者消费"+ num+"个产品");
            //消费者要进入阻塞状态
            flag = false;
            //叫醒生产者起来生产
            condition.signalAll();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }finally {
            lock.unlock();
        }

    }

}


class  Service2 extends Thread{
    ThreadProAndCon threadProAndCon ;

    public Service2(ThreadProAndCon threadProAndCon){
        this.threadProAndCon = threadProAndCon;
    }

    @Override
    public void run(){
        for (int i = 0; i < 10 ; i++) {
            threadProAndCon.produce();
        }
    }
}

class  Service3 extends Thread{
    ThreadProAndCon threadProAndCon ;

    public Service3(ThreadProAndCon threadProAndCon){
        this.threadProAndCon = threadProAndCon;
    }

    @Override
    public void run(){
        for (int i = 0; i < 10 ; i++) {
            threadProAndCon.consume();
        }
    }
}

    public static void main(String[] args) {
        ThreadProAndCon threadProAndCon = new ThreadProAndCon();
        Service2 productor = new Service2(threadProAndCon);
        Service3  consmtor= new Service3(threadProAndCon);

        productor.start();
        consmtor.start();


    }

/*
生产者生产1个产品
消费者消费0个产品
生产者生产1个产品
消费者消费0个产品
生产者生产1个产品
消费者消费0个产品
生产者生产1个产品
消费者消费0个产品
。。。
/
```

**Condition** **类和** **Object** **类锁方法区别区别**

- Condition 类的 awiat 方法和 Object 类的 wait 方法等效
- Condition 类的 signal 方法和 Object 类的 notify 方法等效
- Condition 类的 signalAll 方法和 Object 类的 notifyAll 方法等效
- ReentrantLock 类可以**唤醒指定条件**的线程，而 object 的唤醒是随机的



#### **Semaphore(信号量)**

一种**基于计数**的信号量,可以控制同时访问的线程个数。

可以设定阈值，在阈值规定的范围内 **同一时间多个线程可以获取信号量来完成自己的工作，用完后归还**，若线程的数量超过了阈值，其他没有获取信号量的线程等待。信号量可以用来实现对象池、资源池。比如：数据库连接池。

**实现代码**

```java
// 创建一个计数阈值为 5 的信号量对象
// 只能 5 个线程同时访问
Semaphore semp = new Semaphore(5);
try { // 申请许可
        semp.acquire();
        try {
            // 业务逻辑
        } catch (Exception e) {
        } finally {
            // 释放许可
            semp.release();
        }
    } catch (InterruptedException e) {
	}
}
```

**Semaphore与ReentrantLock**

- Semaphore几乎可以完成ReentrankLock所有的功能。Semaphore中acquire()和release()获取资源和释放资源的。

  Semaphore中acquire()和ReentrankLock中lock()方法是一样的，它们都可以向响应中断（**接受中断指令中断了持有锁的线程，但是它并不能立刻unlock解锁，而是机械式执行完所有的操作，在释放锁。**），调用Thread.interrupt()中断。

- Semaphore实现了**可轮询的锁请求与定时锁的功能**，tryAcquire()和ReentrankLock中的tryLock()方法几乎一致。

- Semaphore也可以实现公平锁和非公平锁。

- Semaphore锁的释放也是手动进行，因此需要在finally块中进行锁定释放。



**Semaphore中的release方法**

该方法用于释放信号量，这里需要注意一点的是：若释放的信号量超过了获取的信号量，当前信号量就动态增加了。

例如：获取一个信号量，释放了四个，当前信号量动态增加了4。

下面这个例子更加具体

```java
//设置信号为1，同时只能有一个线程进程。
Semaphore semp = new Semaphore(1);
```

```java
//Mutex类的源码
import java.util.concurrent.Semaphore;

public class Mutex {
     private Semaphore s = new Semaphore(1);

    //获取锁
     public void acquire() throws InterruptedException {
      s.acquire();
     }
    //释放锁
    public void release(){
      s.release();
     }
    //可轮询的锁请求与定时锁的功能
    public boolean attempt(int ms) throws InterruptedException {
      return s.tryAcquire(ms);
     }
}
```

```java
public class TestMutex {
    public static void main(String[] args) throws InterruptedException{
        Mutex mutex=new Mutex();
        //获取一个信号量
        mutex.acquire();
        //释放两个信号量
        mutex.release();
        //mutex.release();
        new MyThread(mutex).start();
        new MyThread(mutex).start();
    }

}

class MyThread extends Thread{
    private Mutex mutex;

    public MyThread(Mutex mutex) {
        this.mutex=mutex;
    }

    public void run(){
        try {
        //获取锁资源
            mutex.acquire();
        } catch (InterruptedException e1) {
            throw new RuntimeException(e1);
        }
        for(int i=0;i<10;i++){
            System.out.print(i);
            if(i%3==0){
                try {
                //睡眠
                    Thread.sleep(100);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }
        //释放锁
        mutex.release();
    }
}

/*
结果  00 123123 456456 789789
本来是想要实现Mutex互斥，因为多释放了一个信号量，导致Semaphore中premit动态增加变成了2，允许两个线程同时运行导致，没法实现互斥，导致了上述结果
*/
/*
去掉一个mutex.release();就是先了互斥：
当前线程Thread-0
0 1 2 3 4 5 6 7 8 9 
当前线程Thread-1
0 1 2 3 4 5 6 7 8 9 
*/
```



#### CountDownLatch

CountDownLatch 类位于 java.util.concurrent 包下，可以实现计数器的功能，主要应用的方面是将n个线程阻塞在一个地方，当这n个线程都执行完毕时，才能执行其他的。

**典型应用场景就是启动一个服务时，主线程需要等待多个组件加载完毕，之后再继续执行。**

场景：这里有5个文件，需要将这5个文件全部加载完毕后，才能继续执行其他文件的加载

```java
public class CountDownLatchDemo {


    public static int fileNumber = 0 ;
    public static void main(String[] args) throws InterruptedException {
        //文件数目
        final int file = 5;
        //计数器设置为5
        final CountDownLatch countDownLatch = new CountDownLatch(file);
        //使用线程池来完成
        ThreadPoolExecutor threadPoolExecutor = new ThreadPoolExecutor(2,10,5, TimeUnit.SECONDS,
                new LinkedBlockingQueue<Runnable>(3));

        for (int i = 0; i < file ; i++) {
            threadPoolExecutor.execute(new Runnable() {
                @Override
                public void run() {
                    System.out.println("当前第"+fileNumber+++"个文件正在处理");

                    //countDown（）递减锁存器的计数，如果计数到达零，则释放所有等待的线程。如果当前计数大于零，则将计数减少.
                    countDownLatch.countDown();
                    System.out.println("当前文件已经处理完毕");
                }
            });
        }

        //使当前线程在锁存器倒计数至零之前一直等待，除非线程被中断或超出了指定的等待时间。如果当前计数为零，则此方法立刻返回true值。
        countDownLatch.await();
        threadPoolExecutor.shutdown();
        System.out.println("线程池关闭");
        System.out.println("文件处理完毕，继续执行其他任务");

    }
}
/*
当前第0个文件正在处理
当前第1个文件正在处理
当前文件已经处理完毕
当前文件已经处理完毕
当前第2个文件正在处理
当前文件已经处理完毕
当前第3个文件正在处理
当前文件已经处理完毕
当前第4个文件正在处理
当前文件已经处理完毕
线程池关闭
文件处理完毕，继续执行其他任务
*/
```

CountDownLatch典型用法：2、实现多个线程开始执行任务的最大并行性。注意是并行性，不是并发，强调的是多个线程在某一时刻同时开始执行。类似于赛跑，将多个线程放到起点，等待发令枪响，然后同时开跑。做法是初始化一个共享的CountDownLatch(1)，将其计算器初始化为1，多个线程在开始执行任务前首先countdownlatch.await()，当主线程调用countDown()时，计数器变为0，多个线程同时被唤醒。



力扣上的一道经典多线程打印问题

[按序打印](https://leetcode-cn.com/problems/print-in-order/)

```java
我们提供了一个类：

public class Foo {
  public void first() { print("first"); }
  public void second() { print("second"); }
  public void third() { print("third"); }
}
三个不同的线程 A、B、C 将会共用一个 Foo 实例。

一个将会调用 first() 方法
一个将会调用 second() 方法
还有一个将会调用 third() 方法
请设计修改程序，以确保 second() 方法在 first() 方法之后被执行，third() 方法在 second() 方法之后被执行。
```



```java
class Foo {
    ReentrantLock lock = new ReentrantLock();
    Condition condition1 = lock.newCondition();
    Condition condition2 = lock.newCondition();
    boolean con1 = true;
    boolean con2 = true;

    public Foo() {
        
    }

    public void first(Runnable printFirst) throws InterruptedException {
        lock.lock();
        try {
            printFirst.run();
            con1  = false;
            condition1.signal();
        }finally {
            lock.unlock();
        }
    }

    public void second(Runnable printSecond) throws InterruptedException {
        lock.lock();
        try{
            while (con1){
                condition1.await();
            }
            printSecond.run();
            con2 = false;
            condition2.signal();
        }finally {
            lock.unlock();
        }
    }

    public void third(Runnable printThird) throws InterruptedException {
        lock.lock();
        try{
            while (con2){
                condition2.await();
            }
            printThird.run();
        }finally {
            lock.unlock();
        }
    }
}
```

```java
class Foo {
    
//使用synchronized锁 和wait和notiefy来完成

    Object object = new Object();
    int  flag = 1;
    public Foo() {
        
    }

    public void first(Runnable printFirst) throws InterruptedException {
        synchronized (object){
            while (flag != 1){
                object.wait();
            }

            printFirst.run();
            flag = 2;
            object.notifyAll();
        }
    }

    public void second(Runnable printSecond) throws InterruptedException {
        synchronized (object){
            while (flag != 2){
                object.wait();
            }

            printSecond.run();
            flag = 3;
            object.notifyAll();
        }
    }

    public void third(Runnable printThird) throws InterruptedException {
        synchronized (object){
            while (flag != 3){
                object.wait();
            }
            printThird.run();
            object.notifyAll();
        }
    }
}
```

```java
class Foo {
    
    //使用CountDown来完成
    //计数器初始化为1
    //两个分别用来控制线程B\C
    CountDownLatch countDownLatch1 = new CountDownLatch(1);
    CountDownLatch countDownLatch2 = new CountDownLatch(1);
    public Foo() {
        
    }

        public void first(Runnable printFirst) throws InterruptedException {
        printFirst.run();
        //当线程A运行完毕后，线程B才能执行，countDownLatch1用来控制线程B
        countDownLatch1.countDown();
    }

    public void second(Runnable printSecond) throws InterruptedException {
        //在countDownLatch1为0之前，都要等待
        countDownLatch1.await();
        printSecond.run();
        //当线程B运行完毕后，线程C才能执行，countDownLatch2用来控制线程C
        countDownLatch2.countDown();
    }

    public void third(Runnable printThird) throws InterruptedException {
        //线程C获取到资源后，执行
        countDownLatch2.await();
        printThird.run();
    }
}
```

```java
class Foo {
    
    /**
     * 使用信号量
     * 起初初始化时：默认为0 表示没有资源可以调用
     * 通过两个信号量来控制线程B、线程C的顺序
     */
    Semaphore one = new Semaphore(0);
    Semaphore two = new Semaphore(0);
    public Foo() {
        
    }

        public void first(Runnable printFirst) throws InterruptedException {
        //first代表线程A 该方法没有被加锁，因此它是第一个执行的，就保证了A在B、C之前运行
        printFirst.run();
        //用one这个信号量来控制线程B，线程A运行完之后，通过release方法给one信号量加1，Semaphore中release方法在信号量为0的情况下
        //Semaphore会动态增加1，此时one信号量为1，表示可以有一个线程运行，线程C是由信号量two控制，此时two为0，C必定在B之后运行
        one.release();
    }

    public void second(Runnable printSecond) throws InterruptedException {
        //线程B尝试获取到one信号量资源
        one.acquire();
        printSecond.run();
        //线程B执行完之后，释放信号量two
        two.release();
    }

    public void third(Runnable printThird) throws InterruptedException {
        //线程C获取到资源后，执行
        two.acquire();
        printThird.run();
    }
}
```



#### CyclicBarrier(回环栅栏)

[to be top java developer (cnblogs.com)](https://www.cnblogs.com/lovelywcc/p/14004699.html#特别感谢)

也是一个同步工具类，它主要的应用场景在：让一组线程相互等待，直到达到某个状态（**这里状态就是barrier**）时在同时运行。

叫做回环的原因是因此它可以在再次使用，这就是不同于CountDownLatch的地方，CountDownLatch不可以重复使用，因此它是计数的形式，减为0之后，没法重复使用。

CyclicBarrier的构造函数

```java
//带Runnable参数的函数
 public CyclicBarrier(int parties, Runnable barrierAction) {
        if (parties <= 0) throw new IllegalArgumentException();
        this.parties = parties;//有几个运动员要参赛
        this.count = parties;//目前还需要几个运动员准备好
        //你要在所有线程都继续执行下去之前要执行什么操作，可以为空
        this.barrierCommand = barrierAction;
    }
//不带Runnable参数的函数
 public CyclicBarrier(int parties) {
     this(parties, null);
 }
/*
Runnable参数：当一组线程都到达指定状态后同时运行完毕之后，若还想要继续运行做一些事情可以使用Runnable参数
需要注意的时这里new Runnable不是新建线程，而是在之前运行完毕的线程中取最后一个到达barrier状态的线程作为载体。

parties：规定到达barrier状态的线程的数目，
count：当前没有到达barrier状态的线程的数目
*/
```



CyclicBarrier中最重要的方法就是**await()**

1. public int await():该方法让线程处于barrier，等待其他线程也到达这个状态，当所有的线程都位于这个状态时让它们在同时运行。
2. public int await(long timeout, TimeUnit unit):设定线程等待的时间，若超过这个时间让已经处于barrier状态的线程先执行。

```java
public int await() throws InterruptedException, BrokenBarrierException{
		try{
			return dowait(false,0L);
        }catch(TimeoutException toe){
            throw new Error(toe);;
        }
}
/*
CyclicBarrier 多用于多个线程同时执行的情况，让他们位于Barrier状态等待，对于同步失败，CyclicBarrier使用一种要么全部要么全不的破坏模式，如果因为终端、失败或者超时等原因，导致线程过早地离开了屏障点，那么在该屏障点等待的其他线程通过BrokenBarrierException(如果所有的线程都被同时中断，则用InterruptedException)以反常的方式离开
*/
```

应用场景：处理6个文件，让6个文件都先准备好，方便一起处理，这样的过程再来一遍(**重复使用CyclicBarrier**)

```java

    public static void main(String[] args) throws InterruptedException {

        CyclicBarrier cyclicBarrier = new CyclicBarrier(6, new Runnable() {
            @Override
            public void run() {
                System.out.println("处理文件之前，需要再检查一遍");
            }
        });

        ThreadPoolExecutor threadPoolExecutor = new ThreadPoolExecutor(6,10,5, TimeUnit.SECONDS,new LinkedBlockingDeque<Runnable>(5));
        int file = 6;
        for (int i = 0; i < file; i++) {
            threadPoolExecutor.execute(new Runnable() {
                @Override
                public void run() {
                    try {

                        Thread.sleep(1000);
                        System.out.println("当前第"+Thread.currentThread().getName()+"个文件已经准备完毕");
                        //处于barrier状态等待
                        cyclicBarrier.await();
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    } catch (BrokenBarrierException e) {
                        e.printStackTrace();
                    }
                    System.out.println("开始处理文件");
                }
            });
        }

        Thread.sleep(10000);

        System.out.println("重用CyclicBarrier");
        System.out.println("第二批文件到达");
        for (int i = 0; i < file; i++) {
            threadPoolExecutor.execute(new Runnable() {
                @Override
                public void run() {
                    try {

                        Thread.sleep(1000);
                        System.out.println("当前第"+Thread.currentThread().getName()+"个文件已经准备完毕");
                        //处于barrier状态等待
                        cyclicBarrier.await();
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    } catch (BrokenBarrierException e) {
                        e.printStackTrace();
                    }
                    System.out.println("开始处理文件");
                }
            });
        }


    }
/*
当前第pool-1-thread-5个文件已经准备完毕
当前第pool-1-thread-2个文件已经准备完毕
当前第pool-1-thread-1个文件已经准备完毕
当前第pool-1-thread-4个文件已经准备完毕
当前第pool-1-thread-3个文件已经准备完毕
当前第pool-1-thread-6个文件已经准备完毕
处理文件之前，需要再检查一遍
开始处理文件
开始处理文件
开始处理文件
开始处理文件
开始处理文件
开始处理文件
重用CyclicBarrier
第二批文件到达
当前第pool-1-thread-6个文件已经准备完毕
当前第pool-1-thread-1个文件已经准备完毕
当前第pool-1-thread-5个文件已经准备完毕
当前第pool-1-thread-2个文件已经准备完毕
当前第pool-1-thread-3个文件已经准备完毕
当前第pool-1-thread-7个文件已经准备完毕
处理文件之前，需要再检查一遍
开始处理文件
开始处理文件
开始处理文件
开始处理文件
开始处理文件
开始处理文件
*/
```



总结：CountDownLatch和CyclicBarrier两个都是同步工具类，CountDownLatch**多应用于某线程A等待其他n个线程执行完之后再执行**，CyclicBarrier   **应用于一组线程互相等待至barrier状态后同时执行**

CountDownLatch无法重用，CyclicBarrier可以重复使用。

CyclicBarrier则利用ReentrantLock的Condition来阻塞和通知线程，CountdownLatch利用继承AQS的共享锁来进行线程的通知,利用CAS来进行。



#### **Atmoic(原子)**

在化学中表示构成一般物质的最小单位，不可分割。**在这里表示操作不可中断**。即使在多个线程一起执行时，一个操作一旦开始，就不会被其他的线程干扰。

原子类：具有原子操作性质的类。

位于：**java.util.concurrent.atomic**

**基本类型**

使⽤原⼦的⽅式更新基本类型

- **AtomicInteger** ：整形原⼦类
- **AtomicLong** ：⻓整型原⼦类
- **AtomicBoolean** ：布尔型原⼦类

**数组类型**

使⽤原⼦的⽅式更新数组⾥的某个元素

- **AtomicIntegerArray** ：整形数组原⼦类
- **AtomicLongArray** ：⻓整形数组原⼦类
- **AtomicReferenceArray** ：引⽤类型数组原⼦类

**引用类型**

- **AtomicReference** ：引⽤类型原⼦类

- **AtomicStampedReference** ：原⼦更新带有版本号的引⽤类型。该类将整数值与引⽤关联起来，可⽤于解决原⼦的更新数据和数据的版本号，可以解决使⽤ CAS 进⾏原⼦更新时可能出现的 ABA 问题。

- **AtomicMarkableReference**：原⼦更新带有标记位的引⽤类型





#### **ReadWriteLock(读写锁)**

读写锁分为：读锁和写锁。

**读锁**

如果在没有写锁的情况下，读锁之间是不互斥的，读是无堵塞的，多个线程访可以同时访问同一资源，不会产生阻塞。

如果想让代码只能被读，不能被写，那就上读锁

**写锁**

在写锁的情况下，同一资源只能被一个线程修改，并且修改的同时不能读取。**因此读锁和写锁是互斥的**。

引出读写锁是为了提高性能，在读的地方使用读锁，在写的地方使用写锁。

例如：**在读的需求远大于写的需求的系统中，使用读写锁的效率远远大于独享锁，读可以保证多个线程同时读同一资源**。

**读写锁是很典型的分离锁**，根据功能将锁分成读锁和写锁，读读不互斥，读写互斥，写写互斥，即保证了线程安全，又提高了性能，一举两得。





### **死锁**

多个线程被同时阻塞，它们当中一个或全部都在等待同一个资源的释放，它们自身可能持有的资源也没有得到释放。

例如：两个线程A、B它们各自获取了一个资源，同时它们又希望获取对方的资源，它们自身也没有对已经持有的资源进行释放，双方都在等待对方释放资源，就会造成永无止尽的等待。

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210730152813416.png" alt="image-20210730152813416" style="zoom:50%;" />



```java
    public class DeadLockDemo {
        private static Object resource1 = new Object();//资源 1
        private static Object resource2 = new Object();//资源 2
        public static void main(String[] args) {
            new Thread(() -> {
                synchronized (resource1) {
                    System.out.println(Thread.currentThread() + "get resource1");
                    try {
                        Thread.sleep(1000);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                    System.out.println(Thread.currentThread() + "waiting get resource2");
                    synchronized (resource2) {
                        System.out.println(Thread.currentThread() + "get resource2");
                    }
                }
            }, "线程 1").start();
            new Thread(() -> {
                synchronized (resource2) {
                    System.out.println(Thread.currentThread() + "get resource2");
                    try {
                        Thread.sleep(1000);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                    System.out.println(Thread.currentThread() + "waiting get resource1");
                    synchronized (resource1) {
                        System.out.println(Thread.currentThread() + "get resource1");
                    }
                }
            }, "线程 2").start();
        }
    }

/*
结果:
Thread 0 get resource1
Thread 1 get resource2
Thread 0 waiting get resource2
Thread 1 waiting get resource2
*/
```

非常典型的死锁，线程1获取 resource1，进入Timed-Waiting状态，线程2获取resource2，进入进入Timed-Waiting状态，因为多线程同步的关系并且synchronized是可重入锁，因此线程1不会释放 resource1，一直等待，线程2也持有 resource2不会释放，请求 resource1得不到也一直等待，两个都一直等待，进入死锁。



突破死锁：只要在开始时将线程2同时和线程1争取同一个资源(resource1)，那么获取到resource1执行，没有获取到的挂起，那么另一个resource2也就没有被抢占，一个线程可以安心执行完所有过程，释放所有的资源。另一个线程也可以执行完成。



**产生死锁的条件**：

- 互斥条件：该资源任意⼀个时刻只由⼀个线程占⽤
- 请求与保持：⼀个进程因请求资源⽽阻塞时，对已获得的资源保持不放。
- 不可剥夺条件：线程已获得的资源在末使⽤完之前不能被其他线程强⾏剥夺，只有⾃⼰使⽤完毕后才释放资源。
- 循环等待：若⼲进程之间形成⼀种头尾相接的循环等待资源关系。



**破坏死锁：破坏产生死锁的四个条件中的一个即可破坏死锁，互斥条件一般无法破坏**

**破坏循环等待条件** ：靠按序申请资源来预防。按某⼀顺序申请资源，释放资源则反序释放。



### 线程池

[你要的线程池来了，还带有10道面试题和答案 (markdowner.net)](https://markdowner.net/article/142328369902858240)

将一个或多个线程使用统一的方式进行调度和管理的技术，减少线程的创建和销毁所带来的开销。



**线程池的作用(为什么要使用线程池)**

- **降低资源消耗：线程的创建和销毁都需要消耗资源，通过重复利用线程减少这方面消耗**。
- **提高响应速度：当请求任务到达时，通常工作线程已经存在，不需要等待线程创建，直接执行**。
- **提高线程的可管理：使用线程池统一对线程进行调度管理**



**线程池的创建**	

在JDK包下的**JUC(java.util.concurrent)**创建线程池的两种方法:**Executor**和**ThreadPoolExecutor**。

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210731095047995.png" alt="image-20210731095047995" style="zoom:67%;" />



#### **ThreadPoolExecutor**

例子：

```java
public class ThreadPoolDemo {

    private static ThreadPoolExecutor threadPoolExecutor = new ThreadPoolExecutor(2, 10,
            10L, TimeUnit.SECONDS, new LinkedBlockingQueue(100));

    public static void main(String[] args) {
        threadPoolExecutor.execute(new Runnable() {
            @Override
            public void run() {
                System.out.println("你好田中");
            }
        });
    }
}
```



ThreadPoolExecutor一共提供了四个构造函数，这里用参数最多构造函数说明。

```java
    public ThreadPoolExecutor(int corePoolSize,
                              int maximumPoolSize,
                              long keepAliveTime,
                              TimeUnit unit,
                              BlockingQueue<Runnable> workQueue,
                              ThreadFactory threadFactory,
                              RejectedExecutionHandler handler) {
        if (corePoolSize < 0 ||
            maximumPoolSize <= 0 ||
            maximumPoolSize < corePoolSize ||
            keepAliveTime < 0)
            throw new IllegalArgumentException();
        if (workQueue == null || threadFactory == null || handler == null)
            throw new NullPointerException();
        this.acc = System.getSecurityManager() == null ?
                null :
                AccessController.getContext();
        this.corePoolSize = corePoolSize;
        this.maximumPoolSize = maximumPoolSize;
        this.workQueue = workQueue;
        this.keepAliveTime = unit.toNanos(keepAliveTime);
        this.threadFactory = threadFactory;
        this.handler = handler;
    }
```

当中三个最要的参数
1. **corePoolSize**:线程池中核心线程数，所谓核心线程就是新创建的线程，若当前线程数量小于核心线程数，该线程是核心线程。

   作用定义最小可以同时运行线程的数目，核心线程默认情况下是一直存活在线程池中，可以通过allowCoreThreadTimeOut 设置核心线程的过期时间。

2. **maximumPoolSize：**线程池中最大线程数量。**线程总数=核心线程+非核心线程**

3. **BlockingQueue<Runnable> workQueue：**线程池中**任务队列**，当所有的核心线程都在工作时，新添加的任务会被放到任务队列中等待处理，若**任务队列也满了**，**那就创建非核心队列执行任务**。

其他参数

1. **keepAliveTime：** **默认是非核心线程闲置超时时长**，非核心线程若超过时间就会被销毁。**若设置allowCoreThreadTimeOut = true，则会作用于核心线程**

2. **TimeUnit unit：**keepAliveTime的时间单位，TimeUnit是一个**枚举类型**

3.  **ThreadFactory threadFactory：**线程池提供创建新线程的线程工厂

4. **RejectedExecutionHandler(饱和策略)：**用来处理当前线程池中线程数量达到最大线程数目并且等待队列中也已经装满的情况。

   - **ThreadPoolExecutor.AbortPolicy**：直接抛出RejectedExecutionException异常拒绝新的任务
   - **ThreadPoolExecutor.DiscardPolicy：**不处理新任务，直接丢弃
   - **ThreadPoolExecutor.DiscardOldestPolicy：**丢弃最早未处理的任务请求
   - **ThreadPoolExecutor.CallerRunsPolicy**：不会抛出异常也不会丢弃任务，而是调用者运行自己的线程来完成新的任务请求，这种策略会降低新任务的提交速率。

   **RejectedExecutionHandler 是一个接口，上面四种策略都是其实现类。**

   若以上四种内置策略都无法满足，可以自定义策略。



**execute()和submit()**

两个方法都是将线程放入线程池中，区别在于execute方法没有返回值，submit方法有线程的返回值。

一般情况下是配合**ExecutorService**来使用的，在ExecutorService接口中声明了若干个submit方法的重载版本

```java
<T> Future<T> submit(Callable<T> task);
<T> Future<T> submit(Runnable task, T result);
Future<?> submit(Runnable task);

//经常使用第一个和第二个
```



​		**补充：Callable、Future**

常用线程的创建方式是extends Thread 或者 implement Runnable，这两种方法存在的缺陷是：**执行完任务后无法获取执行的结果。**

JAVA 1.5之后引入了**Callable**和**Future**。这两个在任务执行完之后都可以获取执行的结果。

先来看一下**Callable**，它是一个接口，位于**JUC**包中

```java
public interface Callable<V> {
    /**
     * Computes a result, or throws an exception if unable to do so.
     *
     * @return computed result
     * @throws Exception if unable to compute a result
     */
    V call()throws Exception;
}
```

泛型结构，根据输入类型返回对应类型结果。



[Java的Future机制详解 - 简书 (jianshu.com)](https://www.jianshu.com/p/43dab9b7c25b)

[JAVA Future类详解 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/364041672)

再来看看**Future**，同样Future也是一个接口，Future模式核心思想在于：**能够让主线程将原来需要同步等待的这段时间用来去做其他事情。(异步)**

举个干饭的例子：同样是吃饭，一个人走去食堂，排队点餐，吃饭。这个过程他只能去做吃饭这一件事，其他事情要等到吃饭完后才能开始。另一个人选择点外卖，在等待外卖这段时间他可以去做别的事情，等外卖到了通知他，他放下当前做的事情去吃饭。



<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/v2-435c7e31f57f8f7bbf68b92b724b37a1_720w.jpg" alt="img" style="zoom: 80%;" />

Future接口中定义了5种方法。

- cancel()：取消执行任务，若任务已经在执行可以通过设置参数来控制是否取消任务。
- isCancelled()：任务是不是已经取消了
- isDone()：任务是不是已经完成了
- get()：获取任务执行的结果
- get(long timeout, TimeUnit unit)：设置获取任务执行结果的时间，若在规定时间内没有获取到返回NULL



**FutureTask**是RunnableFuture的实现类，RunnableFuture接口继承了Runnable接口和Future接口，FutureTask既可以作为Runnable被线程执行，又可以作为Future得到Callable的返回值。



FutureTask中构造函数

```java
public FutureTask(Callable<V> callable) {
    if (callable == null)
        throw new NullPointerException();
    this.callable = callable;
    this.state = NEW;       // ensure visibility of callable
}
    
public FutureTask(Runnable runnable, V result) {
    this.callable = Executors.callable(runnable, result);
    this.state = NEW;       // ensure visibility of callable
}
```

第一个构造函数执行返回结果就是callable执行的返回结果。

第二个构造函数执行返回结果是参数中的result。



执行一个**异步过程**，输入两个数做加法计算，看看时间差。

```java
public class futureTaskDemo {

    public static void main(String[] args) throws ExecutionException, InterruptedException {
        //开始时间
        long startTime = System.currentTimeMillis();

        FutureTask<Integer> thread1 = new FutureTask<>(new Callable<Integer>() {
            //callabel中 的call方法
            @Override
            public Integer call() throws Exception {
                //睡眠两秒
                Thread.sleep(2000);
                //第一个数
                return 15;
            }
        });

        //启动线程
        new Thread(thread1).start();


        FutureTask<Integer> thread2 = new FutureTask<>(new Callable<Integer>() {
            //callabel中 的call方法
            @Override
            public Integer call() throws Exception {
                //睡眠4秒
                Thread.sleep(4000);
                //第二个数
                return 5;
            }
        });
        new Thread(thread2).start();

        //通过future接口中get方法获取线程中结果
        Integer num1 = thread1.get();
        Integer num2 = thread2.get();
        System.out.println("结果： "+(num1 + num2));
        System.out.println("用时："+String.valueOf(System.currentTimeMillis() - startTime));
    }
}
/*
结果： 20
用时：4006

异步执行，最终结果只花费了4秒，第一个线程开始执行时，直接返回，第二线程同时开始执行。
*/
```



再来看看ThreadPoolExecutor中submit方法，**线程池会返回一个Future对象，通过Futrue可以判断任务是否执行成功，通过Future中get方法得到任务的返回结果，get方法会阻塞当前线程直到任务完成**。

**executor.submit()源码**

```java
    public <T> Future<T> submit(Callable<T> task) {
        if (task == null) throw new NullPointerException();
        // 根据Callable对象，创建一个RunnableFuture，newTaskFor方法就是new一个FutureTask对象
        RunnableFuture<T> ftask = newTaskFor(task);
        //将ftask推送到线程池
        //在新线程中执行的，就是run()方法，在下面的代码中有给出
        execute(ftask);
        //返回这个Future，将来通过这个Future就可以得到执行的结果
        return ftask;
    }
    protected <T> RunnableFuture<T> newTaskFor(Callable<T> callable) {
        return new FutureTask<T>(callable);
    }


/*
FutureTask作为一个线程单独执行时，会将结果保存到outcome中，并设置任务的状态
*/


public void run() {
    //volatile修饰的state字段；表示FutureTask当前所处的状态
        //如果状态不是new，或者runner旧值不为null(已经启动过了)，就结束
        if (state != NEW ||!UNSAFE.compareAndSwapObject(this, runnerOffset, null, Thread.currentThread()))
            return;
        try {
            Callable<V> c = callable; // 这里的callable是从构造方法里面传人的
            if (c != null && state == NEW) {
                V result;
                boolean ran;
                try {
                    result = c.call(); //执行任务，并将结果保存在result字段里。
                    ran = true;
                } catch (Throwable ex) {
                    result = null;
                    ran = false;
                    setException(ex); // 保存call方法抛出的异常
                }
                //set方法把结果放到outcome里保存，同时设置任务状态
                if (ran)
                    set(result); // 保存call方法的执行结果
            }
        } finally {
            // runner must be non-null until state is settled to
            // prevent concurrent calls to run()
            runner = null;
            // state must be re-read after nulling runner to prevent
            // leaked interrupts
            int s = state;
            if (s >= INTERRUPTING)
                handlePossibleCancellationInterrupt(s);
        }
    }
```



#### Executors

通过Executor框架的**工具类Executors**可以创建4中常见的线程池，这四种线程池都是直接或间接配置ThreadPoolExecutor的参数实现的。

- **CachedThreadPool()(可缓存线程池)**

  - 线程数无限制
  - 有空闲线程就复用空闲线程，没有就创建新的线程
  - 一定程度上较少系统开销，能够减少线程的创建和销毁

  ```java
  ExecutorService cachedThreadPool = Executors.newCachedThreadPool();
  
  //源码
  public static ExecutorService newCachedThreadPool() {
      return new ThreadPoolExecutor(0, Integer.MAX_VALUE,
                                    60L, TimeUnit.SECONDS,
                                    new SynchronousQueue<Runnable>());
  }
  ```

- **FixedThreadPool()(固定大小线程池)**

  - 可以控制线程最大并发数量
  - 超出的线程被放入等待队列中

  ```java
  public static ExecutorService newFixedThreadPool(int nThreads) {
      return new ThreadPoolExecutor(nThreads, nThreads,
                                    0L, TimeUnit.MILLISECONDS,
                                    new LinkedBlockingQueue<Runnable>());
  }
  ```

- **ScheduledThreadPool()(定期线程池)**

  - 支持定时及周期性任务执行。

  ```java
  //nThreads => 最大线程数即maximumPoolSize
  ExecutorService scheduledThreadPool = Executors.newScheduledThreadPool(int corePoolSize);
  
  public static ScheduledExecutorService newScheduledThreadPool(int corePoolSize) {
      return new ScheduledThreadPoolExecutor(corePoolSize);
  }
  
  //ScheduledThreadPoolExecutor():
  public ScheduledThreadPoolExecutor(int corePoolSize) {
      super(corePoolSize, Integer.MAX_VALUE,
            DEFAULT_KEEPALIVE_MILLIS, MILLISECONDS,
            new DelayedWorkQueue());
  }
  ```

- **SingleThreadExecutor()（单线程化的线程池）**

  - 创建一个单线程的工作任务
  - 所有任务按照指定顺序执行，即遵循队列的入队出队规则

  ```java
  ExecutorService singleThreadPool = Executors.newSingleThreadPool();
  
  public static ExecutorService newSingleThreadExecutor() {
      return new FinalizableDelegatedExecutorService
          (new ThreadPoolExecutor(1, 1,
                                  0L, TimeUnit.MILLISECONDS,
                                  new LinkedBlockingQueue<Runnable>()));
  }
  ```



**线程池关闭**

**shutdown() 或 shutdownNow() 方法**

shutdown() 

关闭线程池的一种方法，**这种方法不会立刻关闭线程池**。一方面：线程池不再接受新的任务请求。另一方面：线程池需要等到队列中所有的任务都完成时，线程池才会关闭。

shutdownNow() 

比较暴力，执行该方法后，线程池的会马上关闭，并试图停止正在执行的任务，任务队列中的任务请求不再执行。



```java
    public static void main(String[] args) {
        ThreadPoolExecutor threadPoolExecutor = new ThreadPoolExecutor
                (5, 10, 20, TimeUnit.SECONDS, new LinkedBlockingQueue<Runnable>(2),new MyThread(),
                      new ThreadPoolExecutor.CallerRunsPolicy());
        threadPoolExecutor.allowCoreThreadTimeOut(true);
        for (int i = 0; i < 10; i++) {
            threadPoolExecutor.execute(new Runnable() {
                @Override
                public void run() {
                    System.out.println("当前线程"+Thread.currentThread().getName()+"正在执行");
                }
            });
        }
      	System.out.println("线程池是否关闭了"+threadPoolExecutor.isShutdown());
        System.out.println("关闭线程池");
        System.out.println(threadPoolExecutor.getCompletedTaskCount());
        threadPoolExecutor.shutdown();
        System.out.println("线程池是否关闭了"+threadPoolExecutor.isShutdown());
        
        });

    }

class MyThread implements ThreadFactory{
    private final AtomicInteger mCount = new AtomicInteger(1);

    @Override
    public Thread newThread(Runnable r) {
        return new Thread(r,"MyThread" +mCount.getAndAdd(1));
    }
}
/*
结果：
当前线程MyThread2正在执行
当前线程MyThread3正在执行
当前线程MyThread1正在执行
当前线程MyThread4正在执行
当前线程MyThread5正在执行
当前线程MyThread1正在执行
当前线程MyThread3正在执行
当前线程MyThread2正在执行
当前线程MyThread4正在执行
线程池是否关闭了false
关闭线程池
9
线程池是否关闭了true
当前线程MyThread6正在执行
我想再次请求任务到线程池中
*/
//一共创建了10个线程，发现再关闭线程池时还有线程在运行，这是任务队列中的线程，当我再次申请加入线程池时线程池已经关闭了，还有一点，线程的名字从1-6，而并不是1-10，说明线程池中复用了空闲的线程，没有在创建新的线程。
```



#### **线程池的工作原理**

 <img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/0e411841387d418c992d1f43f37c0dcf~tplv-k3u1fbpfcp-zoom-1.image" alt="img" style="zoom: 67%;" />

- 创建线程池，设置线程池的**核心线程数(运行同时运行线程的数目)**、最大线程数、存活时间、时间单位、等待队列长度、线程工厂、饱和策略。
- 通过execute方法将线程放入线程池中
  1. 提交的任务后会先判断当前正在执行的任务数量是否大于核心线程数，没有超过核心线程数，立刻为新任务创建线程执行。
  2. 若当前正在执行的任务数量超过核心线程数，就将新的任务放入等待队列，等待核心线程中有空闲的线程
  3. 若等待队列中也已经装满，**但是并没有超过最大线程数目**，**就创建非核心线程来执行任务**
  4. 若等待队列装满并且最大线程数目到达峰值，此时线程池是饱和状态，抛出**RejectExecutionException**，采用设定的拒绝策略来处理。
- 上面是一般线程池工作的过程，当一个线程完成工作后，它会从等待队列中取下一个任务继续执行，这就是线程池中**线程复用**，这也是线程池的最大优点。
- 当一个线程处于空闲状态时(**这里指的是非核心线程**)，当他超过**KeepAliveTime**设定的时间时，它就会被销毁，默认核心线程是处于一直存活的状态，当然也可以通过参数来设定核心线程的时间。**因此当线程池中任务都完成时，最终线程池的大小都会收缩到corePoolSize的大小。**



#### **线程池的状态**

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/08000847-0a9caed4d6914485b2f56048c668251a.jpg" alt="image" style="zoom: 67%;" />

- Running：初始化线程池，等待新的任务加入执行
- ShutDown：关闭线程池，线程池不再接受新的任务，处理队列中剩余的任务
- Stop（ShutDownNow）：关闭线程池，不接受新的任务，不处理队列中剩余的任务，尝试终止正在执行的任务线程
- Tidying：线程池自主整理状态，调用terminated()方法进行线程池整理
- Terminated：线程池终止状态



#### 线程的复用

线程池实现了线程的复用，大大减少了线程创建和销毁带来的开销。

一般一个线程是对应一个任务，从线程的创建、运行再到销毁，一个线程只能执行一个任务。线程池将线程和任务分开，不再是一对一，而是一对多，一个线程可以执行很多个任务，这个功能的实现依靠阻塞队列实现。同一个线程可以从阻塞队列中不断获取新的任务来执行，线程实现了复用。

核心原理：每次执行任务的时候不再是创建新的线程调用Thread.start(),而是继承Thread类重写start方法，在start方法中添加循环传递过来的Runnable对象。让线程去做一个循环的过程，循环的对象就是阻塞队列，通过获取任务调用对应任务的run方法，这样就实现了一对多，线程的复用。



#### **阻塞(等待)队列的原理**

阻塞队列(**BlockingQueue**)在线程池创建时就设置的一种队列，其主要的作用如下(**类似于消费者生产者的关系**)

线程相当于消费者，阻塞队列相当于生产者存放产品的地方

1. 在队列中没有任务时**阻塞获取任务的线程**，使得线程进入wait状态，释放cpu的资源。
2. 在队列中有任务进来时唤醒对应的线程取走任务执行。

使得线程不会一直占用cpu的资源。



**为什么要使用阻塞队列：**

- 若线程无限制的创建，都占用一定的资源，线程池和cpu的资源是有限的，内存占用可能会导致内存溢出。采用阻塞队列能够有效减少资源消耗
- 创建线程池的消耗较高



#### **阻塞队列的种类**

![image-20210801141826630](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210801141826630.png)

1. **ArrayBlockingQueue**(**公平、非公平**) ：由数组结构组成的**有界**阻塞队列。按照先进先出（FIFO）的原则对元素进行排序。

   默认情况下采用公平访问队列，先来先到，位于队列前列的任务优先被线程执行。

   

2. **LinkedBlockingQueue**(**两个独立锁提高并发**) ：由链表结构组成的有界阻塞队列。按照先进先出（FIFO）的原则对元素进行排序.

   两个独立锁分别位于线程端(消费者)，新任务放入阻塞队列端(生产者)，两把锁分别独立，实现并行工作，提高效率。

   

3. **PriorityBlockingQueue** ：支持优先级排序的**无界**阻塞队列。 默认情况下元素采取自然顺序升序排列。可以自定义实现

   compareTo()方法来指定元素进行排序规则

   

4. **DelayQueue(缓存失效、定时任务)**：**支持延时获取元素的**无界阻塞队列。实现 Delayed 接口，在创建元素时可以指定多久才能从队列中获取当前元素。

   **缓存系统的设计**：可以用 DelayQueue 保存缓存元素的有效期，使用一个线程循环查询DelayQueue，一旦能从 DelayQueue 中获取元素时，表示缓存有效期到了。

   **定时任务调度**：使用 DelayQueue 保存当天将会执行的任务和执行时间，一旦从DelayQueue 中获取到任务就开始执行。

   

5. **SynchronousQueue(不存储数据、可用于传递数据)**：不存储元素的阻塞队列。队列本身并不存储任何元素，非常适合于传递性场景,比如在一个线程中使用的数据，传递给另外一个线程使用



------



### **volatile关键字**

在了解volatile的特性之前，先要补充一点内存方面的知识。

[Java并发编程：volatile关键字解析 - Matrix海子 - 博客园 (cnblogs.com)](https://www.cnblogs.com/dolphin0520/p/3920373.html)

**内存模型**

计算机在运行程序时，执行的是一条条的指令，而指令是在cpu上执行的，这个过程势必有数据的读写过程。程序中运行的临时数据都存放在**主存(物理内存)**中，这时候就存在一个问题，cpu的执行速度是很快的，而从主存中读数据和写数据的速度肯定是远远低于cpu执行的速度，cpu需要等主存的数据， 这样就会导致执行的速率大大降低。**高速缓存的出现解决了这样的问题**。

高速缓存位于cpu和主存之间，程序在运行时将数据从主存中复制一份放入到高速缓存中，cpu对缓存中的数据进行修改，运行结束后，将缓存中的数据更新到主存中。

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210802144349185.png" alt="image-20210802144349185" style="zoom:50%;" />

例如：

```java
 i = i+1;
```

先从主存中读取数据i的数据放入到缓存中，cpu执行执行进行i+1，然后将数据写入高速缓存，最后将高速缓存中的数据更新的主存中。

看似没有问题了，但其实存在很大的缺陷，上面说的这种情况在**单线程**中不会出现问题，**若出现在多线程中呢？**

**假设当前是多核(多个cpu)的环境**,多个线程各自占有一个cpu，一个cpu对应一个高速缓存，那么现在多个线程同时对一个数据做操作，就会出现问题。

例如

```java
i = 0;
//线程1
i = i + 1;
//线程2
i = i + 1;
```

让两个线程都对i做操作，理想的结果应该是2，但是实际的结果是1。

两个线程同时执行，各自复制i的值到缓存中，此时i的值是1，两个线程各个执行+1操作，i变为1，把更新后的缓存中的值写入到主存中，最后的结果就是1，并不是你所想要的答案。问题：**缓存一致性问题**

在硬件上解决缓存一致性的问题有两种

1. **通过总线加Lock**

   cpu和其他部件通讯通过总线，现在对总线加锁，其他cpu只能等待当前cpu执行完后才可以执行，保证了缓存一致性。

   缺点：效率下降

2. **缓存一致性协议**

   最出名的就是Intel 的MESI协议，希望能够保证操作共享变量时得到的变量的副本是一致的。

   **核心思想：当cpu在做写操作时，发现当前变量为共享变量，并且其他cpu中也存在着这个变量的副本，当前cpu对共享变量做了写操作，通知其他cpu将该变量的缓存设置为无效，需要通过访问主存获取该变量，这样保证了使用的是最新变量的副本**

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210802145644356.png" alt="image-20210802145644356" style="zoom: 50%;" />

**并发编程中三个概念**

1. **原子性**

   一个操作或多个操作要么都执行要么都不执行。经典案例：**银行转账问题**

2. **可见性**

   多个线程访问同一个变量时，若该变量被其中一个线程修改了，同一时刻其他线程能够知道该变量修改后的值。(**主要的问题就是围绕可见性讨论**)

3. **有序性**

   ```java
   int i =0;              
   boolean flag =false; 
   i =1;               //语句1  
   flag =true;         //语句2
   ```

   定义了i 和 flag 变量，之后进行复制操作。语句1一定会在语句2之前运行吗，**不一定** ，**JVM不一定会按照代码的顺序来运行**。

   原因是因为**指令重排序**。

   **指令重排序**：为了提高程序运行的效率，对输入代码进行优化，**它不保证代码中所有的代码都是按照代码顺序执行的**，**但是它能够保证最后得出结果是一致的。**

   **注意：若各语句之间存在依赖性关系，那么者之间的顺序就无法被改变，因为改变了顺序可能导致结果不一致的情况。**

   ```java
   int a =10;   //语句1
   int r =2;   //语句2
   a = a +3;   //语句3
   r = a*a;    //语句4
   
   //语句4不可能在语句2之前运行的，语句3也不可能在语句1之前运行
   ```

   上面说的情况都在单线程的代码顺序块，我们再来看看多线程中的情况。

   ```java
   //线程1:
   context = loadContext();  //语句1
   inited =true;            //语句2
    
   //线程2:
   while(!inited ){
     sleep()
   }
   doSomethingwithconfig(context);
   ```

   线程1中各个语句之间没有依赖性，看似好像可以重排序，但是在看看线程2中，就会发现线程1中不可以进行重排序，因为如果先执行了语句2，线程2中认为context已经赋值好了，跳出循环，执行doSomethingwithconfig(context); 但是最后的结果会出错。

   **重排序会对并发执行的正确性产生影响**



**java内存模型**

JVM规范定义一种内存模型，该模型提出为了屏蔽各个硬件平台和操作系统之间的差异性，让java程序在各个平台中能够达到一致的内存访问效果，因此有了java内存模型。

java内存模型中规定了程序执行的次序。

java内存模型中没有限制使用寄存器或高速缓存来提升执行速度，也没有限制编译器对指令进行重排序。

在java内存模型中也会产生缓存一致性和指令重排序的问题。

java内存模型中执行运行过程和上面所说的计算机操作系统类似，所有的变量都是存在主存当中（类似于前面说的物理内存），每个线程都有自己的工作内存（类似于前面的高速缓存）。线程对变量的所有操作都必须在工作内存中进行，而不能直接对主存进行操作。

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210802152100344.png" alt="image-20210802152100344" style="zoom:67%;" />

1. **原子性**

   在java中，对基本数据类型的赋值或读取操作时具有原子性的，这些操作是不可以被中断的。

   ```java
   x =10;        //语句1
   y = x;        //语句2
   x++;          //语句3
   x = x +1;    //语句4
   ```

   这四个语句中只有语句1是原子性，其他都不具有原子性。

   语句2包含两个操作：读取x的值，再将x值赋值给y

   语句3和语句4相似，包含三个操作：读取x的值，x+1操作，赋值给x

   不具原子性的操作，可能因为多个线程，导致数据混乱。

   

   java内存模型只保证最基本数据类型的赋值和取读操作的原子性，更大范围的可以通过synchronized和Lock来实现，同一时刻只有一个线程执行该代码块，那么自然就不存在原子性问题了，从而保证了原子性。

   

2. **可见性**

   java中使用**volatile关键字**保证可见性。

   将一个共享变量使用volatile关键字修饰后，当变量被一个线程修改之后，变量的值会被强制更新到主存中，其他线程获取它时需要重新到主存中获取，保证缓存的一致性。

   通过synchronized和Lock也能够保证可见性，synchronized和Lock能保证同一时刻只有一个线程获取锁然后执行同步代码，并且在释放锁之前会将对变量的修改刷新到主存当中。因此可以保证可见性。

3. **有序性**

   **在JMM中，提供了以下三种方式来保证有序性：**

   - **happens-before原则**
   - **synchronized机制**
   - **volatile机制**

   

   java内存模型具备**先行发生原则(happens-before)**

   ```
   《并发编程的艺术》中的定义如下
   
   在JMM中，如果一个操作执行的结果需要对另一个操作可见，那么这两个操作之间必须要存在happens- before关系。这里提到的两个操作既可以是在一个线程之内，也可以是在不同线程之间。两个操作之间具有happens-before关系，并不意味着前一个操作必须要在后一个操作之前执行！happens-before仅仅要求前一个操作（执行的结果）对后一个操作可见，且前一个操作按顺序排在第二个操作之前（the f irst is visible toand ordered before the second）
   ```

   上述这段话我的理解是：后一个操作依赖于前一个操作，因此前一个操作按顺序排在前面

   

   这里主要列举4个规律

   1. **程序次序规律：**一个线程内，按照代码顺序，书写在前面的操作先行发生于书写在后面的操作

      准确来说是**控制流顺序而不是代码顺序**，确保代码最后结果一致。顺序不一定按照写的代码顺序，除了存在依赖关系的操作。

   2. **锁定规律：**一个unlock操作先行发生于后面对同一个锁的lock操作。

   3. **volatile变量规律：**对一个volatile变量的写操作先行发生于后面对这个变量的读操作。

   4. **传递规律：**如果操作A先行发生于操作B，操作B先行发生于操作C，那就可以得出操作A先行发生于操作C的结论。

   

   因为运行编译器进行指令的重排序，对于单线程中不会产生影响，对于多线程来说会产生问题。

   通过volatile保证一定的有序性。

   可以通过synchronized和Lock来保证有序性，很显然，synchronized和Lock保证每个时刻是有一个线程执行同步代码，相当于是让线程顺序执行同步代码，自然就保证了有序性。



**volatile关键字细说**

```java
//线程1
boolean stop = false;
while(!stop){
    doSomething();
}
 
//线程2
stop = true;
```

如上代码，这段代码之前也出现过类似的，用来进行线程中断的一种方式，如果这段代码放在单线程中执行，按照顺序能够保证线程的中断，如果这是一个多线程的环境，可能导致线程无法中断。

场景：线程1执行，线程1从主存中将stop变量拷贝到对应的工作内存中(缓存)。线程2也拷贝了一份stop变量到自己的工作内存中，对stop变量做了修改，按理说此时线程1中的while循环应该结束，但是while并没有结束循环。原因线程1中的stop变量还是false，线程1并不知道线程2对stop做了修改，因此会一直执行。



被volatile关键字修饰的变量(**共享变量:类的静态变量，成员变量**)，具有两种性质

1. 保证不同线程对同一变量操作的可见性，也就是当一线程改变变量后，其他线程能够立刻知道最新的变量值。

    例如

   线程1 先执行，线程2再执行。

   ```java
   //线程1
   volatile boolean stop =false;
   while(!stop){
       doSomething();
   }
    
   //线程2
   stop =true;
   ```

    线程1执行完后，执行线程2，stop的值发生了改变，stop被volatile所修饰，因此会让被修改的值立刻在主存中得到更新，同时让线程1中的stop的缓存变成无效，当线程1再次读取时因为缓存失效，必须从主存中获取，保证了线程1得到了最新stop的值，结束了while循环。

2. 禁止指令重排序

   禁止执行指令重排序有两层含义

   1. 当程序运行到当前被volatile修饰的变量时，在该变量之前的操作肯定已经执行完毕，当前运行后的结果也对后续的操作具有可见性，因此之后的操作肯定还有进行。

   2. 在进行指令优化时，不能将被volatile修饰的变量之后的语句放在该变量执行顺序之前，该变量之前的语句也不能放在这之后，

      volatile使用**内存屏障**来保证有序性
      
      **内存屏障有两个能力：**
      
      - 就像一套栅栏分割前后的代码，阻止栅栏前后的没有数据依赖性的代码进行指令重排序，保证程序在一定程度上的**有序性**。
      - 强制把写缓冲区/高速缓存中的脏数据等写回主内存，让缓存中相应的数据失效，保证数据的**可见性**。
      
      ```java
      //x、y为非volatile变量
      //flag为volatile变量
       
      x =2;       //语句1
      y =0;       //语句2
      volatile flag ; //语句3
      x =4;        //语句4
      y = -1;      //语句5
      ```
      
      由于flag变量为volatile变量，保证语句3之前的语句1、2不会重排序到语句3之后，同样语句4、5也不会重排序到语句3之前。



**volatile无法保证原子性**

[volatile为什么不能保证原子性？ - 知乎 (zhihu.com)](https://www.zhihu.com/question/329746124)

拿最经典的i++来说

```java
volatile i = 10;
//线程1
i++;
//结果:11

//线程2
i++;
//结果:11

//理想结果:12
//原因:线程不安全，i++这个操作过程不是原子性的
```

i++和 i = i+1**操作都是不具有原子性的**，将这个过程分为三个基本部分

```
1. 线程取读i的值  //放入缓存中

2. tmp = i+1  //做加一操作，注意此时i的值还是10，i还没有得到更新，这个中间值被放在寄存器中

3.  i = tmp  //更新 缓存中i的值，

4. 插入内存屏障，更新主存中的值，使其他线程中的缓存失效
```

接下来说一说为什么不具有原子性。

若线程1先执行，将i的值复制一份放入缓存中，此时i =10，接着做加一操作，放入寄存器(tmp)，i的值还是10，到目前为止，i没有发生变化，因此不会通知其他线程，我们先将线程1阻塞了。再来看看线程2，若线程2也执行到了这里，接着执行第三步 更新 i的值，此时i的值为11，发生了变化，(**通过内存屏障**)先将主存中的i值强制更新为11，要通知其他线程缓存中的值无效了，我们再来看看线程1，唤醒线程1，线程1中缓存值原来为10，但是现在无效了，它要从主存中读取数据更新缓存，此时缓存中i的值更新为11，寄存器中的值tmp =11（这个11是通过 上一次 10+1得到的），因为已经进行过加1的操作了，指令不可能再次执行，接着往下，将i更新，i的值被赋值为11，最后得出的结果也就是11。

**补充：**修改volatile变量通知其他线程和强制修改主存中的变量，有一个操作叫**插入内存屏障**，即lock指令。



**volatile和synchronized的区别**

**synchronized 关键字和 volatile 关键字是两个互补的存在，而不是对立存在**

1. volatile 是线程同步的轻量级实现，性能高于synchronized。

    synchronized 可以修饰方法和代码块，volatile 只能修饰变量

2. 多线程访问volatile 变量时，不会产生阻塞，而synchronized 可能会发生阻塞

3. volatile 可以保证数据的可见性和有序性，不能保证原子性。**synchronized关键字都能**

   **保证。**

4. **volatile关键字主要用于解决变量在多个线程之间的可见性，⽽** **synchronized关键字解决的是**

   **多个线程之间访问资源的同步性。**

------



### ThreadLocal

[Java中的ThreadLocal详解 - 夏末秋涼 - 博客园 (cnblogs.com)](https://www.cnblogs.com/fsmly/p/11020641.html)

多线程在访问一个共享变量时，若该变量不做任何处理可能导致数据不一致，出现线程不安全问题。一般通过加锁(**volatile关键字主要是修饰共享变量，保证变量可见性和有序性**)来保证线程安全。

ThreadLocal是通过另一种方式来保证线程的安全性，不过不是通过同步数据，而是将变量拷贝给每一个调用该变量的线程，把变量存储在线程的内部，因此每个线程之间的变量的数据是独立的，每次调用的都是自己的那一份，这样就不同担心线程安全问题。

ThreadLocal**叫做线程本地变量，或者线程本地存储，用于提供线程内部的局部变量**。在多线程环境中用来保证各个线程中的变量独立其他线程。

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/1368768-20190613220434628-1803630402.png" alt="img" style="zoom:67%;" />

ThreadLocal的作用和同步机制：同步机制保证多线程中同一数据的一致性，ThreadLocal保证多线程中同一数据的独立性。



**简单的例子**

```java
public class ThreadLocalDemo {

    static ThreadLocal threadLocal = new ThreadLocal();
    static  int num  = 111222;

    public static void main(String[] args) throws InterruptedException {

        ThreadPoolExecutor threadPoolExecutor = new ThreadPoolExecutor(1,5,5, TimeUnit.SECONDS,
                new LinkedBlockingDeque<Runnable>(4));

//        创建两个线程
        for (int i = 0; i < 2; i++) {
            threadPoolExecutor.execute(new Runnable() {
                @Override
                public void run() {
                    //每个线程调用threadLocal放入公共变量
                    threadLocal.set(num);
                    System.out.println("num原来的值"+threadLocal.get());
                    threadLocal.set(Math.random()*100);
                    System.out.println("当前线程"+Thread.currentThread().getName()+"num值:"+threadLocal.get());
                }
            });
        }

        Thread.sleep(3000);

        System.out.println("main线程中num的值"+num);
    }
}

/*
结果
num原来的值111222
当前线程pool-1-thread-1num值:95.97532385548654
num原来的值111222
当前线程pool-1-thread-1num值:4.016108131350837
main线程中num的值111222
*/
```



**ThreadLocal的实现原理**

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/1368768-20190614000329689-872917045.png" alt="img" style="zoom:50%;" />

先来看看Thread类

```java
public class Thread implements Runnable {
 ......
ThreadLocal.ThreadLocalMap threadLocals = null;

ThreadLocal.ThreadLocalMap inheritableThreadLocals = null;
 ......
}
```

Thread类中有两个变量，分别是**threadLocals和inheritableThreadLocals**，这两个变量默认值为空。

这两个变量属于ThreadLocal中内部的静态类ThreadLocalMap类型，而ThreadLocalMap中类似一个HashMap的结构，用来存放数据。

只有当线程第一次调用ThreadLocal的set()和get()方法时才会创建。



再来看看ThreadLocal类

**set()方法源码**

```java
//将传入的数据进行存储  
public void set(T value) {
    //获取当前线程
        Thread t = Thread.currentThread();
    //将当前线程作为参数传给getMap方法获取threadLocals
        ThreadLocalMap map = getMap(t);
    //若当前map不为空，说明线程之前存放过数据
        if (map != null)
            //ThreadLocalMap是以键值对形式存放数据，key对应当前线程的引用，value对应传入的值，该变量存入线程的本地变量中
            map.set(this, value);
        else
            //若map为空,说明当前线程是首次添加，因此创建对应的map
            createMap(t, value);
}


//获取当前线程的threadLocals
ThreadLocalMap getMap(Thread t) {
    //threadLocals是ThreadLocalMap类型
    return t.threadLocals;
}

//创建map
void createMap(Thread t, T firstValue) {
    //这里可以看到当前线程中threadLocals就是存放变量的地方，这里新创建了map绑定当前线程，存入数据
    t.threadLocals = new ThreadLocalMap(this, firstValue);
}
```

同上面可以知道线程中本地变量保存的位置是位于Thread中的threadLocals变量中，threadLocals是ThreadLocalMap类型，以键值对的形式被保存下来，通过线程可以找到对应的值，实现了同一数据的独立性。



**get()方法源码**

```java
//获取当前线程绑定数据
public T get() {
    //获取当前线程
    Thread t = Thread.currentThread();
    //通过getMap获取threadLocals，threadLocals中存储对应的值
    ThreadLocalMap map = getMap(t);
    //若threadLocals不为空，说明当前线程已经有对应的数据存入threadLocals中
    if (map != null) {
        //获取数据
        ThreadLocalMap.Entry e = map.getEntry(this);
        if (e != null) {
            @SuppressWarnings("unchecked")
            T result = (T)e.value;
            return result;
        }
    }
    //若threadLocals为空，说明对应该线程的本地变量为空，调用setInitialValue方法进行初始化
    return setInitialValue();
}

private T setInitialValue() {
    //value 设置为 null
    T value = initialValue();
    //获取当前线程
    Thread t = Thread.currentThread();
    //判断当前线程的本地变量是否为空
    ThreadLocalMap map = getMap(t);
    //不为空
    if (map != null)
        //在当前线程中添加
        map.set(this, value);
    else
        //为空，首次添加，进行创建
        createMap(t, value);
    return value;
}

protected T initialValue() {
    return null;
}
```



remove()方法：用来把当前线程中的threadLocals清空(本地变量)。

当前线程若使用完毕后，需要将对应的本地变量(threadLocals)清空，不然可能会导致(内存溢出)。

```java
public void remove() {
    //获取当前线程绑定的threadLocals
     ThreadLocalMap m = getMap(Thread.currentThread());
     //如果map不为null，就移除当前线程中指定ThreadLocal实例的本地变量
     if (m != null)
         m.remove(this);
 }
```



**ThreadLocal不支持继承性**

同一个ThreadLocal实例在父线程中设置本地变量后，子线程不能获取到父线程中的本地变量（threadLocals和对应线程绑定）。

```java
    static  ThreadLocal threadLocal = new ThreadLocal();

    public static void main(String[] args) throws InterruptedException {

        threadLocal.set("父线程变量");

        Thread thread = new Thread(new Runnable() {
            @Override
            public void run() {
                System.out.println("子线程运行"+"尝试获取父线程中本地变量"+threadLocal.get());
            }
        });

        thread.start();

        Thread.sleep(1000);

        System.out.println("父线程中本地变量:"+threadLocal.get());
    }
//结果：子线程运行尝试获取父线程中本地变量null  ， 父线程中本地变量:父线程变量
```

补充：InheritableThreadLocal类能够实现继承，InheritableThreadLocal类继承了ThreadLocal类。

ThreadLocal中另一个变量inheritableThreadLocals就是被InheritableThreadLocal所使用到的。



**ThreadLocal内存泄漏问题**

从ThreadLocal中静态类ThreadLocalMap来看内存泄漏的问题。

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/1368768-20190614105112553-1657649661.png" alt="img" style="zoom:50%;" />

ThreadLocal是一个工具类，提供了set、get、remove方法，这些方法实际上都是在操作threadLocals这个变量，这个变量的类型是ThreadLocalMap，而这个类内部实际上是一个Entry类型的数组，键值对形式。

来看看ThreadLocalMap中Entry的源码

```java
//Entry这个静态类是继承WeakReference(弱引用)
static class Entry extends WeakReference<ThreadLocal<?>> {
    //ThreadLocal中set方法传递的值，用来存放线程对应的本地变量的值
    Object value;

    //k代表键值，ThreadLocal类型的引用
    //构造方法初始化
    Entry(ThreadLocal<?> k, Object v) {
        //调用WeakReference的构造方法
        super(k);
        value = v;
    }
}

//WeakReference构造方法(public class WeakReference<T> extends Reference<T> )
//referent:ThreadLocal类型的引用
public WeakReference(T referent) {
    super(referent);
}

Reference(T referent) {
    this(referent, null);
}
```

从上面可以看出来，threadLocals变量通过set方法存值时，对应传入的ThreadLocal类型key被传递给WeakReference构造方法，因此threadLocals中key是ThreadLocal类型的**弱引用(当进行GC时，它无法逃脱，只能被GC)**，threadLocals中value**是强引用(只要当前对象可达还存在，它就会一直存在，不会被GC)**。当ThreadLocal没有被外部强引用，当前线程还存在，在进行GC时，对应线程中ThreadLocalMap中ThreadLocal类型的引用就会被回收，而对应的value不会被回收，导致ThreadLocalMap中出现key为null，value不为null的情况，若不做任何的措施，那么value永远无法被回收，最后导致**内存泄漏**。

好在ThreadLocalMap 实现中已经考虑了这种情况，在调⽤ set() 、 get() 、 remove() ⽅法的时候，会清理掉 key 为 null的记录。使⽤完 ThreadLocal ⽅法后 最好⼿动调⽤ remove() ⽅法。



ThreadLocal多应用于**数据库连接、Session管理**

```java
public class TransactionThreadLocal {
 
	private static ThreadLocal<Connection> tc = new ThreadLocal<>();
	/**
	 * 返回当前线程的数据库连接
	 * @return
	 * @throws SQLException
	 */
	public static Connection getConnection() throws SQLException{
		Connection connection = tc.get();
		if(connection == null){
			connection = C3P0Utils.getConnection();
			tc.set(connection);
		}
		return connection;
	}
}
//tc.get()用来获取当前线程中本地变量，对应当前线程在数据库的状态
```

------



### java中的线程调度

#### 抢占式调度

1. 线程执行的时间、线程的切换都是由系统来决定调度的
2. 不会出现一个线程阻塞导致后续的都无法进行

#### 协同式调度

1. 一个线程执行完毕后通知系统切换到下一个线程继续执行(**如同接力赛一般**)
2. 线程执行的时间由其本身决定，线程的切换是可预知的，不存在线程同步问题
3. 若一个线程出现问题阻塞了会导致其不会通知系统导致后续线程无法运行

java中线程采用**抢占式调用**，java中线程是按照线程的优先级来分配cpu时间片，优先级越高可能可以获取到更多的时间片，优先级低可能获得少量的时间片，但不会存在得不到时间片的情况。

------



### **CAS(compare and swap/set)**

[CAS原理解析 CAS底层 - YoungDeng - 博客园 (cnblogs.com)](https://www.cnblogs.com/youngdeng/p/12869037.html)

CAS：比较 和 交换。判断内存中某个位置的值是否和预期值相符(**比较**)，如果相符将对应内存中的值更新为新的值(**交换/设置**),整个过程是原子性的。



CAS的原语体现在java中的sun.misc.Unsafe类的各个方法。**Unsafe类中的CAS方法**，JVM帮助我们实现**CAS的汇编语言**，这个过程是依赖于硬件的功能，通过它实现了**原子操作**。CAS是一种系统源语，属于操作系统的范畴，由若干条指令组成，原语的执行过程必须是连续的，执行过程中无法被中断，因此CAS的操作具有原子性，不会造成数据的不一致，保证了多线程的线程安全。



JDK1.5 的原子包：java.util.concurrent.atomic 这个包里面提供了一组**原子类,**这里使用**AtomicInteger**来展示一下CAS操作的基本过程。

```java
    public static void main(String[] args) {
        AtomicInteger atomicInteger = new AtomicInteger(10);

        System.out.println("是否交换成功"+atomicInteger.compareAndSet(10,2233)+" 查看当前atomicInteger内存中的值"+atomicInteger.get());
        System.out.println("是否交换成功"+atomicInteger.compareAndSet(10,1122)+" 查看当前atomicInteger内存中的值"+atomicInteger.get());
    }
/*
是否交换成功true 查看当前atomicInteger内存中的值2233
是否交换成功false 查看当前atomicInteger内存中的值2233
*/
```

上面在AtomicInteger原子类中设置初始值value为10，调用compareAndSet方法设置期望值为：10，更新值：2233，第一次对比发现，期望着和内存中的值相符，因此将内存中的值更新为2233，第二次调用对比：内存中的值为2233，期望值为10，不相符，因此无法更新。



**CAS底层实现**

先来看看AtomicInteger的内部

```java
public class AtomicInteger extends Number implements java.io.Serializable {

    //更新的过程是调用Unsafe类中的compareAndSwapInt方法
    private static final Unsafe unsafe = Unsafe.getUnsafe();
    //此变量表示内存中存储值的位置，内存偏移量
    private static final long valueOffset;

    static {
        try {
            valueOffset = unsafe.objectFieldOffset(AtomicInteger.class.getDeclaredField("value"));
        } catch (Exception ex) { throw new Error(ex); }
    }

    //被volatile修饰的变量，保证在多线程中变量的可见性和有序性
    private volatile int value;
}
```



借用刚才的例子看看compareAndSet方法

```java
//位于AtomicInteger类中
public final boolean compareAndSet(int expect, int update) {
    return unsafe.compareAndSwapInt(this, valueOffset, expect, update);
}
/*
expect:期望值
update:更新值
this:当前对象
valueOffset:之前提到的内存偏移量
*/
```

AtomicInteger类借助Unsafe类完成CAS操作，由此可见**Unsafe是CAS操作的核心类，由于java无法直接访问系统底层，需要通过本地方法(Native)来访问，通过Unsafe类中的方法可以完成对内存数据的定位和操作，和c语言一样直接操作内存**。

我们来看一看Unsafe类的内部

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210805130145407.png" alt="image-20210805130145407" style="zoom:67%;" />

可以看到当中方法都是被**Native**关键字所修饰方法，我们接着往下看，下面会介绍上图所示的一些方法。

我们接着上面的方法继续，进入Unsafe方法中

```java
 unsafe.compareAndSwapInt(this, valueOffset, expect, update);
```

我们来看看下面这个方法

```java
  public final native boolean compareAndSwapInt(Object var1, long var2, int var4, int var5);
```

```java
public final int getAndIncrement() {
    return unsafe.getAndAddInt(this, valueOffset, 1);
}
//getAndAddInt方法中运用了compareAndSwapInt方法，来完成CAS操作
public final int getAndAddInt(Object var1, long var2, int var4) {
        //用来存放主内存中的数据
    	int var5;
        do {
            //va1:当前AtomicInteger对象，
            //var2:内存偏移量
            //通过getIntVolatile方法拿到主内存中的数据放入工作内存(线程操作变量的地方)
            var5 = this.getIntVolatile(var1, var2);
            //var5从主存中对应数据和compareAndSwapInt方法中var4期望值作比较
        } while(!this.compareAndSwapInt(var1, var2, var5, var5 + var4));
        return var5;    
}
```

工作流程：

这里说一说**getAndIncrement()**方法

从主存中读取数据（**var5**），然后和期望值进行CAS比较，若返回true，内存值和期望值一致进行更新(**var5+var4**)，若返回false，继续读取主存数据直到成功为止。

上面就是CAS的操作过程，这个过程没有进行加锁操作(**Synchronized**)，在实现了并发性的同时，也保证了数据的一致性。

每个线程进来后，进入do while语句进行判断，内存中的值是否和期望值相符，不相符就一直循环，相符就进行更新操作。



接下来举个例子来看看，多线程中如何实现CAS操作的。

线程A和线程B，它们在多核cpu上工作，调用还是原子类AtomicInteger来进行数值操作。

1. AtomicInteger对象存放value初始值为10，value被**volatile关键字修饰**，根据JMM(**java memory model**)，线程A和线程B从主存中各复制了一份value放在工作内存中(缓存)。
2. 线程A通过getIntVolatile方法获取value的值，然后线程A被挂起(让出cpu)
3. 线程B通过getIntVolatile方法获取value的值，线程B没有被挂起，继续工作执行compareAndSwapInt方法，发现主存中的值和预期值相符，将主存中的值修改成15，线程B结束了
4. 线程A此时开始运行，执行CAS操作，发现主存中的值不再是10，说明在自己挂起的期间主存的值已经被别的线程修改，本次CAS操作没有成功，继续循环
5. 线程A重新获取value值，被volatile修饰value，线程A能够看到其他线程修改后的值，这一次compareAndSwapInt方法，执行成功，更新数据。

**CAS操作不进行加锁，是一个非阻塞的过程，dowhile循环这个过程就是一个自旋的过程**



再来看看**compareAndSet()**方法

[(12条消息) 并发实战——原子类AtomicReference及底层源码CompareAndSwapObject分析_qqqqq1993qqqqq的博客-CSDN博客_compareandswapobject](https://blog.csdn.net/qqqqq1993qqqqq/article/details/75211993)

compareAndSet方法直接调用compareAndSwapInt方法，该方法是Unsafe的一个本地方法，方法的实现位于unsafe.cpp中

```java
//这里借助CompareAndSwapObject
UNSAFE_ENTRY(jboolean, Unsafe_CompareAndSwapObject(JNIEnv *env, jobject unsafe, jobject obj, jlong offset, jobject e_h, jobject x_h))
  UnsafeWrapper("Unsafe_CompareAndSwapObject");
  oop x = JNIHandles::resolve(x_h); // 新值
  oop e = JNIHandles::resolve(e_h); // 预期值
  oop p = JNIHandles::resolve(obj);
  HeapWord* addr = (HeapWord *)index_oop_from_field_offset_long(p, offset);// 在内存中的具体位置
  oop res = oopDesc::atomic_compare_exchange_oop(x, addr, e, true);// 调用了另一个方法
  jboolean success  = (res == e);  // 如果返回的res等于e，则判定满足compare条件（说明res应该为内存中的当前值），但实际上会有ABA的问题
  if (success) // success为true时，说明此时已经交换成功（调用的是最底层的cmpxchg指令）
    update_barrier_set((void*)addr, x); // 每次Reference类型数据写操作时，都会产生一个Write Barrier暂时中断操作，配合垃圾收集器
  return success;
UNSAFE_END


UNSAFE_ENTRY(jboolean, Unsafe_CompareAndSwapInt(JNIEnv *env, jobject unsafe, jobject obj, jlong offset, jint e, jint x))
  UnsafeWrapper("Unsafe_CompareAndSwapInt");
  oop p = JNIHandles::resolve(obj);
  jint* addr = (jint *) index_oop_from_field_offset_long(p, offset);
  return (jint)(Atomic::cmpxchg(x, addr, e)) == e;//这里调用的就是CPU指令cmpxchg
UNSAFE_END
    
    /*
    x:需要更新的值
    e:主存中的值
    */
```

```java
inline jint     Atomic::cmpxchg    (jint     exchange_value, volatile jint*     dest, jint     compare_value) {
  // alternative for InterlockedCompareExchange
  int mp = os::is_MP();
  __asm {
    mov edx, dest  // eax,ecx,edx都是32位寄存器
    mov ecx, exchange_value
    mov eax, compare_value
    LOCK_IF_MP(mp)
    cmpxchg dword ptr [edx], ecx
  }
}

/*
上述是cpu层面的CAS，介绍如下：
若期望值等于对象地址存储的值，则用新值来替换对象地址存储的值，否则，把期望值变为当前对象地址存储的值
*/
```

正如前面介绍的CAS操作调用Unsafe类中的本地方法，本地方法最终转换成一条CPU指令**cmpxchg**(汇编语言)，**它不会被多线程的调度所打断，能够保证CAS操作的原子性，JVM中的CAS的原子性是处理器保障的**。

由此可知，原子变量(AtomicInteger)提供的原子性来自CAS操作，CAS来自Unsafe的本地(**native**)方法，由CPU的cmpxchg指令保证。

由于CAS仅仅是一条指令，因此它不会被多线程的调度所打断，所以能够保证CAS操作是一个原子操作。

**补充**:当代的很多CPU种类都支持cmpxchg操作，但不是所有CPU都支持，对于不支持的CPU，会自动加锁来保证其操作不会被打断。



**CAS缺点**

cas不加锁的特点，保证原子性过程中需要多次比较

- 循环时间长，开销大(若某个线程在进行CAS比较后没有成功更新，一直执行do while循环，最坏的情况可能导致无线循环)
- 只能保证一个共享变量操作的原子性
  - 对于一个共享变量操作时，通过CAS循环比较方法保证操作原子性
  - 对于多个共享变量操作时，CAS循环无法保证操作的原子性，可以采用加锁来保证原子性,封装成对象类解决
- **ABA问题**
  - 当一个线程进行CAS操作时，它需要先获取某时刻的主存中的数据，然后获取到后进行比较，然而可能在获取到比较的这个时间段内其他线程对内容进行了修改，例如：A线程获取主存值2，此时B线程也获取了主存值2，主存值进行了更改3，B线程又将其改成了2，线程A进行比较，完成了更新。**这就是ABA问题**，当中可能存在着问题(**但是实际上该值已经被其他线程改变过，这与乐观锁的设计思想不符合**)。
  - 部分乐观锁采取添加**版本号**(version)的方式来解决，，乐观锁每次在执行数据的修改操作时，都会带上一个版本号，一旦版本号和数据的版本号一致就可以执行修改操作并对版本号执行+1 操作，否则就执行失败。因为每次操作的版本号都会随之增加，所以不会出现 ABA 问题，因为版本号只会增加不会减少。
  - 在JDK的java.util.concurrent.atomic包中提供了**AtomicStampedReference来解决ABA问题**



使用线程池放入20个线程，使用CountDownLatch/CyclicBarrier是实现多线程并发，每个线程访问5次

```java
    public static void request() throws InterruptedException {
        TimeUnit.MILLISECONDS.sleep(5);
        count.getAndIncrement();
        //普通count下使用
        cout++;
    }
    
/*    public static synchronized void request() throws InterruptedException {
        TimeUnit.MILLISECONDS.sleep(5);
        count.getAndIncrement();
      }
  */ 

    static CountDownLatch countDownLatch = new CountDownLatch(20);

//    static  int count = 0;
    static AtomicInteger count = new AtomicInteger(0);
    public static void main(String[] args) throws InterruptedException {
        long startTime = System.currentTimeMillis();

        ThreadPoolExecutor threadPoolExecutor = new ThreadPoolExecutor(10,30,5, TimeUnit.SECONDS,
                new LinkedBlockingQueue<Runnable>(20));

        for (int i = 0; i < 20 ; i++) {
            threadPoolExecutor.execute(new Runnable() {
                @Override
                public void run() {
                    try {
                        for (int j = 0; j < 5 ; j++) {
                            request();
                        }
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }finally {
                        countDownLatch.countDown();，
                    }
                }
            });
        }

        countDownLatch.await();

        long endTime = System.currentTimeMillis();
        System.out.println("消耗时间： "+( endTime - startTime));
        System.out.println("访问次数:" + count);
    }

/*
1.
 static  int count = 0;
 只使用普通变量，最后count结果如下
消耗时间： 63
访问次数:64
发现访问次数只有64次，多线程访问导致数据不一致，count++操作也无法保证数据的原子性，即使把count变量使用volatile关键字修饰也没有办法实现100次访问。

2.
使用synchronized可保证数据的一致性
结果
消耗时间： 540
访问次数:100

3.
使用原子类保证，去掉synchronized
static AtomicInteger count = new AtomicInteger(0);
count.getAndIncrement();
结果
消耗时间： 64
访问次数:100

结果很显然CAS在保证了多线程数据一致性的基础上，还减少了消耗的时间，CAS是一种无锁、非阻塞、自旋的操作。
*/
```



------





### AQS(抽象的队列同步器)

[Java并发之AQS详解 - waterystone - 博客园 (cnblogs.com)](https://www.cnblogs.com/waterystone/p/4920797.html)

[从ReentrantLock的实现看AQS的原理及应用 - 美团技术团队 (meituan.com)](https://tech.meituan.com/2019/12/05/aqs-theory-and-apply.html)

AQS（Abstract Queued Synchronizer）

抽象式队列同步器，是一套多线程访问共享资源的同步框架。许多同步类都是基于它实现同步、线程安全。例如：ReentrantLock/

Semaphore/CountDownLatch



**AQS原理框架**

![img](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/721070-20170504110246211-10684485.png)

AQS**核心思想：如果被请求的共享资源空闲，就将当前请求资源的线程设置为有效的工作线程，并将共享资源的状态锁定；如果被请求的共享资源空间已经被占用，就需要一些阻塞唤醒机制保证锁资源分配。**

这个机制主要是用**CLH队列(先进先出特性FIFO)**实现，其本身是一个单向链表，在AQS中是**虚拟双向队列**的存在，AQS通过将请求共享资源的线程封装成一个结点**Node**实现锁资源的分配。

它维护了一个**volatile int state**的变量来代表共享资源，通过设定state的值来代表当前资源是否被占用。通过关键字volatile和CAS操作来更新state，保证了多线程情况下state的原子性、可见性、有序性。

**访问state变量的方法如下**

- getState()  :获取state的值
- setState() ：设置state的值
- compareAndSetState()：通过CAS操作更新state

上面三个方法都是final所修饰，因此不能被子类重写，可以通过State表示同步状态实现多线程的**独占模式(ReentrantLock)和共享模式（CountDownLatch）**。

**AQS定义资源共享方式**: **Exclusive(独占方式，只能是一个线程使用)**,**Share（共享方式，多个线程同时使用）**

| <img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210806110616859.png" alt="image-20210806110616859" style="zoom: 80%;" /> | <img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210806124124206.png" alt="image-20210806124124206" style="zoom:80%;" /> |
| ------------------------------------------------------------ | ------------------------------------------------------------ |

AQS提供了大量用于**自定义同步器实现的Protected方法**,自定义同步器实现时只需要对**state**进行修改来实现独占或共享模式。

自定义同步器实现的主要方法如下：

- isHeldExclusively()：该线程是否正在独占资源。只有用到condition才需要去实现它。
- tryAcquire(int)：独占方式。尝试获取资源，成功则返回true，失败则返回false。
- tryRelease(int)：独占方式。尝试释放资源，成功则返回true，失败则返回false。
- tryAcquireShared(int)：共享方式。尝试获取资源。负数表示失败；0表示成功，但没有剩余可用资源；正数表示成功，且有剩余资源。
- tryReleaseShared(int):共享方式。尝试释放资源，如果释放后允许唤醒后续等待结点返回true，否则返回false。



以ReentrantLock（**独占锁**）为例，state初始化为0.表示没有线程使用共享资源，当线程A进入调用tryAcquire独占该锁资源并将state进行＋1，当其他线程进入尝试获取锁资源，进行state值的判断，若state不为0，表明已经有线程占用资源，其他线程进入队列中等待，直到线程A对锁资源进行解锁，state状态修改成0时，其他线程才有机会获取锁。当然，在线程A没有解锁之前，还可以继续获取此锁，这就是重入，每获取一次state加1，每释放一次锁state减1，最后保证在释放完锁后，state状态归为0



以CountDownLatch(**共享**)为例，让N个子线程同时执行，共用同一资源，state初始化为N，每运行一个子线程对应调用countDown()减一，直到state = 0 时表明N个子线程已经运行完成，阻塞在某一点，之后主线程调用await()方法完成后续工作。



一般来说，自定义同步器要么是独占式，要么时共享式，对应实现tryAcquire---tryRelease、tryAcquireShared---tryReleaseShared一种即可。但是AQS也支持同时实现独占和共享模式，比如：ReentrantReadWriteLock



上面主要说的是使用AQS实现自定义同步器，接下来说说AQS中**获取锁的过程以及未获得锁在队列中如何实现等待、唤醒获取锁的过程。**

这里先来说一下**CLH队列中Node结点**，它是AQS中最基本的数据结构。

| 方法和属性值 | 含义                                                         |
| ------------ | ------------------------------------------------------------ |
| waitStatus   | 当前节点在队列中的状态                                       |
| thread       | 表示处于该节点的线程                                         |
| prev         | 前驱指针                                                     |
| predecessor  | 返回前驱节点，没有的话抛出npe                                |
| nextWaiter   | 指向下一个处于CONDITION状态的节点（由于本篇文章不讲述Condition Queue队列，这个指针不多介绍） |
| next         | 后继指针                                                     |

waitStatus**属性中的几个枚举值**

| 枚举      | 含义                                                         |
| --------- | ------------------------------------------------------------ |
| 0         | 当一个Node被初始化的时候的默认值                             |
| CANCELLED | 为1，表示线程获取锁的请求已经取消了                          |
| CONDITION | 为-2，表示节点在等待队列中，节点线程等待唤醒                 |
| PROPAGATE | 为-3，当前线程处在SHARED情况下，该字段才会使用前继结点不仅会唤醒其后继结点，同时也可能会唤醒后继的后继结点。 |
| SIGNAL    | 为-1，表示线程已经准备好了，就等资源释放了                   |

**负值表示结点处于有效等待状态，而正值表示结点已被取消。所以源码中很多地方用>0、<0来判断结点的状态是否正常**。



#### tryAcquire(int) ------tryRelease(int)



以非公平锁为例，这里主要阐述一下非公平锁与AQS之间方法的关联之处

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/b8b53a70984668bc68653efe9531573e78636.png" alt="img" style="zoom:80%;" />

1. 定义非公平锁，尝试通过CAS去修改state的值，若修改成功设置成独占模式,获取到锁的资源。

   ```java
   static final class NonfairSync extends Sync {
   	...
   	final void lock() {
           //期望值0，希望更新的值1，state 设置为1
   		if (compareAndSetState(0, 1))
   			setExclusiveOwnerThread(Thread.currentThread());
   		else
   			acquire(1);
   	}
     ...
   }
   ```

2. 通过CAS操作没能修改成功表明共享资源已经被其他线程调用，就调用acquire方法

   1. **acquire(int)**

      此方法是独占模式下线程获取共享资源的**顶层入口**，如果线程获取到资源，线程直接返回，否则进入等待队列中，直到获取到资源为止，**且整个过程忽略中断的影响**。

      ```java
      //arg 传入值：1 
      public final void acquire(int arg) {
           if (!tryAcquire(arg) && acquireQueued(addWaiter(Node.EXCLUSIVE), arg))
               selfInterrupt();
       }
      ```
   
       函数流程：
   
      1. 先去调用**tryAcquire()**方法(**需要自定同步器来实现**)，尝试获取锁，如果成功就直接返回(**体现了非公平锁的特性**，即使等待队列中已经有线程在等待资源，而当前线程不会马上进入等待队列中，而是尝试获取锁)
      2. **addWaiter**()方法将没有获取到锁的线程加入到等待队列中，并标记为独占模式
      3. **acquireQueued**()使线程阻塞在等待队列中，直到获取资源。整个阻塞的过程是否发生过中断，若发生过，返回true，反之false。
      4. 若线程在阻塞的过程中发生了中断，在获取锁资源后调用selfInterrupt()方法，将中断补上。
   
   2. **tryAcquire（）**
   
      源码
   
      ```java
       protected boolean tryAcquire(int arg) {
               throw new UnsupportedOperationException();
       }
      ```
   
       发现该方法中方法体只有一个抛出异常，具体获取锁资源的代码呢？
   
      **前面也说了AQS提供的这些方法是需要自定义同步器自行去实现的**，该方法返回true，说明当前线程获取锁成功，返回false表示失败，就需要加入到等待队列中。
   
   3. **addWaiter()**
   
       通过addWaiter方法将线程加入到等待队列中，当前线程被放入队列的尾部。
   
      ```java
      private Node addWaiter(Node mode) {
          //以给定模式构造结点。mode有两种：EXCLUSIVE（独占）和SHARED（共享）
          Node node = new Node(Thread.currentThread(), mode);
      
          //尝试快速方式直接放到队尾。
          //pred指针指向队列尾结点tail
          Node pred = tail;
          if (pred != null) {
              //当前线程结点的前驱指针指向尾结点tail
              node.prev = pred;
              //compareAndSetTail完成尾节点的设置
              if (compareAndSetTail(pred, node)) {
                  //原尾结点tail的后继指针指向当前线程结点
                  pred.next = node;
                  return node;
              }
          }
      
          //上一步失败则通过enq入队。
          enq(node);
          return node;
      }
      ```
   
      若pred == null(**说明队列中没有结点**)，或者当前Pred指针和Tail指向的位置不同（说明被别的线程已经修改）
   
      调用enq方法将线程加入到队尾中。
   
      **enq()**
   
      ```java
      private Node enq(final Node node) {
          //CAS"自旋"，直到成功加入队尾
          for (;;) {
              //获取尾结点
              Node t = tail;
              if (t == null) { // 队列为空，创建一个空的标志结点作为head结点，并将tail也指向它。
                  if (compareAndSetHead(new Node()))
                      tail = head;
              } else {//正常流程，放入队尾
                  node.prev = t;
                  if (compareAndSetTail(t, node)) {
                      t.next = node;
                      return t;
                  }
              }
          }
      }
      ```
   
   4. **acquireQueued(Node int)**
   
       前面通过调用tryAcquire和addWaiter方法将没有获取到锁资源的线程放入到等待队列的队尾中。
   
      这个方法就是让等待队列中的线程不断尝试获取锁，**直到成功获取成功**。现在线程需要做的只有一件事：排队等待。
   
      ```java
      final boolean acquireQueued(final Node node, int arg) {
          boolean failed = true;//标记是否成功拿到资源
          try {
              boolean interrupted = false;//标记等待过程中是否被中断过
      
              //又是一个“自旋”！要么获取锁，要么中断
              for (;;) {
                  final Node p = node.predecessor();//拿到前驱结点
                  //如果前驱是head(头结点---->虚结点)，即当前结点已经成为真实数据的首结点，那么便有资格去尝试获取资源（可能是老大释放完资源唤醒自己的，当然也可能被interrupt了）。
                  if (p == head && tryAcquire(arg)) {
                      setHead(node);//拿到资源后，将head指向该结点。所以head所指的标杆结点，就是当前获取到资源的那个结点或null。
                      p.next = null; // setHead中node.prev已置为null，此处再将head.next置为null，就是为了方便GC回收以前的head结点。也就意味着之前拿完资源的结点出队了！
                      failed = false; // 成功获取资源
                      return interrupted;//返回等待过程中是否被中断过
                  }
      
                  //当程序走到这一步时，说明当前p为头节点并没有获取到锁(非公平锁被抢占)或者不为头节点，此时需要判断当前node是否需要被阻塞，防止无线循环造成资源浪费
                  if (shouldParkAfterFailedAcquire(p, node) && parkAndCheckInterrupt())
                      interrupted = true;//如果等待过程中被中断过，哪怕只有那么一次，就将interrupted标记为true
              }
          } finally {
              if (failed) // 如果等待过程中没有成功获取资源（如timeout，或者可中断的情况下被中断了），那么取消结点在队列中的等待。
                  cancelAcquire(node);
          }
      }
      ```
   
       上述方法的流程
   
      <img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210806145150447.png" alt="image-20210806145150447" style="zoom:80%;" />
   
      
   
      
   
      **shouldParkAfterFailedAcquire(Node pred, Node node)**
   
      ```java
      // 靠前驱节点判断当前线程是否应该被阻塞
      private static boolean shouldParkAfterFailedAcquire(Node pred, Node node) {
      	// 获取头结点的节点状态
      	int ws = pred.waitStatus;
      	// 说明头结点处于唤醒状态,signal:表示线程已经准备好了，就等资源释放了
      	if (ws == Node.SIGNAL)
      		return true; 
      	// 通过枚举值我们知道waitStatus>0是取消状态
      	if (ws > 0) {
      		do {
      			// 循环向前查找取消节点，把取消节点从队列中剔除（GC）
      			node.prev = pred = pred.prev;
      		} while (pred.waitStatus > 0);
      		pred.next = node;
      	} else {
      		// 设置前任节点等待状态为SIGNAL
      		compareAndSetWaitStatus(pred, ws, Node.SIGNAL);
      	}
      	return false;
      }
      ```
   
       **parkAndCheckInterrupt()**     挂起当前线程，阻塞调用栈，返回当前线程的中断状态
   
      ```java
      private final boolean parkAndCheckInterrupt() {
          LockSupport.park(this);
          return Thread.interrupted();
      }
      ```
   
       上述方法流程
   
      <img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210806145217882.png" alt="image-20210806145217882" style="zoom:80%;" />

总结一下流程

1. 首先尝试通过compareAndSetState方法，更新state值为0，若可以成功，设置成独占模式，直接获取锁
2. 流程1失败，就调用acquire方法通过tryAcquire方法尝试获取锁资源，若获取成功直接返回
3. 若失败，就调用addWaiter方法将线程放入等待队列的队尾等待获取资源。
   1. 自旋过程获取锁资源，获取当前结点的前驱结点，若前驱结点为头节点，并且当前结点获取锁成功，当前结点设置成头节点。
   2. 没能获取到锁资源(非公平锁被抢占)，防止因死循环造成cpu资源被浪费，判断当前结点的前驱结点状态来判断当前结点是否要被挂起。



加锁的过程看完了，现在来看看解锁的过程

解锁的过程是调用**release**方法，**该方法是独占模式下线程释放公共资源的顶层入口**。它会释放定量的资源，若释放了全部资源(**state == 0**)，它会唤醒等待队列中其他的线程来获取资源。



先来看看release方法中的**tryRelease方法**，

```java
 protected boolean tryRelease(int arg) {
     throw new UnsupportedOperationException();
 }
```

在独占模式下，和tryAcquire方法一样，需要自定义同步器实现该方法，该方法用来释放资源，那么对应线程肯定已经拿到独占的资源，

直接剪掉相应量的资源(**getState() - arg**)，因为是独占模式，不存在线程安全的问题，**判断当前所持有资源state是否为0，0表示资源已经彻底释放**，根据返回值boolean，0返回true，否则返回false。所以我们可以知道**tryRelease方法是用来判断资源是否已经释放完毕的**。

回到**release方法中**，源码如下

```java
// java.util.concurrent.locks.AbstractQueuedSynchronizer

public final boolean release(int arg) {
    //判断当前线程是否已经释放了所持有的所有资源
	if (tryRelease(arg)) {
        //获取头节点
		Node h = head;
        //头结点不为空并且头结点的waitStatus不是初始化节点情况
        //h == null Head还没初始化。
        //waitStatus == 0 表明后继节点对应的线程仍在运行中，不需要唤醒。
        //waitStatus < 0 表明后继节点可能被阻塞了，需要唤醒
		if (h != null && h.waitStatus != 0)
            //唤醒队列中的下一个等待获取资源的线程
			unparkSuccessor(h);
		return true;
	}
	return false;
}
```

**unparkSuccessor（）**

源码如下

```java
private void unparkSuccessor(Node node) {
    //获取头节点的状态
    int ws = node.waitStatus;
    if (ws < 0)//置零当前线程所在的结点状态，允许失败。
        compareAndSetWaitStatus(node, ws, 0);
	//获取当前结点的下一个结点
    Node s = node.next;
    //如果为空或已取消，就找队列中最开始的没有取消的结点
    if (s == null || s.waitStatus > 0) {
        s = null;
        // 从后向前找，找到队列第一个waitStatus<0的节点。
        for (Node t = tail; t != null && t != node; t = t.prev) 
            //从这里可以看出，<=0的结点，都是还有效的结点。
            if (t.waitStatus <= 0)
                s = t;
    }
    //当前结点的下一个结点不为空，状态<= 0
    if (s != null)
        //唤醒
        LockSupport.unpark(s.thread);
}
```

过程不复杂，资源释放完毕后，需要找到队列中请求资源的结点，将其唤醒的过程。**用unpark()唤醒等待队列中最前边的那个未放弃线程S**，这里就和前面acquireQueued()联系起来，唤醒队列中等待获取资源的**S**结点(**当然可能当前结点的前驱结点不一定是头节点，没关系在获取锁的过程中有处理当前问题的办法，就是通过shouldParkAfterFailedAcquire（）进行调整，S结点是队列中最前端的未放弃请求资源的结点，经过调整后，S结点最终会成为head的next的结点**)，通过（p == head && tryAcquire(arg)）方法判断是否是头节点并且是否获取到资源，若获取到资源，将S结点设置为**标杆节点**表明获取到了资源，成功返回。若没能够获取到资源，**通过当前节点的前驱节点判断是否要阻塞**。

这样就完成了加锁------>解锁----->加锁。。。。的循环



**有趣的问题：如果获取锁的线程在release时异常了，没有unpark队列中的其他结点，这时队列中的其他结点会怎么办？是不是没法再被唤醒了？**

给出答案：**yes**,此时等待队列中的线程都无法被唤醒，永远处于**park状态**

**release方法产生异常的原因**

1. 线程突然停止死亡，Thread.stop，**这个方法会产生线程安全问题已经被 Deprecated(弃用)**
2. 自定义同步器，实现AQS提供的Protect方法中，tryRelease方法产生了bug。



#### **tryAcquireShared(int) ------tryReleaseShared(int)**

来看看共享模式下的代码，其实和独占整体上差不多，有一些细节上的差别

**acquireShared(int)**

此方法是共享模式下线程获取共享资源的顶层入口。它会获取指定量的资源，获取成功则直接返回，获取失败则进入等待队列，直到获取到资源为止，整个过程忽略中断。

```java
 public final void acquireShared(int arg) {
     if (tryAcquireShared(arg) < 0)
         doAcquireShared(arg);
 }
```

- tryAcquireShared()尝试获取资源，成功则直接返回；
- 失败则通过doAcquireShared()进入等待队列，直到获取到资源为止才返回。

这里**tryAcquireShared**()依然需要自定义同步器去实现。但是AQS已经把其返回值的语义定义好了：

1. 小于0 :表示没有资源可以获取，
2.   等于0：获取成功，但是没有剩余资源，其他线程没有资源可以获取
3. 大于0:获取成功，还有资源，其他线程还可以获取



**doAcquireShared(int)**

此方法用于将当前线程加入等待队列尾部休息，直到其他线程释放资源唤醒自己，自己成功拿到相应量的资源后才返回。

```java
private void doAcquireShared(int arg) {
    final Node node = addWaiter(Node.SHARED);//加入队列尾部
    boolean failed = true;//是否成功标志
    try {
        boolean interrupted = false;//等待过程中是否被中断过的标志
        for (;;) {
            final Node p = node.predecessor();//前驱
            if (p == head) {//如果到head的下一个，因为head是拿到资源的线程，此时node被唤醒，很可能是head用完资源来唤醒自己的
                int r = tryAcquireShared(arg);//尝试获取资源
                if (r >= 0) {//成功
                    setHeadAndPropagate(node, r);//将head指向自己，还有剩余资源可以再唤醒之后的线程
                    p.next = null; // help GC
                    if (interrupted)//如果等待过程中被打断过，此时将中断补上。
                        selfInterrupt();
                    failed = false;
                    return;
                }
            }

            //判断状态，寻找安全点，进入waiting状态，等着被unpark()或interrupt()
            if (shouldParkAfterFailedAcquire(p, node) &&
                parkAndCheckInterrupt())
                interrupted = true;
        }
    } finally {
        if (failed)
            cancelAcquire(node);
    }
}
```

跟独占模式比，还有一点需要注意的是，这里只有线程是head.next时（“老二”），才会去尝试获取资源，有剩余的话还会唤醒之后的队友。

那么问题就来了，假如老大用完后释放了5个资源，而老二需要6个，老三需要1个，老四需要2个。老大先唤醒老二，老二一看资源不够，他是把资源让给老三呢，还是不让？答案是否定的！老二会继续park()等待其他线程释放资源，也更不会去唤醒老三和老四了。独占模式，同一时刻只有一个线程去执行，这样做未尝不可；但共享模式下，多个线程是可以同时执行的，现在因为老二的资源需求量大，而把后面量小的老三和老四也都卡住了。当然，这并不是问题，只是AQS保证严格按照入队顺序唤醒罢了（保证公平，但降低了并发）。

**setHeadAndPropagate(Node, int)**

```java
private void setHeadAndPropagate(Node node, int propagate) {
    Node h = head;
    setHead(node);//head指向自己
     //如果还有剩余量，继续唤醒下一个邻居线程
    if (propagate > 0 || h == null || h.waitStatus < 0) {
        Node s = node.next;
        if (s == null || s.isShared())
            doReleaseShared();
    }
}
```

此方法在setHead()的基础上多了一步，就是自己苏醒的同时，如果条件符合（比如还有剩余资源），还会去唤醒后继结点，毕竟是共享模式！



小结

1. 1. tryAcquireShared()尝试获取资源，成功则直接返回；
   2. 失败则通过doAcquireShared()进入等待队列park()，直到被unpark()/interrupt()并成功获取到资源才返回。整个等待过程也是忽略中断的。

　　其实跟acquire()的流程大同小异，只不过多了个**自己拿到资源后，还会去唤醒后继队友的操作（这才是共享嘛）**。



 **releaseShared()**

此方法是共享模式下线程释放共享资源的顶层入口。它会释放指定量的资源，如果成功释放且允许唤醒等待线程，它会唤醒等待队列里的其他线程来获取资源。下面是releaseShared()的源码：

```java
public final boolean releaseShared(int arg) {
    if (tryReleaseShared(arg)) {//尝试释放资源
        doReleaseShared();//唤醒后继结点
        return true;
    }
    return false;
}
```

**tryReleaseShared方法**与独占模式下的**tryRelease方法**不同之处在于，tryRelease方法需要判断state==0，也就是将资源全部释放，才会考虑后续等待队列中的唤醒过程，**毕竟独占下可以实现可重入，因此要考虑锁的加锁和释放过程**。而共享模式下tryReleaseShared方法则是**若有线程释放了部分资源，并且满足等待队列中请求资源线程的需要，就可以唤醒线程获取资源进行执行**，**这就展现了共享过程并发的实现**。

例如，资源总量是13，A（5）和B（7）分别获取到资源并发运行，C（4）来时只剩1个资源就需要等待。A在运行过程中释放掉2个资源量，然后tryReleaseShared(2)返回true唤醒C，C一看只有3个仍不够继续等待；随后B又释放2个，tryReleaseShared(2)返回true唤醒C，C一看有5个够自己用了，然后C就可以跟A和B一起运行。

**而ReentrantReadWriteLock读锁的tryReleaseShared()只有在完全释放掉资源（state=0）才返回true，所以自定义同步器可以根据需要决定tryReleaseShared()的返回值。**



 **doReleaseShared()**

此方法主要用于唤醒后继。下面是它的源码：

```java
private void doReleaseShared() {
    for (;;) {
        Node h = head;
        if (h != null && h != tail) {
            int ws = h.waitStatus;
            if (ws == Node.SIGNAL) {
                if (!compareAndSetWaitStatus(h, Node.SIGNAL, 0))
                    continue;
                unparkSuccessor(h);//唤醒后继
            }
            else if (ws == 0 &&
                     !compareAndSetWaitStatus(h, 0, Node.PROPAGATE))
                continue;
        }
        if (h == head)// head发生变化
            break;
    }
}
```



自定义同步器实现独占

```java
public class DefinedSyn {


//    自定义实现一个独占锁
    private static class Syn extends AbstractQueuedSynchronizer{

        //获取资源
        @Override
        protected boolean tryAcquire(int arg){
            //期望state == 0 ，获取锁后，将state设置成1
            return compareAndSetState(0,1);
        }

        //释放资源
        @Override
        protected boolean tryRelease(int arg) {
            //将state状态设置为0，表示其他线程可以请求资源
            setState(0);
            return true;
        }

        //当前线程是否独占资源
        @Override
        protected boolean isHeldExclusively(){
            return getState() == 1;
        }

    }

    private Syn syn = new Syn();

    //加锁
    public void lock(){
        syn.acquire(1);
    }

    //解锁
    public void unlock(){
        syn.release(1);
    }

    public boolean isLock(){
       return syn.isHeldExclusively();
    }


}
```

测试

```java
public class Test {

    static int count =0;
    static DefinedSyn definedSyn = new DefinedSyn();

    public static void main(String[] args) throws InterruptedException {
        for (int i = 0; i <5 ; i++) {
            new Thread(new Runnable() {
                @Override
                public void run() {
                    try {
                        definedSyn.lock();
                        if (definedSyn.isLock()){
                            System.out.println("已经获取当前资源并且独占");
                        }
                        System.out.println("当前线程："+Thread.currentThread().getName());
                        count++;
                    } catch (Exception e) {
                        e.printStackTrace();
                    }finally {
                        definedSyn.unlock();
                        if (!definedSyn.isLock()){
                            System.out.println("已经释放当前资源");
                        }
                    }
                }
            }).start();
        }

        Thread.sleep(5000);
        System.out.println(count);
    }
}

/*
已经获取当前资源并且独占
当前线程：Thread-3
已经释放当前资源
已经获取当前资源并且独占
当前线程：Thread-2
已经释放当前资源
已经获取当前资源并且独占
当前线程：Thread-0
已经释放当前资源
已经获取当前资源并且独占
当前线程：Thread-1
已经释放当前资源
已经获取当前资源并且独占
当前线程：Thread-4
已经释放当前资源
5
*/
```

