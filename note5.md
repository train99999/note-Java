## 接口

接口就是一种公共的规范标准   是一种引用数据类型                                                           

定义格式

public interface 接口名称{}

java7 中接口可以包含常量，抽象方法；Java8 还可以额外包含默认方法，静态方法；Java 9 还可以额外包含私有方法

```java
public interface MyInterfaceAbstract{
    //这是一个抽象方法
    public abstract void methodAbs();
    //接口中的抽象方法，修饰符必须是两个固定的关键字:public abstract
    //这两个关键字可以选择性的省略
    abstract void methodAbs2();
    public void methodAbs3();
    void methodAbs4();
    
}
```

#### 接口的抽象方法使用

接口使用步骤：

1. 接口不能够直接使用，必须有一个“实现类”来实现该接口

   格式：

   public class 实现类名称  implements 接口名称{}

2. 接口的实现类必须覆盖重写接口中所有的抽象方法
3. 创建实现类对象(new)，进行使用

```java 
//按照定义格式定义一个接口
//public interface 接口名称{}
public interface InterfaceDemo {
    //接口里面可以有抽象方法，普通方法
    //定义一个抽象方法
    public abstract void methodAbs1();
    //默认方法
    public abstract void methodAbs2();

}
```

```java 
public class InterfaceDemoImpl implements InterfaceDemo{
    //回顾一些重写的概念
    //方法名和形参列表一样
    //权限修饰符必须大于或者等于父类的权限修饰符
    //子类的返回值类型必须小于或者等于父类的返回值类型
    @Override
    public void methodAbs1() {
        System.out.println("天下武功，唯快不破");
    }

    @Override

    public void methodAbs2() {
        System.out.println("认真的人，自带光芒");
    }

}
```

```java 

public class newInterfaceDemo {
    public static void main(String[] args){
        InterfaceDemoImpl inter = new InterfaceDemoImpl();
        inter.methodAbs1();
        inter.methodAbs2();
    }
}
```

##### 注意事项

如果实现类并没有覆盖重写接口中的所有的抽象方法，那么这个实现类就必须是抽象类

###### 接口的默认方法定义

```java
public interface InterfaceDemo {
    /*
    java 8开始，接口允许定义默认方法
    格式:
    public default 返回值类型 方法名称（参数列表）{
    方法体
    }
    备注:接口当中的默认方法，可以解决接口升级的问题
    默认方法可以有方法体
     */
    public abstract void methodAbs1();

    public default void methodAbs2(){
        System.out.println("我是默认方法，可以解决升级问题");
    }
```

````java 
public class InterfaceDemoImpl implements InterfaceDemo{
    @Override
    public void methodAbs1() {
        System.out.println("天下武功，唯快不破");
    }
    //我在这里并没有重写public default void methodAbs2()
    //实现接口自动继承方法
}

````

```java 
public class newInterfaceDemo {
    public static void main(String[] args){
        InterfaceDemoImpl inter = new InterfaceDemoImpl();
        //接口的默认方法也是可以覆盖重写的
        //这里就不写了
        inter.methodAbs1();
        inter.methodAbs2();
    }
}
```

##### 接口的静态方法的定义

```java
/*
格式
public static 返回值类型 方法名称（参数列表）{}

 */
public interface InterfaceStatic {
    public static void method1(int a,int b){
        System.out.println("今天要敲"+a*b+"行代码");
    }
}
```

```java
public class InterfaceStaticImpl {
    //接口中的静态方法的使用
    public static void main(String[] args) {
        //直接通过接口名称.静态方法的名称调用即可
        InterfaceStatic.method1(15,67);
    }
}
```

##### 接口的私有方法定义

```java
/*
问题描述：
我们需要抽取一个共有方法，用来解决两个默认方法之间重复代码的问题
但是这个共有方法，不应该被是实现类使用，应该私有化的

解决方案
从Java 9 开始，接口当中允许定义私有方法
1.普通私有方法，解决多个默认方法之间重复代码问题
格式
private 返回值类型 方法名称(参数列表){}
2.静态私有方法，解决多个静态方法之间重复代码问题
    格式：
    private static 返回值类型 方法名称（参数列表）{}
 */
    public interface InterfaceStatic {
        public default void method1(){
            System.out.println("认真的人，自带光芒");
            method3();
        }
        public default void method2(){
            System.out.println("作日的最佳表现，是今日的最低要求");
            method3();
        }
        private void method3(){
            System.out.println("乘风破浪会有时，直挂云帆济沧海");
        }
}
```

```java
public class InterfaceStaticImpl implements InterfaceStatic{
    public static void main(String[] args) {
        InterfaceStaticImpl inter = new InterfaceStaticImpl();
        inter.method1();
        inter.method2();
        //接口中的静态方法的使用
        //想要使用接口的方法，必须要实现接口
        //实现完接口后，需要new对象使用
    }

}
```

##### 接口的常量定义和使用

1.接口当中的常量，可以省略public static final ,注意，不写也照样是这样

2. 接口当中的常量，必须进行复制，不赋值不能使用

3. 接口当中的常量名称，使用完全大写的字母，用下划线进行分割

   

使用格式

接口名称.常量名称

## 多态

多态的前提：extends继承或者Implements实现，

一个对象拥有多种形态，这就是：对象的多态性

代码当中体现多态性：父类引用指向子类对象

多态格式

父类名称  对象名 = new 子类名称（）；

或者

接口名称 对象名= new 实现类名称（）；

#### 多态中成员变量的使用特点

```java
//访问成员变量的两种方式
//1.直接通过对象名称访问成员变量：看等号左边是谁，优先用谁，没有向上找
//2.间接通过成员方法访问
public class Fu {
    //子类也有相同的成员变量num
    int num = 10;

    public void shownum(){
        System.out.println(num);
    }
}
```

```java 
public class Zi extends Fu{
    //与父类相同的成员变量num
    int num = 20;
    //子类特有的成员变量
    int num1 =30;
    //重写方法
    @Override
    //重写了父类的方法，
    public void shownum(){
        System.out.println(num);
    }
}

```

```java

public class Demo01MultiField {
    public static void main(String[] args) {
        //使用多态的写法，父类引用指向子类对象
        Fu obj  = new Zi();
        //等号左边是Fu，优先使用左边的的成员变量，没有则向上找
        System.out.println(obj.num);//10
        //不可能向下找
        //System.out.println(obj.num1);编译报错

        //shownum属于Fu，则使用Fu的成员变量//10
        //当子类覆盖重写父类，就属于Zi类//20
        obj.shownum();
    }
}
```

### 多态中成员方法的使用特点

```java
public class Fu {
    //成员方法的访问规则
    //看new的是谁，就优先用谁，没有则向上找
    public void method(){
        System.out.println("我是父类");
    }
    public void methodFu(){
        System.out.println("我是父类特有方法");
    }
}
```

```java
public class Zi extends Fu{
    public void method(){
        System.out.println("我是子类");
    }
    public void methodZi(){
        System.out.println("我是子类特有方法");
    }
}
```

java

```java
public class Demo01MultiField {
    public static void main(String[] args) {
       Fu obj  = new Zi();//多态
       obj.method();// 父子都有，new的是zi，优先用zi  //输出结果我是子类
       obj.methodFu();//子类没有，向上找，           //输出结果我是父类特有方法
    }
}
```

**多态中成员变量访问规则和成员方法访问规则总结**

成员变量：看左边，左边是哪一个类就优先使用哪一个类。没有像上找                                      

成员方法：看右边，new的是哪一个对象就优先使用哪一个对象的方法。没有向上找

## 对象的向上转型

1. 对象的向上转型，其实就是多态的写法

   格式 父类名称 对象名 = new 子类名称（）; 

   含义：右侧创建一个子类对象，把他当作父类来看待使用

   Animal animal = new Cat();创建了一只猫，当作动物看待

注意事项：向上转型一定是安全的从小范围（猫）转成大范围（动物）

## 对象的向下转型

对象的向下转型，其实是一个还原的动作

格式：子类名称 对象名 = （子类名称）父类对象；

含义，将父类对象，还原成本来的子类对象

```java
Animal animal = new Cat();//本来是猫，向上转型成为动物
Cat cat = (cat) animal;//本来是猫，已经被当成动物了，还原回来成为本来的猫向下转型；

```

### instanceof关键字进行类型判断

格式：

对象 instanceof类名称

这将会得到一个Boolean值结果，也就是判断前面的对象能不能当作后面类型的实例

#### 笔记本USB接口案例

```java

//先确定一下笔记本电脑有什么功能
//关机，开机，可以使用各种USB设备
//功能确定好之后写方法
public class Computer {
    public void powerOn() {
        System.out.println("笔记本电脑开机了");
    }

    public void powerOff() {
        System.out.println("笔记本电脑关机了");
    }

    public void usbDevice(USB usb) {
        usb.open();
        if (usb instanceof Mouse) {
            Mouse mouse = (Mouse) usb;
            mouse.click();
        } else if (usb instanceof KeyBoard) {
            KeyBoard keyboard = (KeyBoard) usb;
            keyboard.type();
        }
        //usb.close();
    }
}

```

```java

//usb设备需要设置成接口，并且有抽象方法，
//因为usb设备都有着共性的方法，和非共性的方法，我们需要把共性的方法给抽取出来
//usb设备都有开关的功能
public interface USB {
    //打开设备的功能
    public abstract void open();
    //关闭设备的功能

    public abstract void close();

}
```



```java

//现在设置一个usb设备
//去实现USB接口
//实现了这个USB接口才可以在Computer类中传递进去，有了USB设备，鼠标才是一个完整的电脑
//现在就去实现这个接口吧
public class Mouse implements USB {
    //必须重写抽象方法
    @Override
    public void open() {
        System.out.println("鼠标插入");
    }
    @Override
    public void close() {
        System.out.println("鼠标拔出");
    }
    //鼠标特有的方法
    public void click() {
        System.out.println("鼠标点击");
    }
}
```

```java

//也是一个USB设备
public class KeyBoard implements USB {
    //重写方法
    @Override
    public void open() {
        System.out.println("键盘插入。。。");
    }
    @Override
    public void close() {
        System.out.println("键盘拔出");
    }
    //键盘特有方法
    public void type() {
        System.out.println("键盘打字");
    }
}
```

```java

//现在可以创建一个计算机了
public class ComputerImple {
    public static void main(String[] args) {
        //创建一个笔记本对象
        Computer computer = new Computer();
        //启动笔记本
        computer.powerOn();
        //创建USB接口
        USB usb = new Mouse();
        //传递接口
        computer.usbDevice(usb);
        USB usb1 = new KeyBoard();
        computer.usbDevice(usb1);
        //关闭笔记本
        computer.powerOff();

    }
}
```







