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
> _A namespace is a container for classes and namespaces._   
> The namespace also gives unique names to its classes thereby you can have the same class name in different namespaces.   
> In C#, a namespace can be defined using the namespace keyword.    
> ```c#    
>  namespace School
> {
>   // define classes here
> 
> }   
> ```   
> Classes under the same namespace can be referred to as namespace.classname syntax. For example, the Student class can be accessed as School.Student.    
> ```c#    
>  namespace CSharpTutorials
> {
>   class Program
>   {
>       static void Main(string[] args)
>       {
>           School.Student std = new School.Student();
>       
>           School.Course cs = new School.Course();
>       }
>   }
> }   
> ```   
> To use classes under a namespace without the fully qualified name, import the namespace with the using keyword at the top of C# class file.   
> ```c#    
>  using System; //built-in namespace
> using School;
> 
> namespace CSharpTutorials
> {
>   class Program
>   {
>       static void Main(string[] args)
>       {
>           Student std = new Student();
>       }
>   }
> }  
> ```   
> A namespace can contain other namespaces. Inner namespaces can be separated using (.).   
> ```c#  
>  namespace School.Education
> {
>   class Student
>   {
> 
>   }
> } 
> ```   
> Beginning with C# 10, you can declare a namespace for all types defined in that file without wrapping classes inside curly braces { .. }, as shown below.     
>      
> ```c#   
> namespace School.Education
>   
> class Student
> {
> 
> }
> ```    
>           


#### Variables in C#   
> **Conventions:**   
> - Variable names must be unique.
> - Variable names can contain letters, digits, and the underscore _ only.
> - Variable names must start with a letter.
> - Variable names are case-sensitive, num and Num are considered different names.
> - Variable names cannot contain reserved keywords. Must prefix @ before keyword if want reserve keywords as identifiers.   
> **Note:** A value must be assigned to a variable before using it.   
> 

#### Create Variables using var   
> In C#, variables must be declared with the data type. These are called **explicitly typed variables**.   
> ```c#   
> int i = 100;// explicitly typed variable      
> ```      
> C# 3.0 introduced var keyword to declare method level variables without specifying a data type explicitly:      
> ```c#    
> var j = 100; // implicitly typed local variable    
> ```     
> The compiler will infer the type of a variable from the expression on the right side of the = operator. Above, var will be compiled as int.    
> ```c#   
> int i = 10;
> var j = i + 1; // compiles as int   
> ```    
> Implicitly-typed variables must be initialized at the time of declaration; otherwise C# compiler would give an error: Implicitly-typed variables must be initialized.   
> ```c#    
> var i; // Compile-time error: Implicitly-typed variables must be initialized:   
> i = 100;   
> ```        
> Multiple declarations of var variables in a single statement are not allowed:     
> ```c#     
>   var i = 100, j = 200, k = 300; // Error: cannot declare var variables in a single statement    
>   //The followings are also valid
>   var i = 100; 
>   var j = 200; 
>   var k = 300;   
> ```   
> var cannot be used for function parameters:    
> ```c#     
> void Display(var param) //Compile-time error
> {
>   Console.Write(param);
> }
> ```   
> var can be used in for, and foreach loops:   
> ```c#    
> for(var i = 0; i < 10; i++)
> {
>   Console.WriteLine(i);
> }  
> ```   
> var can also be used with LINQ queries:    
> ```c#   
>  // string collection
>  IList< string> stringList = new List< string>() { 
>   "C# Tutorials",
>   "VB.NET Tutorials",
>   "Learn C++",
>   "MVC Tutorials" ,
>   "Java" 
>  };
>  
>  // LINQ Query Syntax
>  var result = from s in stringList
>           where s.Contains("Tutorials") 
>           select s;   
> ```   
> 
  
  
#### Data Types in C#  
> C# mainly categorized data types in two types: Value types and Reference types:    
> ![image](https://user-images.githubusercontent.com/58625165/215862575-07c7cbc3-ae93-4136-8a4e-046600fef5bc.png)   
> 
<table>
    <thead>
        <tr>
            <th>Bit Length</th>
            <th>Signed/Unsigned</th>
            <th>Data Type</th>
            <th>Suffix</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td rowspan=3>8-bit</td>
            <td>unsigned</td>
            <td>byte</td>
            <td></td>
        </tr>
        <tr> 
            <td>signed</td>
            <td>sbyte</td>
            <td></td>         
        </tr>
        <tr>
            <td></td>
             <td>bool</td>
            <td></td>         
        </tr> 
        <tr>
            <td rowspan=3>16-bit</td>
            <td>signed</td>
            <td>short</td>
            <td></td>         
        </tr>
        <tr>
            <td>unsigned</td>
            <td>ushort</td>
            <td></td>         
        </tr>
        <tr>
            <td></td>
            <td>char</td>
            <td></td>         
        </tr>
      <tr>
            <td rowspan=3>32-bit</td>
            <td>signed</td>
            <td>int</td>
            <td></td>
        </tr>
        <tr>
            <td>unsigned</td>
            <td>uint</td>
            <td>u</td>
        </tr>
        <tr>
            <td></td>
            <td>float</td>
            <td>f</td>
        </tr> 
      <tr>
            <td rowspan=3>64-bit</td>
            <td>signed</td>
            <td>long</td>
            <td>l</td>
        </tr>
        <tr>
            <td>unsigned</td>
            <td>ulong</td>
            <td>ul</td>
        </tr>
        <tr>
            <td></td>
            <td>double</td>
            <td>d</td>
        </tr>
      <tr>
            <td>128-bit</td>
            <td></td>
            <td>decimal</td>
            <td>m</td>
        </tr>
    </tbody>
</table>   
> - The predefined data types are alias to their .NET type (CLR class) name.   
> - byte is an alias of System.Byte (.NET type), int (alias) of System.Int32 (.NET Type). So, both are same:    
> ```c#    
>   int i = 345;
>   Int32 i = 345;// same as above   
> ```   
> - Every data type has a default value. Numeric type is 0, boolean has false, and char has '\0' as default value.      
> - Use the default(typename) to assign a default value of the data type or C# 7.1 onward, use default literal:   
> ```c#   
> int i = default(int); // 0
> float f = default(float);// 0
> decimal d = default(decimal);// 0
> bool b = default(bool);// false
> char c = default(char);// '\0'
> 
> // C# 7.1 onwards
> int i = default; // 0
> float f = default;// 0
> decimal d = default;// 0
> bool b = default;// false
> char c = default;// '\0' 
> ```   
> 
> **Conversions:**   
> _The values of certain data types are automatically converted to different data types in C#. This is called an **implicit conversion**._   
> ```c#    
> int i = 345;
> float f = i;
> 
> Console.WriteLine(f); //output: 345  
> ```   
> However, not all data types are implicitly converted to other data types. For example, int type cannot be converted to uint implicitly. It must be specified explicitly, as shown below:   
> ```c#   
>  public static void Main()
>  {
>      int i = 100;
>      uint u = (uint) i;
>      Console.Write(i);
>  }   
> ```   
>                

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
