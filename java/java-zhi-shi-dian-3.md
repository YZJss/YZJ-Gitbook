# java知识点(3)

### 关键字：abstract

可以用来修饰：类、方法

**修饰类：抽象类**

1. 此类不能实例化
2. 抽象类中一定有构造器，便于子类实例化时调用（涉及：子类对象实例化的全过程）
3. 开发中，都会提供抽象类的子类，让子类对象实例化，完成相关的操作 --->抽象的使用前提：**继承性**

**修饰方法：抽象方法**

1. 抽象方法只方法的声明，没方法体
2. 包含抽象方法的类，一定是一个抽象类。反之，抽象类中可以没有抽象方法的。
3. 若子类重写了父类中的所的抽象方法后，此子类方可实例化；若子类没重写父类中的所的抽象方法，则此子类也是一个抽象类，需要使用abstract修饰。

**注意**

1. abstract不能用来修饰：属性、构造器等结构
2. abstract不能用来修饰私方法、静态方法、final的方法、final的类

### 关键字：final

可以用来修饰：类、方法、变量

**修饰类：**

此类不能被其他类所继承。例如：String类、System类、StringBuffer类

**修饰方法：**

表明此方法不可以被重写。例如：Object类中getClass()

**修饰变量：**

此时的"变量"就称为是一个常量

1. final修饰属性：可以考虑赋值的位置：显式初始化、代码块中初始化、构造器中初始化
2. final修饰局部变量：使用final修饰形参时，表明此形参是一个常量。当我们调用此方法时，给常量形参赋一个实参。一旦赋值以后，就只能在方法体内使用此形参，但不能进行重新赋值。

static final 用来修饰属性：全局常量