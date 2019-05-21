## 静态static

如果一个成员变量使用了static关键字，那么这个变量不再属于对象自己，而是属于所在的类，多个对象共享同一份数据

静态static 关键字修饰成员变量

```java
public class Student {
    private String name;
    private int age;
    static String room;
    public Student() {
    }

    public Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
}

```

```java
public static void main(String[] args){
    Student one = new Student("郭靖",18);
    //用对象名.变量名给变量赋值
    one.room = "101";
    Student two = new Student("黄蓉",16);
     //姓名:郭靖  年龄18  教室105
    System.out.println("姓名:" +one.getName()+"  年龄"+one.getAge()+"  教室"+one.room);
    
    //没有对two.room赋值但是也输出了教室101,可见被static修饰过的变量的数据是共享的
    //姓名:黄蓉  年龄16  教室105
    System.out.println("姓名:" +two.getName()+"  年龄"+two.getAge()+"  教室"+two.room);
    }
```

静态static关键字修饰成员方法

一旦使用static修饰成员方法，那么这就成为了静态方法，静态方法不属于对象，而是属于类的

如果没有static关键字，那么必须首先创建对象，然后通过对象才可以使用他

有static关键字可以通过类名.静态方法名调用方法

```java
public class MethodDemo {
   public void method(){
       System.out.println("这是一个成员方法");
   }
   public static void method1(){
       System.out.println("这是一个静态方法");
   }
}
```

```java
public class MethodTest {
    public static void main(String[] args){
        MethodDemo one = new MethodDemo();
        //对象名调用方法
        one.method();
        //对象名调用方法
        one.method1();
        //类名调用静态方法
        MethodDemo.method1();
    }
```

如果有了static，都推荐使用类名称来调用



**注意事项**

1. 静态不能直接访问非静态

```java
public class MethodDemo {
    int num ;
    static int num1;
   public void method(){
       System.out.println("这是一个成员方法");
       //成员方法访问成员变量和静态变量
       System.out.println(num);
       System.out.println(num1);
       
   }
   public static void method1(){
       System.out.println("这是一个静态方法");
       //静态方法访问静态变量
       System.out.println(num1);
       //静态方法不能够访问非静态变量
       //System.out.println(num);编译报错
   }

```

2. 静态方法不能使用this，因为this代表当前对象，而静态方法属于类。

###### 静态代码块

特点，当第一次用到本来的时候，静态代码块执行唯一一次

```java
/*格式
public class 类名{
	static{}
}*/
public class StaticDemo {
    static{
        System.out.println("静态代码块执行了");
    }
    public StaticDemo(){
        System.out.println("构造方法执行了");
    }
}
```

```java
public class StaticDemotest {
    public static void main(String[] args) {
        //静态代码块只会执行一次，并且优先于其他语句执行
        StaticDemo one =new StaticDemo();
        StaticDemo two = new StaticDemo();
    }

}
//输出结果
静态代码块执行了
构造方法执行了
构造方法执行了
```

###### Arrays工具类

public static String toStirng(数组),将参数数组变成字符串

```java
public static void main(String[] args) {
        int[] arrays= new int[]{1,2,3,4,5};
        String[] arrays1 = new String[]{"骐骥一跃","不能十步","驽马十驾","功在不舍"};
        //调用Arraysd的toString方法把数组变成字符串
        String str = Arrays.toString(arrays);
        String str1 = Arrays.toString(arrays1);
        //打印字符串
        System.out.println(str);
        System.out.println(str1);

    }
```

public static void  sort(数组),按照默认升序，对数组元素排序

```java
public static void main(String[] args) {
        int[] arrays= new int[]{1,63,45,55,88};
        String[] arrays1 = new String[]{"骐骥一跃","不能十步","驽马十驾","功在不舍"};

        //对数组进行排序
        Arrays.sort(arrays);
        Arrays.sort(arrays1);
        //排序完之后，把他变成字符串，打印输出
        System.out.println(Arrays.toString(arrays));
        System.out.println(Arrays.toString(arrays1));
//输出结果如下
//[1, 45, 55, 63, 88]
//[不能十步, 功在不舍, 驽马十驾, 骐骥一跃]
    }
```

###### Arrays字符串倒序练习

```java
public static void main(String[] args) {
        //先创建一个字符串
        String str = "ERsdf485dfW";
        //要排序字符串，需要把字符串变成char数组，可以使用toCharArray方法
        char[] chars = str.toCharArray();
        //把字符串用sort方法排序好
        Arrays.sort(chars);
        //然后就可以for循环遍历来倒序
        //chars数组的最大索引为长度减一，索引为0也有元素，索引需要>=0
        for(int i=chars.length-1;i>=0;i--){
            System.out.println(chars[i]);
        }

    }
```

##### 继承

继承的格式

```java
public class zi extends fu{}
```

继承中成员变量的访问特点

在子父类的继承关系当中，如果有成员变量重名，则创建子类对象时，访问有两种方式

直接通过子类对象访问成员变量

等号左边是谁，就优先有谁，没有则向上找

```java
public class Fu {
    //父类
    int num = 100;
}
```

```java
public class Zi extends Fu{
    //子类
    int num = 200;
}
```

```java
public static void main(String[] args) {
     Zi zi = new Zi();
    //输出的时100还是200？
     System.out.println(zi.num);//200
    }
```



间接通过成员方法访问成员变量

方法属于谁，就优先用谁，没有则向上找

```java
public class Fu {
    //父类
    int num = 100;
    public void methodFu(){
        System.out.println(num);
    }
}
```

```java
public class Zi extends Fu{
    int numZi = 10;
    int num = 200;
    public void methodzi(){
        System.out.println(num);
    }
```

```java
public static void main(String[] args) {
        Zi zi = new Zi();
        //输出的时100还是200？
        System.out.println(zi.num);//200
        //这个方法是子类的，优先使用子类的成员变量
        zi.methodzi();//200
        //这个方法是父类的，优先使用父类的成员变量
        zi.methodFu();//100
    }
```

### 区分子类方法中重名的三种变量

```java
public class Fu {
    int num = 10;
}
```

```java
public class Zi extends Fu{
    int num = 20;
    public void method(){
        int num = 30;
        //输出局部变量
        System.out.println(num);
        //输出本类变量
        System.out.println(this.num);
        //输出父类变量
        System.out.println(super.num);
    }
}
```

```java
/*
*局部变量:
* 本类的成员变量
* 父类的成员变量
* */
public class ExtendsTest {
    public static void main(String[] args) {
        Zi zi = new Zi();
        //调用Zi类方法
        zi.method();
    }
}
```

继承中成员方法的访问特点

```java
public class Fu {
    public void methodFu(){
        System.out.println("父类方法");
    }
    public void method(){
        System.out.println("父类重名方法执行");
    }
}
```

```java

public class Zi extends Fu{
    public void methodZi(){
        System.out.println("子类方法执行");
    }
    public void method(){
        System.out.println("子类重名方法执行");
    }
}
```

```java
public class ExtendsTest {
    public static void main(String[] args) {
        Zi zi = new Zi();
        //调用Zi类方法
        zi.methodFu();
        zi.methodZi();
        //方法重名，优先使用子类方法
        zi.method();
    }
}
```

#### 重写（Override）

概念：在继承关系当中，方法的名称一样，参数列表也一样

重写（Override），方法的名称一样，参数列表也一样

重载（Overload），方法的名称一样，参数列表不一样

#### 继承中构造方法的访问特点

```java
public class Fu {
    public Fu(){
        System.out.println("我是无参数的父类构造方法");
    }
    public Fu(int num){
        System.out.println("我是有参数的父类重载构造");
    }
}
```

```java
public class Zi extends Fu{

    public Zi(){
        //在继承关系中，编译器都会默认赠送一个super()父类构造方法;
        //而且还是在子类构造方法的第一行，所以在new对象的时候会先执行
        // 父类的构造方法
        // super();
        super(5);
        //在继承关系中，子类会有一个默认的super();
        System.out.println("子类构造方法");
    }
}
```

````java
/*
继承关系中，父子类构造方法的访问特点
1.子类构造方法当中有一个默认隐含的"super()"调用
2.子类构造可以通过super关键字来调用父类重载构造
super的父类构造调用，必须在构造方法的第一句
 */
public class ConstructorDemo {
    public static void main(String[] args) {
        Zi zi = new Zi();
        //父类构造方法
        //子类构造方法
    }
}
````

#### super关键字的三种用法

1.在子类的成员方法中，访问父类的成员变量。super.numFu

2.在子类的成员方法中，访问父类的成员方法。super.methodFu

3.在子类的构造方法中，访问父类的构造方法。

##### this关键字的三种用法

super关键字用来访问父类内容，而this关键字用来访问本类内容，用法也有三种

1.在本类中的成员方法中，访问本类的成员变量

```java
public class Zi extends Fu {
    int num = 55;
public void athis() {
    int num = 66;
    System.out.println(num);//66
    System.out.println(this.num);//55
   }
}
```

2.在本类的成员方法中，访问本类的另一个成员方法，

```java
    int num = 55;
    public void athis() {
        int num = 66;
        System.out.println(num);//66
        System.out.println(this.num);//55
    }
    public void bthis(){
        System.out.println("bbb");
    }
    public void cthis(){
        this.athis();
        System.out.println("ccc");
    }
```

```java
 public static void main(String[] args) {
        new Zi().cthis();//输出结果为66 55 ccc
    }
```

3.在本类的构造方法中，访问本类的另一个构造方法

```java
public Zi(){
    	//重载构造方法两个
    	//调用下一个构造方法
       this(123);
    }
    public Zi(int n){
        //调用下一个构造方法
       this(1,2);
    }
    public Zi(int a,int b){
        
    }
//注意this()调用跟super()一样也必须是构造方法的第一个语句，super和this两张构造调用，不可以同时使用。
```



#### 练习

```java
public class Fu {
    int num = 5;
    public Fu(){
        System.out.println("我是构造方法");
    }
    public void method(){
        System.out.println("我是父类");
    }
}

```

```

public class Zi extends Fu {
    int num = 6;

    public void method1(){
        int num = 7;
        System.out.println(num);
        System.out.println(this.num);
        System.out.println(super.num);
    }
    @Override
    public void method(){
        super.method();
        System.out.println("我是子类");
    }
}
```

```java
public class ConstructorDemo {
    public static void main(String[] args) {
        Zi zi = new Zi();
        zi.method1();
        zi.method();
		//我是构造方法
		//7
		//6
		//5
		//我是父类
    }
}
```



#### Java继承的三个特点

 1.Java语言是单继承的，一个类的直接父类只有由唯一一个

2. Java语言可以多级继承，也就是A类继承B类,B类继承C类
3. 一个类的直接父类是唯一的，但是父类可以由很多个子类,

## 抽象类

```java
public abstract class 类名{
    public abstract void 方法名(){}
    //抽象类中也可以定义普通成员方法
    public void 方法名(){}
}
```

#### 抽象方法和抽象类的使用

1. 抽象类不能够直接new的抽象类对象
2. 必须用一个子类继承抽象类才可以使用
3. 子类必须重写抽象父类当中的所有抽象方法
4. 创建子类对象进行使用

抽象方法和抽象类的注意事项

1. 抽象类不能够创建对象

2. 抽象类，可以有构造方法的，是供子类创建对象时，初始化成员使用的

3. 抽象类中，不一定包含抽象方法，但是抽象方法一定包含在抽象类中

4. 抽象类的子类，必须重写抽象父类的所有抽象方法

   

**红包案例**

```JAVA
public class AUser {
    private int money ;
    private String name ;

    public AUser() {
    }


    public AUser(int money, String name) {
        this.money = money;
        this.name = name;
    }

    public int getMoney() {
        return money;
    }

    public void setMoney(int money) {
        this.money = money;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public void show(){
        System.out.println("我"+name+"现在的余额是"+money);
    }
}

```

```JAVA

import java.lang.reflect.Array;
import java.util.ArrayList;

public class Admin extends AUser{
    public Admin() {
    }

    public Admin(int aBalance, String aName) {
        super(aBalance, aName);
    }

    public ArrayList<Integer> send(int totalMoney, int count){
        ArrayList<Integer> redList = new ArrayList<>();
        int  i= totalMoney/count;
        //判断群主有多少钱
        int leftMony = super.getMoney();
        if(totalMoney>leftMony){
            System.out.println("余额不足");
            return redList;
        }
        //扣钱
        super.setMoney(leftMony -totalMoney);
        int avg = totalMoney/count;
        int mod = totalMoney%count;

        for(int d=0;d<count-1;d++){
            redList.add(avg);
        }
        int last=  avg+mod;
        redList.add(last);
        return redList;
    }
}

```

```JAVA

import java.util.ArrayList;
import java.util.Random;

public class Menber extends  AUser{
    public Menber() {
    }

    public Menber(int money, String name) {
        super(money, name);
    }
    public void receive(ArrayList<Integer> list){
        int index = new Random().nextInt(list.size());
        int delta = list.remove(index);
        int money = super.getMoney();
        super.setMoney(money+delta);

    }

}

```

```JAVA

import java.util.ArrayList;

public class RedPacket {
    public static void main(String[] args) {
        Admin admin = new Admin(100,"群主");
        Menber one = new Menber(0,"aaa");
        Menber two = new Menber(0,"aaa");
        Menber three = new Menber(0,"aaa");
        admin.show();
        one.show();
        two.show();
        three.show();

        ArrayList<Integer> redList = admin.send(20,3);
        one.receive(redList);
        two.receive(redList);
        three.receive(redList);

        admin.show();
        one.show();
        two.show();
        three.show();
    }
}

```

