Java基础知识

## Java思维导图(借鉴)

![image-20210407165423891](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210407165423891.png)



<img src="https://img-blog.csdn.net/20141128150157417" style="zoom:150%;" />

## 基础知识部分

对象在JVM中的存储

##### JVM（虚拟机）

![image-20210407145303591](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210407145303591.png)

perObject----->引用地址存放在JVM中的堆中，指向存放在JVM栈中的对象。

new Person()----->对象存放在JVM中的栈中。

访问对象时，不能直接访问。

![image-20210407150314733](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210407150314733.png)

JVM堆中可以有多个引用变量地址指向同一个栈中的对象。（句柄）



##### 静态方法

静态方法属于类，不属于对象。

通过类名. 直接调用，使用关键字:static

this关键字不允许出现在静态方法中，静态方法中不能直接访问实列属性和方法。



![image-20210407162017168](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210407162017168.png)

继承中上转型对象不能访问子类中新添加的属性和方法，可以访问继承类(父类)的默认情况下的属性和方法。。

上转型对象可以在需要的时候通过强制类型转换成子类。



##### 继承中子类重写父类方法

条件:

![image-20210407162840878](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210407162840878.png)

![image-20210407162914273](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210407162914273.png)



##### 抽象类

特点:

![image-20210407173031721](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210407173031721.png)

![image-20210407174351707](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210407174351707.png)



##### 适配器

实现一个非抽象子类选择性的实现抽象父类的方法

![image-20210407175748793](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210407175748793.png)



##### 对象运行时多态

![image-20210407180217491](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210407180217491.png)





##### 接口

一个普通类可以是实现多个接口，接口与接口之间是可以继承的。

特征：

![image-20210407182647036](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210407182647036.png)

接口回调含义：根据接口实现类来体现接口中抽象方法的具体实现过程并进行调用。

接口继承

![image-20210407185150749](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210407185150749.png)





##### java内部类

- 内部类的作用

  ![image-20210408154351639](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210408154351639.png)

- 内部类的定义和创建

  ![image-20210408154736015](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210408154736015.png)

  ![image-20210408154952538](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210408154952538.png)

- 局部类

  只存在于局部中的类，类似于局部变量

- 匿名类对象

  ![image-20210408162054995](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210408162054995.png)

  

##### 静态块 （属于类）

与对象无关，随着类的加载而加载

![image-20210408163937939](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210408163937939.png)

 

```
不允许调用非静态方法和非静态字段
如果静态块中定义了局部对象，此局部对象是可以调用非静态方法
可以定义局部类，不允许定义接口
```

加载过程

![image-20210408171623539](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210408171623539.png)



#### JAVA常用类库

##### Object类

所有类的父类

toString方法

 ![image-20210408181457823](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210408181457823.png)

equals方法

![image-20210408182817640](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210408182817640.png)

![image-20210408182855581](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210408182855581.png)



getClass方法

![image-20210408183830812](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210408183830812.png)

class-->关键字   		Class-->java se中提供的**字节码类型文件**

 字节码文件在运行时被JVM加载到内存中并且创建Class对象，所有此类产生的对象共享一个Class(字节码对象),不能够被创建。



hashCode方法

![image-20210408185318735](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210408185318735.png)

JVM也规定一个对象在不同时期运行hashCode可以不返回相同值，大多数情况下，也该保持同一个对象中哈希表中哈希码值返回相同的int。



clone方法

![image-20210408190523942](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210408190523942.png)



##### Integer包装类

![image-20210410092729845](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210410092729845.png)

作用

![image-20210410092823733](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210410092823733.png)

![image-20210410093925543](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210410093925543.png)

![image-20210410094152179](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210410094152179.png)

![image-20210410094630265](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210410094630265.png)

![image-20210410095035428](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210410095035428.png)

parseInt方法重载

![image-20210410095417953](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210410095417953.png)

![image-20210410100346868](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210410100346868.png)

```java
 //toBinaryString
        String stringSwitch =IntegerTest.fromIntegerToStringBinary(10,2);
        String stringSwitch1 =IntegerTest.fromIntegerToStringBinary(10,8);
        String stringSwitch2 =IntegerTest.fromIntegerToStringBinary(10,16);
        System.out.println(stringSwitch);
        System.out.println(stringSwitch1);
        System.out.println(stringSwitch2);
```



![image-20210410102622876](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210410102622876.png)



```java
  //valueOf()
        String num = "123";
  System.out.println(Integer.valueOf(num).intValue());
        String num1 = "10101010";
        System.out.println(Integer.valueOf(num1,2));
        System.out.println(Integer.valueOf(num1,8));
        System.out.println(Integer.valueOf(num1,16));
```



toString 方法

```java
 //toString 方法
        Integer num2 = 2233;
        System.out.println(num2.toString());
        //静态toString重载方法
        System.out.println(Integer.toString(10));
        System.out.println(Integer.toString(num2,2));
        System.out.println(num2.toString().length());
```



##### Character包装类

![image-20210410104918097](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210410104918097.png)



![image-20210410104945903](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210410104945903.png)

![image-20210410105506914](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210410105506914.png)

![image-20210410110151598](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210410110151598.png)

```java
  char[] passwordArr ={'T','5','.','6','a','6','h','O',};
        CharacterTest.validatePassword(passwordArr);
        
     /**
     * 统计密码中多少大写字母、小写字母、字符、数字的个数
     * @param pwd
     */
    public static void validatePassword(char[] pwd){
        int num = 0;
        int capitalTheLetter = 0;
        int lowercaseTheLetter = 0;
        int characters = 0;

        for (int i = 0; i <pwd.length ; i++) {
            if (!Character.isLetterOrDigit( pwd[i])){
                characters++;
            }
            if (Character.isDigit(pwd[i])){
                num++;
            }
            if (Character.isUpperCase(pwd[i])){
                capitalTheLetter++;
            }
            if (Character.isLowerCase(pwd[i])){
                lowercaseTheLetter++;
            }
        }

        System.out.println("数字数量"+num);
        System.out.println("字符数量"+characters);
        System.out.println("大写字母数量"+capitalTheLetter);
        System.out.println("小写字母数量"+lowercaseTheLetter);

    }
```

![image-20210410132202788](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210410132202788.png)



##### System系统类  

 映射jvm

类概述

![image-20210410133306465](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210410133306465.png)

实用方法

![image-20210410133527143](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210410133527143.png)

![image-20210410133624583](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210410133624583.png)

![image-20210410135336180](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210410135336180.png)

##### Math计算类

![image-20210410140451035](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210410140451035.png)

![image-20210410140440613](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210410140440613.png)

![image-20210410140511176](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210410140511176.png)



##### String类

![image-20210410141553218](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210410141553218.png)

概述

![image-20210410141631525](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210410141631525.png)

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210410141659371.png" alt="image-20210410141659371" style="zoom:200%;" />

![image-20210410142610160](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210410142610160.png)

```java
  //charAt 方法
        String name = "奥菲利亚.大流士";
        char res  = name.charAt(2);
        System.out.println(res);

        //compareTo 方法
        String a = "abcd";
        String b = "abcde";
        System.out.println(a.compareTo(b));

        //endWith  方法  测试某个字符串正则表达式所描述的为开头或结尾的方法
        String email = new String("abc@123.com");
        System.out.println(email+" 是否以.com为结尾的"+(email.endsWith(".com")));
```



![image-20210410143827367](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210410143827367.png)

```java
//去掉空格的trim方法
        String hero = " 你是英雄吗 ";
        System.out.println(hero.length());
        System.out.println(hero.trim().length());

        //indexOf 查找目标字符或字符串
        int index = email.indexOf("@");
        System.out.println(index);
```

![image-20210410145933893](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210410145933893.png)

```java
        //字符串分割方法 split
        String splitString = "易大师,薇恩,恕瑞玛";
        String[] newSplitString = splitString.split(",");
        for (int i = 0; i <newSplitString.length ; i++) {
            System.out.println(newSplitString[i]);
        }

        //提取字符串  substring方法，提取的开始位置必须不超出原串的位置
        //提取字符串结束索引的位置的字符被忽略(舍弃),结束位置必须不超出原串的位置
        String string1 = "我是Chinese";
        System.out.println(string1.substring(2));

        //将字符串转换成char型数组的toCharArray
        char[] chars = splitString.toCharArray();
        System.out.println(chars.length == splitString.length());
        for (int i = 0; i <chars.length ; i++) {
            System.out.println(chars[i]);
        }
        //大小写转换
        System.out.println("abcdfe".toUpperCase());
        System.out.println("AJDBDS".toLowerCase());
```

![image-20210410151721154](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210410151721154.png)

```java
 //字符串替换方法
        String color = "red";
        System.out.println(color.replace('r','['));
        System.out.println(color.replace("red","blue"));

        //静态方式构建字符串
        String dest1 = String.valueOf(new Employee());

        System.out.println(dest1);
```



##### StringBuilder类

可以修改自身字符序列

**StringBuilder和StringBuffer的区别**

![image-20210410153533078](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210410153533078.png)

![image-20210410153735688](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210410153735688.png)

![image-20210410155312410](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210410155312410.png)

```java
public class StringBuilderTestTest {

    @Test
    public void createStringBuilder() {
        StringBuilder builder = new StringBuilder("我是大哥大");
        System.out.println(builder.toString());
        System.out.println("长度"+builder.length());
        System.out.println("默认容量"+builder.capacity());
    }

    @Test
    public void testAppendMethod(){
        StringBuilder builder = new StringBuilder("贡巴瓦");
        builder.append("123");
        System.out.println(builder);
    }

    @Test
    public void testDeleteMethod(){
        String str  =StringBuilderManagement.removeStringFromStartToEnd("东风不与周郎便,铜雀春深锁二乔",2,8);
        System.out.println(str);
    }

    @Test
    public void testReplaceMethod(){
        String str  = "{name =\"king\", address = \"人民大街\",age = 12, email = \"java@163.com\"}";
        System.out.println(StringBuilderManagement.replaceStringFromStartToEnd(str,":"));
    }

    @Test
    public void testInsertMethod(){
        String str  = "{name =\"king\", address = \"人民大街\",age:, email = \"java@163.com\"}";
        System.out.println(StringBuilderManagement.insertObject(str,"age:,","12"));
    }
}



/**
*StringBuilder类的方法实现
**/
public class StringBuilderManagement {

    //delete
    public static String removeStringFromStartToEnd(String str,int start,int end){
        StringBuilder builder =new StringBuilder(str);
        builder.delete(start,end);
        return builder.toString();

    }
    
    //replace
    public static String  replaceStringFromStartToEnd(String str,String replace){
        StringBuilder builder =new StringBuilder(str);
        if ( builder.toString().contains("=")){
            builder.replace(builder.indexOf("="),builder.indexOf("=")+1,replace);
            return replaceStringFromStartToEnd(builder.toString(),replace);
        }
        return builder.toString();

    }

    //insert
    public static String  insertObject(String str,String target,String insertObj){
        StringBuilder builder =new StringBuilder(str);
        if (builder.toString().contains(target)){
            builder.insert(builder.indexOf(target)+4,insertObj);
            return insertObject(builder.toString(),target,insertObj);
        }
        return builder.toString();

    }
}
```





##### Date类

![image-20210412121658248](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210412121658248.png)

![image-20210412121845245](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210412121845245.png)

![image-20210412122733098](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210412122733098.png)

```java
public class DateTest {
    public static void main(String[] args) {
        Employee employee = new Employee("1",new Date(System.currentTimeMillis() -1000));
        Employee employee1 = new Employee("2",new Date(System.currentTimeMillis() - 100));
        System.out.println(eqEmpAge(employee,employee1));

    }

    private static String eqEmpAge(Employee employee, Employee employee1) {
        return employee.getDateTime().before(employee1.getDateTime())? "1": "2" ;
                return employee.getDateTime().after(employee1.getDateTime())? "1": "2" ;

    }


}
```

```java
 Date date = new Date(100000);
        int tag = -1;
        int num = 1;
        System.out.println(new DateTest().changeDateStatus(date,num,tag).getTime());
        System.out.println(date.getTime());



 /**
     * desc  对给定的date对象实现时间的运算，如果tag > 0 则date增加num毫秒，如果tag < 0 则date减少num毫秒
     * @param date
     * @param num
     * @param tag
     * @return
     */
    public Date changeDateStatus(Date date,long num, int tag){
        if (tag > 0 ){
            date.setTime(date.getTime() + num);
        }else{
            date.setTime(date.getTime() - num);
        }

        return date;
    }
```

##### DateFormat类

![image-20210412130530308](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210412130530308.png)

```java
   //利用DateFormat 实现对Date对象的格式化输出
        Date d0 = new Date();
        //以默认的日期方式
        DateFormat dateFormatClass = DateFormat.getDateInstance();
        System.out.println(dateFormatClass.format(d0));

        //使用给定的格式化构建DateFormat
        DateFormat dateFormatClass1 = DateFormat.getDateInstance(DateFormat.FULL);
        System.out.println(dateFormatClass1.format(d0));
```



##### SimpleDateFormate类

![image-20210412181131183](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210412181131183.png)

```java
   Date d0 = new Date();
        //默认格式
        SimpleDateFormat simpleDateFormat = new SimpleDateFormat();
        System.out.println(simpleDateFormat.format(d0));

        //给定格式
        SimpleDateFormat simpleDateFormat1 = new SimpleDateFormat("yyyy-MM-dd : HH:mm:ss a", Locale.US);
        System.out.println(simpleDateFormat1.format(d0));
```



![image-20210412182626384](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210412182626384.png)

![image-20210412182803072](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210412182803072.png)

![image-20210412183347300](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210412183347300.png)

```java
public class SimpleDateFormatClass {

     final static String  TYPE1 = "yyyy-MM-dd:HH:mm:ss";
     final static String  TYPE2 = "yyyy-MM-dd";
     final static String  TYPE3 = "  HH:mm:ss";
     final static String  TYPE4 = "G yyyy : HH:mm:ss S a";


    //格式化Date对象转换成字符串方法
     static void change(Date date,String type1){
        SimpleDateFormat simpleDateFormat = new SimpleDateFormat(type1);
        System.out.println(simpleDateFormat.format(date));
    }

    //格式化字符串转换成Date对象
     static void changeStringToObject(String str,String type1) throws ParseException {
         Date date = null;
         SimpleDateFormat simpleDateFormat = new SimpleDateFormat(type1);
         date = simpleDateFormat.parse(str);
         System.out.println(date.toLocaleString());
     }
}
```



##### Calendar类

![image-20210412190450145](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210412190450145.png)

![image-20210412190820699](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210412190820699.png)

![image-20210412192135010](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210412192135010.png)

![image-20210412192246802](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210412192246802.png)

![image-20210412192317864](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210412192317864.png)

![image-20210412192446994](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210412192446994.png)

![image-20210412192732171](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210412192732171.png)



##### List接口

List接口和实现类

List接口规范

ArrayList集合类应用（数组链表）

Vector集合类应用(向量)  **多用于多线程**



![image-20210414135137831](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210414135137831.png)

List接口下常用方法

![image-20210414135529197](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210414135529197.png)

![image-20210414140243627](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210414140243627.png)

Vector 、ArrayList是List接口的实现类

ArrayList是非线程安全



![image-20210414151928770](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210414151928770.png)



##### Set接口

Set接口和实现类

![image-20210414155446120](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210414155446120.png)

TreeSet(红黑树)

![image-20210414155506439](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210414155506439.png)

![image-20210414155841509](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210414155841509.png)

![image-20210414155949531](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210414155949531.png)





hashSet

![image-20210414160216544](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210414160216544.png)



 TreeSet

![image-20210414164840662](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210414164840662.png)

![image-20210414165402962](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210414165402962.png)

 



LinkedHashSet集合

![image-20210414174526253](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210414174526253.png)

```java
    public static void main(String[] args) {
        IEmployee iEmployee = new IEmplyoeeImp();
        Set empSet = iEmployee.loadAllEmployee();
        //获取Set接口的迭代器实现对集合元素的遍历
        Iterator iterator = empSet.iterator();

        while (iterator.hasNext()){
            Employee employee = (Employee) iterator.next();
            System.out.println("id: "+employee.getId());
            System.out.println("name: "+employee.getName());
            System.out.println("birth: "+new SimpleDateFormat("yyy-MM-dd").format(employee.getBirth()));
            System.out.println("entryDate: "+new SimpleDateFormat("yyy-MM-dd").format(employee.getEntryDate()));
            System.out.println("phoneNumber: "+employee.getPhoneNumber());
        }

        int capicaty = 5;
        Set set = new HashSet(capicaty,20);
        String name = "king";
        String name1 = name;
        set.add(name);
        set.add(name1);
        System.out.println(set.size());
        for (Object o : set) {
            System.out.println(o);
        }


        //默认是按照自然顺序(升序)排序
        TreeSet treeSet = new TreeSet();
        treeSet.add(Integer.valueOf(394));
        treeSet.add(Integer.valueOf(1));
        treeSet.add(Integer.valueOf(2));
        treeSet.add(Integer.valueOf(10000));
        treeSet.add(Integer.valueOf(200));

        for (Object num: treeSet) {
            System.out.println(num);
        }

        //获取迭代器降序排序
        Iterator it =  treeSet.descendingIterator();
        while (it.hasNext()){
            System.out.println(it.next());
        }

        //取出第一个元素
        System.out.println(treeSet.first());

        //取出最后一个元素
        System.out.println(treeSet.last());

        //TreeSet自定义排序
       TreeSet treeSet1 =   iEmployee.loadAllEmployeeSortByBirth();
        for (Object num: treeSet1) {
            Employee employee = (Employee) num;
            System.out.println("birth: "+new SimpleDateFormat("yyy-MM-dd").format(employee.getBirth()));
            System.out.println("id: "+employee.getId());
            System.out.println("name: "+employee.getName());
            System.out.println("entryDate: "+new SimpleDateFormat("yyy-MM-dd").format(employee.getEntryDate()));
            System.out.println("phoneNumber: "+employee.getPhoneNumber());
        }


        //LinkedHashSet
        //拥有Set不重复以及Linked顺序结构
        LinkedHashSet linkedHashSet = new LinkedHashSet();
        linkedHashSet.add(1);
        linkedHashSet.add(2);
        linkedHashSet.add(3);
        linkedHashSet.add(4);
        linkedHashSet.add(4);
        for (Object o:linkedHashSet) {
            System.out.println(o);
        }

    }

```







##### Map接口

Map接口规范

HashMap集合类应用

HashTable集合类应用

TreeMap集合类应用

![image-20210418090835144](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210418090835144.png)

![image-20210418091351219](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210418091351219.png)

![image-20210418091951982](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210418091951982.png)



HashMap

![image-20210418092238094](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210418092238094.png)

![image-20210418092438158](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210418092438158.png)

```java
   		//keySet 得到Map中所有的键
        Set key = map.keySet();

        //values 得到Map中所有的值
        Collection cl  = map.values();
        
        //获取键值对集合
        Set kenAndValue = map.entrySet();
        System.out.println(kenAndValue);
```





HashTable

![image-20210418101442360](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210418101442360.png)

```java
        //hashtable不允许键值对为空
//        map1.put(null,"king");
//        map1.put("king",null);

//        map1.put(null,null);
```



TreeMap

![image-20210418101955186](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210418101955186.png)



#### JAVA异常处理机制

##### 异常处理

![image-20210418103121053](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210418103121053.png)

**java异常组织结构**

**定义方法中声明和抛出异常**

**异常的捕获和处理**

**1.7版本异常新特性**

**自定义异常**



![image-20210418103834275](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210418103834275.png)







**Throwable是JAVA异常继承机构中的顶级父类**

![image-20210418104621695](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210418104621695.png)

Exception:分为运行时异常、非运行时异常(编译异常)

Error(致命错误):分为虚拟机错误、IO错误



![image-20210418105252006](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210418105252006.png)

throw:抛出、抛掷  异常对象

throws：定义异常类型(基本上时编译时异常)







![image-20210418110359160](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210418110359160.png)

![image-20210418115124256](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210418115124256.png)

一个子类的异常永远可以被它的父类处理

```java
    public void saveFileToTarget()  {
        FileManagement fileManagement = new FileManagement();
        File  file = new File("c:\\file\\test");
        try {
            fileManagement.saveFileToTarget(file,"wer");
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (SQLException e) {
            e.printStackTrace();
        }finally {//此处释放异常出现前被占用的系统资源对象

        }
    }

```



自定义异常

![image-20210418132752044](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210418132752044.png)

```java
public static void main(String[] args) {
        interfaceClass.Employee employee = new interfaceClass.Employee();
        typeManagment typeManagment = new typeManagment();
        try {
            typeManagment.manageType(employee);
        } catch (customException e) {
            e.printStackTrace();
        }
    }
    

    public void manageType(Object obj) throws customException{
        if (!(obj instanceof Employee)) {
            throw new  customException("对象类型不符合Employee");

        }
        System.out.println("处理成功");

    }
```



##### IO流

###### File类

![image-20210418134600518](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210418134600518.png)

![image-20210418134914388](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210418134914388.png)

```java
    public static  void main(String[] args){
        /*不同File构造器的实用特点*/
        /*构建File对象时，无论文件是否真实存在file对象都不是null*/
        File  file = new File("D:\\files\\zhanghHui.txt");

        /*作为文件的父路径*/
        File dir = null;
        File file1 = new File(dir,"D:\\files\\zhanghHui.txt");


        try {
            /*URI作为构建File对象的参数必须保证其字符串描述前缀(资源格式)为file*/
            /*用'/'反斜杠来连接路径*/
            URI uri = new URI("file:/123");

            File file2 = new File(uri);
        } catch (URISyntaxException e) {
            e.printStackTrace();
        }
    }

```



![image-20210418141410251](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210418141410251.png)

```java
public class fileSupport {

    /**
     * 根据给定路径创建File对象
     * @param filePath
     * @return
     */
    public static File createFile(String filePath){
        return  new File(filePath);
    }

    /**
     * 打印显示目标文件file的相关信息
     * @param file
     */
    public static void displayFileInfo(File file) throws IOException {
        System.out.println(file.canRead() ? "此文件能够被读取":"此文件不能被读取");
        System.out.println(file.canWrite() ? "此文件能够写入":"此文件是只读");
        System.out.println(file.exists() ? "此文件存在":"此文件不存在");
        System.out.println(file.createNewFile() ? "文件创建成功":"文件创建失败");

    }
}

```

![image-20210418142931751](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210418142931751.png)

```java
 public static void displayFileMessage(File file) throws IOException {
        System.out.println("文件绝对路径"+file.getAbsolutePath());
        System.out.println("文件名称"+file.getName());
        System.out.println("文件路径"+file.getPath());
        System.out.println("文件父路径"+file.getParent());
        System.out.println(file.isFile() ? "此文件是具体文件":"此文件是目录");
        System.out.println(file.isDirectory() ? "此文件是目录":"此文件是具体文件");
    }
```



![image-20210418143741885](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210418143741885.png)

File:不只是表示文件也可以表示目录

listFiles方法只对目录起作用，此方法返回当前目录下的文件或者是子目录数量

**mkdir和mkdirs的不同**

使用mkdir创建文件，成功的条件：给定的路径中的所有的父路径都存在

使用mkdirs创建文件，无论当前给定的路径中父路径是否存在（首先创建依赖的父目录），它都能够创建成功(前提：能够用权限访问)

###### 文件流分类

![image-20210419181244697](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210419181244697.png)

**节点流**:针对某一个具体的文件直接建立

**处理流**：和其他流对接，不是直接指向具体的文件





###### 输入流

![image-20210419181835882](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210419181835882.png)



字节输入流

![image-20210419182225729](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210419182225729.png)

![image-20210419182949552](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210419182949552.png)

```java
    public static void testReadStoreToByteArray3(String filePath){
        File file = new File(filePath);
        InputStream  inputStream = null;
        if (file.exists()){
            try {
                /*以二进制形式读取文件*/
                inputStream = new FileInputStream(file);
                //作为读取字节数据的临时缓存区
                byte[] bytes = new byte[6];
                //记录实际读取并填充缓冲区的实际字节数
                int count = 0 ;
                /*读取二进制文件范围(0-----bytes.length)*/
                while ((count = inputStream.read(bytes,0,bytes.length))!= -1){
                    String string = new String(bytes,0,count);
                    System.out.print(string);
                }
            } catch (IOException e) {
                e.printStackTrace();
            } finally{
                try {
                    inputStream.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }

```





文件上传下载------->BufferedInputStream(文件过大、使用它效率高)

```java
    /**
     * 利用二进制缓冲输入流读取文件（较大文件）
     * @param file
     * @return
     */
    public static long useBufferedInputStream(File file){
        long fileSize = 0;
        if (file.exists()){
            InputStream inputStream = null;
            BufferedInputStream bufferedInputStream = null;
            try {
                /*建立基于普通文件的二进制输入流*/
                inputStream = new FileInputStream(file);
                /*基于二进制输入流建立的缓冲流*/
                bufferedInputStream = new BufferedInputStream(inputStream);
                /*临时缓存区*/
                byte[] bytes = new byte[1024*10];
                int count = 0;
                while ((count = bufferedInputStream.read(bytes,0,bytes.length)) != -1){
                    fileSize += count;
                }
            } catch (FileNotFoundException e) {
                e.printStackTrace();
            } catch (IOException e) {
                e.printStackTrace();
            }finally {
                try {
                    bufferedInputStream.close();
                    inputStream.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }

        return fileSize;
    }

```





字符输入流

![image-20210419193010273](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210419193010273.png)

![image-20210419193721928](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210419193721928.png)

```JAVA
    /**
     * 字符流
     * 使用文本流读取文本文件
     * @param file
     */
    public static void useCharInputStream(File file){
        if (file.exists()){
            Reader reader = null;
            try {
                reader = new FileReader(file);
                /*文本缓存区*/
                char[] chars = new char[124];
                int count =0;
                while ((count = reader.read(chars,0,chars.length)) != -1){
                    System.out.println(new String(chars,0,count));
                }
            } catch (FileNotFoundException e) {
                e.printStackTrace();
            } catch (IOException e) {
                e.printStackTrace();
            } finally {
                try {
                    reader.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }

```



BufferedReader可以实现**按行读取**

```java
    /**
     *
     * @param userFile 存储用户信息的文本文件
     * @return用户列表
     */
    public static List<User> readUserInformationFile(File userFile){
        List<User> userList = new ArrayList<>();
        if (userFile.exists()){
            Reader reader = null;
            BufferedReader bufferedReader = null;

            try {
                reader = new FileReader(userFile);
                bufferedReader = new BufferedReader(reader);

                String lineString = "";
                while ((lineString = bufferedReader.readLine()) != null && !lineString.equals("")){
                    User user = new User();
                    String[] userInfo = lineString.split(" ");user.setBirth(new String(userInfo[3].getBytes(),"UTF-8"));
                    user.setId(userInfo[0]);
                    user.setName(userInfo[1]);
                    user.setSex(userInfo[2]);
                    user.setBirth(userInfo[3]);
                    userList.add(user);
                }
            } catch (FileNotFoundException e) {
                e.printStackTrace();
            } catch (IOException e) {
                e.printStackTrace();
            } finally {
                try {
                    reader.close();
                    bufferedReader.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }

        return userList;
    }
```



###### 输出流

字符输出流

![image-20210420183519956](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210420183519956.png)

```java
    /**
     *字符流输出
     * @param source
     * @param target
     * @return
     */
    public static long copyTextFile(File source, File target){
       long length = 0;
       if (!target.exists()){
           target.mkdirs();
       }


        Reader reader = null;
        BufferedReader bufferedReader = null;

        Writer writer = null;
        BufferedWriter bufferedWriter = null;

        try {
            reader = new FileReader(source);
            bufferedReader = new BufferedReader(reader);

            writer = new FileWriter(target);
            bufferedWriter = new BufferedWriter(writer);

            char[] chars = new char[1024*10];
            int count = 0;
            while ((count = bufferedReader.read(chars,0,chars.length)) != -1){
                bufferedWriter.write(chars,0,count);
                System.out.println("正在拷贝");
                length +=count;
            }


        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }finally {
            try {
                bufferedWriter.close();
                writer.close();
                bufferedReader.close();
                reader.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }

       return length;
    }

```







字节流输出

```java
    /**
     * 将用户给定的content内容以文件file形式进行保存在文件中
     * @param content
     * @param target
     * 字节流输出
     */
    public static void saveContentToFile(String content,File target){
        if (target.exists()){
            //将content内容放入成字节数组
            byte[] bytes = content.getBytes();
            OutputStream outputStream = null;

            try {
                outputStream = new FileOutputStream(target);
                /*将内容写入到目标文件*/
                outputStream.write(bytes);
            } catch (FileNotFoundException e) {
                e.printStackTrace();
            } catch (IOException e) {
                e.printStackTrace();
            } finally {
                try {
                    outputStream.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
            }
        }

```



小结:

1. File 是唯一表示硬盘文件或者目录的类型

   通过方法判断目录File对象是文件还是目录

2. 文件的读写操作

   流的分类

   - 按照方向:输入（读取）和输出（写入）

   - 按照处理数据方式：字节流和字符流

   - 流的功能：基于目标文件建立的普通节点流和基于某节点流建立处理

     

   - 读写文件过程

     建立目标文件

     基于目标文件建立文件流

     进行读写操作

     关闭相关文件流对象，释放资源（要注意文件的读写操作异常处理）

###### 序列化

![image-20210420185840298](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210420185840298.png)



序列化对象定义

![image-20210420190109641](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210420190109641.png)



序列化文件流

输出：序列化

读取：反序列化

![image-20210420190624464](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210420190624464.png)

```java
    /**
     * 序列化对象到目标文件中
     * @param userList
     * @param target
     */
    public static void serializableJavaObjectOutput(List<user> userList, File target){
        if (target.exists()){
            OutputStream outputStream = null;
            //序列化输出流
            ObjectOutputStream objectOutputStream = null;

            try {
                outputStream = new FileOutputStream(target);
                objectOutputStream = new ObjectOutputStream(outputStream);

                for (int i = 0; i <userList.size() ; i++) {
                    objectOutputStream.writeObject(userList.get(i));
                }

            } catch (FileNotFoundException e) {
                e.printStackTrace();
            } catch (IOException e) {
                e.printStackTrace();
            }finally {
                try {
                    outputStream.close();
                    objectOutputStream.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}
```



反序列化

```java
    /**
     * 反序列操作读取目标file中的对象
     * @param target
     */
    public static List<user> deserReader(File target){
        List<user> userList = new ArrayList<>();

        if (target.exists()){
            InputStream inputStream = null;
            //反序列化输入
            ObjectInputStream objectInputStream = null;

            try {
                inputStream = new FileInputStream(target);
                objectInputStream = new ObjectInputStream(inputStream);
                Object obj = null;
                while ((obj  = objectInputStream.readObject()) != null){
                    if (obj instanceof user){
                        user user = (user) obj;
                        userList.add(user);
                    }
                }
            } catch (FileNotFoundException e) {
                e.printStackTrace();
            } catch (IOException e) {
                e.printStackTrace();
            } catch (ClassNotFoundException e) {
                e.printStackTrace();
            } finally {
                try {
                    objectInputStream.close();
                    inputStream.close();
                }catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }

        return userList;
    }

```



##### 多线程



###### **进程和线程的概念**

![image-20210420200037156](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210420200037156.png)



###### 多线程应用

![image-20210421180450107](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210421180450107.png)





###### **Java多线程概念**

![image-20210421180832495](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210421180832495.png)

###### 多线程结构

![](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210421181430541.png)



###### 线程组件

![image-20210421182241851](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210421182241851.png)



![image-20210421182556068](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210421182556068.png)

Thread和TimerTask都是实现Runnable接口的实现类

Thread是普通类

TimerTask是一个抽象类



###### **Thread线程类及常用方法**

![image-20210421183205312](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210421183205312.png)

![image-20210421184156839](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210421184156839.png)



###### **Runnable线程接口**

![image-20210421184414512](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210421184414512.png)

![image-20210421184600275](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210421184600275.png)

![image-20210421184657572](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210421184657572.png)



###### Thread常用构造器

![image-20210421184729420](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210421184729420.png)



```java
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



###### 线程的生命周期

![image-20210421190345724](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210421190345724.png)



###### 线程启动和优先级

![image-20210421193634849](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210421193634849.png)



###### 线程状态

![image-20210421194744185](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210421194744185.png)



###### 线程的阻塞和处理

![image-20210421201352178](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210421201352178.png)



###### 线程阻塞的原因

![image-20210421201815713](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210421201815713.png)



###### 线程休眠和唤醒

![image-20210421202256368](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210421202256368.png)

```java
/**
 * 农民和地主
 */
public class LadnlordAndFarmerRunnable implements Runnable {
    //地主线程
    private Thread landlord;
    //农名
    private Thread farmer;

    public Thread getLandlord() {
        return landlord;
    }

    public void setLandlord(Thread landlord) {
        this.landlord = landlord;
    }

    public Thread getFarmer() {
        return farmer;
    }

    public void setFarmer(Thread farmer) {
        this.farmer = farmer;
    }

    private List<Integer> list  = new ArrayList<>();


    @Override
    public void run() {
        //当前线程是农名
        if (Thread.currentThread() == farmer){
            for (int i = 0; i < 1000 ; i++) {
                list.add((int) (Math.random()*1000));
                try {
                    if (list.size() % 100 == 0){
                        Thread.sleep(20000);
                    }
                } catch (InterruptedException e) {
                    System.out.println("农民没有休息到20s就又开始干活");
                    e.printStackTrace();
                }
            }
        }

        //当前线程是地主
        if (Thread.currentThread() == landlord){
            while (true){
                //发现农民休息了就开始催促工作
                if (farmer.getState() == Thread.State.TIMED_WAITING){
                    System.out.println("干活！！！！");
                    //调用线程的interrupt方法，中断sleep
                    farmer.interrupt();
                }
            }
        }

        System.out.println("工作完毕");
        System.out.println(Arrays.toString(list.toArray()));
    }
}
```



###### 线程联合

![image-20210422181503958](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210422181503958.png)

![image-20210422182217205](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210422182217205.png)

​	![image-20210422182652278](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210422182652278.png)



###### 守护线程

![image-20210424134825678](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210424134825678.png)



###### 线程之间的通信(线程安全)

![image-20210422191320453](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210422191320453.png)

synchronized(线程锁)

![image-20210422191928179](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210422191928179.png)

```java
public class SyncDataSupport  {

    private List<Integer> list = new ArrayList<>();

    private Vector<Integer> vector = new Vector<>();

    public void addData(){

        for (int i = 1; i <= 10000 ; i++) {
            //List不是线程安全的
            /*使用synchronized 同步代码块处理线程同步数据访问的安全问题*/
            synchronized (list){
                list.add(i);
            }
            //Vector是线程安全的
//            vector.add(i);
        }
    }

    public Vector<Integer> getVector() {
        return vector;
    }

    public List<Integer> getList() {
        return list;
    }
}
```

![image-20210422194124627](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210422194124627.png)



实现线程安全

**Synchronized作用**

![image-20210422192848867](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210422192848867.png)



**Lock(锁)**

![image-20210422193914096](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210422193914096.png)

![image-20210422194421088](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210422194421088.png)



JVM对锁的管理

![image-20210422195037122](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210422195037122.png)



一个线程在拥有了锁之后，其他线程只能够等待，如何等待，怎么等待，后续的线程如何获取锁，需要一个能够协调这一切的功能。

**Monitor(监视器)** ----->在锁的基础上建立一个管理机制

房子房间模型

![image-20210422201018788](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210422201018788.png)

![image-20210422201709357](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210422201709357.png)



###### 同步代码块

![image-20210424093005210](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210424093005210.png)

```java
    public static void main(String[] args) {
        SynchronizedRunnable synchronizedRunnable = new SynchronizedRunnable();

        Thread thread = new Thread(synchronizedRunnable,"one");
        Thread thread1 = new Thread(synchronizedRunnable,"two");
        thread.setPriority(Thread.MAX_PRIORITY);

        thread.start();

        thread1.start();
    }

public class SynchronizedRunnable implements Runnable {

    private List<String> stringList = new ArrayList<>();

    public List<String> getStringList() {
        return stringList;
    }

    public void setStringList(List<String> stringList) {
        this.stringList = stringList;
    }

    @Override
    public void run() {
        System.out.println("当前持有监视器线程对象"+Thread.currentThread().getName());

        synchronized (stringList){

            for (int i = 0; i < 100 ; i++) {
                System.out.println("当前持有监视器线程对象"+Thread.currentThread().getName());
                if (i == 20){
                    delete();//调用另一个同步方法（重入的概念）
                }

                stringList.add("字符串"+i);
                try {
                    Thread.sleep(100);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }

    }


    public synchronized void delete(){
        for (int i = 0; i < stringList.size() ; i++) {
            System.out.println("当前线程"+Thread.currentThread().getName()+"正在删除");
        }
    }
}
```



###### 重入

概念

![image-20210424100154624](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210424100154624.png)

![image-20210424100204075](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210424100204075.png)

重入是独享的，只有当前 获取监视器（持有锁）的线程才能连续重入（自动获取锁），不必等待释放，等待释放，就会造成死锁。



###### 同步当前对象（this）

![image-20210424101429927](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210424101429927.png)

![image-20210424101813972](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210424101813972.png)



###### 同步方法

![image-20210424104910401](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210424104910401.png)

![image-20210424105243555](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210424105243555.png)



###### 同步线程的等待和唤醒

![image-20210424124438051](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210424124438051.png)

等待命令

wait（）方法**条件**：当前被锁定被监视的对象（正在运行的线程），从代码角度来看:只能位于synchronized中使用。

![image-20210424123544327](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210424123544327.png)





![image-20210424130513221](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210424130513221.png)

![image-20210424131203109](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210424131203109.png)



wait方法和notify方法执行者都是：同步对象(拥有监视器、锁)，而不是线程。

注意：不可以使用this、线程(Thread)调用。



唤醒命令

notify()

```java
/**
 * 线程的等待与唤醒
 *
 */
public class ThreadWaitAndNotify implements Runnable {
    private List<Integer> list = new ArrayList<>();

    @Override
    public void run() {
        synchronized (list){
            for (int i = 0; i < 100; i++) {

                //当前线程进行等待调用wait方法
                //可以被其他监视器所有权的线程使用notify方法唤醒
                if (i  == 20 && Thread.currentThread().getName().equals("one")) {
                    try {
                        //使用被监视的对象调用， 让当前线程处于等待状态
                        list.wait();
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }

                }
                if (Thread.currentThread().getName().equals("two")){
                    //随机唤醒任意一个再对象监视器上等待的线程对象
                    list.notify();
                }
                System.out.println("当前线程是"+Thread.currentThread().getName());
                System.out.println("当前i的值是"+i);

            }
        }
    }
}


    public static void main(String[] args) {

        ThreadWaitAndNotify threadWaitAndNotify = new ThreadWaitAndNotify();

        Thread thread = new Thread(threadWaitAndNotify,"one");
        Thread thread1 = new Thread(threadWaitAndNotify,"two");

        thread.start();
        thread1.start();

        while (true){

            System.out.println("one状态"+thread.getState());
            System.out.println("two状态"+thread1.getState());
            if (thread.getState() == Thread.State.TERMINATED && thread1.getState() == Thread.State.TERMINATED){
                break;
            }
            try {
                Thread.sleep(30);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }

```

###### 死锁

![image-20210424132939387](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210424132939387.png)





#### 网络编程

###### **网络应用程序概念**

**Internet(因特网)概念**

www（万维网）

![image-20210426203715860](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210426203715860.png)

1. **iso/osi七层模型**

   iso：国际标准化组织

   osi：开放系统互联模式

   ios：苹果操作系统

   | 层级名称   | 特点                                                         | 常见设备   |
   | ---------- | ------------------------------------------------------------ | ---------- |
   | 物理层     | 数据传递，设备之间的比特流的传输、物理接口、电气特性等。二进制：0101010 | 网线、网卡 |
   | 数据链路层 | 成帧、用MAC(物理地址)地址访问媒介、错误检测与修正            |            |
   | 网络层     | 提供逻辑地址（ip地址），选路                                 |            |
   | 传输层     | 可靠与不可靠的传输，传输前的错误检测、流控                   |            |
   | 会话层     | 对应用会话的管理、同步                                       |            |
   | 表示层     | 数据的表现形式、特定功能的实现如-加密                        |            |
   | 应用层     | 用户接口                                                     |            |

   

2. **TCP/IP四层模型**

   ![image-20210426203504538](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210426203504538.png)

   ![img](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/1295451-20180306155925918-725762113.png) 

   | 层级名称   | 概念                                                         |
   | ---------- | ------------------------------------------------------------ |
   | 网络接口层 | 网络接入层与OSI参考模型中的物理层和数据链路层相对应。它负责监视数据在主机和网络之间的交换。事实上，TCP/IP本身并未定义该层的协议，而由参与互联的各网络使用自己的物理层和数据链路层协议，然后与TCP/IP的网络接入层进行连接。地址解析协议(ARP)工作在此层，即OSI参与模型的数据链路层。 |
   | 网际互联连 | 网际互联层对应于OSI参考模型的网络层，主要解决主机到主机的通信问题。它所包含的协议设计数据包在整个网络上的逻辑传输。该层有三个主要协议：网际协议(IP)、互联网组管理协议(IGMP)和互联网控制报文协议(ICMP) |
   | 传输层     | 传输层对应于OSI参考模型的传输层，为应用层体提供端到端的通信功能，保证了数据包的顺序传送及数据的完整性。该层定义了两个主要的协议：传输控制协议(TCP)和用户数据报协议(UDP). |
   | 应用层     | 应用层对应OSI参考模型的高层，为用户提供所需要的各种服务。例如:FTP、Telnet、DNS、SMTP等 |

   


1. **IP地址**

   ip包头![这里写图片描述](http://www.pianshen.com/images/631/bc269448946232ada0023f482600b69f.png) 

   

    IP地址分类

   ![ip地址分类](http://www.bo56.com/wp-content/uploads/2014/11/ip_class.png) ![image-20210815180958681](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210815180958681.png)

    注：**不同类型的ip地址中对应的不同的网络号和主机号的位数，这是由子网掩码所决定的。**

   ip地址和子网掩码必须要在一起查看，不能分开查看。

4. **端口的作用**

   ​       TCP包头![fb1a4e4988fa28ce8395d61329ebbd47.png](http://kwin.xyz/passages/Linux/NetworkManage/%E7%BD%91%E7%BB%9C%E5%9F%BA%E7%A1%80/18.png) 

   UDP包头

    ![img](http://kwin.xyz/passages/Linux/NetworkManage/%E7%BD%91%E7%BB%9C%E5%9F%BA%E7%A1%80/19.png) 

   常见端口号

   FTP (文件传输协议) : 20、21

   SSH (安全shell协议) ：22

   telnet (远程登录协议)：23

   DNS (域名系统)：53

   http (超文本传输协议)：80

   SMTP (简单邮件传输协议)： 25

   POP3 (邮局协议3代)： 110



###### **TCP和UDP协议**

![image-20210426205027769](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210426205027769.png)







![image-20210426205730383](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210426205730383.png)

**TCP三次握手、TCP/IP 四次告别**

![img](http://kwin.xyz/passages/Linux/NetworkManage/%E7%BD%91%E7%BB%9C%E5%9F%BA%E7%A1%80/11.png) 

TCP/IP模型与OSI模型的比较

- 共同点

  OSI参考模型和TCP/IP参考模型都采用了层次结构的概念

  都能够提供面向连接和无连接两种通信服务机制

- 不同点

  前者为七层模型、后者是四层结构

  对可靠性要求不同(后者更高)

  OSI模型是在协议开发前设计的，具有通用性。TCP/IP是先有协议集然后建立模型，不适用于非TCP/IP网络。

  实际市场应用不同(OSI模型只是理论上的模型，并没有成熟的产品，而TCP/IP已经成为“实际上的国际标准”)。







**Java TCP和UDP网络通信实现**

Socket---->套接字

![image-20210427174825249](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210427174825249.png)

![image-20210427175026385](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210427175026385.png)



###### **java.net网络组件包**

![image-20210427175554937](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210427175554937.png)



URL

![image-20210427175945136](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210427175945136.png)

![image-20210427181016450](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210427181016450.png)

![image-20210427181134794](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210427181134794.png)



InetAddress/SocketAddress

![image-20210427181733024](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210427181733024.png)

![image-20210427181914575](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210427181914575.png)



构建SocketAddress

![image-20210427182518154](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210427182518154.png)



```java
/**
 * java套接字网络通讯应用，服务器端
 * */
public class ServerSystem {

    //本地欲绑定到ServerSocket套接字的辅助组件
    private InetAddress localhostIP;



    /**
     * 构建主机IP地址
     */
    private void InitInetAddress(){
        if (localhostIP == null){
            try {
                localhostIP  =  Inet4Address.getLocalHost();
                System.out.println(localhostIP);
            } catch (UnknownHostException e) {
                e.printStackTrace();
            }

        }
    }

    /**
     * 初始化
     */
    private void init(){
        InitInetAddress();
    }

    public ServerSystem() {
        init();
    }
}

```

**基于TCP协议**

###### **构建服务器端套接字(SocketServer)**

![image-20210427183951888](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210427183951888.png)

![image-20210427184123866](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210427184123866.png)

![image-20210427185210247](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210427185210247.png)

```java
/**
 * java套接字网络通讯应用，服务器端
 * */
public class ServerSystem {

    //允许最大请求连接的队列数
    private static final int MAX_BACL_LOG = 20;

    //本机绑定的端口号
    private static final int PORT = 9090;
    private static final int PORT_SPARE =  9999;

    //本地欲绑定到ServerSocket套接字的辅助组件
    private InetAddress localhostIP;

    private  Socket client;

    //客户端输入流，用来读取用户发送的数据
    private InputStream inputStream;

    private DataInputStream dataInput;


    //实现套接字网络信息交互服务器端套接字对象
    private ServerSocket serverSocket;
    private OutputStream out;
    private DataOutputStream dataOut;

    /**
     * 构建主机IP地址
     */
    private void InitInetAddress(){
        if (localhostIP == null){
            try {
                localhostIP  =  Inet4Address.getLocalHost();
                System.out.println(localhostIP);
            } catch (UnknownHostException e) {
                e.printStackTrace();
            }

        }
    }


    /**
     * 构建ServerSocket对象
     */
    private void InitServerSocket() {
        if (serverSocket == null){
            try {
                serverSocket = new ServerSocket(PORT,MAX_BACL_LOG,localhostIP);
//                serverSocket.setSoTimeout(3000);
            } catch (IOException e) {
                e.printStackTrace();
            }

        }
    }

    /**
     * 启动服务器套接字等待客户端请求
     */
    public void startAccepts(){
        try {
            //检查服务器套接字是否已经绑定
            if (!serverSocket.isBound()){
                serverSocket.bind(new InetSocketAddress(PORT_SPARE),MAX_BACL_LOG);
            }
            System.out.println("服务器创建成功，等待连接");
            //等待客户端连接进来，此方法是阻塞（没有连接时处于阻塞）
            client  = serverSocket.accept();
            System.out.println("客户端发来请求，服务器端已接受");
            /*基于客户端套接字建立输入输出流*/
            inputStream =  client.getInputStream();
            //使用缓冲流
            dataInput = new DataInputStream(inputStream);

            out = client.getOutputStream();
            dataOut = new DataOutputStream(out);

            //实现信息交互
            sendAndReceive();

        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    /**
     * 实现信息交互
     */
    private void sendAndReceive(){
        Scanner  scanner = new Scanner(System.in);
        //服务器端处于连接中
        if (client.isConnected() && !client.isClosed()){
            while (true){
                //读取用户信息，返回字符串
                try {
                    String message =  dataInput.readUTF();
                    System.out.println("用户信息"+message);
                    String replyMess = scanner.next();
                    //服务器回复信息给客户端
                    dataOut.writeUTF(replyMess);
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }

    }


    /**
     * 初始化
     */
    private void init(){
        InitInetAddress();
        InitServerSocket();
    }


    public ServerSystem() {
        init();
    }
}
```



###### 套接字客户端实现(Socket)

**Socket**

![image-20210427194519759](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210427194519759.png)

![image-20210427195046614](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210427195046614.png)

![image-20210427195814294](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210427195814294.png)

创建一个本地服务器和本地客户端，实行信息的交互。

```java
/**
 * 客户端套接字主程序
 */
public class ClientSocket {
    //本地地址
    private InetSocketAddress localAddress;
    //本地端口号
    private static final Integer localPort = 7777;

    //远程套接字服务器地址
    private InetSocketAddress remoteAddress;

    private static final Integer remotePort = 9090;

    //客户端套接字对象
    private Socket client;

    //输入流
    private InputStream in;

    //输出流
    private OutputStream out;

    private DataInputStream dataInputStream;

    private DataOutput dataOutput;


    /**
     * 构建客户端套接字
     */
    private void initClientSocket() {
        if (client == null) {
            //构建未绑定的客户端套接字
            client = new Socket();
        }
    }

    /**
     * 构建本机（客户端）IP地址
     */
    private void initLocalAddress() {
        if (localAddress == null) {
            try {
                localAddress = new InetSocketAddress(Inet4Address.getLocalHost(), localPort);
            } catch (UnknownHostException e) {
                e.printStackTrace();
            }
        }
    }

    /**
     * 套接字绑定本机地址
     */
    private void boundAddress() {
        try {
            client.bind(localAddress);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    /**
     *初始化远程地址
     */
    private void initRemoteAddress () {
        if (remoteAddress == null) {
            try {
                remoteAddress = new InetSocketAddress(Inet4Address.getLocalHost(), remotePort);
            } catch (UnknownHostException e) {
                e.printStackTrace();
            }
        }
    }


    /**
     * 实现与服务器进行信息交互的方法
     */
    public void sendAndReceive(){
        System.out.println("输入信息回车发送");
        //连接服务器的方法
        connectRemoteServer();
        //创建文件流的方法
        createSocketInputAndOutput();

        Scanner scanner = new Scanner(System.in);

        while (true){
            String mess = scanner.next();
            try {
                //发送消息给服务器
                dataOutput.writeUTF(mess);
                //服务器返回的信息
                String  backMess = dataInputStream.readUTF();
                System.out.println("服务器消息: "+backMess);
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }


    /**
     * 请求连接到远程服务器
     */
    private void connectRemoteServer () {
        try {
            client.connect(remoteAddress);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }


    /**
     * 基于套接字创建输入输出流
     */
    public void createSocketInputAndOutput() {
        if (client.isConnected()) {
            try {
                in = client.getInputStream();
                out = client.getOutputStream();
                dataInputStream = new DataInputStream(in);
                dataOutput = new DataOutputStream(out);
            } catch (IOException e) {
                e.printStackTrace();

            }
        }
    }

    public ClientSocket() {
        //调用创建ip地址方法
        initLocalAddress();
        //调用套接字对象(客户端)创建方法
        initClientSocket();
        //创建远程主机地址
        initRemoteAddress();
        //调用绑定地址
        boundAddress();
    }
}

```

创建一个本地服务器（SocketServer）和本地客户端（Socket），实行信息的交互。





###### **基于UDP协议的套接字实现**

![image-20210428172027321](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210428172027321.png)



**DatagramPacket**

![image-20210428172306988](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210428172306988.png)

![image-20210428172508457](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210428172508457.png)

![image-20210428172843572](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210428172843572.png)



DatagramPacket 常用API

![image-20210428173428697](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210428173428697.png)



**DatagramSocket**

![image-20210428174618357](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210428174618357.png)

![image-20210428174858172](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210428174858172.png)



DatagramSocket 常用API

![image-20210428182029878](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210428182029878.png)



![image-20210428182745433](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210428182745433.png)

基于UDP协议创建客户端和服务器端进行信息交互。

