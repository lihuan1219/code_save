# 1 回顾

+ 接口：是一种特殊的类
  + 1、制定标准
  + 2、克服类单继承的局限性，方便扩展类的功能
+ 使用接口多继承的方式：
  + 一个类实现多个接口
  + 先将所有接口功能集合在一个接口中，再用一个类实现这个接口
  + 一个类继承另一个类之后，再去实现其他接口

# 2 对象类型的转换

## 2.1 向上转型（小转大）

```Java
父类类型 父类对象 = 子类对象
// 类似第二章的自动类型转换
```

+ 缺点：父类变量无法调用子类独有的方法（局限性），其解决方法：向下转型
+ 优点：向上转型应用多态方法的参数中，可以扩大方法参数的接收范围，可以接收所有子类的对象，使得多态方法变得更加灵活

## 2.2 向下转型（大转小）

+ 注意：
  + 向下转型不是自动进行的，需要强制类型转换
  + 向下转型之前，必须要向上转型

```java
父类类型 父类对象 = 子类对象
子类类型 子类对象 = （子类类型） 父类对象
```

```java
public class Test {
	
	public static void main(String[] args) {
		// 强制类型转换
		byte a = (byte)10000;
		
		// 向下转型
		Graph g1 = new Circle(5.5);
		Circle c2 = (Circle)g1;
		System.out.println(c2.getRadius()); // 5.5
	}
}
```

# 3 多态

+ 打：打字、打架、打招呼、打工、打开、打扫、打印、一打、打哈欠、打赌、打牌、打卡、打球
+ 为什么要一词多义：方便，不用造那么多字（复用性）
+ 多态在Java中的体现：不同的对象，调用同一个方法，得到的结果不一样
+ 体现方式：1、方法重载（太片面）。2、方式重写
+ 实现多态的基本条件：
  + 1、要存在继承（实现）
  + 2、要存在重写
  + 3、要存在向上转型

## 3.1 多态案例

### 3.1.1 Graph（父接口）

```java
public interface Graph {
	// 成员变量
	// 成员方法
	public abstract double getArea();
	public abstract double getZhouChang();
	void state();
	// 构造方法
}
```

### 3.1.2 Circle（子实现类1）

```java
public class Circle implements Graph{
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
	@Override
	public void state() {
		System.out.printf("半径为%.2f的圆的面积是%.2f,周长是%.2f\n",
				radius,getArea(),getZhouChang());
	}
}
```

### 3.1.3 Square（子实现类2）

```java
public class Square implements Graph{
	// 成员变量
	private double side;
	// 构造方法
	public Square(int side) {
		super();
		this.side = side;
	}
	public Square() {
		super();
	}
	// 成员方法
	public double getSide() {return side;	}
	public void setSide(int side) {this.side = side;}
	
	@Override
	public double getArea() {
		return side*side;
	}
	@Override
	public double getZhouChang() {
		return 4*side;
	}
	@Override
	public void state() {
		System.out.printf("边长为%.2f的正方形的面积是%.2f,周长是%.2f\n",
				side,getArea(),getZhouChang());
	}
}
```

### 3.1.4 测试类

```java
public class Test {
	
	public static void main(String[] args) {
		
		Graph g1 = new Circle(5.5);
		print(g1);
		
		Graph g2 = new Square(5);
		print(g2);
		
	}
	
	public static void print(Graph graph){
		graph.state();
	}
	
}
// 半径为5.50的圆的面积是95.03,周长是34.56
// 边长为5.00的正方形的面积是25.00,周长是20.00
```

# 4 instanceof关键字

+ 如果要在多态方法中，调用子类独有的方法的话，会遇到问题
+ 此时，就需要在多态方法中，向下转型，但具体转变为哪个子类类型呢？还需要使用instanceof关键字判定

```java
public class Test {
	
	public static void main(String[] args) {
		Graph g1 = new Circle(5.5);
		print(g1);
		
		Graph g2 = new Square(5);
		print(g2);
	}
	
	public static void print(Graph graph){
		graph.state();
		if (graph instanceof Circle){
			Circle circle = (Circle)graph;
			System.out.printf("该圆的半径是%.2f\n",
					circle.getRadius());			
		}else if (graph instanceof Square){
			Square square = (Square)graph;
			System.out.printf("该正方形的边长是%.2f\n",
					square.getSide());			
		}
	}	
    
}
// 半径为5.50的圆的面积是95.03,周长是34.56
// 该圆的半径是5.50
// 边长为5.00的正方形的面积是25.00,周长是20.00
// 该正方形的边长是5.00
```





