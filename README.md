# Java面向对象编程精简模板

## 1. 类的定义与构造函数

```java
// 基本类定义
public class Animal {
    // 成员变量
    private String name;
    private int age;
    
    // 构造函数
    public Animal(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    // 无参构造函数
    public Animal() {
        this("未命名", 0);
    }
    
    // getter和setter方法
    public String getName() { return name; }
    public void setName(String name) { this.name = name; }
    public int getAge() { return age; }
    public void setAge(int age) { this.age = age; }
    
    // 普通方法
    public void makeSound() {
        System.out.println("动物发出声音");
    }
}
```

## 2. 继承

```java
// 子类继承父类
public class Dog extends Animal {
    private String breed;
    
    // 子类构造函数，调用父类构造函数
    public Dog(String name, int age, String breed) {
        super(name, age); // 调用父类构造函数
        this.breed = breed;
    }
    
    // 重写父类方法(多态的体现)
    @Override
    public void makeSound() {
        System.out.println(getName() + "汪汪叫");
    }
    
    // 子类特有方法
    public void fetch() {
        System.out.println(getName() + "在捡东西");
    }
}
```

## 3. 多态

```java
public class Cat extends Animal {
    // 构造函数
    public Cat(String name, int age) {
        super(name, age);
    }
    
    // 重写父类方法(多态的另一体现)
    @Override
    public void makeSound() {
        System.out.println(getName() + "喵喵叫");
    }
    
    // 猫特有的方法
    public void climb() {
        System.out.println(getName() + "在爬树");
    }
}
```

## 4. 抽象类

```java
// 抽象类
public abstract class Shape {
    // 抽象类可以有普通属性
    protected String color;
    
    // 构造函数
    public Shape(String color) {
        this.color = color;
    }
    
    // 抽象方法(没有方法体)
    public abstract double getArea();
    
    // 普通方法
    public String getColor() {
        return color;
    }
}

// 抽象类的子类
public class Circle extends Shape {
    private double radius;
    
    public Circle(String color, double radius) {
        super(color);
        this.radius = radius;
    }
    
    // 实现抽象方法
    @Override
    public double getArea() {
        return Math.PI * radius * radius;
    }
}
```

## 5. 接口

```java
// 接口定义
public interface Movable {
    // 接口常量（默认public static final）
    int MAX_SPEED = 100;
    
    // 抽象方法（默认public abstract）
    void move(int distance);
    
    // 默认方法（Java 8特性）
    default void stop() {
        System.out.println("停止移动");
    }
}

// 接口实现
public class Vehicle implements Movable {
    private String type;
    
    public Vehicle(String type) {
        this.type = type;
    }
    
    @Override
    public void move(int distance) {
        System.out.println(type + "移动了" + distance + "米");
    }
}
```

## 6. 接口多实现与继承组合

```java
// 另一个接口
public interface Flyable {
    void fly(int height);
}

// 一个类可以实现多个接口
public class Bird extends Animal implements Movable, Flyable {
    public Bird(String name, int age) {
        super(name, age);
    }
    
    @Override
    public void move(int distance) {
        System.out.println(getName() + "走了" + distance + "米");
    }
    
    @Override
    public void fly(int height) {
        System.out.println(getName() + "飞到" + height + "米高空");
    }
    
    @Override
    public void makeSound() {
        System.out.println(getName() + "叽叽喳喳叫");
    }
}
```

## 7. 主函数

```java
public class Main {
    public static void main(String[] args) {
        // 使用父类引用指向子类对象(多态)
        Animal animal1 = new Dog("旺财", 3, "金毛");
        Animal animal2 = new Cat("咪咪", 2);
        
        // 多态调用方法
        animal1.makeSound(); // 输出: 旺财汪汪叫
        animal2.makeSound(); // 输出: 咪咪喵喵叫
        
        // 使用抽象类
        Shape circle = new Circle("红色", 5.0);
        System.out.println("圆的面积: " + circle.getArea());
        
        // 使用接口
        Movable car = new Vehicle("汽车");
        car.move(200);
        
        // 接口多实现
        Bird sparrow = new Bird("麻雀", 1);
        sparrow.move(10);
        sparrow.fly(50);
        sparrow.makeSound();
        
        // instanceof检查类型
        if(animal1 instanceof Dog) {
            // 向下转型
            Dog dog = (Dog)animal1;
            dog.fetch(); // 调用子类特有方法
        }
    }
}
```

## 考试记忆要点

1. **类定义核心**：类名、成员变量、构造函数、普通方法

2. **继承关键点**：
   - 使用`extends`关键字继承
   - 子类构造函数通过`super()`调用父类构造
   - 方法重写使用`@Override`注解

3. **多态核心**：
   - 父类引用指向子类对象
   - 同一方法不同表现形式
   - 可通过instanceof判断类型并向下转型

4. **抽象类要点**：
   - 使用`abstract`修饰类和方法
   - 不能实例化，但可以有构造函数
   - 子类必须实现所有抽象方法

5. **接口要点**：
   - 只有常量和抽象方法(Java 8之前)
   - 实现接口用`implements`关键字
   - 一个类可以实现多个接口

6. **析构函数类比**：
   Java没有显式析构函数
