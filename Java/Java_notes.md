# 一、面向对象－上

## 1. 类与对象

### 1.1 Java面向对象学习的三条主线

#### 	1.1.1 Java类及类的成员

​			属性、方法、构造器；代码块、内部类

#### 	1.1.2 面向对象的三大特征

​			封装性、继承性、多态性（、抽象性）

#### 	1.1.3 其它关键字

​			this, super, static, final, abstract, interface, package, import等

<font color='red'>**学习模式：“大处着眼，小处着手”**</font>

### 1.2 面向对象与面向过程（理解）

#### 	1.2.1 面向过程

​			强调的是功能行为，以函数为最小单位，**考虑怎么做**

#### 	1.2.2 面向对象

​			强调具备了功能的对象，以类/对象为最小单位，**考虑谁来做**

#### 	1.2.3 “人把大象塞进冰箱”

```java
人{
	打开(冰箱){
		冰箱.开门();
	}
	抬起(大象){
		大象.进入(冰箱);
	}
	关闭(冰箱){
		冰箱.关门();
	}
}

冰箱{
	开门();
	关门();
}

大象{
	进入(冰箱){
	}
}
```

#### 		1.2.4 <font color='red'>由面向过程的执行者转化为了面向对象的指挥者</font>

### 1.3 完成一个项目（或功能的思路）　

- 根据问题需要，选择问题所针对的<font color='red'>现实世界中的实体</font>
- 从实体中寻找解决问题相关的属性和功能，这些属性和功能就形成了<font color='red'>概念世界中的类</font>
- 把抽象的实体用计算机语言进行描述，形成<font color='red'>计算机世界中类的定义</font>。即借助某种程序语言，把类构造成计算机能够识别和处理的数据结构
- 将<font color='red'>类实例化成计算机世界中的对象</font>。对象是计算机世界中解决问题的最终工具

### 1.4 面向对象中的两个重要概念

#### 	1.4.1 类

​			对一类事物的描述，是抽象的、概念上的定义

​			常见类的成员：

​			1）属性：对应类中的成员变量

​			2）行为：对应类中的成员方法

#### 	1.4.2 对象

​			是实际存在的该类事物的每个个体，因此也称为实例(instance)

​			1）**面向对象程序设计的重点就是类的设计**

​			2）<font color='red'>**类的设计，其实就是类的成员的设计**</font>

#### 	1.4.3 二者的关系

​			对象是由类new出来的，派生出来的

### 1.5 面向对象思想落地实现的规则

#### 	1.5.1 创建类，设计类的成员

```java
class Person{
	// 属性
    String name;
    int age = 1;
    String sex;
    // 方法
    public void eat(){
        System.out.println("人可以吃饭。");
    }
    public void sleep(){
        System.out.println("人可以睡觉。");
    }
    public void talk(String language){
        System.out.println("人可以说话，使用的是：" + language);
    }
}
```

​		**也可称之为面向对象思想落地的实现**

#### 	1.5.2 创建类的对象

```java
// 创建Person类的对象
Person person = new Person();
```

​			如果创建了一个类的多个对象，则每个对象都独立的拥有一套类的属性（非static的），意味着：如果我们修改一个对象的属性a，则不影响另外一个对象属性a的值。

#### 	1.5.3 通过“对象.属性”或“对象.方法”调用对象的结构

```java
// 调用对象的结构：属性、方法
// 调用属性："对象.属性"
person.name = "Tom";
person.sex = "Male";
System.out.println(person.name);
// 调用方法："对象.方法"
person.eat();
person.sleep();
person.talk("中文");
```

#### 	Hint

 			 1> 属性 = 成员变量 = field = 域、字段

​			  2> 方法 = 成员方法 = 函数 = method

​			  3> 创建类的对象 = 类的实例化 = 实例化类	

### 1.6 对象的创建与对象的内存解析

![](/media/rong/_dde_data/java_code/java_notes/java_images/对象的内存解析.png)

![](./java_images/对象数组的内存解析.png)

**引用类型的变量：只可能存储两类值：null或地址值（含变量的类型）**

### 1.7 匿名对象的使用

```java
new Class().method();		
```

#### 	1.7.1 理解

​			我们创建的对象，没有显式的赋给一个变量名，即为匿名对象

#### 	1.7.2 特征

​			匿名对象只能调用一次

#### 	1.7.3 使用

```java
// 匿名对象的使用
PhoneMall mall = new PhoneMall();
mall.show(new Phone());

class PhoneMall{
	public void show(Phone phone){
		phone.sendEmail();
		phone.playGames();
	}
}
```

### 1.8 JVM内存结构

![](./java_images/JVM内存结构.png)

​	《JVM规范》

​	**虚拟机栈**：即为平时提到的栈结构。我们将局部变量存储在栈结构中

​	**堆**：我们将new出来的结构（比如：数组、对象）加载到堆空间中。对象的属性（非static的）加载在堆空间中

​	**方法区**：类的加载信息、常量池、静态域

​	*编译完源程序以后，生成一个或多个字节码文件。我们使用JVM中的类的加载器和解释器对生成的字节码文件进行解释运行。意味着，需要将字节码文件对应的类加载到内存中，涉及到内存解析*

## 2. 类的结构之一：属性(Field)

### 2.1 属性（成员变量）  　VS       局部变量

#### 2.1.1 相同点

​		1）定义变量的格式：数据类型 变量名 = 变量值;

​		2）先声明，后使用

​		3）变量都有其对应的作用域

#### 2.1.2 不同点

##### 2.1.2.1 在类中声明的位置

​			1）属性：直接定义在类的一对{}内

​			2）局部变量：声明在方法内、方法形参、代码块内、构造器形参、构造器内部的变量

##### 2.1.2.2 权限修饰符

​			1）属性：可以在声明属性时，指明其权限，使用权限修饰符

​							 常用的权限修饰符：private、public、缺省、protected    					------> 封装性

​						 	目前，大家声明属性时，都使用缺省就行了

​			2）局部变量：不可以使用权限修饰符

#### 	2.1.3 默认初始化值

​			1）属性：类的属性，根据其类型，都有默认初始化值

​					1> 整型(byte、short、int、long)：0

​					2> 浮点型(float、double)：0.0

​					3> 字符型(char)：'\0'

​					4> 布尔型(boolean)：false

​					5> 引用数据类型(类、数组、接口)：null

​			2）局部变量：没有默认初始化值

​					意味着我们在使用局部变量之前，必须要显式赋值

​					特别的，形参：我们在调用时赋值即可

#### 	2.1.4 在内存中的加载位置

​			1）属性：加载到堆空间中（非static）

​			2）局部变量：加载到栈空间

### 2.2 回顾变量的分类

#### 	2.2.1 方式一：按照数据类型

<img src="./java_images/数据类型分类.png"  />

#### 	2.2.2 方式二：按照在类中声明的位置

![](./java_images/成员变量和局部变量.png)

##  3. 类的结构之二：方法(Method)

​		**方法：描述类应该具有的功能**

​		比如：Math类：sqrt() \ random() ...

​				   Scanner类：nextInt() \ next() ...

​				   Arrays类：sort() \ binarySearch() \ toString() \ equals() ...

### 3.1 举例

```java
class Customer{
    // 属性
    String name;
    int age;
    boolean isMale;
    // 方法
    public void eat(){
        System.out.println("客户吃了饭");
    }
    public void sleep(int hour){
        System.out.println("客户睡了" + hour + "个小时");
    }
    public String getName(){
        return name;
    }
    public String getNation(String nation){
        String info = "我的国籍是：" + nation;
        return info;
    }
}
```

public void eat(){}

public void sleep(int hour){}

public String getName(){}

public String getNation(String nation){}

### 3.2 方法的声明

```java
权限修饰符 返回值类型 方法名(形参列表){
	方法体;
}
```

​		<font color='red'>注意：static、final、abstract来修饰的方法，后面再讲</font>

#### 	3.2.1 权限修饰符

​			Java规定的4种权限修饰符：private、public、缺省、protected（封装性再说）

​			默认方法的权限修饰符先都使用**public**

#### 	3.2.2 返回值类型

##### 			3.2.2.1 声明

​			如果方法有返回值，则必须在方法声明时，指定返回值的类型，同时，方法中需要使用return关键字来返回指定类型的变量或常量

​			如果方法没有返回值，则方法声明时，使用void来表示。通常，没有返回值的方法中，就不使用return。但是如果使用的话，只能"return;" 表示结束此方法的意思

##### 			3.2.2.2 要不要返回值？

​			1）题目要求

​			2）凭经验，具体问题具体分析

##### 			3.2.2.3 return关键字的使用

​			1）使用范围：使用在方法体中

​			2）作用							

​					1> 结束方法

​					2> 针对有返回值类型的方法，使用"return 数据"方法返回所要的数据

​			3）注意点：return关键字后面不可以声明执行语句

#### 	3.2.3 方法名

​			属于标识符，遵循标识符的规则和规范，“见名知意”

#### 	3.2.4 形参列表

​			方法可以声明0个，1个或多个形参

##### 			3.2.4.1 格式

```java
(数据类型1 形参1, 数据类型2 形参2, ...)
```

##### 			3.2.4.2 要不要形参？

​			1）题目要求

​			2）凭经验，具体问题具体分析

#### 	3.2.5 方法体

​			方法功能的实现

### 3.3 方法的使用

#### 	3.3.1 调用当前类中的属性或方法

​			特殊的：当方法 A 中又调用了方法 A：递归方法

​			方法中：不可以定义方法

## 4. 类的结构之三：构造器(Constructor)

Construct：建设、建造

Construction:  CCB(中国建设银行)

Constructor：建设者

### 4.1 构造器的作用

​		<font color='red'>**造对象一定要用到构造器（绝对正确）**</font>

​		1）创建对象

​		2）初始化对象的属性

### 4.2 说明

​		1）如果没有显式定义类的构造器的话，则系统默认提供一个空参的构造器，**这个构造器的权限和类的权限相同**

​		2）如果自己定义的话，格式为：

```java
权限修饰符 类名(形参列表){}
```

​		3）一个类中定义的多个构造器，彼此构成重载

​		4）一旦我们显式的定义了类的构造器以后，系统就不再提供默认的空参构造器

​		5）<font color='red'>一个类中至少会有一个构造器</font>

### 4.3 总结属性赋值的先后顺序

​		1）默认初始化

​		2）显式初始化

​		3）构造器中初始化

---------------------------------------------------------------------------------------------------

​		4）通过"对象.属性"或"对象.方法"的方式，赋值

​		以上操作的先后顺序：1）－　2）－　3）－　4）

### 4.4 JavaBean

​		JavaBean是一种Java语言写成的可重用组件

​		所谓JavaBean，是指符合如下标准的Java类：

​		1）类是公共的

​		2）有一个无参的公共的构造器

​		3）有属性，且有对应的get、set方法

### 4.5 扩展知识　UML图

![](./java_images/扩展知识：UML图.png)

## 5. “万事万物皆对象”

​		**1）**在Java语言范畴中，我们都将功能、结构等封装到类中，通过类的实例，来调用具体的功能结构

​				1> Scanner，String等

​				2> 文件：File

​				3> 网络资源：URL

​		**2）**涉及到Java语言与前端HTML、后端的数据库交互时，前后端的架构在Java层面交互时，都体现为类、对象

## 6. 再谈方法

### 6.1 方法的重载(overload)

#### 	6.1.1 定义

​			**在同一个类中，允许存在一个以上的同名方法，只要它们的参数个数或者参数类型不同即可**

​			"两同一不同"：同一个类、相同方法名

​									  参数列表不同：参数个数不同、参数类型不同

#### 	6.1.2 举例

​			Arrays类中重载的sort() / binarySearch()

#### 	6.1.3 是否是重载

​			与方法的权限修饰符、返回值类型、形参变量名、方法体都没有关系！

#### 	6.1.4 调用方法时

​			如何确定某一个指定的方法：

​			1）方法名

​			2）参数列表

### 6.2 可变个数形参

​		**JDK 5.0新增的内容**

#### 6.2.1 具体使用

##### 6.2.1.1 格式

​		数据类型 ... 变量名

##### 6.2.1.2 可变个数形参的数目

​		传入参数的数目可以是0个，1个，2个或者多个

##### 6.2.1.3 可变个数形参方法的重载

​		可变个数形参的方法与本类中方法名相同，形参不同的方法之间也构成重载

##### 6.2.1.4 特殊注意

​		可变个数形参的方法与本类中方法名相同，形参类型相同但是为数组的方法之间不构成重载，换句话说，两者不能共存

```java
// 重载
public void show(int a){}
public void show(String str){}
public void show(String ... strs){}

// 不构成重载
//　两者不能共存
public void show(String ... strs){}
public void show(String[] str){}
```

##### 6.2.1.5 可变个数形参的声明

​		1）可变个数形参在方法的形参中，<font color='red'>**必须声明在末尾**</font>

​		2）可变个数形参在方法的形参中，<font color='red'>**最多只能声明一个可变个数形参**</font>

### 6.3 方法参数传递<font color='red'>(难点)</font>

#### 6.3.1 变量的赋值

​		1）如果变量是基本数据类型，此时赋值的是变量真实存储的数据值

​		2）如果变量是引用数据类型，此时赋值的是变量真实存储的地址值

#### 6.3.2 方法形参的传递机制：<font color='red'>值传递</font>

##### 6.3.2.1 形参

​		方法定义时，声明的小括号内的参数

##### 6.3.2.2 实参

​		方法调用时，实际传递给形参的数据

#### 6.3.3 值传递机制

##### 6.3.3.1 基本数据类型

```java
public class ValuePass{
    public static void main(String[] args){
		int m = 10;
    	int n = 20;
        ValuePass test = new ValuePass();
        test.swap(m ,n);
        System.out.println("m is " + m + ", n is " + n);
    }
    
    // 失败的基本数据类型交换值方法
    public void swap(int m, int n){
        int temp = m;
        m = n;
        n = temp;
        //System.out.println("m is " + m + ", n is " + n);
    }
}
```

![](./java_images/基本数据类型交换.png)

##### 6.3.3.2 引用数据类型

```java
public class ValuePass2{
	public static void main(){
		Data data = new Data();
        data.m = 10;
        data.n = 20;
        
        ValuePass2 test = new ValuePass2();
        test.swap(data);
        System.out.println("m is " + m + ", n is " + n);
	}
    
    // 引用数据类型的交换值方法
    public void swap(Data data){
        int temp = data.m;
        data.m = data.n;
        data.n = temp;
    }
}

class Data{
    int m;
    int n;
}
```

​	![](./java_images/引用数据类型交换.png)

​		1）如果参数是基本数据类型，那么此时实参赋给形参的是实参真实存储的数据值，这时形参和实参是两块不同的内存，保存的数值相同

​		2）如果参数是引用数据类型，那么此时实参赋给形参的是实参真实存储的地址值，这时形参和实参是两块不同的内存，保存的数值相同

​		3）<font color='red'>**总结：**</font>传递的都是值，所以叫做值传递机制。但是两者主要的区别是由于 引用数据类型变量存的是一个地址，所以实际上分别操作两者就相当于操作同一块内存，而基本数据类型变量存的是一个值，所以操作两者相当于操作两个独立的变量

#### 6.3.4 内存解析练习

```java
public class TransferTest{
    public static void main(String[] args){
        TransferTest test = new TransferTest();
        test.first();
    }
    public void first(){
        int i = 5;
        Value v = new Value();
        v.i = 25;
        System.out.println(v.i);
    }
    public void second(Value v, int i){
        i = 0;
        v.i = 20;
        Value val = new Value();
        v = val;
        System.out.println(v.i + " " + i);
    }
}
class Value{
    int i = 15;
}
```

**答案见：./images/究级内存解析.png**

### 6.4 递归(recursion)方法(了解)

#### 6.4.1 定义

​		递归方法：一个方法体内调用它自身

#### 6.4.2 说明

​		1）方法递归包含了一种隐式的循环，它会重复执行某段代码，但这种重复执行无需循环控制

​		2）递归一定要向已知方向递归，否则这种递归就变成了无穷递归，类似于死循环

#### 6.4.3 示例

```java
// 例1：计算1-n之间所有自然数的和
// 例2：计算1-n之间所有自然数的乘积
// 例3：裴波那契数列
// 例4：汉诺塔问题
// 例5：快排
```

## 7. 面向对象的特征之一：封装与隐藏

### 7.1 为什么要引入封装性

​		概念：封装是把过程和数据包围起来，对数据的访问只能通过已定义的接口。面向对象计算始于这个基本概念，即现实世界可以被描绘成一系列完全自洽、封装的对象，这些对象通过一个受保护的接口访问其他对象。封装是一种信息隐藏技术，在 java 中通过关键字 **private**、**protected**和 **public** 实现封装。什么是封装？封装把对象的所有组成部分组合在一起，封装定义程序如何引用对象的数据，封装实际上使用方法将类的数据隐藏起来，控制用户对类的修改和访问数据的程度。适当的封装可以让程序代码更容易理解和维护，也加强了程序代码的安全性。

#### 7.1.1 高内聚，低耦合

 		我们程序设计追求”高内聚，低耦合“

​		**高内聚：**类的内部数据操作细节自己完成，不允许外部干涉

​		**低耦合：**仅对外暴露少量的方法用于使用

#### 7.1.2 隐藏对象内部的复杂性

​		只对外公布简单的接口，便于外界调用，从而提高系统的可扩展性、可维护性。通俗的说，<font color='red'>把该隐藏的隐藏起来，该暴露的暴露出来。这就是封装性的设计思想</font>

### 7.2 问题的引入

​		当我们创建一个类的对象以后，我们可以通过“对象.属性”的方式，对对象的属性进行赋值。这里，赋值操作要受到属性的数据类型和存储范围的制约。除此之外，没有其他制约条件。但是在实际问题中，我们往往需要给属性赋值加入额外的限制条件，这个条件就不能在属性声明时体现，我们只能通过方法进行限制条件的添加。（比如：set）同时，我们需要避免用户再使用“对象.属性”的方式对属性进行赋值，则需要将属性声明为私有的（private）

​		**此时针对于属性，就体现了封装性**

```java
public class AnimalTest{
	public static void main(String[] args){
		Animal a = new Animal();
        a.legs = -4; // 不应该允许这种负数的赋值
	}
}
class Animal{
	String name;
	int age;
	int legs; // 腿的个数
}
```

```java
public class AnimalTest{
	public static void main(String[] args){
		Animal a = new Animal();
        a.setLegs(-4);
        a.legs = -4; // 但是依旧可以直接赋值，所以需要对属性封装
	}
}
class Animal{
	String name;
	int age;
	int legs; // 腿的个数
        // 提供一个赋值的方法
        public void setLegs(int l){
        if(l >= 0 && l % 2 == 0){
            legs = l;
        }else{
            legs = 0;
        }
    }
}
```

```java
public class AnimalTest{
	public static void main(String[] args){
		Animal a = new Animal();
        a.setLegs(-4);
        a.legs = -4; // 这行会报错，Animal.legs is not visible
	}
}
class Animal{
	String name;
	int age;
	private int legs; // 腿的个数
        // 提供一个赋值的方法
        public void setLegs(int l){
        if(l >= 0 && l % 2 == 0){
            legs = l;
        }else{
            legs = 0;
        }
    }
}
```



### 7.3 封装性的体现

​		体现一：我们将类的属性xxx私有化(private)，同时提供公共的(public)方法来获取(getXxx)和设置(setXxx)此属性的值

​		体现二：不对外暴露的私有的方法

​		体现三：单例模式（将构造器私有化）

​		体现四：如果不希望类在包外被调用，可以将类设置为缺省的

### 7.4 权限修饰符

​		**封装性的体现，需要权限修饰符来配合**

#### 7.4.1 Java规定的四种权限

​		（从小到大排列）:private、缺省、protected、public

<img src="./java_images/权限修饰符.png" style="zoom: 200%;" />

#### 7.4.2 修饰符的使用范围

​		4种权限可以用来修饰**类以及类的内部结构**：属性、方法、构造器、内部类

#### 7.4.3 具体使用

​		1）4种权限都可以用来修饰**类的内部结构**：属性、方法、构造器、内部类

​		2）修饰**类**的话，只能用缺省、public

#### 7.4.4 总结

​		Java提供了4种权限修饰符来修饰类及类的内部结构，体现类及类的内部结构在被调用时的可见性的大小

## 8. 关键字

### 8.1 this的使用

#### 8.1.1 this的使用范围

​		this可以用来修饰：属性、方法；构造器

#### 8.1.2 this调用属性、方法

​		this理解为：当前对象或当前正在创建的对象

​		1）在类的方法中，我们可以使用"this.属性"或"this.方法"的方式，调用当前对象属性或方法。但是，通常情况下，我们都选择省略"this"。特殊情况下，如果方法的形参和类的属性同名时，我们必须显式的使用"this.变量"的方式，表示此变量是属性，而非形参

​		2）在类的构造器中，我们可以使用"this.属性"或"this.方法"的方式，调用当前正在创建的对象属性或方法。但是，通常情况下，我们都选择省略"this"。特殊情况下，如果构造器的形参和类的属性同名时，我们必须显式的使用"this.变量"的方式，表示此变量是属性，而非形参

#### 8.1.3 this调用构造器

​		1）我们在类的构造器中，可以显式的使用"this(形参列表)"方式，调用本类中指定的其他构造器

​		2）构造器中不能通过"this(形参列表)"的方式调用自己

​		3）如果一个类中有n个构造器，则最多有n - 1个构造器使用了"this(形参列表)"

​		4）规定："this(形参列表)"必须声明在当前构造器的首行

​		5）构造器内部：最多只能声明一个"this(形参列表)"用来调用其他的构造器

### 8.2 package的使用

#### 8.2.1 package的出现

​		为了更好的实现项目中类的管理，提出包的概念

#### 8.2.2 使用注意

​		1）使用package声明类或接口所属的包，声明在源文件的首行

​		2）包：属于标识符，遵循标识符的命名规则、规范(xxxyyyzzz)、“见名知意”

​		3）每"."一次，就代表一层文件目录

**补充：**同一个包下，不能命名同名的接口、类

​		    不同的包下，可以命名同名的接口，类

#### 8.2.3 JDK中常见包

​		1）java.lang：提供常用功能

​		2）java.net：包含执行与网络相关的操作的类和接口

​		3）java.io：包含能提供多种输入/输出功能的类

​		4）java.util：包含一些实用的工具类

​		5）java.text：包含了一些Java格式化相关的类

​		6）java.sql：包含了Java进行JDBC数据库编程的相关类/接口

​		7）java.awt：包含了构成抽象窗口工具集的多个类

#### 8.2.4 MVC设计模式

​		MVC是常用的设计模式之一，将整个程序分为三个层次：

​		1）数据模型层：model主要处理数据

​		2）视图模型层：view显示数据

​		3）控制器层：controller处理业务逻辑

![](./java_images/MVC设计模式.png)

### 8.3 import的使用

#### 8.3.1 作用

​		import：导入

​		在源文件中显式的使用import结构导入指定包下的类、接口

#### 8.3.2 使用注意

​		1）声明在包的声明和类的声明之间

​		2）如果需要导入多个结构，则并列写出即可

​		3）可以使用"xxx.*"的形式，表示可以导入xxx包下的所有结构

​		4）如果使用的类或接口是java.lang包下定义的，则可以省略import结构

​		5）如果使用的类或接口是本包下定义的，则可以省略import结构

​		6）如果在源文件中使用了不同包下的同名的类，则必须至少有一个类需要以全类名的方式显示

​		7）如果使用"xxx.*"方式表明可以调用xxx包下的所有结构，但是如果使用的是xxx子包下的结构，则仍需要显式导入

​		8）import static：导入指定**类或接口中的静态结构：**属性或方法

### 8.4 super的使用

#### 8.4.1 super的使用范围

​		super可以用来调用：属性、方法、构造器

#### 8.4.2 super调用属性、方法

​		super理解为：父类的

​		1）我们可以在子类的方法或构造器中，使用"super.属性"的方式，显式的调用父类中声明的属性，但是通常情况下，我们习惯省略"super"

​			  特殊情况：当子类和父类中定义了同名的属性时，我们想要在子类中调用父类中声明的属性，则必须显式的使用"super.属性"的方式，表明调用的是父类中声明的属性

​		2）我们可以在子类的方法或构造器中，使用"super.方法"的方式，显式的调用父类中声明的方法，但是通常情况下，我们习惯省略"super"

​			  特殊情况：当子类重写了父类中的方法以后，我们想要在子类中调用父类中被重写的方法时，则必须显式的使用"super.方法"的方式，表明调用的是父类中被重写的方法 

#### 8.4.3 super调用构造器

​		1）我们可以在子类的构造器中显式的使用"super(形参列表)"的方式，调用父类中声明的指定的构造器

​		2）"super(形参列表)"的使用，必须声明在子类构造器的首行

​		<font color='red'>3）我们在类的构造器中，针对于"this(形参列表)"或"super(形参列表)"只能二选一，不能同时出现</font>

​		<font color='red'>4）在构造器的首行，没有显式的声明"this(形参列表)"或"super(形参列表)"，则默认调用的是父类中空参的构造器：super()</font>

​		<font color='red'>5）在类的多个构造器中，至少有一个类的构造器中使用了"super(形参列表)"，调用父类中的构造器</font>

## 9. Eclipse快捷键

1. 补全代码的声明：alt + /

2. 快速修复：ctrl + 1

3. 批量导包：ctrl + shift + o

4. 使用单行注释：ctrl + /

5. 使用多行注释：ctrl + shift + /

6. 取消多行注释：ctrl + shift + \

7. 复制指定行的代码：ctrl + alt + down 或 ctrl + alt + up

8. 删除指定行的代码：ctrl + d

9. 上下移动代码：alt + up或alt + down

10. 切换到下一行代码空位：shift + enter

11. 切换到上一行代码空位：ctrl + shift + enter

12. 如何查看源码：ctrl + 选中指定结构　或　ctrl + shift + t

13. 退回到前一个编辑的页面：alt + left

14. 进入到下一个编辑的页面（针对于上面那条）：alt + right

15. 光标选中指定的类，查看继承树结构：ctrl + t

16. 复制代码：ctrl + c

17. 撤销：ctrl + z

18. 反撤销：ctrl + y

19. 剪切：ctrl + x

20. 粘贴：ctrl + v

21. 保存：ctrl + s

22. 全选：ctrl + a

23. 格式化代码：ctrl + shift + f

24. 选中数行，整体向后移动：tab

25. 选中数行，整体向前移动：shift + tab

26. 在当前类中，显示类结构，并支持搜索指定的方法、属性等：ctrl + o

27. 批量修改指定的变量名、方法名、类名等：alt + shift + r

28. 选中结构的大小写的切换：变成大写：ctrl + shift + x

29. 选中结构的大小写的切换：变成小写：ctrl + shift + y

30. 调出生成getter/setter/构造器等结构：alt + shift + s

31. 显示当前选择资源（工程/文件）的属性：alt + enter

32. 快速查找：参照选中的Word快速定义到下一个：ctrl + k

    -----------------------------------------------------------------------------------

33. 关闭当前窗口：ctrl + w

34. 关闭所有的窗口：ctrl + shift + w

35. 查看指定的结构使用过的地方：ctrl + alt + g

36. 查找和替换：ctrl + f

37. 最大化当前的View:  ctrl + m

38. 直接定位到当前行的首位：home

39. 直接定位到当前行的末位：end

# 二、面向对象－中

## 1. 面向对象的特征之二：继承性(inheritance)

### 1.1 继承性的好处

​		1）减少了代码的冗余，提高了代码的复用性

​		2）便于功能的扩展

​		3）为之后的多态性的使用，提供了前提

### 1.2 继承性的格式

```java
class A extends B{}
```

- A: 子类、派生类、subclass


- B: 父类、超类、基类、superclass


#### 1.2.1 继承性的体现

​		一旦子类A继承父类B以后，子类A中就获取了父类B中声明的所有的属性和方法

​		<font color='red'>特别的，父类中声明为private的属性或方法，子类继承父类以后，仍然认为获取了父类中私有的结构。</font>只是因为封装性的影响，使得子类不能直接调用父类的结构而已

####  1.2.2 继承性的扩展

​		子类继承父类以后，还可以声明自己特有的属性或方法：实现功能的扩展

​		**子类和父类的关系不同于子集和集合的关系**

​		extends: 延展、扩展

### 1.3 继承性的规定

​		1）一个类可以被多个子类继承

​		2）Java中类的单继承性：一个类只能有一个父类

​		3）子父类是相对的概念

​		4）子类直接继承的父类，称为直接父类；间接继承的父类称为间接父类

​		5）子类继承父类以后，就获取了直接父类以及所有间接父类中声明的属性和方法

### 1.4 “众类之父”

​		1）如果我们没有显式的声明一个类的父类的话，则此类继承于java.lang.Object类

​		2）所有的Java类（除java.lang.Object类之外）都直接或间接的继承于java.lang.Object类

​		3）意味着，所有的Java类具有java.lang.Object类声明的功能

## 2. 项目

### 2.1 代码

​		至少独立完成一遍以上的项目代码

### 2.2 Bug

​		积累完成项目的过程中常见的bug的调试

​		方式一：“硬”看，必要时，添加输出语句

​		方式二：Debug

### 2.3 思路和逻辑

​		捋顺思路，强化逻辑

### 2.4 内存解析

​		对象、数组等内存结构的解析

### 2.5 规范

​		遵守编码的规范，标识符的命名规范等

```java
int i1 = 10;
int total = 0;
```

### 2.6 注释

​		在类前、方法前、方法内具体逻辑的实现步骤等添加必要的注释

​		1）类前、方法前、属性前：文档注释

​		2）逻辑步骤：单行注释、多行注释

## 3. 方法的重写(Override/Overwrite)

### 3.1 定义

​		在子类中可以根据需要对从父类中继承来的方法进行改造，也称为方法的<font color='red'>重置、覆盖</font>。在程序执行时，子类的方法将覆盖父类的方法

### 3.2 要求

​		子类继承父类以后，可以对父类中<font color='red'>同名同参数</font>的方法，进行覆盖操作

### 3.3 应用

​		重写以后，当创建子类对象以后，通过子类对象调用子父类中同名同参数的方法时，实际上执行的是子类重写父类的方法

### 3.4 注意

```java
权限修饰符 返回值类型 方法名(形参列表) throws 异常的类型{
	// 方法体
}
```

约定俗成：子类中的叫重写的方法，父类中的叫被重写的方法

#### 3.4.1 重写的规定

​		1）子类重写的方法的方法名和形参列表与父类被重写的方法的方法名和形参列表相同	

​		2）子类重写的方法的权限修饰符不小于父类中被重写的方法的权限修饰符

​			  <font color='red'>**特殊情况：子类不能重写父类中声明为private权限的方法**</font>

​		3）返回值类型：

​				1> 父类被重写的方法的返回值类型是void，则子类重写的方法的返回值类型只能是void

​				2> 父类被重写的方法的返回值类型是A类型，则子类重写的方法的返回值类型可以是A类或A类的子类

​				3> 父类被重写的方法的返回值类型是基本数据类型，则子类重写的方法的返回值类型必须是相同的基本数据类型

​		4）子类重写的方法抛出的异常类型不大于父类被重写的方法抛出的异常类型（具体放到异常处理时候讲）

![](./java_images/重载与重写的区别.png)

---------------------------------------------------------------------------------------------------

​		子类和父类中的同名同参数的方法要么都声明为非static的（考虑重写），要么都声明为static的（不是重写）

## 4. 子类对象实例化的全过程

![](./java_images/子类对象的实例化过程.png)

### 4.1 从结果上来看（继承性）

​		子类继承父类以后，就获取了父类中声明的属性或方法

​		创建子类的对象，在堆空间中，就会加载所有的父类中声明的属性

### 4.2 从过程上来看

​		当我们通过子类的构造器构造子类对象时，我们一定会直接或间接的调用其父类的构造器，进而调用父类的父类的构造器...直到调用了java.lang.Object类中空参的构造器为止。正因为加载过所有父类的结构，所以才可以看到内存中有父类中的结构，子类对象才可以考虑进行调用

### 4.3 注意

![](./java_images/子类只创建一个对象.png)

​		明确：虽然创建子类对象时，调用了父类的构造器。但是自始自终就创建过一个对象，即为new的子类对象

## 5. 面向对象特征之三：多态性

### 5.1 理解

​		可以理解为一个事物的多种形态

### 5.2 体现

​		对象的多态性：父类的引用指向子类的对象（或子类的对象赋给父类的引用）

​		可以直接应用在抽象类和接口上

### 5.3 原因

#### 5.3.1 编译时类型和运行时类型

​		Java引用数据类型变量有两个类型：

​		1）**编译时类型：**由声明该变量时使用的类型决定

​		2）**运行时类型：**由实际赋给该变量的对象决定

​		<font color='red'>简称：编译时看左边，运行时看右边</font>

#### 5.3.2 编译时类型和运行时类型不一致

​		**若编译时类型和运行时类型不一致，就出现了对象的多态性**

​		多态情况下，“看左边”：看的是父类的引用（父类中不具备子类特有的方法）

​							   “看右边”：看的是子类的对象（实际运行的是子类重写父类的方法）

### 5.4 使用：虚拟方法调用

```java
public class AnimalTest{
    public static void main(String[] args){
        AnimalTest test = new AnimalTest();
        test.func(new Dog());
        
        test.func(new Cat());
    }
    
    public void func(Animal animal){
        animal.eat();
        animal.shout();
    }
}

class Animal{
    public void eat(){
        System.out.println("动物：进食");
    }
    public void shout(){
        System.out.println("动物：叫");
    }
}
class Dog extends Animal{
    public void eat(){
        System.out.println("狗吃骨头");
    }
    public void shout(){
        System.out.println("汪！汪！汪！");
    }
}
class Cat extends Animal{
    public void eat(){
        System.out.println("猫吃鱼");
    }
    public void shout(){
        System.out.println("喵！喵！喵！");
    }
}
```

​		有了对象的多态性以后，我们在编译期，只能调用父类中声明的方法；但在运行期，我们实际执行的是子类重写父类的方法

#### 5.4.1 正常的方法调用

```java
Person e = new Person();
e.getInfo();

Student e = new Student();
e.getInfo();
```

#### 5.4.2 虚拟方法调用

​		子类中定义了与父类同名同参数的方法，在多态情况下，将此时父类的方法称为虚拟方法，父类根据赋给它的不同子类对象，动态调用属于子类的该方法。这样的方法调用在编译期是无法确定的

```java
Person e = new Student();
e.getInfo();   // 调用Student类的getInfo()方法
```

​		编译时e为Person类型，而方法的调用是在运行时确定的，所以调用的是Student类的getInfo()方法——<font color='red'>动态绑定</font>

**思考：如何证明多态性是运行时行为**

### 5.5 使用前提

​		1）类的继承关系

​		2）方法的重写

​		3）父类引用指向子类对象

### 5.6 适用范围

​		<font color='red'>**只适用于方法，不适用于属性(编译和运行都看左边)**</font>

### 5.7 instanceof操作符

#### 5.7.1 为什么要有instanceof操作符

![](./java_images/向下转型与多态.png)

```java
class Person(){
    int name;
}
class Man extends Person{
    boolean isSmoking;
    public void earnMoney(){
        Systemout.println("男人赚钱养家");
    }
}
class Woman extends Person{
    public void goShopping(){
        System.out.println("女人喜欢逛街");
    }
}
// 在使用多态性时，不能调用子类特有的方法、属性；编译时p是Person类型
Person p = new Man();
// 有了对象的多态性以后，内存中实际上是加载了子类特有的属性和方法的，但是由于变量声明为父类类型，导致编译时，只能调用父类中声明的属性和方法，子类特有的属性和方法不能调用
p.name = "Tom";
// 这两行都会报错
p.earnMoney();
p.isSmoking = true;
// 如何才能调用子类特有的属性和方法
// 向下转型：使用强制类型转换符
Man man1 = (Man)p;
man1.earnMoney();
man1.isSmoking = true;
// 使用强转时，可能会出现ClassCastException的异常
Woman woman1 = (Woman)p;
woman1.goShopping();
```

#### 5.7.2 使用

```java
a instanceof A：判断对象 a是否是类 A的实例，如果是返回true，否则返回false
```

```java
if(p instanceof Woman){
	Woman woman2 = (Woman)p;
	woman2.goShopping();
	System.out.println("***Woman***");
}else if(p instanceof Man){
	Man man2 = (Man)p;
	man2.earnMoney();
	System.out.println("***Man***");
}
```

#### 5.7.3 使用情境

为了避免在向下转型时出现ClassCastException的异常，我们在向下转型之前，先进行instanceof的判断，一旦返回true，就进行向下转型；如果返回false，则不进行向下转型

#### 5.7.4 返回值

如果a instanceof A返回true，则a instanceof B也返回true（其中类B是类A的父类）

#### 5.7.5 使用规则

要求a所属的类与类A必须是子类和父类的关系，否则编译错误（编译器就能判断两者无关）

### 5.8 面试题

#### 5.8.1 方法的重载和重写的区别

​		1）**二者的定义细节：**略

​		2）**从编译和运行的角度来看：**

​		重载，是指允许存在多个同名的方法，而这些方法的参数不同。编译器根据方法不同的参数列表，对同名方法的名称做修饰。对于编译器而言，这些同名方法就成了不同的方法。<font color='red'>它们的调用地址在编译期就已经绑定了。</font>Java的重载是可以包括父类和子类的，即子类可以重载父类的同名不同参数的方法

​		所以：对于重载而言，在方法调用之前，编译器就已经确定了所要调用的方法，这称为<font color='red'>“早绑定”</font>或<font color='red'>“静态绑定”</font>

​		而对于多态，只有等到方法调用的那一刻，解释运行器才会确定所要调用的具体方法，这称为<font color='red'>“晚绑定”</font>或<font color='red'>“动态绑定”</font>

​		引用一句Bruce Eckel的话：<font color='red'>“不要犯傻，如果它不是晚绑定，它就不是多态”</font>

#### 5.8.2 谈谈你对多态性的理解

​		1）实现**代码的通用性**

​		2）Object类中定义的public boolean equals(Object obj){}

​			   JDBC：使用Java程序操作（获取数据库连接、CRUD）数据库（MySQL、Oracle、DB2、SQL、Server）

​		3）抽象类、接口的使用肯定体现了多态性（抽象类、接口不能实例化　）

### 5.9 多态的深入理解

​		1）若子类重写了父类的方法，就意味着子类里定义的方法彻底的覆盖了父类里的同名方法，系统将不可能再把父类里的方法转移到子类中：编译看左边，运行看右边

​		2）对于实例变量则不存在这样的现象。即使子类里定义了与父类完全相同的实例变量，这个实例变量依然不可能覆盖父类中定义的实例变量：编译运行都看左边 

### 5.10 面试答题套路

​		先直接描述问题

​		然后说一下使用情境（多说项目中的使用情景　）

## 6. Object类的使用

### 6.1 Object类介绍

​		1）Object类是所有Java类的根父类

​		2）如果在类的声明中未使用extends关键字指明其父类，则默认父类为java.lang.Object类

​		3）Object类中的功能（属性、方法）就具有通用性

​				属性：无

​				方法：equals() / toString() / getClass() / hashCode() / clone() / finalize()

​						   wait()、notify()、notifyAll()

​		4）Object中只声明了一个空参的构造器　

​		5）数组也作为Object类的之类出现，可以调用Object类中声明的方法

### 6.2 面试题：== 和 equals()区别

#### 6.2.1 ==的使用

​		1）可以使用在基本数据类型变量和引用数据类型变量中

​		2）如果比较的是基本数据类型变量：比较两个变量保存的数据是否相等（不一定类型要相同）

​	  		如果比较的是引用数据类型变量：比较两个对象的地址值是否相同，即两个引用是否指向堆空间中同一个对象实体

​		3）==符号使用时，必须保证符号左右两边的变量类型一致

#### 6.2.2 equals()的使用

​		1）是一个方法，而非运算符

​		2）只能使用在引用数据类型变量中

​		3）Object类中equals()的定义：

```java
public boolean equals(Object obj){
	return (this == obj);
}
```

​		说明：Object类中定义的equals()和==的作用是相同的：比较两个对象的地址值是否相同，即两个引用是否指向同一个对象实体

​		4）像String、Date、File、包装类等都重写了Object类中的equals()方法。重写以后，比较的不是两个引用的地址是否相同，而是比较这两个对象的“实体内容”是否相同

​		5）通常情况下，我们自定义的类如果使用equals()方法的话，也通常是比较两个对象的“实体内容”是否相同，那么我们就需要对Object类中的equals()方法进行重写

​		6）重写的原则：比较两个对象的“实体内容“是否相同

### 6.3 toString()方法

#### 6.3.1 toString()的使用

​		当我们输出一个对象的引用时，实际上就是调用当前对象的toString()方法

```java
@Test
public void test(){
    String s = "abc";
    System.out.println(s); // abc
    System.out.println(s.toString); // abc
    s = null;
    System.out.println(s); // null
    System.out.println(s.toString); // 出现NullPointerException
}
```

#### 6.3.2 toString()的定义

```java
public String toString(){
	return getClass().getName() + "@" + Integer.toHexString(hashCode());
}
```

#### 6.3.3 重写toString()方法

​		像String、Date、File、包装类等都重写了Object类中的toString()方法，使得在调用对象的toString()时，返回“实体内容”信息

#### 6.3.4 自定义重写toString()方法

```java
public class Person{
    // 属性
    private String name;
    private int age;
    // 构造器
    public Person(){
        
    }
    public Person(String name, int age){
        this.name = name;
        this.age = age;
    }
    // 重写toString()方法
    public String toString(){
        return "Person [name = " + name + ", age = " + age + "]";
    }
}
```

## 7. 单元测试

**JUnit 单元测试**

### 7.1 步骤

​		1）选中当前工程－右键选择: build path－add libraries－JUnit 4－下一步

​		2）创建Java类，进行单元测试

​			  此时的Java类要求

​					1> 此类是public的

​					2> 此类提供公共的无参的构造器

​		3）此类中声明单元测试方法

​			  此时的单元测试方法：方法的权限是public，没有返回值，没有形参

​		4）此单元测试方法上需要声明注解@Test，并在单元测试类中导入：import org.junit.Test;

​		5）声明好单元测试方法以后，就可以在方法体内测试相关的代码

​		6）写完代码以后，左键双击单元测试方法名，右键：run as－JUnit Test

### 7.2 说明

​		1）如果执行结果没有任何异常：绿条

​		2）如果执行结果出现异常：红条

## 8. 包装类(Wrapper)

### 8.1 介绍

​		针对八种基本数据类型相应的引用类型－包装类（封装类）

​		有了类的特点，就可以调用类中的方法，Java才是真正的面向对象

### 8.2 使用

​		Java提供了8种基本数据类型对应的包装类，为了使基本数据类型的变量具有类的特征

![](./java_images/包装类.png)

### 8.3 转换

​		基本类型、包装类与String类间的转换

---------------------------------------------------------------------------------------------------

​		基本数据类型----->包装类：调用包装类的构造器

```java
int number1 = 10;
Integer n1 = new Integer(number1);
float number2 = 10.5f;
Float n2 = new Float(number2);
```

​		包装类----->基本数据类型：调用包装类Xxx的xxxValue()

```java
Integer n1 = new Integer(10);
int number1 = n1.intValue();
```

---------------------------------------------------------------------------------------------------

​		基本数据类型、包装类--->String类：

```java
// 方式1：连接运算
int num1 = 10;
String str1 = num1 + "";
// 方式2：调用String的valueOf(Xxx xxx)
float f1 = 12.3f;
String str2 = String.valueOf(f1);  // "12.3"

Double d1 = new Double(12.4);
String str3 = String.valueOf(d1);  // "12.4"
```

​		String类--->基本数据类型、包装类：调用包装类的parseXxx()

```java
int num2 = Integer.parseInt("123");
boolean b1 = Boolean.parseBoolean("true");
// 可能会报NumberFormatException
```

### 8.4 JDK 5.0新特性

​		**自动装箱与自动拆箱**

#### 8.4.1 自动装箱

```java
int num1 = 10;
Integer num2 = num1;  // 自动装箱

boolean b1 = true;
Boolean b2 = b1;  // 自动装箱

public void method(Object obj){
    System.out.println(obj);
}
```

#### 8.4.2 自动拆箱

```java
Integer num1 = new Integer(10);
int num2 = num1;  // 自动拆箱
```

### 8.5 关于包装类使用的面试题

```java
@Test
public void test(){
    Integer i = new Integer(1);
    Integer j = new Integer(1);
    System.out.println(i == j);  // false
    
    // Integer内部定义了IntegerCache结构，IntegerCache中定义了Integer[]
    // 保存了从－128 - 127范围的整数。如果我们使用自动装箱的方式，给Integer赋值
    // 的范围在-128 - 127范围内时，可以直接使用数组中的元素，不用再去new了。目的：提高效率
    Integer m = 1;
    Integer n = 1;
    System.out.println(m == n);  // true
    
    Integer x = 128;   // 相当于new了一个Integer对象
    Integer y = 128;   // 相当于new了一个Integer对象
    System.out.println(x == y);  // false
}
```

### 8.6 应用场景举例

​		1）Vector类中关于添加元素，只定义了形参为Object类型的方法：

```java
v.addElement(Object obj);  //基本数据类型－>包装类－>使用多态
```

## 9. 总结

### 9.1 如何实现向下转型？需要注意什么问题？如何解决此类问题？

```java
Person p = new Man();
// 使用强转符：()
Man m = (Man)p;
// 可能ClassCastException异常
// 使用instanceof在进行向下转型前判断
if(p instanceof Man){
    Man m = (Man)p;
}
```

### 9.2 == 和 equals()有何区别？

### 9.3 写出8种基本数据类型及其对应的包装类

int Integer

char Character

### 9.4 基本数据类型、包装类与String三者之间如何转换

自动装箱、自动拆箱

基本数据类型、包装类--->String: String.valueOf(Xxx xxx);

String--->基本数据类型、包装类: Xxx.parseXxx(str);

# 三、面向对象－下

## 1. static关键字的使用

### 1.1 原因

​		当我们编写一个类时，其实就是在描述其对象的属性和行为，而并没有产生实质上的对象，只有通过new关键字才会产生出对象，这时，系统才会分配内存空间给对象，其方法才可以供外部调用。

​		我们有时候希望无论是否产生了对象或无论产生了多少对象的情况下，<font color='red'>某些特定的数据在内存空间里只有一份</font>，例如所有的中国人都有个国家名称，每一个中国人都共享这个国家名称，不必在每一个中国人的实例对象中都单独分配一个用于代表国家名称的变量。

### 1.2 使用

​		1）static：静态的

​		2）static可以用来修饰：属性、方法、代码块、内部类 

### 1.3 修饰属性：静态变量（或类变量）

#### 1.3.1 静态属性  vs  非静态属性（实例变量）

​		属性，按照是否使用static关键字修饰分为静态属性  vs   非静态变量

​		**实例变量：**我们创建了类的多个对象，每个对象都独立的拥有一套类中的非静态属性。当修改其中一个对象中的非静态属性时，不会导致其他对象中同样的属性值的修改。

​		**静态变量：**我们创建了类的多个对象，多个对象共享同一个静态变量。当通过某一个对象修改静态变量时，会导致其他对象调用此静态变量时，是修改过了的

#### 1.3.2 其他说明

​		1）静态变量随着类的加载而加载。可以通过"类.静态变量"的方式进行调用

​		2）静态变量的加载要早于对象的创建。

​		3）由于类只会加载一次，所以静态变量在内存中也只会存在一份：存在方法区的静态域中

|      | 类变量 | 实例变量 |
| ---- | ------ | -------- |
| 类   | yes    | no       |
| 对象 | yes    | yes      |

#### 1.3.3 静态属性举例

​		System.out

​		Math.PI

#### 1.3.4 内存解析

![](./java_images/类变量vs实例变量内存解析.png)

### 1.4 修饰方法：静态方法

#### 1.4.1 使用

​		1） 随着类的加载而加载，可以通过"类.静态方法"的方式进行调用

​		2）通过类名只能调用静态方法，无法调用非静态方法

|      | 静态方法 | 非静态方法 |
| ---- | -------- | ---------- |
| 类   | yes      | no         |
| 对象 | yes      | yes        |

​		3）静态方法中，只能调用静态的方法或属性

​			  非静态方法中，既能够调用非静态的方法或属性，也可以调用静态的方法或属性

### 1.5 static注意点

​		1）在静态的方法中，不能使用this关键字、super关键字

​		2）关于静态属性和静态方法的使用，大家都从生命周期的角度去理解

### 1.6 开发中，如何确定一个属性是否需要声明为static的？

​		1）属性是可以被多个对象共享的，不会随着对象的不同而不同的

​		2）类中的常量也常常声明为static的

### 1.7 开发中，如何确定一个方法是否要声明为static的？

​		1）操作静态属性的方法，通常设置为static的

​		2）工具类中的方法，习惯上声明为static的。比如：Math、Arrays、Collections

## 2. 单例(Singleton)设计模式

### 2.1 设计模式

​		**设计模式**<font color='red'>是在大量的实践中总结和理论化以后优选的代码结构、编程风格、以及解决问题的思考方式。</font>设计模式免去我们自己再思考和摸索。模式就像是经典的棋谱，不同的棋局，我们用不同的棋谱。<font color='red'>**“套路”**</font>

### 2.2 单例模式

#### 2.2.1 单例模式的含义

​		所谓类的单例设计模式，就是采取一定的方法保证在整个的软件系统中，对某个类<font color='red'>**只能存在一个对象实例**</font>，并且该类只提供一个取得其对象实例的方法

#### 2.2.2 如何实现单例模式

​		我们首先必须将<font color='blue'>类的构造器的访问权限设置为private</font>，这样，就不能在类的外部使用new操作符构造类的对象了。但在类的内部，仍然可以产生对象。因为在类的外部无法得到类的对象，只能<font color='blue'>调用该类的某个静态方法</font>以返回类内部创建的对象。静态方法只能访问类中的静态变量，所以，指向类内部产生的<font color='blue'>该类对象的变量也必须定义为静态的</font>。

#### 2.2.3 代码实现

##### 2.2.3.1 饿汉式实现

```java
class Bank{
	// 1. 私有化类的构造器
    private Bank(){
        
    }
    // 2. 内部创建类的对象
    // 4. 要求此对象也声明为静态的
    private static Bank instance = new Bank();
    // 3. 提供公共的静态的方法，返回类的对象
    private static Bank getInstance(){
        return instance;
    }
}
```

##### 2.2.3.2 懒汉式实现

```java
class Order{
    // 1. 私有化类的构造器
    private Order(){
        
    }
    // 2. 声明当前类对象，没有初始化
    // 4. 此对象也必须声明为static的
    private static Order instance = null;
    // 3. 声明public、static的返回当前类对象的方法
    public static Order getIntance(){
        if(instance == null){
	        instance = new Order();
        }
        return instance;
    }
}
```

##### 2.2.3.3 区分饿汉式和懒汉式

​		**饿汉式：**

​				坏处：对象加载时间过长。

​				好处：饿汉式是线程安全的

​		**懒汉式：**

​				好处：延迟对象的创建。

​				坏处：目前的写法，线程不安全－－－>到多线程内容时，再修改

### 2.3 单例模式的优点

​		由于单例模式只生成一个实例，减少了系统性能开销，当一个对象的产生需要比较多的资源时，如读取配置、产生其他依赖对象时，则可以通过在应用启动时直接产生一个单例对象，然后永久驻留内存的方式来解决

#### 2.3.1 举例

​		java.lang.Runtime

#### 2.3.2 单例模式应用场景

​		1）网站的计数器

​		2）应用程序的日志应用

​		3）数据库连接池

​		4）读取配置文件的类

​		5）Application也是单例的典型应用

​		6）Windows的Task Manager（任务管理器）

​		7）Windows的Recycle Bin（回收站）

## 3. 理解main

### 3.1 main()方法的使用说明

​		1）main()方法作为程序的入口

​		2）main()方法也是一个普通的静态方法

​		3）main()方法可以作为我们与控制台交互的方式。（之前使用Scanner）  

## 4. 类的结构之四：代码块（或初始化块）

### 4.1 作用

​		用来初始化类、对象的信息

### 4.2 分类

​		<font color='red'>**代码块如果有修饰的话，只能使用static**</font>

​		根据代码块前是否有static修饰，代码块分为：

​				1）静态代码块

​				2）非静态代码块

### 4.3 静态代码块

​		1）内部可以有输出语句

​		2）随着类的加载而执行，而且只执行一次

​		3）作用：初始化类的信息

​		4）如果一个类中定义了多个静态代码块，则按照声明的先后顺序执行

​		5）静态代码块的执行要优先于非静态代码块的执行

​		6）静态代码块内只能调用静态的属性、静态的方法，不能调用非静态的结构

### 4.4 非静态代码块

​		1）内部可以有输出语句

​		2）随着对象的创建而执行

​		3）每创建一个对象，就执行一次非静态代码块

​		4）作用：可以在出创建对象时，对对象的属性等进行初始化

​		5）如果一个类中定义了多个非静态代码块，则按照声明的先后顺序执行

​		6）非静态代码块内可以调用静态的属性、静态的方法，或非静态的属性、非静态的方法

### 4.5 对属性可以赋值的位置

​		1）默认初始化

​		2）显式初始化

​		3）构造器初始化

​		4）有了对象以后，可以通过"对象.属性"或"对象.方法"的方式进行赋值

​		5）在代码块中进行赋值

其中先后顺序为：1    -     2 / 5    -    3    -    4

### 4.6 总结

​		<font color='red'>**由父及子，静态先行**</font>

## 5. final关键字的使用

 ### 5.1 可修饰的结构

​		类、方法、变量

### 5.2 final修饰类

​		final用来修饰一个类：此类不能被其他类所继承

​											   比如：String类、System类、StringBuffer类

### 5.3 final修饰方法

​		final用来修饰一个方法：表明此方法不可以被重写

​												   比如：Object类中的getClass()方法

### 5.4 final修饰变量

​		final用来修饰一个变量：此时的”变量“就称为是一个常量

​		修饰基本数据类型时，该变量的值不可被更改

​		<font color="red">**修饰引用数据类型时，该变量的地址值不可更改，但指向的对象的属性可以更改**</font>

#### 5.4.1 final修饰属性

​		可以考虑的赋值的位置有：

​		1）显式初始化

​		2）代码块中初始化

​		3）构造器中初始化

#### 5.4.2 final修饰局部变量

​		尤其是使用final修饰形参时，表明此形参是一个常量。当我们调用此方法时，给常量形参赋一个实参。一旦赋值以后，就只能在方法体中使用此形参，但不能重新赋值。

### 5.5 static final合用

​		只能用来修饰属性、方法

#### 5.5.1 用来修饰属性

​		全局常量

#### 5.5.2 用来修饰方法 

### 5.6 小结：一叶知秋

```java
public static void main(String[] args){// 方法体}

权限修饰符：private 缺省　protected public
修饰符：static \ final \ abstract \ native 可以用来修饰方法
返回值类型：无返回值 / 有返回值 -->return
方法名：需要满足标识符命名的规则、规范：“见名知意”
形参列表：重载 vs 重写：参数的值传递机制：体现对象的多态性
方法体：来体现方法的功能
```

## 6. abstract关键字的使用

### 6.1 抽象的

​		随着继承层次中一个个新子类的定义，类变得越来越具体。有时我们将父类设计的非常抽象，以至于我们每次造对象都是造子类的对象，不需要去造父类的对象了，这个时候我们就将这个父类叫做抽象类，表示规定该类不能在造实例了

### 6.2 abstract用来修饰类和方法

#### 6.2.1 abstract修饰类：抽象类

​		1）<font color='red'>**此类不能实例化**</font>

​		2）抽象类中一定有构造器，便于子类实例化时调用（涉及：子类对象实例化的全过程）

​		3）开发中，都会提供抽象类的子类，让子类对象实例化，完成相关的操作

```java
public class AbstractTest{
    public static void main(String[] args){
		
        // 一旦Person类抽象了，就不可实例化
        // Person p = new Person();
        // p1.eat();
	}   
}

abstract class Person{
    String name;
    int age;
    
    public Person(){
        
    }
    public Person(String name, int age){
        this.name = name;
        this.age = age;
    }
    
    public void eat(){
        System.oout.println("Person can eat.");
    }
}

class Student extends Person{
    public Student(String name, int age){
        super(name, age);
    }
}
```

#### 6.2.2 abstract修饰方法：抽象方法

​		1）抽象方法只有方法的声明，没有方法体

​		2）包含抽象方法的类，一定是一个抽象类。反之，抽象类中可以没有抽象方法

​		3）若子类重写了父类中的所有抽象方法以后，此子类方可实例化

​			  若子类没有重写父类中的所有抽象方法，则此子类也是一个抽象类，需要使用abstract修饰

```java
public class AbstractTest{
    public static void main(String[] args){
		
        // 一旦Person类抽象了，就不可实例化
        // Person p = new Person();
        // p1.eat();
	}   
}

abstract class Person{
    String name;
    int age;
    
    public Person(){
        
    }
    public Person(String name, int age){
        this.name = name;
        this.age = age;
    }
    
    public void eat(){
        System.oout.println("Person can eat.");
    }
    public abstract walk();
}

class Student extends Person{
    public Student(String name, int age){
        super(name, age);
    }
    public void walk(){
        System.out.println("Student can walk and run!");
    }
}
```

### 6.3 abstract使用上的注意点

​		1）abstract不能用来修饰：属性、构造器等结构

​		2）abstract不能用来修饰私有方法、静态方法、final的方法、final的类

### 6.4. 抽象类的匿名子类

```java
abstract class Creature{
    public abstract void eat();
    public abstract void breathe();
}

abstract class Person extends Creature{
    
}

class Worker extends Person{
    public void eat(){
        System.out.println("工人要吃的多。");
    }
    public void breathe(){
        System.out.println("工人呼吸很粗重。");
    }
}

public class AbstractClassTest{
	public static void main(String[] args){
        Worker worker = new Worker();
        method(worker);  // 非匿名的类非匿名对象
        
        method(new Worker()); // 非匿名的类匿名对象
        // 创建匿名子类的非匿名对象
        Person p = new Person(){ 
    	
            @Override
    		public void eat(){
        		System.out.println("吃东西");
    		}
    		@Override
    		public void breathe(){
       			System.out.println("好好呼吸");
    		}
		};
		method(p);
        System.out.println("********************");
        // 创建匿名子类的匿名对象
        method(new Person(){
            
            @Override
    		public void eat(){
        		System.out.println("吃东西");
    		}
    		@Override
    		public void breathe(){
       			System.out.println("好好呼吸");
    		}
        });
    }
    
    public static void method(Person p){
        p.eat();
        p.breathe();
    }
}
```

## 7. 接口的使用

### 7.1 概述

​		1）使用interface来定义

​		2）Java中，接口和类是并列的两个结构

​		3）接口中不能定义构造器的！意味着接口不可以实例化

​		4）Java开发中，接口通过让类去实现(implements)的方式来使用

​			  如果实现类覆盖了接口中所有的抽象方法，则此实现类就可以实例化

​			  如果实现类没有覆盖接口中所有的抽象方法，则此实现类仍为一个抽象类

​		5）接口的具体使用，体现了多态性

​		6）接口，实际上就可以看做是一种规范

​		7）Java只有单继承，但是还有多实现（一个类继承其他类，只能直接继承一个父类，但是实现类实现接口的时候，可以实现多个接口。）

### 7.2 接口的定义

#### 7.2.1  JDK1.8及以前

​		只能定义全局常量和抽象方法

​		1）全局常量：public static final

​		2）抽象方法：public abstract的

​		但是书写时可以省略不写，新手建议写上防止遗忘

```java
interface Flyable{
    // 全局常量
    public static final MAX_SPEED = 7900;   // 第一宇宙速度
    int MIN_SPEED = 1; // 省略了public static final
    
    // 抽象方法
    public abstract void fly();
    // 省略了public abstract
    void stop();
}

interface Attackable{
    public abstract attack();
}
```

#### 7.2.2 JDK1.8之后

​		除了定义全局常量和抽象方法以外，还可以定义非抽象方法

​		1）被 public default 修饰的非抽象方法，此时的 default 必须加上，否则会出错。<font color="red">**实现类中要是想重写接口中的非抽象方法，那么 default 修饰符必须不能加，否则出错**</font>

​		2）静态方法

```java
public interface Flyable{
    // 全局常量
    public static final MAX_SPEED = 7900;
    public static final MIN_SPEED = 1;
    
    // 抽象方法
    public abstract void fly();
    // 省略 public abstract  
    // 非抽象方法
    public default void begin(){
        System.out.println("起飞，芜湖！");
    }
    // 不可省略 default
    default void end(){
        System.out.println("安全着陆！");
    }
    // 静态方法
    public static void c(){
        System.out.println("---Flyable----c()静态方法---");
    }
}

class demo implements Flyable{
    public void fly(){
        System.out.println("我用飞机飞！");
    }
    /*public default void begin() */  // 不能这么写，会报错
    public void begin(){ // 应该不能加default
        System.out.println("对接口中的方法重写了")
    }
    // 静态方法不涉及到重写，即能够重写的都是非静态方法
    public static void c(){
        System.out.println("---demo---c()静态方法----");
    }
}
```

**问：为什么要在接口中加入非抽象方法？**

**注：如果接口中只能定义抽象方法的话，那么我要是修改接口中的内容，那么对所有的实现类来说，都需要重新实现该抽象方法。现在在接口中加入非抽象方法，对实现类没有影响，想调用可以直接调用**

### 7.3 接口、抽象类与继承

#### 7.3.1 接口的作用

​		定义规则，只是和抽象类不同，他是接口不是类。接口定义好规则以后，实现类负责实现即可。

#### 7.3.2 继承与实现

​		继承：子类对父类的继承

​		实现：实现类对接口的实现

​		**什么时候使用继承？什么时候使用接口？**

​				继承：手机 extends 照相机	-->    "is a" 的关系，手机是一个照相机<font color="red">（×）</font>

​				实现：手机 implements 拍照功能   -->  "has a" 的关系，手机有拍照的功能<font color="gree">（√）</font>

### 7.4 接口的继承

​		接口与接口之间可以继承，而且可以多继承

```java
interface AA{
	void method1;
}
interface BB{
    void method2;
}
interface CC extends AA, BB{
    
}
```

### 7.5 接口的使用

​		1）接口的使用上也满足多态性

​		2）接口，实际上就是定义了规范

​		3）开发中，体会面向接口编程

```java
	public class USBTest{
	public static void main(String[] args){
        Computer com = new Computer();
        // 1. 创建了接口的非匿名实现类的非匿名对象
		Flash flash = new Flash();
        com.transferData(flash);
        // 2. 创建了接口的非匿名实现类的匿名对象
        com.transferData(new Flash());
        // 3. 创建了接口的匿名实现类的非匿名对象
        USB phone = new USB(){
            @Override
            public void start(){
                System.out.println("手机开始工作");
            }
            @Override
            public void stop(){
                System.out.println("手机结束工作");
            }
        };
        com.transferData(phone);
        // 4. 创建了接口的匿名实现类的匿名对象
        com.transferData(new USB(){
            @Override
            public void start(){
                System.out.println("mp3开始工作");
            }
            @Override
            public void stop(){
                System.out.println("mp3结束工作");
            }
        });
	}
}

class Computer{
    public void transferData(USB usb){// USB usb = new Flash();
        usb.start();
        
        System.out.println("具体传输数据的细节");
        
        usb.stop();
    }
}

class Flash implements USB{
    @Override
    public static void start(){
        System.out.println("Flash start working.");
    }
    @Override
    public static void stop(){
        System.out.println("Flash stop working.");
    }
} 

interface USB{
    // 常量：定义了长、宽、最大最小的传输速度等
    public abstract void start();
    
    public abstract void stop();
}
```

## 8. 内部类

### 8.1 内部类概述

​		类的组成：属性、方法、构造器、代码块（普通块、静态块、构造块、同步块）、内部类

​		一个类 TestOuter 内部的类 SubTest 叫内部类，内部类：SubTest，外部类：TestOuter 

​		内部类：成员内部类（静态的、非静态的）   和  局部内部类（位置：方法内，块内，构造器内）

### 8.2 内部类与外部类冲突

```java
public class TestOuter {
    // 属性
    int age = 10;
    // 非静态的成员内部类
    public class A {
        int age  = 20;
        public void method() {
            int age = 30;
            // 内部类与外部类属性重名的时候，如何进行调用
            System.out.println(age); //  30
            System.out.println(this.age);  // 20
            System.out.println(TestOuter.this.age);  // 10
        }
    }
    // 静态的成员内部类
    static class B {
        public void method() {
            // 静态内部类中只能访问外部类中被 static 修饰的内容
        }
    }
}
```



### 8.3 成员内部类

​		成员：属性、方法、构造器等

​		修饰符：private、default、protected、public、final、abstract、static

​		**注：静态内部类中只能访问外部类中被 static 修饰的内容，外部类想要访问内部类的东西，需要创建内部类的对象然后进行调用**

### 8.4  局部内部 类

```java
public class TestOuter {
    // 1、在局部内部类中访问到的变量必须是被 final 修饰的
    public void method() {
        final int num = 10;
        class A {
            public void a() {
                // num = 20;
                System.out.println(num);
            } 
        }
    }
    // 如果类 B 在整个项目中只使用一次，那么就没有必要单独创建一个 B 类，使用内部类就可以了
    public Comparable method2() {
        class B implements Comparable {
            @Override
            public int compareTo(Object o) {
                return 0;
            }
        }
        return new B();
    }
    // 匿名内部类
    public Comparable method3() {
        return new Comparable() {
            @Override
            public int compareTo(Object o) {
                return 200;
            }
        };
    }
    
    // 匿名内部类 + 多态
    public void test() {
        Comparable com = new Comparable(){
            @Override
            public int compareTo(Object o) {
                return 100;
            }
        };
        System.out.println(com.compareTo("abc"));
    }
}
```

# 四、异常

## 1. 异常的引入

```java
import java.util.Scanner
public class Test {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        // 从键盘录入两个数，求商
        System.out.println("请录入第一个数：");
        int num1 = sc.nextInt();
        System.out.println("请录入第二个数：");
        int num2 = sc.nextInt(); 
        System.out.println("商：" + num1/num2);
    }
}
```

​		可能会出现两个异常：输入类型不匹配和除零异常

## 2. 异常的处理

### 2.1 if-else

```java
import java.util.Scanner
public class Test {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        // 从键盘录入两个数，求商
        System.out.println("请录入第一个数：");
        if(sc.hasNextInt()){
            int num1 = sc.nextInt();
            System.out.println("请录入第二个数：");
            if(sc.hasNextInt()){
                int num2 = sc.nextInt(); 
                if(num2 == 0) {
                    System.out.println("对不起，除数不能为 0");
               } else {
                   System.out.println("商：" + num1/num2);
               }
            } else {
                System.out.println("对不起，请输入一个整数。");
            }
        } else {
            System.out.println("对不起，请输入一个整数。");
        }
    }
}
```

​		缺点：

​			1）代码臃肿、业务代码和处理异常的代码混在一起

​			2）可读性差

​			3）程序员需要花费大量精力维护漏洞

​			4）程序员很难堵住所有的漏洞

### 2.2 try-catch

```java
import java.util.Scanner
public class Test {
   	public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
       try{
            // 从键盘录入两个数，求商
	    System.out.println("请录入第一个数：");
    	int num1 = sc.nextInt();
            System.out.println("请录入第二个数：");
            int num2 = sc.nextInt(); 
            System.out.println("商：" + num1/num2);
       } catch (Exception ex) {
           System.out.println("对不起，程序出现异常！");
       }
        
        System.out.println("------1------");
        System.out.println("------2------");
        System.out.println("------3------");
        System.out.println("------4------");
        System.out.println("------5------");
    }
}
```

​		原理：把可能出现异常的代码放入 try 代码块中，然后将异常封装成对象，被 catch 后的 () 中的那个异常对象接收，接收以后，执行 catch 后面的 {} 里面的代码，然后 try-catch 之后的代码，该怎么执行还怎么执行

​		**注：1、try 中如果出现异常，然后用 catch 成功捕获的话，那么 try 中后续的代码是不会执行的**

​	  		**2、如果 catch 捕获异常成功，那么 try-catch 后面的代码该执行还执行**

# 、设计模式

## 1. 23种经典的设计模式 GoF

### 1.1 创建型模式：5种

​		工厂方法模式（Factory）

​		抽象工厂模式

​		单例模式（Singleton）

​		建造者模式

​		原型模式

### 1.2 结构型模式：7种

​		适配器模式（Adapter）

​		装饰器模式

​		代理模式

​		外观模式

​		桥接模式

​		组合模式（

​		享元模式

### 1.3 行为型模式：11种

#### 1.3.1 策略模式（Strategy）

#### 1.3.2 Template Method

​		多态的应用：模板方法设计模式

​		

​		观察者模式（Observer）

​		迭代子模式

​		责任链模式

​		命令模式（Commander）

​		备忘录模式

​		状态模式

​		访问者模式

​		中介者模式

​		解释器模式 

<font color='red'>**开闭原则**</font>(Open-Closed Principle, OCP)：在尽量不修改现有代码的基础上，引入新功能

<font color='red'>**面向接口编程**</font>

<font color='red'>**用组合而不是继承**</font>

## 2. MVC设计模式

​		**model：**模型

​		**view：**视图

​		**controller：**控制逻辑

## 3. 七种设计模式

### 3.1 Factory

​		**工厂模式**

#### 		3.1.1 简单工厂模式

​		根据提供给它的数据，返回几个可能类中的其中的一个类的实例。

​		简单工厂模式的**实质**：由一个工厂类根据传入的参数，动态决定应该创建哪一个产品类的实例

#### 		3.1.2 模式的参与者

​		**工厂(Factory)角色**：接受客户端的请求，负责创建相应的产品对象

​		**抽象产品(Abstract Product)角色**：是工厂模式所创建对象的父类或是共同拥有的接口，可以是<font color='red'>抽象类或接口</font>

​		**具体产品(Concrete Product)对象**：工厂模式所创建的对象都是这个角色的实例

#### 		3.1.3 简单工厂模式的优缺点

##### 					3.1.3.1 优点

​		工厂含有必要的判断逻辑，可以决定在什么时候创建哪一个产品类的实例，客户端可以免除直接创建产品对象的责任，而仅仅消费产品。简单工厂模式通过这种做法实现了对责任的分割

##### 					3.1.3.2 缺点

​		1）当产品有复杂的多层等级结构时，工厂类只有自己，以不变应万变，就是模式的缺

​		2）系统扩展困难，一旦添加新产品就不得不修改工厂逻辑，有可能造成工厂逻辑过于复杂，违背了开闭原则

#### 		3.1.4 工厂模式

​		对于简单工厂模式的扩展

##### 									3.1.4.1 优点

​		克服了简单工厂违背开闭原则的缺点，又保持了封装对象创建过程的优点

##### 					3.1.4.2 问题

​		1）每增加一个产品，就需要加一个产品工厂的类，增加了额外的开发量

​	　2）由客户端决定实例化哪一个工厂来实现选择类，选择的问题还是存在

#### 		3.1.5 取消选择逻辑

​		反射 + 抽象工厂

### 3.2 Facade

​		**门面模式**

#### 		3.2.1 门面模式

​		外部与一个子系统的通信必须通过一个统一的门面(Facade)对象进行

#### 		3.2.2 意图

​		为子系统中的一组接口提供一个一致的界面，易于使用

​		<font color='red'>**注：门面模式无法在子系统中加入新的功能**</font>

#### 		3.2.3 注意

​		1）不同于控制器模式

​		2）不增加新的功

​		3）对外提供方便的接口（不表示接口类）

### 3.3 Observer

又叫**发布－订阅模式**

#### 		3.3.1 观察者模式

​				定义对象之间的一对多依赖关系，当一个对象改变状态时，所有依赖于它的对象都会自动获得通知

​				notify()：调用所有attach列表里成员的update()函数

#### 		3.3.2 被观察者

​				subject，在模式中有Notify(), Attach(), Detach()函数

#### 		3.3.3 观察者

​				observer，在模式中只有一个update()函数

#### 		3.3.4 观察者模式的两种模式

​				推模式：

​				拉模式：

### 3.4 Adapter

**对象的适配器模式：**将原来不兼容的接口转变为兼容的接口

​		**Target：**目标

​		**Adapter：**适配器

​		**Adaptee：**源

​		**Client：**客户端

### 3.5 Singleton

**单例模式**：多用在多进程中

```java
public class Singlenton{
    private static Singleton _instance = null; 
	private Singleton(){}
    public Singleton getInstance(){
        if(_instance == null){
            sychronize (_instance.class)
                if(_instance == null){
                    _instance = new Singleton;
                }
            return _instance;
        }
    }
}
```

​		根据什么时候初始化实例：

​			Constuctor: Hungry instantiation（饿汉实例化）

​			When used: Lazy instantiation（懒汉实例化）

​		Singleton的三大特征：

​			1）

​			2）

​			3）

​		二次判断（double check）

### 3.6 Strategy

**策略模式**

做同一个事情，方式不一样，所以有不同的策略

### 3.7 Composite

又叫<font color='red'>部分－整体</font>模式 (Part-Whole)

**合成模式：**一个类中能包含自身的集合，就叫做合成模式

​		常见的如目录下有目录和文件

​		树是合成模式的一种抽象

合成模式的三个角色：

​		抽象构件(Component)：

​		树叶构件(Leaf)：

​		树枝构件(Composite)：

合成模式实现有两种方式：

​		安全模式：不同的构件类拥有他们该有的接口（足够安全，但是不够透明）

​		透明模式：所有的构件类都有相同的接口即方法相同（对于客户端来说是透明的，但是不够安全）

## 4. Command

**命令模式**

客户(Client)角色：

命令(Command)角色：

具体命令(ConverteCommand)者：

请求者(Invoker)角色：

接收者(receiver)角色：



domain knowledge

需求

Use Case的一部分：System Sequence Diagram SSD