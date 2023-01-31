[ Reference: [Tutorials Teacher](https://www.tutorialsteacher.com/csharp)    ]    
## Index:
* [C# Fundamentals](#c-fundamentals)
* [C# Conditions & Loops](#c-conditions--loops)  
* [C# Collections](#c-collections)  
* [C# Exception Handling, File Operation](#c-exception-handling-file-operation)
* [C# Events & Delegates](#c-events--delegates) 
* [C# Articles](#c-articles)    

## C# Fundamentals
#### Reserved Keywords in C#  
> _Note_: this section is not much of importance (try not to memorize all this instead visit [Tutorials Teacher](https://www.tutorialsteacher.com/csharp/csharp-keywords))   
> **Modifier Keywords:**   
> _Modifier keywords are specific keywords that indicate who can modify types and type members._  
> abstract, async,   
> const,    
> event, extern,  
> new,     
> override,   
> partial,   
> readonly,   
> sealed,  static,      
> unsafe,   
> virtual, volatile   
 
> **Access Modifier Keywords:**   
> _They define the accessibility of the class and its members._   
> 
| Access Modifiers  |    Usage      |
| ----------------- | ------------- |
| public    | The Public modifier allows any part of the program in the same assembly or another assembly to access the type and its members. |
| private   | The Private modifier restricts other parts of the program from accessing the type and its members. Only code in the same class or struct can access it. |
| internal  | The Internal modifier allows other program code in the same assembly to access the type or its members. This is default access modifiers if no modifier is specified. |
| protected | The Protected modifier allows codes in the same class or a class that derives from that class to access the type or its members. |   

> **Statement Keywords:**   
> _Statement keywords are related to program flow._    
> if, else, switch, case, do, for, foreach, in, while, break, continue, default, goto, return, yield, throw, try, catch, finally, checked, unchecked, fixed, 
lock,   

> **Method Parameter Keywords:**   
> _These keywords are applied to the parameters of a method._    
> params, ref, out    

> **Namespace Keywords:**   
> _These keywords are applied with namespace and related operators._    
> using, . (operator), :: (operator), "extern alias"    

> **Operator Keywords:**   
> _Operator keywords perform miscellaneous actions._   
> as, await, is, new, sizeof, typeof, stackalloc, checked, unchecked    

> **Access Keywords:**  
> _Access keywords are used to access the containing class or the base class of an object or class._   
> base, this   

> **Literal Keywords:**   
> _Literal keywords apply to the current instance or value of an object._   
> null,    
> false,    
> true,    
> value,    
> void    

> **Type Keyword:**   
> _Type keywords are used for data types._    
> bool, byte, char, class, decimal, double, enum, float, int, long, sbyte, short, string, struct, uint, ulong, ushort    

> **Contextual Keywords:**   
> _Contextual keywords are considered as keywords, only if used in specific contexts. They are not reserved and so can be used as names or identifiers._   
> add, var, dynamic, global, set, value   
> ![image](https://user-images.githubusercontent.com/58625165/215641595-7abefee8-b00e-4232-8c13-5398dca423f2.png)    


> **Query Keywords:**   
> _Query keywords are contextual keywords used in LINQ queries._   
>  from, where, select, group, into, orderby, join, let, in, on, equals, by, ascending, descending    
> ![image](https://user-images.githubusercontent.com/58625165/215641842-6aa343d7-c148-4fd5-93fa-fc809f9e17e6.png)    
> Note, here "class" is used as an identifier (name of the variable, **class**, interface, etc.)    



#### Classes in C#   
> _A class is like a blueprint of a specific object that has certain attributes and features._    
> - A class can contain one or more constructors, fields, methods, properties, delegates, and events. They are called **class members**.   
> 
> **Field:**   
> - A class can have one or more fields.   
> - It is a class-level variable that holds a value.  
> ```c#          
>  class Student
> {
>    public int id;
>
> }
> ```   
> 
> **Property:**   
> _A property encapsulates a private field using setter and getter to assign and retrieve underlying field value._    
> ```c#    
> class Student
> {
>   private int id;
> 
>   public int StudentId
>   {
>       get { return id; }
>       set {
>       if (value > 0)
>           id = value;
>   }
>   }
> } 
> ```   
> - In the above example, the id is a private field that cannot be accessed directly.    
> - It will only be accessed using the StudentId property.    
> - The get{ } returns the value of the underlying field and set{ } assigns the value to the underlying field id.   
> - **Note:** set may or may not have additional logic.             
> 
> **Auto-implemented Property:**   
> - From C# 3.0 onwards, property declaration has been made easy if you don't want to apply some logic in getter or setter.   
> - Using auto-implemented property, you don't need to declare an underlying private field. C# compiler will automatically create it in IL code.   
> ```c#    
> class Student
> {
>   public string FirstName { get; set; }
>   public string LastName { get; set; }
> }  
> ```   
> **Note:** In the above example, backing private field for the FirstName and LastName will be created internally by the compiler. This speed up the development time and code readability.     
> 
> **Method:**   
> - _A method can contain one or more statements to be executed as a single unit._    
> - A method may or may not return a value.   
> - A method can have one or more input parameters.    
> Syntax:   
> ```c#    
>  [access-modifier] return-type MethodName(type parameterName1, type parameterName2,...)
> {
>   
> 
> }  
> ```   
> 
> **Constructor:**   
> _A constructor is a special type of method which will be called automatically when you create an instance of a class._    
> A constructor is a special type of method which will be called automatically when you create an instance of a class.   
> ```c#      
> class Student
> {
>   public Student()
>   {
>       //constructor
>   }
> }
> ```        
> - A constructor name must be the same as a class name.
> - A constructor can be public, private, or protected.   
> - The constructor cannot return any value so cannot have a return type.    
> - A class can have multiple constructors with different parameters but can only have one parameterless constructor.   
> - If no constructor is defined, the C# compiler would create it internally.    
> 
> **Objects of a Class:**   
> Create an object:   
> ```c#    
>  Student mystudent = new Student();      
> ```   
> 
  
#### Namespaces in C#
#### Variables in C#
#### Create Variables using var
#### Data Types in C#
#### Working with Numbers in C#
#### Strings in C#
#### Working with Date and Time in C#
#### Struct type in C#
#### Enum type in C#
#### StringBuilder over String in C#
#### Anonymous types in C#
#### Dynamic type in C#?
#### Nullable types in C#
#### Value types & Reference types
#### Declare and implement interfaces in C#
#### Operators in C#
#### Partial Classes in C#
#### Static types in C#
#### Object Initializer Syntax
#### Covariance and Contravariance
#### Extension methods in C#

## C# Conditions & Loops  
#### if, elseif, else Condition
#### Ternary Operator ?:
#### Switch Statement
#### For Loop
#### While Loop
#### do while Loop

## C# Collections  
#### Array
#### Multidimensional Array
#### Jagged Array
#### ArrayList
#### List
#### SortedList
#### Dictionary
#### Hashtable
#### Stack
#### Queue
#### Tuple
#### ValueTuple

## C# Exception Handling, File Operation  
#### Built-in Exception Classes
#### Exception Handling
#### throw keyword
#### Working with Custom Exceptions
#### Stream Input/Output
#### Working with File System
#### Access File using FileInfo Class

## C# Events & Delegates 
#### What is Delegates?
#### Func Delegate
#### Action Delegate
#### Predicate Delegate
#### Anonymous Methods

## C# Articles    
#### Static vs Singleton in C#
#### Difference between == and Equals() Method in C#
#### Asynchronous programming with async, await, Task in C#
#### Difference between static, readonly, and constant in C#
#### IndexOutOfRangeException in C#
#### Foreach Loop in C#
#### How to loop through an enum in C#?
#### NullReferenceException in C#
#### Generate Random Numbers in C#
#### Set Default Value to Property in C#
#### Variable Scopes in C#
#### When to use Struct over Class in C#
#### Difference between Two Dates in C#
#### Convert int to enum in C#
#### BigInteger Data Type in C#
#### Convert String to Enum in C#
#### Convert an Object to JSON in C#
#### Convert JSON String to Object in C#
#### The Main() Method in C#
#### How to Pass or Access Command-line Arguments in C#?
#### DateTime Formats in C#
#### How to convert date object to string in C#?
#### Searching in C# array
#### Compare strings in C#
#### How to count elements in C# array?
#### How to combine two arrays without duplicate values in C#?
#### Difference between String and string in C#.
#### How to get a comma separated string from an array in C#?
#### How to remove duplicate values from an array in C#?
#### How to sort an array in C#?
#### How to sort object array by specific property in C#?
#### ref Keyword in C#
#### Query geolocation & proxy data in .NET using IP2Location
#### Boxing and Unboxing in C#
#### out keyword in C#
#### How to convert string to int in C#?
#### Design Principle vs Design Pattern
#### How to calculate the code execution time in C#?
#### How to read file using StreamReader in C#?
#### Difference between delegates and events in C#
#### How to sort the generic SortedList in the descending order?
#### How to write file using StreamWriter in C#?
#### Difference between Array and ArrayList
#### Difference between Hashtable and Dictionary
#### C# Q & A
