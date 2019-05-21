# 面向对象

面向对象的思想就是值我们要实现一个共功能的时候，我们不自己去做，而是找别人帮我们去做，帮我们去做的这个人就是对象。面向对象强调的是谁来帮我实现这个功能。



## **类与对象的关系**

**类**：是一组相关属性和行为的集合，类可以看成是事物的模板

**对象**：对象是一类事物的具体体现，对象是类的一个实列，必然具备该类的事物属性和行为。

类是对象的模板，对象是类的实体

下面来定义一个学生类

```java
//类具有属性和行为，属性也叫做成员变量，行为也叫做成员方法
public class Student{
    //定义成员变量,因为每一个学生都有不同的姓名和年龄，所以可以把这两个作为成员变量,成员变量要定义在类中，方法外面，如果定义在方法里面，就叫做局部变量。变量是有作用域的，成员变量的作用域在整个类中，局部变量的作用域在该方法的里面。
    String name;
    int age;
    //定义方法，每一个学生都有着吃饭，睡觉，学习的行为，也就是方法
    public void eat(){
        System.out.println("我是"+name+"在吃饭");
    }
    public void sleep(){
        System.out.println("我是"+name+"在睡觉");
    }
    public void study(){
        System.out.println(name+"今年"+age+"岁了，要认真学习了");
    }
}
```

刚刚定义好了类，现在让我们来使用他吧

类的使用需要创建对象

```java
//创建对象的格式
//类的名称 对象名 = new 类名称();
//成员变量的使用   对象名.成员变量
//成员方法的使用    对象名.成员方法()
public class AStudent{
    public static void main(String[] args){
        /*创建Student类对象，对象创建好之后就可以使用类了，也就是说可以
        使用对象名去调用类的成员方法，还可以对该类的成员变量赋值*/
        Student stu = new Student();
        //对成员变量赋值,将右侧的刘备赋值交给stu对象当中的name成员变量
        stu.name = "刘备";
        stu.age = "18";
        //调用成员方法
        stu.eat();
        stu.sleep();
        stu.study();
    }
}
```

## 使用对象类型作为方法的参数

什么是对象类型，new出来的就是对象类型

```java
public class AStudent{
    public static void main(String[] args){
        Student one = new Student();
        one.age = 18;
        one.name = "新垣结衣";
        method(one);
    }
    //以Student类做为参数传递，传递进来的对象中的方法和变量可以使用param参数名称来调用
    public static void method(Student param) {
        System.out.println(param.name);//新垣结衣
        System.out.println(param.age);//18
        param.study();//新垣结衣今年18岁了，要认真学习了
    }

}
```

使用对象类型作为方法的返回值

```java
  public static void main(String[] args){
        //返回值类型是一个Student，所以需要Student来接收该返回值
        Student two = method();//method()方法的返回值类型是Student;
        two.study();
    }
    public static Student method() {
       Student one = new Student();
       one.name="曹操";
       one.age = 90;
       
       return one;
```

## 局部变量与成员变量的不同

1. **定义的位置不一样**

   局部变量：在方法的内部

   成员变量：在方法的外部，直接写在类当中

2. **作用范围不一样**

   局部变量：只有方法当中才可以使用，出了方法就不能再用

   成员变量：整个类都可以通用

3. **默认值不一样**

   局部变量：没有默认值，如果想使用，必须要手动赋值

   成员变量：如果没有赋值，会有默认值，规则和数组一样

   

## 面向对象的三大特征之封装性

1. **方法就是一种封装**
2. **关键字private也是一种封装**

封装就是将一些细节信息隐藏起来，对于外界不可见

**private**关键字一旦用于成员变量，那么该成员变量就只能够在本来中访问，不能再其它类中访问

```java
public class Student{
    String name;
    //写在对age设置private，使他只能够再本类中访问
    private int age;

    public void  setAge(int num){
        //未来避免年龄传入进来的不合理加上if判断语句
        //条件为真就把num赋值给age
        if(0<num&&num<150){
        	age = num;
        }else{
            System.out.println("年龄不合理")；
        }
    }
    public int getAge(){
        return age;
    }
}
```

现在写多一个类来间接访问age;

```java
public class AStudent{
    public static void main(String[] args){
     //创建了Student对象，就可以使用她的变量和方法了
    Student one = new Student();
    //调用了方法setAge.传递了参数
    one.setAge(18);//int age = 18;
    //设置了private的要通过setAge来访问，没有设置private的可以直接对象名.成员变量来访问
    System.out.println(one.name+"  "+one.getAge());
    }
}
```

## 构造方法

构造方法是专门用来创建对象的方法，当我们通过关键字new来创建对象是，其实就是再调用构造方法,构造方法的名称必须和所在类的名称完全一样，构造方法不要写返回值类型。

如果没有编写任何构造方法，那么编译器将会默认赠送一个构造方法，没有参数，没有方法体。

一旦自己编写了构造方法，那么编译器将不会给你赠送构造方法

格式：

public 类名称（参数类型 参数名称）{方法体}

```java
public class Student{
    public Student(//我是参数){
        System.out.println("构造方法被调用了");//我是方法体
    }
}
```

```java
//new 对象就是在调用构造方法
public class AStudent{
    public static void main(String[] args){
        //构造方法new对象的时候就被执行
        Student stu = new Student();//创建Student对象，就是在调用Student的构造方法
        //运行程序将会得到  构造方法被调用了
    }
}
```

## 定义一个标准类

```java
//new 对象就是在调用构造方法
public class AStudent{
    public static void main(String[] args) {
        Student one = new Student();
        one.setAge(20);
        one.setName("孙权");
        System.out.println("姓名--"+one.getName()+"   年龄--"+one.getAge());

        Student two = new Student("曹操",30);
        System.out.println("姓名--"+two.getName()+"   年龄--"+two.getAge());
    }
}
```

