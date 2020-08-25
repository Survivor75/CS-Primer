## Object Oriented Design

 1. Fundamentals
	 - Class
	 - Object
	 - Constructors
	 - This
	 - Garbage Collection
	 - Argument Passing
	 - Access Control
	 - Static
	 - Final
	 - Nested and Inner Classes
	 - Inheritance
	 - Super
	 - Multilevel Hierarchy
	 - When Constructors Are Executed
	 - Method Overriding
	 - Dynamic Method Dispatch
	 - Abstract Class
	 - Final With Inheritance
	 - Packages
	 - Packages And Member Access
	 - Interfaces
	 - Use static Methods in an Interface
	 - Private Interface Methods 
2. SOLID Design Principles 
	 - The First 5 Principles of Object Oriented Design
	 - Becoming a better developer by using the SOLID design principles by Katerina Trajchevska
3. Design Patterns
	 - Strategy Pattern
	 - Observer Pattern
	 - Decorator Pattern
	 - Factory Pattern
	 - Singelton Pattern
	 - Facade Pattern
	 - Adapter Pattern
	 - Proxy Pattern
	 - Command Pattern
	 - Abstract Factory Pattern
4. Design Problems-Solutions
5. Credits



## Fundamentals

### Class

Perhaps the most important thing to understand about a class is that it defines a new data type. Once defined, this new type can be used to create objects of that type. Thus, a class is a template for an object, and an object is an instance of a class.

A simplified general form of a class definition is shown here:

    class className {
	    type instance-variable-1
	    type instance-variable-2
	    //...
	    type instance-variable-N
	    type methodName1(parameterList) {// body of method}
	    type methodName2(parameterList) {// body of method}
	    //...
	    type methodNameN(parameterList) {// body of method}
    }

The data, or variables, defined within a class are called instance variables. The code is contained within methods. Collectively, the methods and variables defined within a class are called members of the class.

Variables defined within a class are called instance variables because each instance of the class (that is, each object of the class) contains its own copy of these variables.

All methods have the same general form as main( ), which we have been using thus far. However, most methods will not be specified as static or public. Notice that the general form of a class does not specify a main( ) method. Java classes do not need to have a main( )method. You only specify one if that class is the starting point for your program. Further, some kinds of Java applications don’t require a main( ) method at all.

### Object

The new operator dynamically allocates (that is, allocates at run time) memory for an object and returns a reference to it. This reference is, essentially, the address in memory of the object allocated by new. This reference is then stored in the variable. Thus, in Java, all class objects must be dynamically allocated.

    Foo obj = new Foo();

![Object-1](https://github.com/Survivor75/Software-Engineering-Primer/blob/master/images/Object-1.png)

Most real-world classes explicitly define their own constructors within their class definition. However, if no explicit constructor is specified, then Java will automatically supply a default constructor.

At this point, you might be wondering why you do not need to use new for such things as integers or characters. The answer is that Java’s primitive types are not implemented as objects. Rather, they are implemented as “normal” variables. This is done in the interest of efficiency. As you will see, objects have many features and attributes that require Java to treat them differently than it treats the primitive types. By not applying the same overhead to the primitive types that applies to objects, Java can implement the primitive types more efficiently. Later, you will see object versions of the primitive types that are available for your use in those situations in which complete objects of these types are needed.

It is important to understand that new allocates memory for an object during run time. The advantage of this approach is that your program can create as many or as few objects as it needs during the execution of your program. However, since memory is finite, it is possible that new will not be able to allocate memory for an object because insufficient memory exists. If this happens, a run-time exception will occur.

Object reference variables act differently than you might expect when an assignment takes place.

![Object-2](https://github.com/Survivor75/Software-Engineering-Primer/blob/master/images/Object-2.png)

### Constructors

A constructor initializes an object immediately upon creation. It has the same name as the class in which it resides and is syntactically similar to a method. Once defined, the constructor is automatically called when the object is created, before the new operator completes. Constructors look a little strange because they have no return type, not even void. This is because the implicit return type of a class’ constructor is the class type itself. It is the constructor’s job to initialize the internal state of an object so that the code creating an instance will have a fully initialized, usable object immediately.

### This

this can be used inside any method to refer to the current object. That is, this is always a reference to the object on which the method was invoked. You can use this anywhere a reference to an object of the current class’ type is permitted.

### Garbage Collection

Java garbage collection is the  **process of releasing unused memory**  occupied by unused objects. This process is done by the JVM automatically because it is essential for memory management.

When a Java programs run on the JVM, objects are created on the heap, which is a portion of memory dedicated to the program. Eventually, some objects will no longer be needed.

When there is no reference to an object, then that object is assumed to be no longer needed and the memory occupied by the object are released. This technique is called  **Garbage Collection**.

**How Garbage Collection Works?**

The garbage collection is a part of the JVM and is an automatic process done by JVM. We do not need to explicitly mark objects to be deleted. However, we can request to the JVM for garbage collection of an object but ultimately it depends on the JVM to call garbage collector.

Unlike C++ there is no explicit way to destroy object.

In the below image, you can understand that if an object does not have any reference than it will be dumped by the JVM.

![garbage collection in java](https://www.studytonight.com/java/images/garbage-collection.jpg)

----------

**Can the Garbage Collection be forced explicitly ?**

No, the Garbage Collection can not be forced explicitly. We may request JVM for  **garbage collection**  by calling  **System.gc()**  method. But This does not guarantee that JVM will perform the garbage collection.

----------

**Advantages of Garbage Collection**

1.  Programmer doesn't need to worry about dereferencing an object.
2.  It is done automatically by JVM.
3.  Increases memory efficiency and decreases the chances for memory leak.

An object is able to get garbage collect if it is non-reference. We can make an object non-reference by using three ways.

1. set null to object reference which makes it able for garbage collection. For example:

```java

Demo demo = new Demo();
demo = null; // ready for garbage collection

```

2. We can non-reference an object by setting new reference to it which makes it able for garbage collection. For example

    `Demo demo = new Demo();
Demo demo2 = new Demo();
demo2 = demo // referring object` 

3.  **Anonymous object**  does not have any reference so if it is not in use, it is ready for the garbage collection.

----------

**`finalize()`  method**

Sometime an object will need to perform some specific task before it is destroyed such as closing an open connection or releasing any resources held. To handle such situation  **finalize()**  method is used.

The  **finalize()**  method is  **called by garbage collection thread before collecting object**. Its the last chance for any object to perform cleanup utility.

Signature of  **finalize()**  method

```java
protected void finalize()
{
 //finalize-code
}
```

----------

**Some Important Points to Remember**

1.  It is defined in java.lang.Object class, therefore it is available to all the classes.
2.  It is declare as proctected inside Object class.
3.  It gets called only once by a Daemon thread named GC (Garbage Collector) thread.

----------

**Request for Garbage Collection**

We can request to JVM for garbage collection however, it is upto the JVM when to start the garbage collector.

Java  **gc()**  method is used to call garbage collector explicitly. However gc() method does not guarantee that JVM will perform the garbage collection. It only request the JVM for garbage collection. This method is present in  **System and Runtime class**.

**Example of gc() Method**

Let's take an example and understand the functioning of the gc() method.

```java
public class Test
{

    public static void main(String[] args)
    {
        Test t = new Test();
        t=null;
        System.gc();
    }
    public void finalize()
    {
        System.out.println("Garbage Collected");
    }
}
```
### Argument Passing

In general, there are two ways that a computer language can pass an argument to a subroutine. The first way is call-by-value. This approach copies the value of an argument into the formal parameter of the subroutine. Therefore, changes made to the parameter of the subroutine have no effect on the argument. The second way an argument can be passed is call-by-reference. In this approach, a reference to an argument (not the value of the argument) is passed to the parameter. Inside the subroutine, this reference is used to access the actual argument specified in the call. This means that changes made to the parameter will affect the argument used to call the subroutine. As you will see, although Java uses call-by-value to pass all arguments, the precise effect differs between whether a primitive type or a reference type is passed.

When you pass a primitive type to a method, it is passed by value. Thus, a copy of the argument is made, and what occurs to the parameter that receives the argument has no effect outside the method.

When you pass an object to a method, the situation changes dramatically, because objects are passed by what is effectively call-by-reference. Keep in mind that when you create a variable of a class type, you are only creating a reference to an object. Thus, when you pass this reference to a method, the parameter that receives it will refer to the same object as that referred to by the argument. This effectively means that objects act as if they are passed to methods by use of call-by-reference. Changes to the object inside the method do affect the object used as an argument.

### Access Control

As you know, encapsulation links data with the code that manipulates it. However, encapsulation provides another important attribute: access control. Through encapsulation, you can control what parts of a program can access the members of a class. By controlling access, you can prevent misuse.

How a member can be accessed is determined by the access modifier attached to its declaration. Java supplies a rich set of access modifiers. Some aspects of access control are related mostly to inheritance or packages. (A package is, essentially, a grouping of classes.)

Java’s access modifiers are public, private, and protected. Java also defines a default access level. protected applies only when inheritance is involved. The other access modifiers are described next.

Let’s begin by defining public and private. When a member of a class is modified by public, then that member can be accessed by any other code. When a member of a class is specified as private, then that member can only be accessed by other members of its class. Now you can understand why main( ) has always been preceded by the public modifier. It is called by code that is outside the program—that is, by the Java run-time system. When no access modifier is used, then by default the member of a class is public within its own package, but cannot be accessed outside of its package.

An access modifier precedes the rest of a member’s type specification. That is, it must begin a member’s declaration statement.

    public int i;
    private double j;
    
    private int foo(int a, char b) { ... }


### Static

There will be times when you will want to define a class member that will be used independently of any object of that class. Normally, a class member must be accessed only in conjunction with an object of its class. However, it is possible to create a member that can be used by itself, without reference to a specific instance. To create such a member, precede its declaration with the keyword static. When a member is declared static, it can be accessed before any objects of its class are created, and without reference to any object. You can declare both methods and variables to be static. The most common example of a static member is main( ). main( ) is declared as static because it must be called before any objects exist.

Instance variables declared as static are, essentially, global variables. When objects of its class are declared, no copy of a static variable is made. Instead, all instances of the class share the same static variable.

Methods declared as static have several restrictions:

• They can only directly call other static methods of their class.  
• They can only directly access static variables of their class.  
• They cannot refer to this or super in any way. (The keyword super relates to inheritance and is described in the next chapter.)

If you need to do computation in order to initialize your static variables, you can declare a static block that gets executed exactly once, when the class is first loaded.

    class UseStatic {
	    static int a = 3;
	    static int b;

	    static void meth(int x){
		    System.out.println("x = " + x)
		    System.out.println("a = " + a)
		    System.out.println("b = " + b)
	    }
	    
		static {
			System.out.println("Static block initialized.");
			b = a*4;
		}
		
		public static void main(String args[]) {meth(42)}
    }

As soon as the UseStatic class is loaded, all of the static statements are run. First, a is set to 3, then the static block executes, which prints a message and then initializes b to a*4 or 12. Then main( ) is called, which calls meth( ), passing 42 to x. The three println( ) statements refer to the two static variables a and b, as well as to the parameter x.

Here is the output of the program:

    Static block initialized. 
    x = 42  
    a=3  
    b = 12

Outside of the class in which they are defined, static methods and variables can be used independently of any object. To do so, you need only specify the name of their class followed by the dot operator. For example, if you wish to call a static method from outside its class, you can do so using the following general form:

    classname.method( )

### Final

A field can be declared as final. Doing so prevents its contents from being modified, making it, essentially, a constant. This means that you must initialize a final field when it is declared. You can do this in one of two ways: First, you can give it a value when it is declared. Second, you can assign it a value within a constructor.

    final int FILE_NEW = 1; 
    final int FILE_OPEN = 2; 
    final int FILE_SAVE = 3; 
    final int FILE_SAVEAS = 4; 
    final int FILE_QUIT = 5;

In addition to fields, both method parameters and local variables can be declared final. Declaring a parameter final prevents it from being changed within the method. Declaring a local variable final prevents it from being assigned a value more than once.

The keyword final can also be applied to methods, but its meaning is substantially different than when it is applied to variables. This additional usage of final.

### Nested and Inner Classes

It is possible to define a class within another class; such classes are known as nested classes. The scope of a nested class is bounded by the scope of its enclosing class. Thus, if class B is defined within class A, then B does not exist independently of A. A nested class has access to the members, including private members, of the class in which it is nested. However, the enclosing class does not have access to the members of the nested class. A nested class that is declared directly within its enclosing class scope is a member of its enclosing class. It is also possible to declare a nested class that is local to a block.

There are two types of nested classes: static and non-static. A static nested class is one that has the static modifier applied. Because it is static, it must access the non-static members of its enclosing class through an object. That is, it cannot refer to non-static members of its enclosing class directly. Because of this restriction, static nested classes are seldom used.

The most important type of nested class is the inner class. An inner class is a non-static nested class. It has access to all of the variables and methods of its outer class and may refer to them directly in the same way that other non-static members of the outer class do.

```java
class Outer
{
  public void display()
  {
    Inner in=new Inner();
    in.show();
  }

  class Inner
  {
    public void show()
    {
      System.out.println("Inside inner");
    }
  }
}

class Test
{
  public static void main(String[] args)
  {
    Outer ot = new Outer();
    ot.display();
  }
}
```

### Inheritance

Inheritance is one of the cornerstones of object-oriented programming because it allows the creation of hierarchical classifications. Using inheritance, you can create a general class that defines traits common to a set of related items. This class can then be inherited by other, more specific classes, each adding those things that are unique to it.

The general form of a class declaration that inherits a superclass is shown here:

    class subclass-name extends superclass-name { 
	    // body of class
    }

You can only specify one superclass for any subclass that you create. Java does not support the inheritance of multiple superclasses into a single subclass. You can, as stated, create a hierarchy of inheritance in which a subclass becomes a superclass of another subclass. However, no class can be a superclass of itself.

Although a subclass includes all of the members of its superclass, it cannot access those members of the superclass that have been declared as private.

*A reference variable of a superclass can be assigned a reference to any subclass derived from that superclass.*

It is important to understand that it is the type of the reference variable—not the type of the object that it refers to—that determines what members can be accessed. That is, when a reference to a subclass object is assigned to a superclass reference variable, you will have access only to those parts of the object defined by the superclass.

### Super

Whenever a subclass needs to refer to its immediate superclass, it can do so by use of the keyword super.

super has two general forms. The first calls the superclass’ constructor. The second is used to access a member of the superclass that has been hidden by a member of a subclass. Each use is examined here.

A subclass can call a constructor defined by its superclass by use of the following form of super:

    super(arg-list);

The second form of super acts somewhat like this, except that it always refers to the superclass of the subclass in which it is used. This usage has the following general form:

    super.member

Here, member can be either a method or an instance variable.  
This second form of super is most applicable to situations in which member names of a subclass hide members by the same name in the superclass.

### Multilevel Hierarchy

Up to this point, we have been using simple class hierarchies that consist of only a superclass and a subclass. However, you can build hierarchies that contain as many layers of inheritance as you like. As mentioned, it is perfectly acceptable to use a subclass as a superclass of another. For example, given three classes called A, B, and C, C can be a subclass of B, which is a subclass of A. When this type of situation occurs, each subclass inherits all of the traits found in all of its superclasses. In this case, C inherits all aspects of B and A.

*super( ) always refers to the constructor in the closest superclass.*

### When Constructors Are Executed

When a class hierarchy is created, in what order are the constructors for the classes that make up the hierarchy executed? 

For example, given a subclass called B and a superclass called A, is A’s constructor executed before B’s, or vice versa? The answer is that in a class hierarchy, constructors complete their execution in order of derivation, from superclass to subclass. 

Further, since super( ) must be the first statement executed in a subclass’ constructor, this order is the same whether or not super( ) is used. 

If super( ) is not used, then the default or parameterless constructor of each superclass will be executed.

### Method Overriding

In a class hierarchy, when a method in a subclass has the same name and type signature as a method in its superclass, then the method in the subclass is said to override the method in the superclass. When an overridden method is called from within its subclass, it will always refer to the version of that method defined by the subclass. The version of the method defined by the superclass will be hidden.

```java
class Animal
{
    public void eat()
    {
        System.out.println("Eat all eatables");
    }
}

class Dog extends Animal
{
    public void eat()   //eat() method overridden by Dog class.
    {
        System.out.println("Dog like to eat meat");
    }
    
    public static void main(String[] args) {
        Dog d = new Dog();
        d.eat();
    }
}
```

*If you wish to access the superclass version of an overridden method, you can do so by using super.*

### Dynamic Method Dispatch

Indeed, if there were nothing more to method overriding than a name space convention, then it would be, at best, an interesting curiosity, but of little real value. However, this is not the case. Method overriding forms the basis for one of Java’s most powerful concepts: dynamic method dispatch. Dynamic method dispatch is the mechanism by which a call to an overridden method is resolved at run time, rather than compile time. Dynamic method dispatch is important because this is how Java implements run-time polymorphism.

Let’s begin by restating an important principle: a superclass reference variable can refer to a subclass object. Java uses this fact to resolve calls to overridden methods at run time. Here is how. When an overridden method is called through a superclass reference, Java determines which version of that method to execute based upon the type of the object being referred to at the time the call occurs. Thus, this determination is made at run time. When different types of objects are referred to, different versions of an overridden method will be called. In other words, it is the type of the object being referred to (not the type of the reference variable) that determines which version of an overridden method will be executed. Therefore, if a superclass contains a method that is overridden by a subclass, then when different types of objects are referred to through a superclass reference variable, different versions of the method are executed.

```java
class Game
{
 	public void type()
 	{  
 		System.out.println("Indoor & Outdoor"); 
 	}
}

Class Basketball extends Game
{
 	public void type()
 	{  
 		System.out.println("Outdoor game"); 
	}

 	public static void main(String[] args)
 	{
   		Game gm = new Game();
   		Basketball bb = new Basketball();
   		gm.type();
   		bb.type();
   		gm = bb;	//gm refers to Basketball object
   		gm.type();	//calls Basketball's version of type
 	}
}
```

### Abstract Class

There are situations in which you will want to define a superclass that declares the structure of a given abstraction without providing a complete implementation of every method. That is, sometimes you will want to create a superclass that only defines a generalized form that will be shared by all of its subclasses, leaving it to each subclass to fill in the details. Such a class determines the nature of the methods that the subclasses must implement. One way this situation can occur is when a superclass is unable to create a meaningful implementation for a method.

You can require that certain methods be overridden by subclasses by specifying the abstract type modifier. These methods are sometimes referred to as subclasser responsibility because they have no implementation specified in the superclass. Thus, a subclass must override them—it cannot simply use the version defined in the superclass. To declare an abstract method, use this general form:

    abstract type name(parameter-list);

Any class that contains one or more abstract methods must also be declared abstract. To declare a class abstract, you simply use the abstract keyword in front of the class keyword at the beginning of the class declaration. There can be no objects of an abstract class. That is, an abstract class cannot be directly instantiated with the new operator. Such objects would be useless, because an abstract class is not fully defined. Also, you cannot declare abstract constructors, or abstract static methods. Any subclass of an abstract class must either implement all of the abstract methods in the superclass, or be declared abstract itself.

In this example, we created an abstract class A that contains a method `callme()` and Using class B, we are extending the abstract class.

```java
abstract class A
{
  abstract void callme();
}
class B extends A
{
  void callme()
  {
    System.out.println("Calling...");
  }
  public static void main(String[] args)
  {  
    B b = new B();
    b.callme();
  }
}
```

Abstract classes can also have non abstract methods along with abstract methods. But remember while extending the class, provide definition for the abstract method.

```java
abstract class A
{
  abstract void callme();
  public void show()
  {
    System.out.println("this is non-abstract method");
  }
}

class B extends A
{
  void callme()
  {
    System.out.println("Calling...");
  }
  public static void main(String[] args)
  {
    B b = new B();
    b.callme();
    b.show();
  }
```

    Output
    calling... 
    this is non-abstract method

### Final With Inheritance

The keyword final has three uses. First, it can be used to create the equivalent of a named constant. This use was described in the preceding chapter. The other two uses of final apply to inheritance. Both are examined here.

1. While method overriding is one of Java’s most powerful features, there will be times when you will want to prevent it from occurring. To disallow a method from being overridden, specify final as a modifier at the start of its declaration. Methods declared as final cannot be overridden.

2. Sometimes you will want to prevent a class from being inherited. To do this, precede the class declaration with final. Declaring a class as final implicitly declares all of its methods as final, too. As you might expect, it is illegal to declare a class as both abstract and final since an abstract class is incomplete by itself and relies upon its subclasses to provide complete implementations.

### Packages

Packages are containers for classes. They are used to keep the class name space compartmentalized. For example, a package allows you to create a class named List, which you can store in your own package without concern that it will collide with some other class named List stored elsewhere. Packages are stored in a hierarchical manner and are explicitly imported into new class definitions.

To create a package is quite easy: simply include a package command as the first statement in a Java source file. Any classes declared within that file will belong to the specified package. The package statement defines a name space in which classes are stored. If you omit the package statement, the class names are put into the default package, which has no name. (This is why you haven’t had to worry about packages before now.) While the default package is fine for short, sample programs, it is inadequate for real applications. Most of the time, you will define a package for your code.

This is the general form of the package statement:

    package pkg;  

Here, pkg is the name of the package. 

You can create a hierarchy of packages. To do so, simply separate each package name from the one above it by use of a period. The general form of a multileveled package statement is shown here:

    package pkg1[.pkg2[.pkg3]];

A package hierarchy must be reflected in the file system of your Java development system. For example, a package declared as

    package a.b.c;

needs to be stored in a\b\c


### Packages And Member Access

Classes and packages are both means of encapsulating and containing the name space and scope of variables and methods. Packages act as containers for classes and other subordinate packages. Classes act as containers for data and code. The class is Java’s smallest unit of abstraction. As it relates to the interplay between classes and packages, Java addresses four categories of visibility for class members:

• Subclasses in the same package  
• Non-subclasses in the same package  
• Subclasses in different packages  
• Classes that are neither in the same package nor subclasses

The three access modifiers, private, public, and protected, provide a variety of ways to produce the many levels of access required by these categories.

![PackageAndMemberAccess](https://github.com/Survivor75/Software-Engineering-Primer/blob/master/images/PackageAndMemberAccess.png)

Anything declared public can be accessed from different classes and different packages. Anything declared private cannot be seen outside of its class. When a member does not have an explicit access specification, it is visible to subclasses as well as to other classes in the same package. This is the default access. If you want to allow an element to be seen outside your current package, but only to classes that subclass your class directly, then declare that element protected.

Above table applies only to members of classes. A non-nested class has only two possible access levels: default and public. When a class is declared as public, it is accessible outside its package. If a class has default access, then it can only be accessed by other code within its same package. When a class is public, it must be the only public class declared in the file, and the file must have the same name as the class.

### Interfaces

Using the keyword interface, you can fully abstract a class’ interface from its implementation. That is, using interface, you can specify what a class must do, but not how it does it. Interfaces are syntactically similar to classes, but they lack instance variables, and, as a general rule, their methods are declared without any body. In practice, this means that you can define interfaces that don’t make assumptions about how they are implemented. Once it is defined, any number of classes can implement an interface. Also, one class can implement any number of interfaces.

To implement an interface, a class must provide the complete set of methods required by the interface. However, each class is free to determine the details of its own implementation. By providing the interface keyword, Java allows you to fully utilize the “one interface, multiple methods” aspect of polymorphism.

Interfaces are designed to support dynamic method resolution at run time.

```java
interface interface_name {  
// fields
// abstract/private/default methods
}
```

When no access modifier is included, then default access results, and the interface is only available to other members of the package in which it is declared. When it is declared as public, the interface can be used by code outside its package. In this case, the interface must be the only public interface declared in the file, and the file must have the same name as the interface. name is the name of the interface, and can be any valid identifier. Notice that the methods that are declared have no bodies. They end with a semicolon after the parameter list. They are, essentially, abstract methods. Each class that includes such an interface must implement all of the methods.

```java
interface Moveable
{
 	int AVG-SPEED = 40;
 	void move();
}

class Vehicle implements Moveable
{
 	public void move()
 	{
  		System .out. print in ("Average speed is"+AVG-SPEED");
 	}
 	public static void main (String[] arg)
 	{
  		Vehicle vc = new Vehicle();
  		vc.move();
 	}
}
```

*As the general form shows, variables can be declared inside interface declarations. They are implicitly final and static, meaning they cannot be changed by the implementing class. They must also be initialized. All methods and variables are implicitly public.*

The general form of a class that includes the implements clause looks like this:

    class classname [extends superclass] [implements interface1, [interface2...]] 
    {
	    // body of class
    }

```java
interface Moveable
{
 	boolean isMoveable();
}

interface Rollable
{
 	boolean isRollable
}

class Tyre implements Moveable, Rollable
{
 	int width;

 	boolean isMoveable()
 	{
  		return true;
 	}

 	boolean isRollable()
 	{
  		return true;
 	}
 	
 	public static void main(String args[])
 	{
  		Tyre tr = new Tyre();
  		System.out.println(tr.isMoveable());
  		System.out.println(tr.isRollable());
 	}
}
```

You can declare variables as object references that use an interface rather than a class type. Any instance of any class that implements the declared interface can be referred to by such a variable. When you call a method through one of these references, the correct version will be called based on the actual instance of the interface being referred to. This is one of the key features of interfaces. The method to be executed is looked up dynamically at run time, allowing classes to be created later than the code which calls methods on them. The calling code can dispatch through an interface without having to know anything about the “callee.”

*An interface reference variable has knowledge only of the methods declared by its interface declaration.*



If a class includes an interface but does not fully implement the methods required by that interface, then that class must be declared as abstract.

An interface can be declared a member of a class or another interface. Such an interface is called a member interface or a nested interface. A nested interface can be declared as public, private, or protected. This differs from a top-level interface, which must either be declared as public or use the default access level, as previously described. When a nested interface is used outside of its enclosing scope, it must be qualified by the name of the class or interface of which it is a member. Thus, outside of the class or interface in which a nested interface is declared, its name must be fully qualified.

A default method lets you define a default implementation for an interface method. The primary difference is that the declaration is preceded by the keyword default.

```java
interface Abc{  
    // Default method   
    default void msg(){  
        System.out.println("This is default method");  
    }  
    // Abstract method  
    void greet(String msg);  
}  
public class Demo implements Abc{  
    public void greet(String msg){        // implementing abstract method   
        System.out.println(msg);  
    }  
    public static void main(String[] args) {  
    	Demo d = new Demo();  
        d.msg();   // calling default method  
        d.greet("Say Hi");  // calling abstract method  
  
    }  
} 
```

Java does not support the multiple inheritance of classes. Now that an interface can include default methods, you might be wondering if an interface can provide a way around this restriction. The answer is, essentially, no. Recall that there is still a key difference between a class and an interface: a class can maintain state information (especially through the use of instance variables), but an interface cannot.

**Difference between an interface and an abstract class?**

|Abstract class|  Interface|
|--|--|
| Abstract class is a class which contain one or more abstract methods, which has to be implemented by its sub classes. |  Interface is a Java Object containing method declaration but no implementation. The classes which implement the Interfaces must provide the method definition for all the methods.|
| Abstract class is a Class prefix with an abstract keyword followed by Class definition.| Interface is a pure abstract class which starts with interface keyword.|
| Abstract class can also contain concrete methods.| Whereas, Interface contains all abstract methods and final variable declarations.|
| Abstract classes are useful in a situation that Some general methods should be implemented and specialization behavior should be implemented by child classes.| Interfaces are useful in a situation that all properties should be implemented.|


### Use static Methods in an Interface

Like static methods in a class, a static method defined by an interface can be called independently of any object. Thus, no implementation of the interface is necessary, and no instance of the interface is required, in order to call a static method. Instead, a static method is called by specifying the interface name, followed by a period, followed by the method name. Here is the general form:

    InterfaceName.staticMethodName

### Private Interface Methods

A private interface method can be called only by a default method or another private method defined by the same interface. Because a private interface method is specified private, it cannot be used by code outside the interface in which it is defined. This restriction includes subinterfaces because a private interface method is not inherited by a subinterface.

## SOLID Design Principles 

[The First 5 Principles of Object Oriented Design](https://scotch.io/bar-talk/s-o-l-i-d-the-first-five-principles-of-object-oriented-design)

[Becoming a better developer by using the SOLID design principles by Katerina Trajchevska](https://www.youtube.com/watch?v=rtmFCcjEgEw&list=PLQLGaWLA2XKMTlPorwfwhiI6OT45rugtH&index=7&t=679s)

## Design Patterns

### Strategy Pattern

[Strategy Pattern](https://www.youtube.com/watch?v=v9ejT8FO-7I&list=PLrhzvIcii6GNjpARdnO4ueTUAVR9eMBpc&index=2&t=0s)

### Observer Pattern

[Observer Pattern](https://www.youtube.com/watch?v=_BpmfnqjgzQ&list=PLrhzvIcii6GNjpARdnO4ueTUAVR9eMBpc&index=3&t=0s)

### Decorator Pattern

[Decorator Pattern](https://www.youtube.com/watch?v=GCraGHx6gso&list=PLrhzvIcii6GNjpARdnO4ueTUAVR9eMBpc&index=4&t=572s)

### Factory Pattern

[Factory Pattern](https://www.youtube.com/watch?v=EcFVTgRHJLM&list=PLrhzvIcii6GNjpARdnO4ueTUAVR9eMBpc&index=5&t=0s)

### Singelton Pattern

[Singelton Pattern](https://www.youtube.com/watch?v=hUE_j6q0LTQ&list=PLrhzvIcii6GNjpARdnO4ueTUAVR9eMBpc&index=7&t=0s)

### Facade Pattern

[Facade Pattern](https://www.youtube.com/watch?v=K4FkHVO5iac&list=PLrhzvIcii6GNjpARdnO4ueTUAVR9eMBpc&index=10&t=0s)

### Adapter Pattern

[Adapter Pattern](https://www.youtube.com/watch?v=2PKQtcJjYvc&list=PLrhzvIcii6GNjpARdnO4ueTUAVR9eMBpc&index=9&t=0s)

### Proxy Pattern

[Proxy Pattern](https://www.youtube.com/watch?v=NwaabHqPHeM&list=PLrhzvIcii6GNjpARdnO4ueTUAVR9eMBpc&index=11&t=0s)

### Command Pattern

[Command Pattern](https://www.youtube.com/watch?v=9qA5kw8dcSU&list=PLrhzvIcii6GNjpARdnO4ueTUAVR9eMBpc&index=8&t=965s)

### Abstract Factory Pattern

[Abstract Factory Pattern](https://www.youtube.com/watch?v=v-GiuMmsXj4&list=PLrhzvIcii6GNjpARdnO4ueTUAVR9eMBpc&index=6&t=0s)

## Credits
(Will Add Soon)
