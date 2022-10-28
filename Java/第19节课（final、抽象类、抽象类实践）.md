# 1 回顾

+ 继承性：类与类之间的关系（is a关系）
+ 作用：提高代码复用性、降低维护成本
  + 子类继承父类的成员
  + 子类可以重写父类的方法（方法重写）
  + 子类继承父类的成员后，还能有自己的成员
+ super关键字：指代父类的对象
  + 访问父类的成员变量（私有的无法访问）
  + 调用父类的成员方法
  + 调用父类的构造方法（super（））

# 2 final关键字

+ final：最终的
+ 作用：用来修饰变量（成员变量、局部变量）、方法、类

## 2.1 使用final修饰变量

+ 使用final修饰的变量，只能赋值一次，不能赋值第二次

```java
public class Test {
	
	private static final int num = 4;
	
	public static void main(String[] args) {
		// 基本数据类型
		final double PI = 3.1415926;
		final int NUMBER_OF_STUDENT = 202101;
		
		// 引用数据类型
		final Animal a1 = new Animal();
		a1.setName("大黄");
		// a1 = new Animal();
		a1.setName("小黄");
		System.out.println(a1.getName());
		
	}
}
```

## 2.2 使用final修饰类

+ 使用final修饰的类，不能有子类，但可以有父类

## 2.3 使用final修饰方法

+ 使用final修饰的方法，不允许重写

# 3 抽象类

- 作用：
  - 1、不让抽象类创建对象。（情理抽象的父类不能创建对象，现在用abstract修饰类之后，从语法上保证了这个类不能创建对象）
  - 2、抽象类可以声明变量，将子类对象赋值给这个变量

## 3.1 抽象方法

+ 使用abstract修饰的方法（父类中有的的方法，没有办法书写方法体，就可以使用abstract将其定义为抽象方法）
+ 说明：
  + 有抽象方法的类，一定是抽象类，抽象类中不一定有抽象方法
  + 抽象方法和抽象类，都用abstract修饰。
+ 注意：
  + 抽象方法，不能使用private修饰

## 3.2 Animal类

```java
public abstract class Animal {
	// 成员变量
	private String name;
	private int age;
	// 构造方法
	public Animal(String name, int age) {
		this.name = name;
		this.age = age;
	}
	public Animal() {
	}
	// 成员方法
	public String getName() {return name;	}
	public void setName(String name) {this.name = name;	}
	public int getAge() {return age;	}
	public void setAge(int age) {this.age = age;}
	
	public abstract void eat();
}
```

## 3.3 Cat类

```java
public class Cat extends Animal{
	// 成员变量
	private String color;
	// 成员方法
	public String getColor() {return color;	}
	public void setColor(String color) {this.color = color;	}
	
	@Override
	public void eat() {
		// TODO Auto-generated method stub
		System.out.println("猫吃猫粮呢");
	}
	
	// 构造方法
	public Cat(String name, int age, String color) {
		super(name, age);
		this.color = color;
	}
}
```

## 3.4 测试类

```java
public class Test {
	
	public static void main(String[] args) {
		
		// Animal a1 = new Animal();
		Animal a1 = new Cat("小花", 3, "黑白花");
		a1.setName("大黄");
		System.out.println(a1.getName());
		
		a1.eat();
	}
}
```

# 4 练习

## 4.1 图形的面积与周长的计算

### 4.1.1 父类（Graph）

```java
public abstract class Graph {
	// 成员变量
	// 成员方法
	public abstract double getArea();
	public abstract double getZhouChang();
	// 构造方法
}
```

### 4.1.2 子类（Circle）

```java
public class Circle extends Graph{
	// 成员变量
	private double radius;
	private static final double PI = 3.1415926;
	// 构造方法
	public Circle(double radius) {
		super();
		this.radius = radius;
	}
	public Circle() {
		super();
	}
	// 成员方法
	public double getRadius() {return radius;	}
	public void setRadius(double radius) {this.radius = radius;	}
	
	@Override
	public double getArea() {
		// TODO Auto-generated method stub
		return PI*radius*radius;
	}
	@Override
	public double getZhouChang() {
		// TODO Auto-generated method stub
		return 2*PI*radius;
	}
}
```

### 4.1.3 测试类（Test）

```java
public class Test {
	
	public static void main(String[] args) {
		Graph g1 = new Circle(5.5);
		System.out.printf("该图形的面积%.2f,周长%.2f\n",
				g1.getArea(),g1.getZhouChang());
	}
}
// 该图形的面积95.03,周长34.56
```









