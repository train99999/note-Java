#### final关键字的概念与四种用法

final关键字代表最终，不可改变的

常见四种用法：

1. 可以用来修饰一个类

   当前这个类不能有任何子类

2. 可以用来修饰一个方法

   当final关键字用来修饰一个方法的时候，这个方法就是最终方法，也就是不能被覆盖重写

3. 还可以用来修饰一个局部变量

   被修饰后，变量不可改变

4. 还可以用来修饰一个成员变量

#### Java中有四种权限修饰符

​	public  > protected > (default) > private



|                            | public | protected | default | private |
| -------------------------- | ------ | --------- | ------- | ------- |
| 在同一个类中               | YES    | YES       | YES     | YES     |
| 在同一个包中               | YES    | YES       | YES     | NO      |
| 在不同包中，但存在继承关系 | YES    | YES       | NO      | NO      |
| 在不同包中，不存在继承关系 | YES    | NO        | NO      | NO      |

### 内部类

分类:

1. 成员内部类
2. 局部内部类

成员内部类的定义格式：

修饰符 class 外部类名{

修饰符 class 内部类{}

}

如何使用成员内部类？有两种方式

1. 间接方式：在外部类的方法中，使用内部类，然后main只是调用外部类的方法

2. 直接方式：公式  

   外部类名称.内部类名称 对象名  = new 外部类（）.new 内部类（）；

   
   
   #### 第一种间接使用方式

```java

//定义一个成员内部类
public class Body{

    public class Heart{
        public void beat(){
            System.out.println("我是内部类的方法+"+"心脏跳动......"+name);
        }
    }
    public void methodBody(){
        System.out.println("我是外部类的方法");
		new Heart().beat();
    }
    //我是成员变量,内部类也可以访问我
    private String name;

    public void setName(String name){
        this.name = name;
    }
    public String getName(){
        return name;
    }
}

```

```java
//使用内部类
public class BodyDemo{
public static void main(String[] args){
//间接使用
//创建对象调用方法，间接使用内部类
Body body = new Body();
body.methodBody();
//直接使用
Body.Heart heart = new Body().new Heart();
heart.beat();
}
}
```

#### 内部类的同名变量的访问

```java
public class Outer{
	//创建一个内部类
	int num = 10;
	
	public class Inner{
		int num = 20;
		public void methodInner(){
			int num = 30;
			System.out.println(num);
			System.out.println(this.num);
			System.out.println(Outer.this.num);
		}
	}
	public void newInner(){
		Inner inner = new Inner();
		inner.methodInner();
	}
}
```

```java
public class OuterDemo{
	public static void main(String[] args){
	Outer outer = new Outer();
	outer.newInner();
	}
}
```

#### 局部内部类

定义格式：

修饰符 class 外部类名称{

​	修饰符 返回值类型 外部类方法名称（）{

​			class 局部内部类名称{}

}

}

```java
public class Outer{//外部类
	public void methodOuter(){
		//内部类
		class Inner{
			//内部类的成员变量
			int num = 10;
			//内部类的成员方法
			public void methodInner(){
				System.out.println(num);
			}
		}
		//让局部变量在方法里直接使用
		Inner inner = new Inner();
		inner.methodInner();
	}
}
```

```java
public class OuterDemo{
	public static void main(String[] args){
	Outer outer = new Outer();
	//局部内部类，存在于方法中，不能超出局部使用
	//局部只属于当前所属的方法才可以使用他
	outer.methodOuter();
	}
}
```

## 匿名内部类

匿名内部类的定义格式：
接口名称 对象名 = new 接口名称(){覆盖重写所有的抽象方法};

```java
public interface MyInterface {

public abstract void method1();

}
```



```java
public class InterfaceDemo {
    public static void main(String[] args) {
        MyInterface myinterface = new MyInterface() {
            public void method1() {
                System.out.println("我是匿名内部类");
            }
        };
        myinterface.method1();
    }
}
```

#### 类作为成员变量类型

```java
//定义一个英雄类
public class Hero{
	private int age;
	private String name;
	private Weapon code;
	//手写的构造方法
	public Hero(){}
	public Hero(int age,String name,Weapon code){
	this.age = age; this.name = name; this.code = code;
	}
	//设置get和set方法
	public void setAge(int age){
		this.age = age;
	}
	public int getAge(){
		return age;
	}
	public void setName(String name){
		this.name = name;
	}
	public String getName(){
		return name;
	}
	public void setWeapon(Weapon code){
		this.code = code;
	}
	public Weapon GetWeapon(){
		return code;
	}
	//英雄特与方法
	public void attack(){
		System.out.println(name+"手持"+code.getName()+"正在大杀四方,可怕的是他今年才"+age);
	}
	
}
```

```java
public class Weapon{
	private String name;//已经是多兰剑了
	public Weapon(){}
	public Weapon(String name){
	this.name = name;
	}
	public void setName(String name){
		this.name = name;
	}
	public String getName(){
		return name;
	}
}
```

```java
//创建英雄吧
public class HeroDemo{
	public static void main(String[] args){
	Weapon weapon = new Weapon("多兰剑");
	Hero hero = new Hero();
	hero.setWeapon(weapon);
	hero.setName("光辉女郎");
	hero.setAge(20);
	hero.attack();
	} 
}
```

#### 接口作为成员变量类型

```java
public class Hero{
	private String name;
	private Skill skill;
	
	public Hero(){}
	public Hero(String name,Skill skill){
		this.name = name;
		this.skill = skill;
	}
	public void setName(String name){
		this.name = name;
	}
	public String getName(){
		return name;
	}
	public void setSkill(Skill skill){
		this.skill = skill;
	}
	public Skill getSkill(){
		return skill;
	}
	
	public void attack(){
		System.out.println("我叫"+name+"开始释放技能");
		//传递那个接口，就用哪一个接口去调用use技能
		skill.use();
		System.out.println("释放技能完成");
	}
}
```

```java
public interface Skill{
	public abstract void use();
}
```

```java
public class HeroDemo{
	public static void main(String[] args){
		Hero hero = new Hero();
		hero.setName("艾希");
		Skill skill = new Skill(){
			public void use(){System.out.println("pia==pia===pia");}
		};
		hero.setSkill(skill);
		hero.attack();
	}
}
```

