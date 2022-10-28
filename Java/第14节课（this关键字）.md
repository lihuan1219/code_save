# 1 回顾

+ 类与对象
+ 封装性
+ 构造方法

# 2 成员变量、局部变量的区别

+ 成员变量：类中方法外
+ 局部变量：在方法体中的变量

```java
public class Test {
	public static void main(String[] args) {
		// 局部变量
		double radius = 5.5; 
		double area = 3.14 * radius * radius;
		System.out.println(area);
	}
}
```

+ 注意：局部变量，不能使用可见修饰符修饰

# 3 this关键字

## 3.1 引入

```java
public class Test {
	public static void main(String[] args) {
		Student stu1 = new Student("男", 1000);
		stu1.inteoduceSelf();
	}
}
// 我是男，我1000岁啦
```

## 3.2 通过this访问成员变量

+ this指代当前类的临时对象
+ 格式：this.成员变量

### 3.3.1 改造构造方法

```java
public class Student {
	// 成员变量
	private String name;
	private int age;
	// 成员方法
	public void inteoduceSelf(){
		System.out.printf("我是%s，我%d岁啦",name,age);
	}
	public String getName() {return name;	}
	public void setName(String name) {this.name = name;	}
	public int getAge() {return age;}
	public void setAge(int age) {
		if(age < 0 || age > 150){
			System.out.println("年龄有误");
		}else{
			this.age = age;			
		}
	}
	// 构造方法
	public Student(String name, int age){
		this.name = name;
		this.age = age;
	}
	public Student(){	
	}
}
```

### 3.3.2 对象的创建和使用

+ 经过使用this改造构造方法后，在创建对象时，就可以明确构造方法各参数的确切含义！

```java
public class Test {
	public static void main(String[] args) {
		Student stu1 = new Student("张三", 18);
		stu1.inteoduceSelf();
	}
}
```

## 3.3 通过this调用成员方法

+ 格式：this.成员方法

```java
public class Student {
    // 在进行很多操作时，都要进行张开嘴这个动作。所以将其抽取为一个方法。供后期直接调用，可提高程序开发效率
	public void openMouth(){
        ...
    }
    public void read(){
        // 读书前，首要张开嘴。直接调用方法，可以提高程序开发效率
        this.openMouth();
        ...
    }
}
```

## 3.4 通过this调用构造方法

+ 注意：
  + 只能在构造方法中使用this调用本类其他构造方法
  + 构造方法之间不能相互同时调用，否则陷入无限循环
  + 使用this调用本类其他构造方法的语句，必须在当前构造方法的第一行

### 3.4.1 类的定义

```java
public class Student {
	// 成员变量
	private String name;
	private int age;
	private String school;
	// 构造方法
	public Student(String name, int age, String school) {
		this.name = name;
		this.age = age;
		this.school = school;
	}
	public Student() {
	}
	public Student(String name, int age) {
		// this.name = name;
		// this.age = age;
		this(name,age,"新疆科技学院");
	}
	// 成员方法
	public void introduceSelf(){
		System.out.printf("我是%s,%d岁,来自%s",name,age,school);
	}
}
```

### 3.4.2 对象的创建和使用

```java
public class Test {
	public static void main(String[] args) {
		Student stu1 = new Student("张三", 18);
		stu1.introduceSelf();
	}
}
// 我是张三,18岁,来自新疆科技学院
```

# 4 实践

## 4.1 解决圆面积周长的计算问题

### 4.1.1 类的定义

```java
public class Circle {
	// 成员变量
	private double radius;
	// 构造方法
	public Circle(double radius) {
		this.radius = radius;
	}
	public Circle() {
	}
	// 成员方法
	public double getRadius() {return radius;}
	public void setRadius(double radius) {this.radius = radius;}
	
	public double getArea(){
		double area = 3.14 * radius * radius;
		return area;
	}
	public double getZhouChang(){
		double zhouChang = 2 * 3.14 * radius;
		return zhouChang;
	}
}
```

### 4.1.2 对象的创建和使用

```java
public class TestCircle {

	public static void main(String[] args) {
		Circle c1 = new Circle(5.5);
		System.out.printf("半径为%.2f的圆的面积为%.2f\n",c1.getRadius(),c1.getArea());
		System.out.printf("半径为%.2f的圆的周长为%.2f\n",c1.getRadius(),c1.getZhouChang());
	}
}
// 半径为5.50的圆的面积为94.99
// 半径为5.50的圆的周长为34.54
```

## 4.2 模拟看电视的操作





