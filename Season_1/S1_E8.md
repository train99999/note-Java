Object类的toString方法

类Object是类层次结构的根类

每个都使用Object作为超类

所有对象都实现这个类的方法

```java
//这个是Object类的子类，实现了其所有方法
public class Person{
	private String name;
	private int age;
	
	public Person(){}
	public Person(String name,int age){
	this.name=name;
	this.age=age;
	}
	
	public void setName(String name){
	this.name = name;
	}
	public String getName(){
	return name;
	}
	
	public void setAge(int age){
	this.age = age;
	}
	public int getAge(){
	return age;
	}
	//重写toString方法
	//重写参数列表要与父类参数列表相同
	public String toString(){
		
		String string = "{name="+name+"   age="+age+"}";
		return string;
		
	}
	
}
```

```java
public class PersonDemo{
	public static void main(String[] args){
	Person person = new Person("李白",22);
	//直接打印对象，打印出来的是地址值
	System.out.println(person);//Person@3b192d32
	//没有重写父类的toString方法打印出来的也是地址值
	String s = person.toString();
	System.out.println(s);//Person@3b192d32
	//现在重写了toString方法，
	person.toString();//{name=李白   age=22}
	
	}
}
```

````java
//这个是Object类的子类，实现了其所有方法
public class Person{
	private String name;
	private int age;
	
	public Person(){}
	public Person(String name,int age){
	this.name=name;
	this.age=age;
	}
	
	public void setName(String name){
	this.name = name;
	}
	public String getName(){
	return name;
	}
	
	public void setAge(int age){
	this.age = age;
	}
	public int getAge(){
	return age;
	}
	
}
````

Object类的equals方法

````java
public class PersonDemo{
	public static void main(String[] args){
	Person p1 = new Person("李白",22);
	Person p2 = new Person("苏轼",23);
	//直接打印对象，打印的其实就是地址值
	System.out.println(p1);
	System.out.println(p2);
	//Object类的方法equals
	//equals源码
	//boolean	equals​(Object obj)	  Indicates whether some other object is "equal to" this one.
	
	/*public boolean equals(Object obj) {
        return (this == obj);
    }*/
	
	boolean b = p1.equals(p2);
	System.out.println(b);
	}
}public class PersonDemo{
	public static void main(String[] args){
	Person p1 = new Person("李白",22);
	Person p2 = new Person("苏轼",23);
	//直接打印对象，打印的其实就是地址值
	System.out.println(p1);
	System.out.println(p2);
	//Object类的方法equals
	//equals源码
	//boolean	equals​(Object obj)	  Indicates whether some other object is "equal to" this one.
	
	/*public boolean equals(Object obj) {
        return (this == obj);
    }*/
	
	boolean b = p1.equals(p2);
	System.out.println(b);
	}
}
````

### 日期时间类 Date类

```java
public class DemoDate{
	public static void main(String[] args){
		long l =System.currentTimeMillis();//获取从1970年1月1日到今天经历了多少毫秒
		System.out.println(l);
		//把毫秒值变成天数
		long  day = 24*60*60*1000;
		long aday = l/day;
		System.out.println(aday);//18036
		//把天数转化成年
		System.out.println(aday/365);//1970年距今49年
	}
}
```

Date类的构造方法和成员方法

```java
import java.util.Date;
public class DateClass{
	public static void main(String[] args){
	Date date = new Date();
	//Date的空参数构造方法会返回系统当前的日期和时间
	System.out.println(date);
	Date date1 = new Date(100000000L);
	//date有参构造方法将会把传递进来的数值转换成日期
	System.out.println(date1);
	
	System.out.println(method());
	}
	//获取毫秒值
	public static long method(){
		
		Date date = new Date();
		return date.getTime();
	}
}
```

DateFormat类的format方法和parse方法

```java
import java.text.*;
import java.util.*; 
public class DemoDateFormat{
	public static void main(String[] args) throws ParseException{
		method2();
	}
	
	
	public static void method(){	//首先创建DateFromat子类SimpleDateFormat对象
	//并且创建对象是使用构造方法指定格式
	SimpleDateFormat sdf = new SimpleDateFormat("yyyy年MM月dd日 HH时mm分55秒");
	//调用方法format，调用方法是需要传递Date类
	
	Date date = new Date();
	System.out.println(date);
	String str = sdf.format(date);
	System.out.println(str);
	}
	public static void method2() throws ParseException{
		SimpleDateFormat sdf = new SimpleDateFormat("yyyy年MM月dd日 HH时mm分55秒");
		Date date = sdf.parse("2019年05月20日 15时21分55秒");
		System.out.println(date);
	}
}
```

```java
import java.util.*;
import java.text.*;
//计算一个人活了多久
public class Survival{
	public static void main(String[] args) throws ParseException{
	System.out.println("让我们来帮你算算你活了多久");
	System.out.println("请按照"+" yyyy-MM-dd"+" 格式输入你的出生日期吧");
	Scanner sc = new Scanner(System.in);
	String birth = sc.next();
	//现在要把出生日期字符串，解析成Date格式
	//需要与出生日期的格式一样，否则会解析异常
	SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd");
	//需要一个指定格式的字符串格式
	Date date = sdf.parse(birth);
	//把日期转换成毫秒值
	long ms = date.getTime();
	//获取当前日期，转换成毫秒值
	long todayTime = new Date().getTime();
	long newMs = todayTime-ms;
	long newDay = newMs/1000/60/60/24;
	System.out.println(newDay);
	}
}
```

Calendar类的常用成员方法

1. public int get( int field ):返回给定日历字段的值
2. public void set （int field ，int value）:将给定的日历字段设置为给定值
3. public abstract void add( int field ,int amount):根据日历的规则，为给定的日历字段添加或减去指定的时间量
4. public Date getTime();返回一个表示此Calendar时间值的Date对象

````java
import  java.util.*;
public class CalendarDemo{
	public static void main(String[] args){
	//public int get(int field):返回给定日历字段的值
	//参数：传递指定的日历字段（YEAR,MONTH....）
	//返回值：日历字段代表的具体的值
	//getInstance是一个比较特殊的方法
	//他会返回一个Calendar的子类
	Calendar c = Calendar.getInstance();
	int year = c.get(Calendar.YEAR);//获取当前系统的年份
	int month = c.get(Calendar.MONTH);
	int day = c.get(Calendar.DAY_OF_MONTH);
	System.out.println("年:"+year+" 月:"+month+" 天:"+day);
	System.out.println("====================================");
	
	c.set(Calendar.YEAR,2520);
	c.set(Calendar.MONTH,5);
	c.set(Calendar.DATE,20);
	
	
	int year1 = c.get(Calendar.YEAR);//获取当前系统的年份
	int month1 = c.get(Calendar.MONTH);
	int day1 = c.get(Calendar.DAY_OF_MONTH);
	System.out.println("年:"+year1+" 月:"+month1+" 天:"+day1);
     //增加年的方法也是一样的
	//c.add(Calendar.YEAR,2);
	//c.add(Calendar.MONTH,3);
     //把日历对象变成日期对象的方法
     //c.getTime();这个方法将返回日期
	}
}
````

### System类

System类提供了大量的静态方法，可以获取与系统相关的信息或系统级操作，在System类的API文档中，常用方法有：

public static long currentTimeMillis():返回以毫秒为单位的当前时间

public static void arraycopy([Object](https://docs.oracle.com/javase/10/docs/api/java/lang/Object.html) src, int srcPos,[Object](https://docs.oracle.com/javase/10/docs/api/java/lang/Object.html) dest, int destPos, int length):将数组中指定的数据拷贝到另一个数组中 ;

````java
import  java.util.*;
public class ArrayDemo{
	public static void main(String[] args){
	int[] src = {1,2,3,4,5};
	int[] dest = {6,7,8,9,10};
	System.out.println("复制前:" +Arrays.toString(dest));
	System.arraycopy(src,0,dest,0,3);
	System.out.println("复制后："+ Arrays.toString(dest));
	
	}
}
````

### StringBuilder类

字符串缓冲区，可以提高字符串的操作效率（可以看成一个长度可以变化字符串）

```java
//StringBuilder的构造方法
public class StringBuilderDemo{
	public static void main(String[] args){
	//空参数构造方法，其中没有字符，初始字符容量为16
	StringBuilder sb = new StringBuilder();
	System.out.println(sb+"羌笛何须怨杨柳，春风不度玉门关，");
	//有参数的构造方法，字符内容为指定的内容
	StringBuilder sb1 = new StringBuilder("云想衣裳花想容，春风拂槛露华浓");
	System.out.println(sb1);
	}
}
```

```java
//StringBuilder的常用方法
public class StringBuilderDemo2{
	public static void main(String[] args){
	StringBuilder sb = new StringBuilder();
	//这里吧sb的地址值赋值给了sb1
	StringBuilder sb1 = sb.append("云想衣裳花想容，春风拂槛露华浓。");
	System.out.println(sb);
	System.out.println(sb1);
	System.out.println(sb==sb1);
	
	//链式编程
	StringBuilder libai =sb.append("若非群玉山头见").append("，会向瑶台月下逢。").append("----清平调").append(".李白");
	System.out.println(libai);
//云想衣裳花想容，春风拂槛露华浓。若非群玉山头见，会向瑶台月下逢。----清平调.李白
	}
}
```

```java
//String与StringBuilder的相互转换
public class StringBuilderDemo3{
	public static void main(String[] args){
	//String--->StringBuilder
	String str = "云想衣裳花想容";
	System.out.println(str);
	StringBuilder sb = new StringBuilder(str);
	sb.append("  春风拂槛露华浓");
	System.out.println(sb);
	
	//StringBuilder-->Strintg
	String sb2 = sb.toString();
	System.out.println(sb2+"  若非群玉山头见，会向瑶台月下逢");

	}
}
```

```java
/*包装类：
	基本数据类型，使用起来非常方便，但是没有对应的方法来操作这些基本类型的数据，可以使用一个类，把基本类型的数据装起来，在类中定义一些方法，这个类叫做包装类，我们可以使用类的方法来操作这些基本类型的数据
*/
```

```java
/*装箱：把基本类型的数据，包装到包装类中(int-->Integer)
	Integer类的构造方法
	Integer​(int value)	
	构造一个新分配的Integer对象，他表示指定的int值
	Integer​(String s)	
	构造一个新分配的Integer 对象，他表示Stirng参数所指示的值
	传递的字符串必须是基本类型的字符串
	
	静态方法：
		Integer valueOf(int i)返回一个表示指定的 int值的 Integer
		Integer valueOf（String s）
		
		
	拆箱：在包装类中取出基本类型 int intValue();
	*/
public class IntegerDemo{
	public static void main(String[] args){
	//装箱，先使用构造方法装箱
	Integer integer = new Integer(5);//传递int值，完成装箱
	//装箱，第二张方式
	Integer integer2 = new Integer("10");//传递基本类型的字符串
	System.out.println(integer);//重写了toString
	System.out.println(integer2);//重写了toString
	//第三种方式装箱
	Integer integer3 = Integer.valueOf(1);
	Integer integer4 = Integer.valueOf("2");
	System.out.println(integer3);
	System.out.println(integer4);
	
	//拆箱
	int i = integer3.intValue();
	System.out.println(i);
	
	
	}

}




```

```java
//自动拆箱与自动装箱
Integer in = 1; //发生了自动装箱Integer in = new Integer(1);

//int  in = in+2;//发生了自动拆箱
```

Integer类可以把基本类型的字符串变成int类型，也可以把int类型变成字符串类型