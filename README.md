# **Rainbow Cats General Java Programming Notes**

## **JDK & Gradle Settings**
#### **Install JDL & Gradle**
- https://www.oracle.com/java/technologies/downloads/#java11
- https://gradle.org/
#### **Check or Add Environment Variables (In Advanced System Settings)**
- `Name: JAVA_TOOL_OPTIONS` | `Value: -Duser.language=en`
- `Name: JAVA_HOME` | `Value: X:\...\Java\jdk-18.0.1.1`
- `Name: Path` | `Value: X:\...\Common Files\Oracle\Java\javapath`
- `Name: Path` | `Value: X:\...\Java\jdk-18.0.1.1\bin`
- `Name: Path` | `Value: X:\...\Gradle\gradle-7.4.2\bin`
#### **Check Installation in Command Line**
- `javac -version`
- `gradle -version`
#### **Run Java Programs in Command Line**
- Compile the program in terminal: `javac myProgram.java`
- If nothing goes wrong in the code, we can run the program in terminal: `java myProgram`
- To stop the program in terminal, use `Ctrl + D`.

## **Access Modifier**
- `public` Accessible everywhere. _[Classes, attributes, methods and constructors.]_
- `default` Only within package. _[Classes, attributes, methods and constructors.]_
- `private` Only within the class. _[Attributes, methods and constructors.]_
- `protected` Within the class. Outside the class through inheritance only. _[Attributes, methods and constructors.]_
```java
//Accessible everywhere
public class someClass{
    public int someVariable;
    public void func(){
        //Do something.
    }
}
```

## **Non-Access Modifiers**
- `final` The class cannot be inherited by other classes. Attributes and methods cannot be overridden or modified.
- `static` Attributes and methods belongs to the class, rather than an object.
- `abstract` Can only be used on classes and methods (Only be used in an abstract class). The abstract class cannot be used to create objects. The abstract method does not have a body.
- `transient` Attributes and methods are skipped when serializing the object containing them.
- `synchronized` Methods can only be accessed by one thread at a time.
- `volatile` The value of an attribute is not cached thread-locally, and is always read from the "main memory".
```java
//The abstract class cannot be used to create objects.
public abstract class someClass{
    //Accessible anywhere outside the class and it belongs to the class. 
    //Call it through class instead of instances.
    //It can not be changed and worked as a constant.
    private static final int someVariable;
    //The abstract method does not have a body.
    public abstract void func();
}
```

## **Call Stack**
- Java is a stack-based language so when a method is executed it is put onto a **call-stack**. 
- The method being executed at the **top of the stack** is the **most recently called method**.
- The method **finishes** executing once it has reached a **return state** or the **end of method scope** for void method.

## **Array**
- Array is a contiguous block of memory containing multiple values of the same type. 
- When the array is initialized, it will be allocated and will return the address of where the array is stored.
- Array can store both primitive types (values) and reference (pointers) types.
#### **General rules with array initialization**
- Primitive integer types (byte, short, int, long) are initialized to `0 by default`.
- Default value of elements of a boolean array are `false`.
- Floating point numbers such as float and double are initialized to `0.0f` and `0.0d` respectively.
- Elements of a char array is initialized to `\u0000` (`null` character).
- Any `Reference type` is initialized to `null`.
```java
//---------One-dimensional Arrays Initialization---------
int[] numbers01 = new int[16];            //Initialize with length.
int[] numbers02 = {1, 2, 3, 4, 5};        //Static initialization.
int[] numbers03 = new int[]{1, 2, 3, 4};  //Similarly, we can also initialize using this.

//Traverse through the array.
for(int i=0; i<numbers02.length; i++){
    //Do stuff.
}

//---------Multi-dimensional Arrays Initialization---------
int[][] array = new int[3][3];  //Matrix-like structure.
int[][] jarray = new int[3][];  //Jagged array. (Different column size on fixed rows count)

//Defining different column size of a Jagged array.
jarray[0] = new int[5];         
jarray[1] = new int[10];

//Traverse through an array.
for(int y=0; y<jarray.length; y++){
    for(int x=0; x<jarray[y].length; x++){
        //Do stuff.
    }
}
```

## **Strings**
- String is **a reference type** that aggregates characters and Java treats Strings as **immutable** (will not be able to change later).
```java
//Creates a Meow at a new Memory Address.
String cat = "Meow";
//Creates another literial "Meow, says the cat!" at another address
//Bind the memory address to the cat variable.
cat += ", says the cat!"
```
### **String Pool**
- To optimise the memory usage, the compiler will use the `same allocation` and provide the same reference to a string variable of refers to the `same literal`.
- This means once a string literial is specified, it will be `added to a string pool`. After that, other string variables that is using the `same literial` will have the `same memory allocation`.
```java
//Case 1: Output is true. As Meow is already in the string pool,
//cat1 and cat2 are using the same memory address.
String cat1 = "Meow";   //0x100
String cat2 = "Meow";   //0x100
System.out.println(cat1 == cat2);

//Case 2: Output is false. Because of the keyword new,
//it specifically creates a literial using the new memory address.
String cat1 = "Meow";               //0x100
String cat2 = new String("Meow");   //0x200
System.out.println(cat1 == cat2);
```
### **Comparing Strings**
- Use method to compare strings properly
```java
String cat1 = "Meow";
String cat2 = "Meow";
//The output is true. To compare strings properly, we need to use methods.
System.out.println(cat1.equals(cat2));
```

## **ArrayList (Dynamic Array)**
ArrayList creates a new array that **doubles the size of the previous array** every time the size **exceeds the limit**, it copys the elements in the previous one to the new extended array and point the pointer to it.

**Syntax:**
```java
List<ReferenceType> name = new ListType<ReferenceType>(SizeDefault10);
```
**Methods:**
- `.add(T element)` Add the element to the end of the list.
- `.add(int index, T element)` Inserts the element at the index position, shift the element previously at the index to the right.
- `.set(int index, T element)` Replace the element at the index to the element given.
- `.remove(int index)` Remove the element at the specific index and shift all to the left.
- `.remove(Object obj)` Remove the element and shift all to the left.
- `.get(int index)` Get element at specific index.
- `.size()` Get the size of the list.
- `.clear()` Remove every element in the list.

**For more instructions:**
*https://docs.oracle.com/javase/8/docs/api/java/util/ArrayList.html*

## **LinkedList**
- A linked list does not have an array containing all the elements stored. **It chains elements** and their values. Each element is located in arbitary memory address.
- Each element in the linked list is known as a `Node`. Each node contains a `value` and a `link to the next element`. To store a linked list, simply store the head of the list so we can access every element.

**Traverse Through a Linked List:**
```java
public int traverseGetSum(Node head){
    Node current = head;
    int sum = 0;
    while(current != null){
        sum += current.value;
        current = current.next;
    }
    return sum;
}

public int traverseGetSize(Node head){
    Node current = head;
    int sum = 0;
    while(current != null){
        sum += 1;
        current = current.next;
    }
    return sum;
}

public void traverseAddNode(Node toBeAdded){
    if(head == null) {
        head = toBeAdded;
    }else{
        Node current = head;
        while(current.next != null){
            current = current.next;
        }
        current.next = toBeAdded;
    }
}

public int traverseRecursiveGetSize(Node node){
    if(node!=null){
        return traverseGetSize(node.next) + 1;
    }else{
        return 0;
    }
}
```

## **HashMap**
- Works as a dictionary in java.

**Methods:**
- `.put(K,V)` _Add element._
- `.replace(K, V)` _Replaces the entry only if it is mapped to some value._
- `.get(K)` _Get value using key._
- `.remove(K)` _Remove the mapping for the specified key._
- `.clear()` _Remove all mappings from the map._
- `.entrySet()` _Get all elements._
- `.containsKey(K)` _Returns true if this map contains key._

**For more instructions:** https://docs.oracle.com/javase/8/docs/api/java/util/HashMap.html
``` java
//Initialization
HashMap<K,V> hashMap = new HashMap<K,V>();

//Iterate Through the HashMap
for(HashMap.Entry e : hashMap.entrySet()){
    System.out.println(e.getKey()+" "+e.getValue());
}
```

## **Classes**
There are two main types: **Primitive types** and **Reference types**.
- Reference types are classes. 
- Class defines a type of object that can be reused.
- Every class that we created will have a constructor. Even there is no constructor defined in code, java will create a constructor automatically.
```java
public class myClass{
    public int variableA;
    public int variableB;

    //Constructor, will be called when object is created.
    public myClass(int variableA, int variableB){
        //this.variableA means we are referring to the variableA in the class,
        //not the local function argument.
        this.variableA = variableA;
        this.variableB = variableB
    }
}
```

## **UML Diagram**
**Access Modifier:**
- `[ + ]` public
- `[ - ]` private
- `[ # ]` protected

**Non-Access Modifier:**
- `[ UnderLine ]` static
- `[ ALL_CAPITAL ]` final
- `[ Italic ]` abstract

**Others:**
- Name at the top
- `[ <<Interface>> <<Enumeration>> ]` Above the name

**Syntax:**
- `[ Name : Type ]` Variables
- `[ Name(Name: Type, Name: Type) : Return Type ]` Functions
- Subclasses points **solid arrows** to **Superclasses**.
- Classes points **dashed arrows** to **implemented interfaces**.
- Classes with **generic type** will show the type in a **dashed line box** at top right corner.

## **Scanner & Binary I/O**
We can use methods in `Scanner`, `DataOutputStream` and `DataInputStream`.

**Read Input: (Scanner)**
```java
import java.util.Scanner;
import java.util.InputMismatchException;

public class ScannerTest {
    /**
     * The main function of the class.
     * @param args String arguments.
     */
    public static void main(String[] args){
        try{
            Scanner scanner = new Scanner(System.in);
            while(scanner.hasNextLine()){
                int line = scanner.nextInt();
                System.out.println("You Entered: " + line);
            }
            scanner.close();

        }catch(InputMismatchException e){
            System.out.println("Must input numbers.");
            return;
        }
    }
}
```

**Read File: (Scanner)**
```java
import java.io.File;
import java.io.FileNotFoundException;
import java.util.Scanner;

public class ScannerTest {
    /**
     * The main function of the class.
     * @param args String arguments.
     */
    public static void main(String[] args){
        readPrintFile(null);
    }

    public static void readPrintFile(String fileName){
        try{
            File file = new File(fileName);
            Scanner scanner = new Scanner(file);
            while(scanner.hasNextLine()){
                String line = scanner.nextLine();
                System.out.println(line);
            }
            scanner.close();

        }catch(FileNotFoundException e){
            System.out.println("No such file.");
            return;
        }catch(NullPointerException e){
            System.out.println("Path given is null.");
        }
    }
}
```

**Write: (Binary I/O)**
```java
import java.io.DataOutputStream;
import java.io.FileOutputStream;
import java.io.FileNotFoundException;
import java.io.IOException;

public class BinaryWriter{
    public static void main(String[] args){
        try{
            //Creates a binary file .bin
            FileOutputStream file = new FileOutputStream("newFile.bin");
            DataOutputStream writer = new DataOutputStream(file);
            writer.writeInt(5);
            writer.close();
        }catch(FileNotFoundException e){
            e.printStackTrace();
        }catch(IOException e){
            e.printStackTrace();
        }
    }
}
```

**Read: (Binary I/O)**
```java
import java.io.DataInputStream;
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.IOException;

public class BinaryWriter{
    public static void main(String[] args){
        try{
            //Loads in a binary file .bin
            FileInputStream file = new FileInputStream("newFile.bin");
            DataInputStream reader = new DataInputStream(file);
            int n = reader.readInt();
            System.out.println(n);
        }catch(FileNotFoundException e){
            e.printStackTrace();
        }catch(IOException e){
            e.printStackTrace();
        }
    }
}
```

**Read Binary File in Terminal:**
```
xxd -b newFile.bin
```

## **Stack and Heap**
- The stack memory has **limited size**. In **JVM** by default, the stack memory limit is **1MB**.
- **A stack frame** can be thought of an instance of a method.
- **The heap** is separate memory space for which objects are **dynamically allocated**.
- Similar to malloc(), whenever we use **a `new` keyword**, memory for the object is **allocated on the heap** and an address is returned.
- When there is **no pointer pointing to the memory loaction**, the memory will **become free automatically** handled by `Java Garbage Collector`. There is no manual deallocation anymore. So we don't need to worry about the memory leak.

## **Inheritance**
- Inheritance is a **significant concept of OOP**. Allowing **reuseability and changes** to inherited methods between different types in a hierarchy.
- If in the parent class we have a method, then in the child class we will have that method too, and we can override the method in the child class.

**What does inheritance offer?**
- Attribute and method reusability.
- Defining sub-class methods in parent.
- Overriding (Make some change) inherited methods.
- Type information.

**Note:**
- **Superclass does not know** about its **subclasses**
- Subclasses cannot be constructed using a superclass constructor.
- You **cannot use subclass properties through a superclass** binding.
- Private is not inherited, **only protected and public is inherited**.
- Ensure the relationship between the superclass and subclass satisfy an **is-a relationship**.
- A class can **only inherit from 1 class**.
- In UML inheritance is shown as a **Generalization**.

**Syntax: (How do we use it?)**
```java
[Access Modifier] class ClassName extends SuperClassName{
    //Content of the class.
}

//Example of inheritance

//Animal.java
public class Animal{
    public String name;

    public Animal(String name){
        this.name = name;
    }

    public void eat(){
        System.out.println(name + " is eating.");
    }
}

//Dog.java
public class Dog extends Animal{
    public Dog(String name){
        //Use super keyword to access the parent constructor. 
        super(name);
    }

    public void makeSound(){
        System.out.println("Woof!");
    }
}
```
>**Note:** In this case, we must access the parent constructor to create the object. Java will not automatically generate a parameterless constructor because we already declared a constructor. If we don't access the parent constructor, java will not know what value to put in the parameter of the only parent constructor. Therefore, it's safe to always explictly access the parent constructor in the child constructor.

**Encapsulation:**
What does `protected` means?
- It is only accessible within the class
- Attributes and methods will be accessible by all subclass

**Create Inheritance When:**
There are two types of relationships we will look at when it comes to inheritance.

- **Is-a relationship (Extension)** - This is a relationship that we should use inheritance.
- **Has-a relationship (Composition)** - We should not use inheritance with this relationship

>**For Example:**
>- Character - Player, Enemy, Ally
>- Media - DVD, Book, Image
>- Controller - Gamepad, Joystick, Keyboard

## **Overloading**
- In regard to Java we are able to use the same method name but with different **method signature**.
- Define method with the **same name** but **different parameters**.
```java
int add(int a, int b){}
int add(int a, int b ,int c){}
int add(double a, double b){}
```
- Also, constructor can be overloaded.
```java
public class Overloading{
    public int variableA;
    public int variableB;
    public int variableC;

    public Overloading(){
        //This() is used to access the constructors in current class.
        this(1, 2, 3);
    }

    public Overloading(int variableA){
        this.variableA = variableA;
        this.variableB = 2;
        this.variableC = 3;
    }

    public Overloading(int variableA, int variableB, int variableC){
        this.variableA = variableA;
        this.variableB = variableB;
        this.variableC = variableC;
    }
}
```

## **Throw Exceptions & Try-Catch Block**
`Checked Exceptions` Exception and any subclasses that is not RuntimeException. **Must handle it using a try-catch block if a method can throw the exception.**
```java
public class Exceptions{
    //The method throws a checked exception.
    public static void imGonnaCrash() throws Exception{
        throw new Exception("Definitely crashing!!");
    }

    public static void main(String[] args){
        //Must use try-catch block.
        try{
            imGonnaCrash();
        }catch(Exception e){
            e.getMessage();
        }
    }
}
```
`Unchecked Exception` RuntimeException and any subclasses. __Does not need to handle it__ but can use try-catch block if they want to. It should be __a case where the program should crash__. It is a state that **should occur** during runtime and you cannot handle nicely prior. Unless you are expecting the code to raise an exception.
```java
public class Exceptions{
    //The method throws an unchecked exception. (RuntimeException)
    //"throws Exception" is not needed.
    public static void imGonnaCrash(){
        throw new RuntimeException("Definitely crashing!!");
    }

    public static void main(String[] args){
        //Does not need to use try-catch block.
        //But can catch it if they want.
        imGonnaCrash();
    }
}
```
`Error` Error is a state that **cannot be handled**. It is typically invoked when the state of the program is considered **unrecoverable**. Error in Java can be handled by a try-catch block, but it is considered **bad practice to catch them**.
```java
Error: StackOverFlow
```
**Create Custom Exception** - We can create our own exception class by **extending** the Exception or RuntimeException class.
```java
class InvalidRefreshRateException extends Exception{
    public InvalidRefreshRateException(){
        super("Unsupported refresh rate.")
    }
}

public class Monitor{
    private double refreshRate;
    public final double MAX_REFRESH_RATE;

    public Monitor(double defaultRate, double max){
        refreshRate = defaultRate;
        MAX_REFRESH_RATE = max;
    }

    public double setRefreshRate(double hz) throws InvalidRefreshRateException {
        if(hz < 0 || hz > MAX_REFRESH_RATE)
            throw new InvalidRefreshRateException();
        else
            refreshRate = hz;
        return refreshRate;
    }
}
```

## **Enum**
- Enums are a set of **defined instances of the same type**. An enum within java allows a finite set of instances to be constructed.
- We are unable to create new unique instance (cannot use the new keyword) of an enum type.
- We may use enums in situatuins where the number of instances anre finite or manageable within a sequence of instances.

**For Example:**
- Telephone State: Busy, Offline, Awaiting, Dialing
- Laptop State: On, Off, Sleeping
- Direction: Left, Right, Up, Down
- Month of a Year: Jan, Feb, Mar, ...

**Syntax: (How do we use it?)**
```java
[public] enum EnumName

//Basic Example.
enum Suit{
    Hearts,     //0
    Diamonds,   //1
    Spades,     //2
    Clubs;      //3
}

//Example Variant 1.
enum Rating{
    //We can also get the number using Rating.BAD.ordinal();
    //We can access all enum values using Rating.values();
    BAD,        //0
    AVERAGE,    //1
    EXCELLENT;  //2
}

public class MovieRating{
    Rating rating = Rating.AVERAGE;

    switch(rating){
        case Rating.BAD:
            System.out.println("Don't waste time watching this.");
            break;
        case Rating.AVERAGE:
            System.out.println("Not bad.");
            break;
        case Rating.EXCELLENT:
            System.out.println("Great movie!");
            break;
    }
}

//Example Variant 2.
//Similar to a class, enum in Java can use attributes, constructors and methods.
enum Color {
    Black   (000,000,000),
    White   (255,255,255),
    Red     (255,000,000),
    Green   (000,255,000),
    Blue    (000,000,255);

    private int R;
    private int G;
    private int B;
    private static final MAX = 255;

    Color(int R, int G, int B){
        this.R = R;
        this.G = G;
        this.B = B;
    }

    public double getBrightness(){
        return (double)(R+G+B)/(double)(MAX*3);
    }
}
```

## **Testing, Assert Keyword and JUnit**
### **Assert keyword**

Assert evaluates an expression and will throw an **AssertionError** if the statement is false. Since it throws an **Error** type, it will cause our program to crash.

- You would utilise this feature in an attempt to ensure that your program is sound. We are able to test **pre-conditions**, **post-conditions** and anything in between.

- **Post-condition**
A post-condition is where any output from a method is considered to adhere to the requirement of the method.
**Simply:** What the method promises to do.

- **Pre-condition**
A pre-condition is where any input from a method is considered to adhere to the requirement of the method.
**Simply:** What the method expect to in take.

**Syntax: (How do we use it?)**
```java
assert expression

//Example.
assert list.size() > 0;
assert isFileLoaded();

private void preCheck(){
    File file = new File(path);
    assert file.exists();
    assert file.verify();
}
```
### **JUnit**
- A common testing framework in the Java ecosystem. You will need to write your own test classes to check if your code is performing correctly.

- **Black Box Testing** - User centric testing, **without knowledge of the internals**, input is given and compared to match the output of the program.

- **White Box Testing** - This is typically where we employ some unit testing software, to help analyse the **internals of the system** and test them independently.

The annotation which we can use in JUnit:
```java
@Test           //Annotates a method as a test method.
@Before         //Allows a method to initialize any object before a test case is executed.
@After          //Allows execution after a test case is executed.
@BeforeClass    //We can initalize class objects when the class is loaded.
@AfterClass     //We can check class objects after the class is loaded.

//Methods that can be used in JUnit.
assertNull(booleanExpression);
assertTrue(booleanExpression);
assertFalse(booleanExpression);
assertEquals(expected, actual);
assertSame(Obj01, Obj02);
```

**Compile Test File**
```
> javac -cp .:junit-4.12.jar:hamcrest-core-1.3.jar MyTestClass.java
```
**Run Test File**
```
> java -cp .:junit-4.12.jar:hamcrest-core-1.3.jar org.junit.runner.JUnitCore MyTestClass.java
```

## **Abstract Classes**
- `Abstract` class is similar to the concrete class, but it **cannot be instantiated**. It can also **enforce** a method implementation for subtypes.

- The only **difference** of an abstract class from a concrete class is that it **cannot be instantiated** and it can **specify methods subtypes must define**.

**Why would we use abstract?**

- The main case for abstract is that we have some type that we do not want to instantiate and is a **generalisation** of many other types.

>**For Example:**
>- Shape is a generalisation of Triangle, Square, Circle but we don't have a concrete instance of Shape.
>- Furniture is a generalisation of Chair, Sofa, Table and Desk.
>- Weapon is a generalisation of Guns, Swords, Missile and Bomb.

**Syntax: (How do we use it?)**
```java
[AccessModifier] abstract class ClassName{}

//Example.
public abstract class Furniture{
    //Class content.
}
```

### **Abstract Methods**
- We are able to declare an abstract method in **only abstract classes**. When we declare an abstract method we **do not define a method body** (The logic of the method). And the **subclasses must implement** the method body.

**Syntax: (How do we use it?)**
```java
[AccessModifier] abstract TypeName MethodName(argType1 argName1, argType2 argName2);

//Example.
public abstract void stack(Furniture furniture); //Don't define the body.
```

## **Interfaces**
`Interface` a list of abstract methods and default methods. Similar to abstract methods, interface **can not be instantiated** and it also defines the methods that a class **must implement**.

- Cannot specify any attributes except static final attributes and only methods can be specified.
- Do not (typically) provide a method definition.
- Cannot be instantiated.
- Whenever a class need to use interface, it uses the keyword `implements`.
- We can implement multiple interfaces in one class.

**When can we use interface?**

- We can use interface when two classes are not is-a relationship but share a same characteristic. For example, a dog and a robot don't have parent-child relationship, but they can both move. We could implement an IMoveable interface.

**For Example:** **There are TONS of objects in the game scene and you want to interact with some of them.**

>**Without interface, you will have to write:**
>- A lot of `interact` methods in different object classes in the scene.
>- If in the player class, detect area is collided with objectA that you know is interactable and button is pressed, call the `objectA.interact()`.
>- If the player detect area is collided with objectB that you know is interactable and button is pressed, call the `objectB.interact()`.
>- If ObjC, ObjD, ObjE, ...

>**With interface, you will just need to write:**
>- If the detect area is collided with anything that implements `IInteractable` and button is pressed, call the `interactObj.interact()`.

**For instance, in `Unity` you can write something like this to interact with objects with `C#`:**
```c#
public void Update(){
    GameObject nearestGameObject = GetNearestGameObject();
    if(nearestGameObject == null) return;
    if (Input.GetButtonDown("Fire1")){
        if (nearestGameObject.TryGetComponent(out IInteractable interactable)) 
            interactable.interact();
    }
}
```

**Syntax: (How do we use it?)**
```java
[AccessModifier] interface InterfaceName{}

//Example.
public interface IDamageable{
    //Interface content.
    public void damage(float amount);
    public void heal(float amount);
    public void destory();
}

//A class that implements the interface.
public class Cat implements IDamageable{
    public float health;
    public float defence;

    public Cat(float health, float defence){
        this.health = health;
        this.defence = defence;
    }

    public void damage(float amount){
        if(amount > 0){
            health -= amount * (1 - defence);
            System.out.println("Meow, it hurts!");
        }
    }

    public void heal(float amount){
        if(amount > 0){
            health += amount;
            System.out.println("Meow, it feels good!");
        }
    }

    public void destory(){
        health = 0;
        System.out.println("Meow, I died...");
    }
}

//A class that implements the interface.
public class Crate implements IDamageable{
    public int hitsCouldWithstand;

    public Crate(int hitsCouldWithstand){
        this.hitsCouldWithstand = hitsCouldWithstand;
    }

    public void damage(float amount){
        if(amount > 0){
            hitsCouldWithstand -= 1
            System.out.println("Crack!");
        }
    }

    public void heal(float amount){
        System.out.println("Cannot heal crate...");
    }

    public void destory(){
        hitsCouldWithstand = 0;
        System.out.println("Boom, Crate is Shattered!");
    }
}

//So you can write something like:
//If my sword collides with anything that is damageable (With IDamageable), call the damage function.
//You will not need to to know what you hit with sword.
//And you will not need to get the class then call the specific method in that concrete class.
```

### **Default Methods**
- Simply we are able to define a default method in the interface by using `default` keyword.

**Syntax: (How do we use it?)**
```java
[Modifier] default <returnType> MethodName(parameters){}

//Example.
public default void talk(String content){
    //Method body.
}
```

## **Generics**
**Why do we need `Generics`?**

- Without generics, we would need to create duplicating code for every data type. We would need to create:
>- `IntArrayList`
>- `DoubleArrayList`
>- `FloatArrayList`
>- `StringArrayList`

- This is awful, now we're maintaining duplicate code for a change in data type. However, with generics, we will know what kind of data type we are storing.

**The advantage of generics:**
- Stronger type checks at complie time
- Elimination of casts
- Enabling programmers to implement generic algorithms

**Syntax: (How do we use this?)**
```java
//Generic variables.
[public] T variable;
[public] type<T> variable;
//Generic classes.
[public] class ClassName<Param0[,Param1...]>{}
//Generic method in generic classes.
[public][static] T methodName(T param){}
//Static generic method in non-generic classes.
[public] static <Param0[,Param1...]> returnType methodName(Param0[,Param1]){}

//Example.
public class Container<T, V>{
    public T variableA;
    public V variableB;
    public ArrayList<T> variableList;

    public T get(){
        //Content.
    }

    public void set(V element){
        //Content.
    }
}

public class Container{
    //Static generic method in non-generic classes.
    public static <T> T find(T needle, T[] sea){
        //Content.
    }
}

public class mainClass{
    class Needle{
        public int value;
        public Needle(int value){
            this.value = value;
        }
    }

    public static void main(String[] args){
        needle n = new Needle(25);
        needle[] ns = {
            new Needle(10),
            new Needle(25),
            new Needle(80)
        };
        //Call static generic method.
        Container.<Needle>find(n, ns);
    }
}
```
**Type Parameters** - We also can specify an upper bound type:
```java
[public] class ClassName<Param0 [extends SuperType]>

//Example.
public class ShoppingCart<T extends Item>{
    //Class content.
}
```
**Generic Arrays** - Java can not create generic array. Unless we store the data in an object array first and cast the target type.

```java
public class JArray<T>{
    private T[] array;
    public JArray(int length){
        array = (T[]) new Object[length];
    }

    public T[] get(){
        return array;
    }

    public T get(int index){
        if(index >= array.length){
            throw new ArrayIndexOutOfBoundsException();
        }
        return array[index];
    }

    public void set(int index, T obj){
        array[index] = obj;
    }

    public void clear(){
        array = (T[]) new Object[array.length];
    }

    public int length(){
        return array.length;
    }
}
```
**Iterable & Iterator** - Implement generic interface to make the foreach loop work in your own class.
```java
public class MyOwnLinkedList<T> implements Iterable<T>{
    //Some linked list logic...

    public Iterator<T> iterator(){
        return new Iterator<T>(){
            Node<T> cursor;

            public boolean hasNext(){
                return cursor != null;
            }

            public T next(){
                T value = cursor.value;
                cursor = cursor.next;
                return value;
            }
        }
    }
}
```

## **Recursion & Memoization**
**What is recursion?**
- Recursion is a technique within computer science that allows calling a function itself.
- Recursive functions are aligned with recursive sequence or series, where the output of a function is dependent on the output from the same function with a change of input.

**Recursive function is made of:**
- **A base case** (or many base cases), where the function terminates.
- **Recursive case** (or many recursive cases), which will converge to a base case. (Goes towards a base case, otherwise it will never stop)
Once it reaches the bottom, it will start **Backtracking**.

_Note: Drawing an execution tree will help understand the complicated recursion._

**Disadvantages of recursion:**
- The java programming model does not allow for infinite recursion.
- Inefficient with memory.
- Potentially more computationally demanding due to the overhead caused by method calls.

**Advantages of recursion:**
- Problem can often be represented easily with recursion.

**What is memorization?**
- Memoization is a technique for storing the results of a computation.
- You may know it as a different term: **Caching**.
- We store the result as we may need to reuse it later.
- Let's say we had a website that computes a simple page, the page doesn't differ between each user access, we could keep the result and send it every time it is asked.

## **Anonymous Classes**
- **Construct an instance of an interface immediately. (A class that implement the interface.)**

- **Format:** `interface = new Type() {[Fields] [Functions]};`

- **Note:** Unlike Lambdas, Anonymous Classes can also create instances of non-functional interfaces. (Interfaces with multiple abstract methods.) But need to implemtent all of the abstract methods.

```Java
/**
 * The output is:
 * こんにちは!
 * Jatutu.
 */

interface Greetings{
    public default void sayComplexHello(String name){
        sayHello();
        System.out.println(name + ".");
    }
    public void sayHello();
}

public class TestGreetings{
    //Set language to Japanese.
    public static String lang = "JPN";
    public static String name = "Jatutu";

    public static void main(String[] args){
        Greetings greetings;

        //We can use different operations using the Greetings interface.
        switch(lang){
            case "ENG":
                greetings = new Greetings() {
                    @Override
                    public void sayHello(){
                        System.out.println("Hello!");
                    }
                };
                break;
            case "CHN":
                greetings = new Greetings() {
                    @Override
                    public void sayHello(){
                        System.out.println("你好!");
                    }
                };
                break;
            case "JPN":
                greetings = new Greetings() {
                    @Override
                    public void sayHello(){
                        System.out.println("こんにちは!");
                    }
                };
                break;
            case "ITY":
                greetings = new Greetings() {
                    @Override
                    public void sayHello(){
                        System.out.println("Ciao!");
                    }
                };
                break;
            default:
                greetings = new Greetings() {
                    @Override
                    public void sayHello(){
                        System.out.println("!");
                    }
                };
                break;
        }

        //We just need to call the function without knowing the operation.
        greetings.sayComplexHello(name);
    }
}
```

## **Lambda Functions**
- **For quick use of interfaces.**
_[If this is not clear, Imaging the use cases of calculator]_

- **Requirement:** The interface must delare only one abstract method.

- **Format:** `interface = (argument1, argument2, ...) -> functionBody`

- **Note:** Prior to Java 8, Lambda does not exist.

```Java
/**
 * The output is also:
 * こんにちは!
 * Jatutu.
 */

interface Greetings{
    public default void sayComplexHello(String name){
        sayHello();
        System.out.println(name + ".");
    }
    public void sayHello();
}

public class TestGreetings{
    //Set language to Japanese.
    public static String lang = "JPN";
    public static String name = "Jatutu";

    public static void main(String[] args){
        Greetings greetings;

        //We can use different operations using the Greetings interface.
        switch(lang){
            case "ENG":
                greetings = () -> System.out.println("Hello!");
                break;
            case "CHN":
                greetings = () -> System.out.println("你好!");
                break;
            case "JPN":
                greetings = () -> System.out.println("こんにちは!");
                break;
            case "ITY":
                greetings = () -> System.out.println("Ciao!");
                break;
            default:
                greetings = () -> System.out.println("!");
                break;
        }

        //We just need to call the function without knowing the operation.
        greetings.sayComplexHello(name);
    }
}
```

## **Wildcards**
Unlike arrays, where we are able to assign types to a variable of an inherited type, Generic types cannot be assigned to a type that specifies a lower bound.
```java
//If you have a parent and a child type.
public class Animal{}
public class Cat extends Animal{}
public class Container<T>{}

//You can do this.
public Animal[] animalArrayA = new Cat[5];
public Animal[] animalArrayB = {
    new Cat("Happy Cat"),
    new Cat("Sad Cat")
};

//But you cannot do this in Generics.
public Container<Animal> animals = new Container<Cat>();
```
In wildcards we can read if we know the super type and we can write if we know the lower bound (Child Type).

**Syntax: (How can we use it?)**
```java
//We don't know the type of the generics.
Type<?> variable;
//We don't know the type of the generics but we know the lower bound.
//Anything that is a parent of the child. (Including the parent)
//We can only write.
Type<? super LowerBound> variable;
//We don't know the type of the generics but we know the upper bound.
//Anything that is a child of the parent. (Including the child)
//We can only read.
Type<? extends UpperBound> variable;

//Write employee into any list that is parent of employee.
//No matter how broad the scope is, employee is still in the scope.
//Adding a employee to a upper bound list is always valid. 
//Eg. Adding employee into an employee list, a person list,
//an animal list, a living being list and an everything list is still valid.
//However, if use ? extends xx, it will go down infinitely.
//Eg. It will not be possible if you put an employee into a product manager list.
//Because not all employees are product managers, no?
public void add(List<? super Employee> list, Employee e){
    list.add(e);
}

//Write customer into any list that is parent of customer.
//No matter how broad the scope is, customer is still in the scope.
//Adding a customer to a upper bound list is always valid.
//Eg. Adding customer to a person list, an animal list,
//a living being list or an everything list is all valid.
public void add(List<? super Customer> list, Customer c){
    list.add(c);
}

//Read a list of anything that is a child of employee.
//No matter what they are specifically, read them as an employee is valid.
public void getEmployees(List<? extends Employee> list){
    for(Employee e : list){
        //Print the employee.
    }
}

//Read a list of anything that is a child of person.
//No matter what they are specifically, read them as a person is valid.
public void getPersons(List<? extends Person> list){
    for(Person p : list){
        //Print the person.
    }
}
```

## **Java Debugger**
You can use Java Debugger to make life easier.
```
> jdb MyProgram                              //Start debugging.
...
> stop at MyProgram:32                       //Set stopping line number.
...
> run                                        //Run the program.
...
FunctionName > locals                        //Check local variables.
...
FunctionName > step                          //Continue one line.
...
FunctionName > set variableName = value      //Set a variable value.
...
FunctionName > cont                          //Continue the program.
...
FunctionName > dump className[.funcName()]   //Call functions or inspect classes.
...
FunctionName > exit                          //Exit debugger.
```

## **Create an Java Archive [JAR]**
Create JAR without manifest:
```
jar -cf MyProgram.jar <List of *.class file [Separate with space]>
vim MyProgram.jar
Inside MANIFEST.MF add Main-Class: MyMainClass
```
Create JAR with a manifest:
```
Create a .txt file in the directory.
jar -cfm MyProgram.jar MyTxtFile.txt <List of *.class>
```
Run the JAR File:
```
java -jar MyProgram.jar
```
Or Create JAR with Gradle Build Command:
```
gradle build
```
Then the built files will be available at: `\build\distributions\zipFile.zip`. We will use the .bat file in the zip to execute the program.

## **Javadoc**
- Documentation is an important aspect to application development. you are producing a technical manual for others to read so they can comprehend your code and utilise it.

**You should:**
- Write Javadoc Comments
- Write with clear method names and style.
```Java
/**
 * A method that finds the cat that is the happiest in scene.
 * @param cats All cats in scene.
 * @return Return the happiest cat.
 */
```
**Identifier:**
- `@return` - Return type description.
- `@param` - Parameter description.
- `@see` - Add a method to `See Also:` in javadoc.
- `@since` - When the method was included in your library.
- `@throws` - Specify what exception it will throw and when to throw.
- `@deprecated` - marks a method/class for removal.

**Export Javadoc:**
```
> javadoc -d <Export Directory> <Path to .java files>
> javadoc -d <Export Directory> -subpackages packageName
```
