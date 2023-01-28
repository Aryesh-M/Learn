#### OOP Concepts:   
> ![image](https://user-images.githubusercontent.com/58625165/215205861-8dd5adad-97bb-4d7f-bba0-4c159e099ff4.png)  
> **TR:** A PIE (🥧) - Abstraction, Polymorphism, Inheritance, and Encapsulation   

#### Abstraction:   
> - A mechanism to provide the details about essential features without describing the background details  
> - For example, when you login into a website, you enter your UserId and password which is the essential information for login.   
> - Here you don't know about the background details like what happens with your userId and password, how it gets verified. All is abstrastracted from you.   

#### Encapsulation:   
> - A mechanism of binding the object state (fields) and behaviour (methods) together into a single unit.  
> - The encapsulation is mainly achieved by creating classes.     
> - The class is a kind of a container or capsule, which encapsulates the set of fields and methods.   

#### Inheritance:   
> - A mechanism of acquiring the features and behaviours of a class by another class.   
> - The class whose members are inherited is called the **base class**, and the class that inherits those members is called the  **derived class**.   

#### Polymorphism:   
> - Ability of an object to behave in multiple ways.     
> - For example, smart phone is a single object but it can be used for making calls, listening music, sending emails, taking pictures, etc.,   
> ![image](https://user-images.githubusercontent.com/58625165/215212595-a7a18f21-d5a7-4ac5-9f7d-b8d33453d6cc.png)   

#### Class:   
> - A user defined data structure that contains data members (like fields, properties) and member functions (like methods, constructor, destructor)  
> - It is a  reference type and it acts as a template (blue print) for an object.   

#### Object:   
> - A representative of the class and allocates memory to its class members (fields)   
> - An object is a real world entity having attributes (fields) and behaviours (methods)   

#### Access Modifiers:  
> - Used to specify the accessibility of a member (field, method) or a type (class, interface)  
> - Support abstraction by exposing only necessary members and hiding other members  
> ![image](https://user-images.githubusercontent.com/58625165/215214269-2c337923-8ed7-4e91-ba0c-0713e251fd8b.png)   
> 
> **Access Modifiers Member Accessibility:**  
> ![image](https://user-images.githubusercontent.com/58625165/215214405-bb3c0a94-6a1b-4ada-984f-0d5fedb2c092.png)    

#### Types of constructor:  
> ![image](https://user-images.githubusercontent.com/58625165/215222241-f2138994-518c-47ac-817f-10761a482975.png)   
> 
> **Default constructor:**   
> - The default constructor has no parameters.   
> - When a class has no constructor, default constructor is served by the compiler to that class.   
> - Used to assign default values to instance variables of class.   
>  
> **Parameterized constructor:**   
> - The parameterized constructor has one or more parameters.   
> - Used to assign values to instance variables of class.  
>  
> **Private constructor:**  
> - Restrict a class _external_ instantiation but in nested class you can instance of this class.   
> - In c# 1.X there was no static class, so developer used private constructor to prevent a class _external_ instantiation.   
> - Used to implement singleton pattern i.e., a single instance for a class.    
> - A class can have multiple private constructors and public constructors.   
> 
> **Static constructor:**   
> - A special type of constructor that gets called before the first object of the class is created.   
> - Used to initialize any static fields, or to perform a particular action that need to perform only one.   
> - A class can have only one static constructor and it must be a defualt constructor, having no access modifier.   
> 
> **Destructor:**  
> - A special type method which has the same name as its class name preceded by a tilde (~) sign.   
> - Used to release unmanaged resources allocated by the object.  
> - Automatically called before an object is destroyed and cannot be called explicitly.   
> - A class can have only one constructor.   
> 
> **Inheritance:**   
> - A mechanism of acquiring the features and behaviours of a class by another class. 
> - The class whose members are inherited is called the **base class,** and the class that inherits those members is called the **derived class**.   
> 
> **Advantages of Inheritance:**   
> - Reduce code redundancy.    
> - Improves code resuability.   
> - Code is easy to manage and divided into parent & child classes.   
> - Supports code extensibility by overriding the base class functionality within derived classes.       
> 
> **Types of Inheritance:**  
> ![image](https://user-images.githubusercontent.com/58625165/215283835-4987d4aa-e5a3-4fb0-9c3b-c2a134e8c96f.png)   
> **Note:** _C# does not support Multiple and Hyrid inheritance._   
> 
> **Single Level Inheritance:**   
> - In this inheritance, a derived class is created from a single base class.   
> ![image](https://user-images.githubusercontent.com/58625165/215283986-a728767c-9f28-4cc0-87f0-ec724efb4db2.png)  
> 
> **Multi-Level Inheritance:**   
> - In this inheritance, a derived class is created from another derived class.   
> ![image](https://user-images.githubusercontent.com/58625165/215283999-640f68fe-3a32-41a2-961a-1e4a552c0da4.png)    
> 
> **Hierarchical Inheritance:**   
> - In this inheritance, more than one derived classes are created from a single base.    
> - Not supported by C#
> ![image](https://user-images.githubusercontent.com/58625165/215284051-343feb29-d371-4bae-9020-c4e307e1847e.png)    
> 
> **Hybrid Inheritance:**   
> - This is combination of more than one inheritance.   
> - Hence, it may be a combination of multilevel or multiple inheritance or hierarchical inheritance.   
> - Not supported by C#   
 
> 
> **Methods:**   
> - A method contains a set of statements   
> - A method has name, parameters (separated by comma), body (wrapped using curly braces {}) and a return type.   
> - Methods are declared in a class or struct by specifying the access modifiers like as public or private.   
> 
> **Method Overloading:**   
> - In method overloading, a class has more than one method with same name but having different signature.  
> - **Adds or extends** the behaviour of an existing method.  
> - Method signature includes number and type (i.e., theirs data types) of parameters.   
> - Method signature does not include method return type and method access modifier.   
> - An example of compile time polymorphism since actual method calling is resolved at compile time.   
> 
> **Method Overriding:**   
> - In method overriding, a derived class have the same methods with exactly the same signature as base class.  
> - **Change** the behaviour of an existing method in the base class.   
> - Unlike method overloading, here methods must have same access modifiers (public, protected, and internal and **not** private)    
> - An example of run time polymorphism since actual method calling is resolved at **runtime**.   
>  ![image](https://user-images.githubusercontent.com/58625165/215285317-2704c05b-435f-4901-a38a-7d74f6149d1d.png)    
>  **Note:** We have to use **virtual** in base class method and **override** in derived class method to perform method overriding.   
>  
>  **Method Hiding:**   
>  - A way to hide a method of base class into derived class using new keyword.   
>  - Unlike method overriding, the base class method you don't need to declare as virtual.   
>  - Unlike method overriding, the actual method calling is resolved at **compile time**.   
>  ![image](https://user-images.githubusercontent.com/58625165/215285854-8037c400-ffd1-456c-9e12-827abe185adc.png)   
>  **Note:** We have removed **virtual** keyword from the base class method and replaced **virtual** with **new** keyword in derived class method.   
>  
