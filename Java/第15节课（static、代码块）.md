# 1 回顾

+ this：指代当前类的临时对象
+ 作用：访问成员变量（用来区分局部变量和成员变量）、调用成员方法（提高代码开发效率、降低维护成本）、调用构造方法：this（）。
+ 采用面向对象的思想，解决了圆面积周长计算问题
+ 面向对象的本质：调用方法解决问题

# 2 static

+ 英文：静止。Java：静态的
+ 作用：用来修饰成员变量（静态变量）、成员方法（静态方法）、代码块（静态代码块）
+ 访问静态变量、调用静态方法的方式：
  + 类名.静态变量。类名.静态方法
  + 对象名.静态变量。对象名.静态方法。（不推荐）

## 2.1 静态变量

+ 引入

```java
public class Test {
	public static void main(String[] args) {
		Student stu1 = new Student("张三", 18, "新疆科技学院");
		Student stu2 = new Student("李四", 18, "新疆科技学院");
		Student stu3 = new Student("王二", 18, "新疆科技学院");
		System.out.println("学校名字改了");
		stu1.setSchool("新疆科技大学");
		
		stu1.introduceSelf();
		stu2.introduceSelf();
		stu3.introduceSelf();
	}
}
// 学校名字改了
// 我是张三,18岁,来自新疆科技大学
// 我是李四,18岁,来自新疆科技学院
// 我是王二,18岁,来自新疆科技学院
```

### 2.1.1 类的定义

+ 用static修饰的school成员变量：类中群体共有的属性
+ 针对类中所有对象共有的属性，必须要用static修饰，修饰之后，改属性就是类的属性，不属于某个对象。

```java
public class Student {
	// 成员变量
	private String name;
	private int age;
	private static String school;
	// 构造方法
	public Student(String name, int age, String school) {
		 this.name = name;
		 this.age = age;
		 Student.school = school;
	}
	public Student() {
	}
	// 成员方法
	public void introduceSelf(){
		System.out.printf("我是%s,%d岁,来自%s\n",name,age,school);
	}
	public String getName() {return name;}
	public void setName(String name) {this.name = name;}
	public int getAge() {return age;}
	public void setAge(int age) {this.age = age;}
	public String getSchool() {return school;}
	public void setSchool(String school) {Student.school = school;	}
}
```

### 2.1.2 对象的创建和使用

```java
public class Test {
	public static void main(String[] args) {
		Student stu1 = new Student("张三", 18, "新疆科技学院");
		Student stu2 = new Student("李四", 18, "新疆科技学院");
		Student stu3 = new Student("王二", 18, "新疆科技学院");
		System.out.println("学校名字改了");
		stu1.setSchool("新疆科技大学");
		
		stu1.introduceSelf();
		stu2.introduceSelf();
		stu3.introduceSelf();
	}
}
// 学校名字改了
// 我是张三,18岁,来自新疆科技大学
// 我是李四,18岁,来自新疆科技大学
// 我是王二,18岁,来自新疆科技大学
```

## 2.2 静态方法

+ 静态方法中，访问的必须是静态变量。
  + 联想main方法，在main方法中，想要访问非静态变量，必须先创建对象，再访问。而类的定义中无法创建对象，所以类中的静态方法只能访问静态变量

### 2.2.1 类的定义

```java
public class Student {
	// 成员变量
	private String name;
	private int age;
	private static String school;
	// 构造方法
	public Student(String name, int age, String school) {
		 this.name = name;
		 this.age = age;
		 Student.school = school;
	}
	public Student() {
	}
	// 成员方法
	public void introduceSelf(){
		System.out.printf("我是%s,%d岁,来自%s\n",name,age,school);
	}
	public String getName() {return name;}
	public void setName(String name) {this.name = name;}
	public int getAge() {return age;}
	public void setAge(int age) {this.age = age;}
	public String getSchool() {return school;}
	public static void setSchool(String school) {
		Student.school = school;
	}
}
```

### 2.2.2 对象的创建和使用

```java
public class Test {
	public static void main(String[] args) {
		Student stu1 = new Student("张三", 18, "新疆科技学院");
		Student stu2 = new Student("李四", 18, "新疆科技学院");
		Student stu3 = new Student("王二", 18, "新疆科技学院");
		System.out.println("学校名字改了");
		// 不推荐使用对象调用静态方法
		// stu1.setSchool("新疆科技大学");
		Student.setSchool("新疆科技大学");
		
		stu1.introduceSelf();
		stu2.introduceSelf();
		stu3.introduceSelf();
	}
}
// 学校名字改了
// 我是张三,18岁,来自新疆科技大学
// 我是李四,18岁,来自新疆科技大学
// 我是王二,18岁,来自新疆科技大学
```

### 2.2.3 查看Arrays类和Scanner类的实现细节

```java
import java.util.Arrays;
import java.util.Scanner;

public class Test {
	public static void main(String[] args) {
//		Scanner input = new Scanner(System.in);
//		int a = input.nextInt();
		
		int[] x = {1,3,2,4};
		Arrays.sort(x);
		for (int i : x) {
			System.out.println(i);
		}
	}
}
```

+ 快捷键：ctrl + 鼠标左键

# 3 代码块

+ 类的成员：成员变量、成员方法、构造方法、代码块
+ {}包裹的代码称之为代码块
+ 代码块的种类：普通代码块、构造代码块、静态代码块、同步代码块

## 3.1 普通代码块

```java
public class Test {
	public static void main(String[] args) {
		{
			int i = 1;
			System.out.println(i);
		}
		System.out.println(i);
		//i cannot be resolved to a variable
	}
}
```

## 3.2 构造代码块

+ 构造代码块的位置：类中、方法外
+ 执行方式：每创建一个对象，构造代码块都会执行一次
+ 本质作用：提高代码编写效率、降低维护成本

### 3.2.1 类的定义

```java
public class Student {
	// 成员变量
	private String name;
	private int age;
	private static String school;
	// 构造方法
	public Student(String name, int age, String school) {
		 this.name = name;
		 this.age = age;
		 Student.school = school;
		 // 完成相应功能的代码
	}
	public Student() {
		// 完成相应功能的代码
	}
	// 构造代码块
	{
		System.out.println("好好学习");
	}
	// 成员方法
	public void introduceSelf(){
		System.out.printf("我是%s,%d岁,来自%s\n",name,age,school);
	}
	public String getName() {return name;}
	public void setName(String name) {this.name = name;}
	public int getAge() {return age;}
	public void setAge(int age) {this.age = age;}
	public String getSchool() {return school;}
	public static void setSchool(String school) {
		Student.school = school;
	}
}
```

### 3.2.2 对象的创建和使用

```java
public class Test {
	public static void main(String[] args) {
		Student stu1 = new Student();
		Student stu2 = new Student();
		Student stu3 = new Student();
	}
}
// 好好学习
// 好好学习
// 好好学习
```

## 3.3 静态代码块

+ 静态代码块：类中方法外的被static修饰的代码块
+ 执行方式：随着类的加载，只执行一次
+ 作用：作用：提前加载静态资源，快
+ 注意：
  + 静态代码块中，只能访问静态变量
  + 静态代码块，伴随着类的加载，只执行一次
  + 静态代码块的执行，与静态代码块的位置无关，类加载后第一时间执行

### 3.3.1 类的定义

```java
public class Student {
	// 成员变量
	private String name;
	private int age;
	private static String school;
	// 构造方法
	public Student(String name, int age, String school) {
		 this.name = name;
		 this.age = age;
		 Student.school = school;
		 // 完成相应功能的代码
	}
	public Student() {
		// 完成相应功能的代码
	}
	// 构造代码块
	{
		System.out.println("好好学习");
	}
	// 静态代码块
	static{
		System.out.println("我是Student类的静态代码块");
	}
	// 成员方法
	public void introduceSelf(){
		System.out.printf("我是%s,%d岁,来自%s\n",name,age,school);
	}
	public String getName() {return name;}
	public void setName(String name) {this.name = name;}
	public int getAge() {return age;}
	public void setAge(int age) {this.age = age;}
	public String getSchool() {return school;}
	public static void setSchool(String school) {
		Student.school = school;
	}
}
```

### 3.3.2 对象的创建和使用

```java
public class Test {
	// 作用：提前加载静态资源，快
	public static void main(String[] args) {
		Student stu1 = new Student();
		Student stu2 = new Student();
		Student stu3 = new Student();
	}
	
	static{
		System.out.println("我是Test类的静态代码块");
	}
}
// 我是Test类的静态代码块
// 我是Student类的静态代码块
// 好好学习
// 好好学习
// 好好学习
```

