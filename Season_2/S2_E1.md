#### Collection集合

数组的长度是固定的，集合的长度是可变的

数组中存储的是同一类型的元素，可以存储基本数据类型值。集合存储的都是对象。而且对象的类型可以不一致。

#### 集合框架

![img](https://s2.ax1x.com/2019/05/21/EzalLj.png)

```java
import java.util.Collection;
import java.util.ArrayList;
//Collection的常用方法
public class CollectionDemo{
	public static void main(String[] args){
	//Collection是一个接口无法创建对象，可以使用多态来使用方法
	Collection<String> collection = new ArrayList<>();
	//add方法，向集合添加元素
	collection.add("李白");
	//collection.add(String);不可以添加非指定的类型，
	collection.add("苏轼");
	collection.add("杜甫");
	collection.add("王安石");
	collection.add("李清照");
	System.out.println(collection);
	//remove方法，返回值类型是boolean，把给定的对象删除
	//collection.remove("林黛玉");
	//System.out.println(aremove);没有则返回false
	collection.remove("李清照");
	//判断当前集合中是否包含了给定的对象，返回值类型为boolean
	boolean acontains = collection.contains("李清照");
	System.out.println(acontains);//false
	//size,返回集合中元素的个数
	int asize = collection.size();
	System.out.println(asize);//4
	//isEmpty,判断集合是否为空，集合是空，返回true，不是空返回false
	boolean aisEmpty = collection.isEmpty();
	System.out.println(aisEmpty);//false
	//toArray,把集合中的元素，存储到数组中,返回值类型为Object[]数组
	Object[] atoArray = collection.toArray();
	//遍历数组
	for(int i=0;i<atoArray.length;i++){
		System.out.println(atoArray[i]);
	}
	//清空数组clear
	collection.clear();
	System.out.println(collection);
	}

}
```

#### Iterator接口

Iterator接口有两个常用的方法

> boolean hasNext() 如果仍有元素可以迭代，则返回true 用来判断集合中还有没有下一个元素，

> E next() 返回迭代的下一个元素
>
> 取出集合中的下一个元素

### Iterator迭代器，是一个接口，无法直接使用，获取Iterator接口实现类的对象,可以通过Collection接口中的方法iterator（）；这个方法返回的就是迭代器的实现类对象



> 迭代器的使用步骤：
>
> 1.使用Collection集合中的方法iterator()获取迭代器的实现类对象，使用Iterator接口来接收
>
> 2.使用Iterator接口中的方法hasNext判断还有没有下一个元素
>
> 3.使用Iterator接口中的方法next取出集合的下一个元素

```java
import java.util.*;
public class IteratorDemo{
	public static void main(String[] args){
	//可以使用多态来使用这个方法
	Collection<String> collection = new ArrayList<>();
	collection.add("李商隐");
	collection.add("李清照");
	collection.add("王安石");
	collection.add("苏轼");
	collection.add("白居易");
	//使用迭代器取出集合中的元素
	//首先要获得一个Iterator的实现类，可以使用方法iterator来获取
	Iterator<String> aIterator = collection.iterator();
	//判断集合有没有元素
	while(aIterator.hasNext()){
	String str = aIterator.next();
	System.out.println(str);
	}
	}
}
```

#### 增强for循环

Collection接口继承了Iterable接口，是JDK1.5之后出现的新特性。

格式

> for(集合   变量名   ： 集合名){}

```java
import java.util.*;
public class ForeachDemo{
	public static void main(String[] args){
	ArrayList<String> arraylist = new ArrayList<>();
	arraylist.add("云想衣裳花想容， ");
	arraylist.add("春风拂槛露华浓。 ");
	arraylist.add("若非群玉山头见，");
	arraylist.add("会向瑶台月下逢。 ");
	
	for(String a : arraylist){
		System.out.println(a);
	}
	}
}
```

### 泛型

泛型是一种未知的数据类型

定义含有泛型的类

```java
public class GenericDemo<E>{
	private E e;
	
	public void setName(E e){
		this.e = e;
	} 
	
	public E getName(){
		return e;
	}
}
```



```java
public class GenericDemoa{
	public static void main(String[] args){
	GenericDemo<String> gd = new GenericDemo<>();
	gd.setName("李白");
	String str = gd.getName();
	System.out.println(str);
	}
}
```

```java
//定义含有泛型的方法
public class GenericDemob{
	public <E> void method1(E e){
		System.out.println(e);
	}
	
	public static <E> void method2(E e){
		System.out.println(e);
	}
}
```

```java
public class GenericDemoc{
	public static void main(String[] args){
	GenericDemo1 gd1 = new GenericDemo1();
	gd1.method1(123);
	gd1.method1("云想衣裳花想容");
	gd1.method1(8.8);
	
	GenericDemo1.method2("春风拂槛露华浓");
	}
}
```

泛型通配符

```java
public static void main(String[] args){
    
     Collection<Integer> list1 = new ArrayList<Integer>();
     Collection<String> list2 = new ArrayList<String>();
     Collection<Number> list3 = new ArrayList<>(Number);
     Collection<Object> list4 = new ArrayList<Object>();
    /*
    类与类之间的继承关系 Integer extends Number extends Object
    
    String extends Objects
    */
    getElement1(list1);//编译通过，是Number的子类
    getElement1(list2);//报错,不是Number的子类
    getElement1(list3);//编译通过，是Number本身
    getElement1(list4);//报错，不是Number的子类
    
    getElement2(list1);//报错
    getElement2(list2);//报错
    getElement2(list3);
    getElement2(list4);{
}
    //泛型的上限：此泛型？，必须是Number类型或者Number类型的子类
public static void getElement1(Collection<? extends Number> coll){}
   //泛型的下限：此泛型？ ，必须是Number类型或者Number类型的父类 
public static void getElenment2(Collection<? super Number> coll)
```

做了一个斗地主的游戏，这个案例分析是看视频的，看完分析后，代码是我自己写的，写的好差，想的也久，写了2个小时了吧，终于完成了

```java
package demo12;

import java.util.ArrayList;
//做一个斗地主的游戏，有3个玩家，一个底牌
public class doudizhu {
    public static void main(String[] args) {
        //创建玩家集合，包含了底牌
        Players aplayers = new Players();
        //这个集合用来装54张牌
        ArrayList<String> pokerArray = new ArrayList<>();
        //这个集合用来装牌的颜色，装好了之后，要跟牌的号码进行组合
        ArrayList<String> color = new ArrayList<String>();
        color.add("♠");
        color.add("♥");
        color.add("♣");
        color.add("♢");
        //这个集合用来装扑克牌的数字
        ArrayList<String> number = new ArrayList<String>();
        number.add("2");
        number.add("A");

        //生成扑克牌
        for (int i = 2; i < 13; i++) {
            int j = i + 1;
            String str = j + "";
            number.add(str);
        }
        for (int i = 0; i < color.size(); i++) {
            for (int j = 0; j < number.size(); j++) {
                String str1 = color.get(i) + number.get(j);
                pokerArray.add(str1);
            }
        }
        //把大小王添加到pokerArray集合中去，到这里牌生成完毕
        pokerArray.add(0, "大王");
        pokerArray.add(1, "小王");
        //传递集合
        aplayers.play(pokerArray);
    }

}

```

```java

import java.util.ArrayList;
import java.util.Collections;

public class Players {
    public void play(ArrayList<String> arrayList) {
        //把传进来的集合打乱排序
        Collections.shuffle(arrayList);
        //玩家的集合
        ArrayList<String> player1 = new ArrayList<String>();
        ArrayList<String> player2 = new ArrayList<String>();
        ArrayList<String> player3 = new ArrayList<String>();
        ArrayList<String> player4 = new ArrayList<String>();
        //发牌
        for(int i=0;i<arrayList.size();i++) {
            //为什么要减三，因为要把三张牌添加到底牌去，把索引51,52,53的牌添加到底牌去
            if(i%3==0&&i<arrayList.size()-3){
                String p1=arrayList.get(i);
                player1.add(p1);
            }else if(i%3==1&&i<arrayList.size()-2){
                String p2 =arrayList.get(i);
                player2.add(p2);
            }else if(i%3==2&&i<arrayList.size()-2){
                String p3 = arrayList.get(i);
                player3.add(p3);
            }else{
                String p4 = arrayList.get(i);
                player4.add(p4);
            }
        }
        //显示牌
        System.out.println(player1);
        System.out.println(player2);
        System.out.println(player3);
        System.out.println(player4);
    }
}

```

#### 数据机构

栈：先进后出，只有一个入口和出口

![img](https://s2.ax1x.com/2019/05/21/VSLmvV.png)

队列：先进先出，一个入口，一个出口![img](https://s2.ax1x.com/2019/05/21/VSOIeO.png)

数组：数组中的地址是连续的  ，可以直接根据索引值查询，，查询快，增删慢

链表：查询慢：链表中的地址不是连续的，每次查询都必须从头开始查询

增删快：链表结构，增加或删除一个元素，对链表的整体结构没有影响，所以增删快

红黑树:查询速度非常快

## List集合

`

```java
import java.util.*;
//List集合继承自Collection接口
//List集合是一个有序的集合，存进去的是1，2，3取出来的也是1，2，3
//List集合可以存储重复的元素
//List集合是一个带索引的集合
public class ListDemo{
	public static void main(String[] args){
	//看一看List集合的常用方法吧
	//List集合是一个接口需要使用多态来调用其方法
	List<String> aList = new ArrayList<>();
	aList.add("云想衣裳花想容, ");
	aList.add(" 春风拂槛露华浓。");
	aList.add("若非群玉山头见， ");
	//将指定的元素，添加都改集合中的指定位置上
	aList.add(3,"会向瑶台月下逢。 ");
	//返回集合中指定位置的元素
	String str1 = aList.get(0);
	System.out.println(str1);
	//移除列表中指定位置的元素，返回的是被移除的元素
	String str2 = aList.remove(1);
	System.out.println(str2);
	//用指定元素替换集合中指定位置的元素，返回值的更新前的元素
	String str3 = aList.set(1,"春风不度玉门关");
	System.out.println(str3);
	System.out.println(aList);//[云想衣裳花想容, , 春风不度玉门关, 会向瑶台月下逢。 ]
	
	
	//遍历集合
	for(int i = 0;i<aList.size();i++){
		String str = aList.get(i);
		System.out.println(str);
	}
	
	//迭代器List集合的iterator方法会返回一个Iterator接口的实现类
	Iterator<String> iterator = aList.iterator();
	//先判断有没有下一个元素
	while(iterator.hasNext()){
		String str5 = iterator.next();
		System.out.println(str5);
	}
	
	for(String s : aList){
		System.out.println(s);
	}
	
	

	
	
	
	
	}
}
```

List集合的子类

ArrayList集合：元素增删慢，查找快，看用于查询数据，遍历数据

LinkedList集合：

> LinkedList集合的常用方法
>
> addFirst(E e);将指定元素插入列表开头
>
> addLast(E e);将指定元素添加到列表结尾
>
> push（E e）；将元素推入次列表所表示的堆栈，相等于addFirst
>
> getFirst();返回次列表的第一个元素
>
> getLast();返回此列表的最后一个元素
>
> removeFirst();移除此列表的第一个元素
>
> removeLast（）；移除此列表的最后一个元素
>
> pop();等效于removeFirst
>
> isEmpty();判断集合是否包含元素，有则返回false，没有则true

#### 