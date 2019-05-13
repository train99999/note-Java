# 笔记-7天学完Java基础之0/7

## 1.常用命令提示符（cmd）

**启动：**Win+R，输入cmd​ :twisted_rightwards_arrows: cmd

###### 

**切换盘符** 盘符名称+:(冒号为英文输入法下的冒号)

![img](https://note.youdao.com/yws/public/resource/4a4b841afdfb484341fb9d67b50f9d4f/xmlnote/D9D77830F41B4CCDAC91FE9FE62FD4D0/371)

**进入指定文件夹** cd +文件夹名称

![img](https://note.youdao.com/yws/public/resource/4a4b841afdfb484341fb9d67b50f9d4f/xmlnote/895418A5E037432A85E7ED000FBFFC17/374)



**注意只能够进入文件夹，不能够进入文件哦**

![img](https://note.youdao.com/yws/public/resource/4a4b841afdfb484341fb9d67b50f9d4f/xmlnote/16DAD06B8EE144DABA877B9024379949/377)

![img](https://note.youdao.com/yws/public/resource/4a4b841afdfb484341fb9d67b50f9d4f/xmlnote/B75134D078E9482AB2B8EDAF3E8C9EFC/379)

**查看当前文件夹下的目录** dir

![img](https://note.youdao.com/yws/public/resource/4a4b841afdfb484341fb9d67b50f9d4f/xmlnote/A1E6CDE90132478D9422FCAE302ED410/385)

**返回上一级** cd..

![img](https://note.youdao.com/yws/public/resource/4a4b841afdfb484341fb9d67b50f9d4f/xmlnote/BD209BB6D5F44E46A98AEE15299D03F1/381)

**直接返回根路径** cd \



![img](https://note.youdao.com/yws/public/resource/4a4b841afdfb484341fb9d67b50f9d4f/xmlnote/90143730434247B1A65B84B5F8ECAACF/383)



清屏 cls:自己直接输入就可以了，不再演示

退出命令行（cmd） exit：自己直接输入就可以了，不再演示

如果嫌命令行进入指定目录太麻烦的话，可以按照下图的方法快速指定目录的命令行



![img](https://note.youdao.com/yws/public/resource/4a4b841afdfb484341fb9d67b50f9d4f/xmlnote/5B62BEBCCFE24C7EBD38EA532BBD5525/390)

![img](https://note.youdao.com/yws/public/resource/4a4b841afdfb484341fb9d67b50f9d4f/xmlnote/B46B7905F851440EA4360E93192FD903/392)

## 2.JDK和JRE的关系

JDK（Java Development kit）是Java程序开发工具包

JRE(Java Runtime Environment)是Java程序的运行时环境

![img](https://note.youdao.com/yws/public/resource/4a4b841afdfb484341fb9d67b50f9d4f/xmlnote/6A46D387EB0D414082B85A1ECC27899B/387)

如果想要运行Java程序的话安装JRE就可以了，想开发并且运行的话就要安装JDK

## 标识符

**标识符：**是指在程序中，我们自己定义的内容，比如类的名字，方法的名字，变量的名字等等，

**标识符命名规则：**可以包含英文字母，数字，$（美元符号）和_(下划线)但不可以数字开头，也不可以时关键字，建议类的命名规范使用大驼峰式（**首字母大写**，后面每一个单词首字母也是大写）变量名和方法名的命名规范使用小驼峰式（**首字母小写**，后面每个单词首字母大写）

## 数据类型转换

数据范围大的变成小的需要使用强制类型转换，但是会损失精度，发生数据溢出

数据类型小的会自动转换成数据类型大的

![img](https://note.youdao.com/yws/public/resource/4a4b841afdfb484341fb9d67b50f9d4f/xmlnote/1B1AA1E1238A4CBFADDD5421C75A5086/394)

> int+double--->double+double在这里int自动转换成了double类型
>
> 对于byte/short/char三种类型来说，如果右侧赋值的数值没有超过范围那么javac编译器将会自动隐含地为我们补上一个（byte）（short）（char）的强类型转换



## 自增自减运算符

前面有++就立刻马上自增1，后面有++就等一下在自增1

```java
public static void main(String[] args){
		int i = 5;
		System.out.println(++i);//先自增1然后再打印结果----->5+1=6
		System.out.println(i++);//先打印出结果，然后再自增1----->直接打印6，然后再加1
		System.out.println(i);//这个就是i++后的结果
	}
```

![img](https://note.youdao.com/yws/public/resource/4a4b841afdfb484341fb9d67b50f9d4f/xmlnote/50073D1E33844CE48E76AD485819FC6F/398)

**注意常量不能自增**

## 逻辑运算符

与（并且）  && 全部是true，才是true；否则就是false

或（或者） || 至少有一个true，就是true，全部是false，才是false

非（取反） ！ 本来是true，变成false，本来是false，变成true

```java
System.out.println(true && false);//打印输出结果为false
System.out.println(true || false);//打印输出结果为true
System.out.println(!true);//打印输出结果为false
```

## 三元运算符

**格式**

数据类型  变量名称  =  条件判断  ？  表达式A ：表达式B；

![img](https://note.youdao.com/yws/public/resource/4a4b841afdfb484341fb9d67b50f9d4f/xmlnote/07BDB0B75B9E48199FFCAA66E666D1D5/401)



## 选择结构if语句

```java
/*

1. if语句第一张格式**
	//表达式成立就执行语句体；否则跳过
   if(关系表达式){

   语句体；

   }

2. **if语句第二种格式**
	//表达式成立，执行语句体1；否则执行语句体2；
   if(关系表达式){

   语句体1；

   }else{

   语句体2；

   }

3. **if语句第三种格式**
	//那个判断条件成立执行那个，然后剩下的跳过，不执行，
	//如果条件都不成立，则执行语句n；
   if（判断条件1）{

   语句1；

   }else if（判断条件2）{

   执行语句2；

   }else if（判断条件n）{

   执行n；

   }else{

   执行语句n；

   }
*/
```



## 选择结构Switch穿透语句

```java

import java.util.Random;
public class ASwitch{
	public static void main(String[] args){
		
		System.out.println("无名小卒：报 主公 上将潘凤率领八十万大军前来攻打我军");
		
		System.out.println("刘备：请问军师该怎么办？哪一位将军可以迎战呢");
        
		System.out.println("诸葛亮：容我卜上一卦");
        
		Random r = new Random();
		int i = r.nextInt(5);//生成0-4之间的整数
		
		switch(i){
			case 0:
				System.out.println("我是大哥刘备"+"字玄德"+"奉军师之命前来应战");
                //如果没有break，则会一直穿透下去
				break;
			case 1:
				System.out.println("我是二哥关羽"+"字云长"+"奉主公之命前来应战");
				break;
			case 2:
				System.out.println("我是三弟张飞"+"字翼德"+"奉主公之命前来应战");
				break;
			case 3:
				System.out.println("我是诸葛亮"+"字孔明"+"奉主公之命前来应战");
				break;
			default:
				System.out.println("吾乃常山赵子龙"+"奉主公之命前来应战");
				break;
		}
	}
}
```

## 循环结构

**for循环**

1. 初始化语句：在循环开始最初执行，而且只能做唯一一次

2. 条件判断：如果成立，则循环继续，如果不成立，则循环退出

3. 循环体：重复要做的事情内容，若干行语句

4. 步进语句：每次循环之后都要进行的扫尾工作。

   ​	

   ```java
   for(初始化表达式；布尔表达式；步进表达式）{
       循环体
   }
   ```

   **while标准格式**

1. while(条件判断){

循环体

}

2. **while******扩展格式****：

初始化语句；

while（条件判断）{

循环体；

步进语句；

}

3. do-while循环的标准格式:

do{

循环体

}while（条件判断）

下面用这些循环来求一下1-100之间奇数偶数的和

```java
//这个是用for循环搭配if结构语句来做的
public class ForXunHuan{
	public static void main(String[] args){
		int evenSum = 0;
		int oddSum = 0;
		for(int i=1;i<=100;i++){
			if(i % 2 == 0){
				evenSum = evenSum +i;
			}else{
				oddSum = oddSum+i;
			}
		}
		System.out.println("偶数和是"+evenSum);
		System.out.println("奇数和是"+oddSum);
	}
}
```

```java
//这个是while循环
public class WhileXunHuan{
	public static void main(String[] args){
		int eventSum = 0;
		int oddSum = 0;
		int i = 1;
		while(i<=100){
			if(i % 2 == 0){
			 eventSum= eventSum + i;
			}else{
				oddSum = oddSum + i;
			}
			i++;
		}
		System.out.println("while的偶数和是"+eventSum);
		System.out.println("while的奇数和是"+oddSum);
	}
}
```

这个是我敲的错误，代码敲的不够多的原因吧！！！！

![img](https://note.youdao.com/yws/public/resource/4a4b841afdfb484341fb9d67b50f9d4f/xmlnote/28B1B8767F5A4998A109F957CB331B05/417)



do...while循环也是大同小异就不再演示了

## 条件控制语句

**break控制语句**

1. 可以用在switch语句当中，一旦执行，整个switch语句立刻结束
2. 还可以用在循环语句中，一旦执行，整个循环语句立刻结束，打断循环

关于循环的选择，凡是次数确定的多用for循环，否则用while循环。

```java
//在for循环中使用break退出for循环
public class BreakXunHuan{
	public static void main(String[] args){
		for(int i=1;i<=10;i++){
			if(i == 5){
				break;
			}
			
			System.out.println("乘风破浪会有时，直挂云帆济沧海");
		}
	}
}
```

![img](https://note.youdao.com/yws/public/resource/4a4b841afdfb484341fb9d67b50f9d4f/xmlnote/D589A37A03CC4F319D09EE52C70B7FF8/419)

**continue控制语句**

程序一旦遇到continue，就立刻马上跳过当次循环剩余的内容，马上开始下一次循环。如果没有下一次循环，程序就结束了，

break和continue的区别用通俗的话讲就是break打断全部循环，continue打断一次循环。

```java

public class ContinueXunHuan{
	public static void main(String[] args){
		for(int i=1;i<=10;i++){
			if(i == 4){
				continue;
			}
			
			System.out.println("乘风破浪会有时，直挂云帆济沧海");
		}
	}
}
```

![img](https://note.youdao.com/yws/public/resource/4a4b841afdfb484341fb9d67b50f9d4f/xmlnote/E7014E4C87804D77BD68A5834BB11333/423)

**for循环的嵌套**

```java
//三重for循环的嵌套，电脑已经爆炸了
public class QianTaoXunHuan{
	public static void main(String[] args){
		for(int i=0;i<24;i++){
			
			for(int j=0;j<60;j++){
				
				for(int k=0;k<60;k++){
					
					System.out.println(i+"点"+j+"分"+k+"秒");
				}
			}
			
		}
	}
}
```

