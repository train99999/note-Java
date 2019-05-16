# API概述

什么叫做API?

API（Application Programming lnterface）,应用程序编程接口。

所谓API就是值好多的类，好多的方法，JDK给我们提供了很多现成的类，我们可以直接去使用，这些类就是API

[API官方文档](https://docs.oracle.com/javase/10/docs/api/overview-summary.html)

#### 常见的几个API之Scanner类的使用

1. ##### 导包

   Scanner类因为存在于java.lang包下，所有不需要导入就可以直接使用

2. ##### 创建

   类名称 对象名 = new 类名称();

3. ##### 使用

   对象名.方法名();

```java
public class AScanner{
    public static void main(String[] args){
        System.out.println("请输入一个数字")
        //System.in代表从键盘进行输入
        Scanner sc = new Scanner(System.in);
        //调用Scanner的方法，获取一个整数
        int num = sc.nextInt();
        System.out.println("数字"+num);
    }
}
```

Scanner的练习题

```java
import java.util.Scanner;

public class MaxInput {
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        System.out.println("请输入第一个数字");
        int a = sc.nextInt();
        System.out.println("请输入第二个数字");
        int b = sc.nextInt();
        System.out.println("请输入第三个数字");
        int c = sc.nextInt();
        int max ;
        if(a>b){
            max = a;
        }else{
            max = b;
        }
        if(max>c){
            System.out.println("最大值为"+max);
        }else{
            max = c;
            System.out.println("最大值为"+max);
        }

    }
}

```

#### 匿名对象

匿名对象就是只有右边的对象，没有左边的名字和赋值运算符

匿名对象的格式:

new 类名称();

匿名对象只能够使用一次，下次再用不得不再创建一个新对象

每一次new都是一个新的对象，所以只能够使用一次

```java
public class Person{
    String name;
    public void showName(){
        System.out.println("我叫"+name);
    }
}
```



```java
public class niming{
    public static void main(String[] args){
        Person one = new Person();
        one.name =( "张飞");
        one.showName();
        
        new Person().name = "吕蒙";
        new Person().showName(); //不能够打印出吕蒙，每一次new都是一个新的对象
        
    }
}
```

#### 常见的几个API之Random

```java
public static void main(String[] args){
    	//创建对象
        Random r = new Random();
    	//调用方法,随机生成无范围的一个整数
        int i = r.nextInt();
        System.out.println(i);
    }
```

```java
 public static void main(String[] args){
        Random r = new Random();
        for(int j = 0;j<100;j++){
            //随机获得一个0-9的数字，
            int i = r.nextInt(10);
            System.out.println(i);
        }
    }
```

#### 练习--猜数字小游戏

## 思路

你要猜一个数字，必须要先把数字给确定下来，也就是在这里，第一步要使用Random类来获取一个随机数

有了随机数，就可以猜了，让用户输入随机数，就要使用到API中的Scanner类

用户一般不可能一次猜中，所以就需要反复猜，这里就要用到while循环

猜一个数字有大了，小了，猜中了，三种结果，所以这里可以使用选择结构if语句



```java
import java.util.Random;
import java.util.Scanner;
//变量名rn是随机数的缩写，sn，是键盘录入数字的缩写
public class aGame{
    public static void main(String[] args) {
        Random aRandom = new Random();
        //获得一个随机整数
        int rn = aRandom.nextInt(101);
       // System.out.println(rn);//作弊大法
        Scanner aScanner = new Scanner(System.in);
        System.out.println("请输入一个0-100之间的整数.....");
        //用户输入的整数
        boolean mark = true;
        while (mark) {
            int sn = aScanner.nextInt();
            if (sn > rn) {
                System.out.println("输入的数字大了，请往小的方向猜吧");
            } else if (sn < rn) {
                System.out.println("输入的数字小了,请往大的方向猜吧");
            } else {
                System.out.println("恭喜你，猜对啦");
                mark = false;
            }
        }
        System.out.println("游戏结束，感谢参与!!!!!!!!!!!!!!");
    }

}
```

## ArrayList集合

ArrayList记得的长度是可以改变的，

```java
public static void main(String[] args){
    //创建一个ArrayList集合，集合的名称是list，里面装的全都是String字符串类型的数据
    //备注：从JDK1.7版本后，右侧的尖括号内容可以不行
    ArrayList<String> list = new ArrayList<>();
    System.out.println(list);//将会打印[]里的内容，如果没有内容，输出结果为  []
    //想集合当中添加数据，需要用到add方法;
    list.add("赵云");
    System.out.println(list);
}
```

#### ArrayList集合的常用方法和遍历

###### 常用方法有：

1. public boolean add(E e);向集合当中添加元素，参数类型和泛型类型一致
2. public E get(int index);从集合中获取元素，参数是索引编号，
3. public int size()，获取集合的尺度长度，返回值是集合包含的元素个数

4. public E remove(int index),从集合中删除元素，参数是索引编号，返回值是被删除的元素

   

```java
 public static void main(String[] args) {
        ArrayList<String> list = new ArrayList<>();
        //add方法的使用
        list.add("贾诩");
        list.add("周瑜");
        list.add("郭嘉");
        System.out.println(list);//[贾诩, 周瑜, 郭嘉]
        //从集合中获取元素，get方法，索引从0开始
        String aname = list.get(2);
        System.out.println(aname);//郭嘉
        //从集合中删除元素
        list.remove(1);
        System.out.println(list);//[贾诩, 郭嘉]
     	//获取集合的长度
     	System.out.println(list.size());//2
     	list.add("诸葛亮");
     	//集合的遍历
     	for(int i = 0;i<list.size();i++){
            System.out.println(list.get(i));
        }
    }
```

##### ArrayList集合存储基本数据类型

ArrayList集合是不能够存储基本类型的，如果要存储基本类型，必须使用基本类型对应的包装类

| 基本类型 |  包装类   |
| :------: | :-------: |
|   byte   |   Byte    |
|  short   |   Short   |
|   int    |  Integer  |
|   long   |   Long    |
|  float   |   Float   |
|  double  |  Double   |
|   char   | Character |
| boolean  |  Boolean  |

```java
public static void main(String[] args){
    ArrayList<Integer> list = new ArrayList<>();
    list.add(100);
    list.add(200);
    System.out.println(list);//[100, 200]
    //自动拆箱，包装类型变成基本类型
    System.out.println(list.get(0));//100
}
```

从JDK 1.5开始，支持自动装箱，自动拆箱

自动装箱:基本类型 ----->包装类型

自动拆箱:包装类型 ------>基本类型

ArrayList集合的练习1

##### 题目：生成6个1~33之间的随机整数，添加到集合，并遍历集合

我的解题思路:,

生成6个随机的整数，就要用到Random类，

把生成的整数添加到集合，就要创建一个集合，

使用集合方法add来添加都集合，所以到这里就会有aList.add(随机数)，这样就把随机数给添加到集合了，重复添加可以使用for循环

接下来就是遍历了

```java

import java.util.ArrayList;
import java.util.Random;

public class AArray {
    public static void main(String[] args) {
        Random aRandom = new Random();
        ArrayList<Integer> aList = new ArrayList<>();
        for(int i=0;i < 6 ;i++){
            aList.add(aRandom.nextInt(33)+1);
            System.out.println(aList.get(i));
        }
        System.out.println(aList);
    }
}
```

##### ArrayList练习二

###### 题目：自定义四个学生对象，添加到集合，并遍历

```java
public class Student {
    private int age;
    private String name;

    public Student(int age, String name) {
        this.age = age;
        this.name = name;
    }

    public Student() {
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}

```

```java
import java.util.ArrayList;

public class AStudent {
    public static void main(String[] args) {
        Student one = new Student(25,"貂蝉");
        Student two = new Student(26,"西施");
        Student three = new Student(27,"王昭君");
        Student four = new Student(28,"杨玉环");
        ArrayList<Student> arrayS = new ArrayList<>();
        arrayS.add(one);
        arrayS.add(two);
        arrayS.add(three);
        arrayS.add(four);
        for (int i=0;i<arrayS.size();i++ ){
            //使用get，获取对象出来
            Student stu = arrayS.get(i);
            //使用对象名.方法名来获取年龄和姓名，到这里就遍历结束
            System.out.println("年龄"+stu.getAge()+"..."+"姓名"+stu.getName());
        }

    }
}

```

##### ArrayList集合练习三

###### 题目：用一个大集合存入20个随机数字，然后筛选其中的偶数元素，放到小集合中

```java
import java.util.ArrayList;
import java.util.Random;
public class AArray {
    //题目：用一个大集合存入20个随机数字，然后筛选其中的偶数元素，放到小集合中
	public static void main(String[] args) {
    //大集合，存放20个随机数字
	ArrayList<Integer> big = new ArrayList<>();
    //小集合，存偶数
	ArrayList<Integer> small = new ArrayList<>();
	Random r = new Random();
	for(int i=0;i<20;i++) {
        //向大集合添加随机数，循环一次添加一个
		big.add(r.nextInt(20));
		}
	System.out.println(big);
	
	for(int i=0;i<big.size();i++) {
		int num = big.get(i);
		if(num%2==0) {
			//向小集合添加偶数
			small.add(num);
		}
	}
	System.out.println(small);
	
	}
}
```

###### 字符串概述和特点

**字符串的特点:**

1. 字符串的内容用不可变

2. 正是因为字符串不可以改变，所以字符串是可以共享使用的

3. 字符串效果上相当于是char[]字符数组，但是底层原理是byte[]字节数组

   

###### 字符串的构造方法和直接创建

 ```java
public static void main(String[] args){
		    //使用空参构造
		    String str1 = new String();
		    System.out.println("第一个字符串"+str1);
		    //根据字符数组创建字符串
		    char[] charArray = {'A','B','C'};
		    String str2 = new String(charArray);
		    System.out.println("第二个字符串"+str2);
		    //根据字节数组创建字符串
		    byte[] byteArray = {97,98,99};
		    String str3 = new String(byteArray);
		    System.out.println("第三个字符串"+str3);
		    //直接创建
		    String  str4 = "Hello";
		    System.out.println("第四个"+str4);
		}
 ```

###### 字符串的常量池

字符串常量池，程序当中直接写上的双引号字符串，就在字符串常量池当中



对于基本类型来说 ==是进行数值的比较

对于引用类型来说 ==是进行地址的比较

```java
public static void main(String[] args){
		String str1 = "abc";//地址存在常量池中
		String str2 = "abc";//地址存在常量池
		char[] charArray = {'a','b','c'};
		String str3 = new String(charArray);//地址不再常量池中
		System.out.println(str1 == str2);//true
		System.out.println(str1 == str3);//false
		System.out.println(str2 == str3);//false
		
	}
```

###### 字符串比较的相关方法

```java
public static void main(String[] args){
	    String str1 = "hello";
	    String str2 = "hello";
	    char[] charArray = {'h','e','l','l','o'};
	    String str3 = new String(charArray);
	    //equals比较的是两个字符串的内容
	    System.out.println(str1.equals(str2));//true
	    System.out.println(str2.equals(str3));//true
	    System.out.println(str3.equals("hello"));//true
 //忽略大小写的比较方法equalsIgnoreCase
 System.out.println(str3.equalsIgnoreCase("Hello"));//true
 
	}
```

字符串的获取相关方法

```java
public static void main(String[] args){
	   //获取字符串的长度;
		int length = "wertrghgffdvscsegh".length();
		System.out.println("字符串的长度是 "+length);
		
		//拼接字符串
		String str1=  "hello";
		String str2 = "world";
		String str3 = str1.concat(str2);
		System.out.println(str3);
		
		//获取指定索引位置的单个字符
		char ch = "hello".charAt(1);
		System.out.println("在1号索引位置的字符是"+ch);
		
		//查找参数字符串在本来字符串当中出现的第一次索引位置
		//如果没有返回-1
		String original = "helloworld";
		int i =original.indexOf("llo");
		System.out.println("第一次出现的索引位置是"+i);
	}
```

###### 字符串的转换相关方法

```java
public static void main(String[] args){
		//把字符串转换成字符数组
	   char[] chars = "原乘风破万里浪".toCharArray();
	   for(int i=0;i<chars.length;i++) {
		   System.out.println(chars[i]);
	   }
	   //把字符串转换成字节数组
	   String str = "甘面壁读是十年书";
	   byte[] bytes = str.getBytes();
	   for(int i=0;i<bytes.length;i++) {
		   System.out.println(bytes[i]);
	   }
	   //字符串的内容替换
	   String str3 = "风声雨声读书声声声入耳";
	   String str4 = str3.replace("声", "sheng");
	   System.out.println(str4);
    	//字符串的切割方法,返回一个string[]
	   String[] str5 =str3.split("声");
	   for(int i=0;i<str5.length;i++) {
		   System.out.println(str5[i]);
	   }
	}
```

