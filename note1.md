## 方法重载

```java
package cn.itcat.day04.demo01;

//方法重载就是参数个数不同，参数类型不同，参数类型的顺序不同
//方法重载与参数名称无关，与方法返回值类型无关
//方法重载方法名称都相同
public class OverloadDemo {
    public static void main(String[] args) {
        
    }
	//没有参数的方法
    public static void aPrint() {
        System.out.println("我是无参数的方法");
    }
	//比上一个方法多了一个参数
    public static void aPrint(int i) {

        System.out.println("我的参数类型是int类型" + "   " + i);
    }
	//与上一个方法参数类型不同
    public static void aPrint(String str) {
        System.out.println("我的参数类型是String类型" + "   " + str);
    }
	//与上一个方法返回值类型不同，参数类型不同，参数个数不同
    public static int aPrint(double i, int j) {
        int sum = (int) i + j;
        System.out.println("你调用的是具有一个是double类型的参数一个是int类型的参数并且他们两个的和是" + sum);
        return sum;
    }
}

```

## 数组

数组跟变量差不多，变量是存储单个数据的，数组是一种容器，可以同时存储多个数据值

**数组的特点**

1. 数组是一种引用数据类型
2. 数组当中的多个数据，类型必须统一
3. 数组的长度在程序运行期间不可以改变

**使用数组的步骤**

1. 数组初始化，在内存当中创建一个数组，并向其中赋予默认值

   两张常见的初始化方式：

   1. 指定长度的叫做动态初始化

      ```java
      //  存储的是什么样的数据类型 我是数组 我的名字  代表创建数组的动作  		代表可以存储多少个数据
      //格式：   数据类型          []    数组名称  =   new      数据类型     [数据长度];
      ```

   2. 指定内容的叫做静态初始化

      ```java
      //基本格式
      //数据类型[] 数组名称 = new 数据类型[]{元素1，元素2，....}
      //省略格式：
      //数据类型[] 数组名称 = {元素1，元素2，...}
      ```

## 访问数组元素进行获取

**获取数组元素的格式**:数据名字[i],i代表索引值

```java
 public static void main(String[] args) {
        int[] array = new int[]{100,200,300,400,500};
        int i = array[1];//索引出0开始
        System.out.println(i);//输出结果为200
    }
```

**数组元素赋值**

```java
public static void main(String[] args) {
    //创建长度为3的字符串数组
    String[] namearray = new String[3];
    //把诸葛亮赋值给字符串数组的索引1
    namearray[1]="诸葛亮";
    String name = namearray[1];
    System.out.println(name);
}
```

**数组长度**

数组长度是不可以改变的，但是值得注意的是每一次new都会产生一个新的数组

```java
int[] array = new int[3]//长度是3
array = new int[5]//长度是5
 //这两个数组是不一样的，他们都指向不同的内存地址，
```

**遍历数组**

```java
public static void main(String[] args) {
        String[] namearray = new String[]{"关羽","张飞","黄忠","赵云","马超"};
        for(int i = 0 ; i<namearray.length;i++){

            System.out.println(namearray[i]);
        }
```

**求数组中的最值**

```java
public static void main(String[] args) {
        int[] array = new int[]{95,96,97,98,99};
        int max = array[0];
        for(int i = 0 ; i<array.length;i++){
            
            if(max<array[i]) {
                max = array[i];
            }
        }
        System.out.println("最大值是"+max);
    }
```

