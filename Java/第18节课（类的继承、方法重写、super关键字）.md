# 1 继承性

+ 子承父业
+ 类与类的关系：子类继承父类
  + 子类可以继承父类的成员变量、成员方法（public、protected）
  + 子类可以重写父类的方法（方法重写）
  + 子类中可以有自己的成员变量、成员方法

+ 作用：1、提高代码的编写效率。2、降低代码维护成本
+ 应用场景：必须在is a关系中应用。例如：猫是一种动物，猫就可以继承动物。反例：猫不能继承人类，虽然在Java中可以让猫类继承人类，但不贴合实际。
+ 扩展：当多个子类具有相同的成员时，就可以考虑将这些成员提取出来，放到父类中，然后再用子类去继承这个父类，也就是将一些相同的成员提取到更高的层次中。

# 2 继承的格式

```java
class ziLei extends fuLei{

}
```

## 2.1 Animal类

```java
public class Animal {
	// 成员变量
	private String name;
	private int age;
	// 成员方法
	public String getName() {return name;}
	public void setName(String name) {this.name = name;}
	public int getAge() {return age;}
	public void setAge(int age) {this.age = age;}
	public void eat(){
		System.out.println(name + "这个动物在吃饭");
	}
	// 构造方法
	public Animal(String name, int age) {
		super();
		this.name = name;
		this.age = age;
	}
	public Animal() {
		super();
	}
}
```

## 2.2 Cat类

```java
public class Cat extends Animal{

}
```

## 2.3 测试类

```java
public class Test {
	public static void main(String[] args) {
		Cat c1 = new Cat();
		c1.setName("小花");
		c1.setAge(3);
		c1.eat();
	}
}
//小花这个动物在吃饭
```

# 3 注意事项

## 3.1 只允许单继承，不允许多继承

```java
class A{}
class B{}
class C extends A,B{} // 这是不允许的
```

## 3.2 允许多层继承

```java
class A{}
class B extends A{}
class C extends B{}
```

## 3.3 多个类可以继承一个类

```java
class A{}
class B extends A{}
class C extends A{}
```

# 4 子类可以有自己的成员

+ 子类中可以有自己的成员变量、成员方法

```java
public class Dog extends Animal{
	// 成员变量
	private String color;
	// 成员方法
	public String getColor() {return color;	}
	public void setColor(String color) {this.color = color;	}
}
```

# 5 方法重写

+ 方法重载：在同一个类中，方法名相同，参数列表不同的方法
+ 方法重写：在不同的类中，方法名相同，参数列表相同，方法体不同的方法
+ static方法不能被重写
+ 在子父类关系中，当父类方法无法满足子类现有需求时，子类可以对对父类的方法进行重写修改。
+ 注意事项
  + 1、需要和父类被重写的方法具有相同的方法名、参数列表以及返回值类型，
  + 2、且在子类重写的方法不能拥有比父类方法更加严格的访问权限（子类重写父类方法时，访问权限只能大于等于父类方法的访问权限。 ）
+ 注解：@Override
  + 用来检测是否是正确的重写方法格式。可加可不加

## 5.1 Dog类

```java
public class Dog extends Animal{
	// 成员变量
	private String color;
	// 成员方法
	public String getColor() {return color;	}
	public void setColor(String color) {this.color = color;	}
	// 方法重写
	@Override
	public void eat(){
		System.out.println("它在吃狗粮");
	}
}
```

## 5.2 测试类

```java
public class Test{
	public static void main(String[] args) {
		Dog dog1 = new Dog();
		dog1.eat();
	}
}
//它在吃狗粮
```

# 6 super关键字

| **区别点**   | **super**                                             | **this**                                                   |
| ------------ | ----------------------------------------------------- | ---------------------------------------------------------- |
| 访问属性     | 直接访问父类中的非私有属性                            | 访问本类中的属性。如果本类中没有该属性,则从父 类中继续查找 |
| 调用方法     | 直接调用父类中的非私有方法                            | 调用本类中的方法。如果本类中没有该方法,则从父 类中继续查找 |
| 调用构造方法 | 调用 父 类 构 造 方 法,必 须 放 在 子类构造方法的首行 | 调用本类构造方法,必须放在构造方法的首行                    |

+ 作用：在子类中调用父类的成员变量、成员方法、构造方法

+ super：用来指代父类的对象
+ this：用来指代本类的对象

## 6.1 通过super访问父类的成员变量

- 无法访问父类私有成员变量，可以通过父类set方法间接访问成员变量

## 6.2 通过super调用成员方法

- 当子类重写父类的方法后，子类对象将无法访问父类被重写的方法，为了解决这个问题，Java提供了super关键字，super关键字可以在子类中调用方法
- 用户希望在调用子类重写方法的同时，看到父类方法的效果，或者扩展父类的方法，可以通过super实现

```java
public class Dog extends Animal{
	// 成员变量
	private String color;
	// 成员方法
	public String getColor() {return color;	}
	public void setColor(String color) {this.color = color;	}
	
	// 方法重写检查机制，可有可无
    // 没有的话，容易出错
    @Override 
	public void eat(){
        // 调用父类的方法
		super.eat();
        
        // 扩展父类方法
		System.out.println("它在吃狗粮");
	}
}
```

## 6.3 通过super调用父类的构造方法

+ 注意：
  + super（）必须位于第一行
  + super（）和this（）不能同时调用
  + 使用super调用的构造方法之间，不能相互同时调用，否则陷入无限循环

```java
public class Dog extends Animal{
	// 成员变量
	private String color;
	// 成员方法
	public String getColor() {return color;	}
	public void setColor(String color) {this.color = color;	}
	
	@Override
	public void eat(){
        // 调用父类的方法
		super.eat(); 
        
        // 扩展父类方法
		System.out.println("它在吃狗粮");
	}
	
	// 构造方法
	public Dog(String name,int age,String color){
		/*super.name = name;
		super.age = age;*/ //无法访问
		
		/*super.setName(name);
		super.setAge(age);*/ //太过繁琐
		
		// 通过super调用父类构造方法提高代码编写效率
		super(name,age); 
		this.color = color;
	}
	public Dog() {
	}
}
```

# 7 总结

+ 如果多个类中存在着相同的成员，就可以考虑用继承将这些成员提取到父类中，之后各个类再去继承这个父类。
+ 使用继承可以沿用父类的成员，但子类也可以通过方法重写改造父类已有的方法。
+ 或者，子类也可以通过super关键字对父类中的某个方法进行扩展