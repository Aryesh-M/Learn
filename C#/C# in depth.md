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
            <th>Alias of</th> 
        </tr>
    </thead>
    <tbody>
        <tr>
            <td rowspan=3>8-bit</td>
            <td>unsigned</td>
            <td>byte</td>
            <td></td>
            <td>Byte</td>
        </tr>
        <tr> 
            <td>signed</td>
            <td>sbyte</td>
            <td></td>
            <td>SByte</td>
        </tr>
        <tr>
            <td></td>
             <td>bool</td>
            <td></td>    
            <td>Boolean</td>
        </tr> 
        <tr>
            <td rowspan=3>16-bit</td>
            <td>signed</td>
            <td>short</td>
            <td></td>  
            <td>Int16</td>
        </tr>
        <tr>
            <td>unsigned</td>
            <td>ushort</td>
            <td></td>    
            <td>UInt16</td>
        </tr>
        <tr>
            <td></td>
            <td>char</td>
            <td></td>   
            <td>Char</td>
        </tr>
      <tr>
            <td rowspan=3>32-bit</td>
            <td>signed</td>
            <td>int</td>
            <td></td>
            <td>Int32</td>
        </tr>
        <tr>
            <td>unsigned</td>
            <td>uint</td>
            <td>u</td>
            <td>UInt32</td>
        </tr>
        <tr>
            <td></td>
            <td>float</td>
            <td>f</td>
            <td>Single</td>
        </tr> 
      <tr>
            <td rowspan=3>64-bit</td>
            <td>signed</td>
            <td>long</td>
            <td>l</td>
            <td>Int64</td>
        </tr>
        <tr>
            <td>unsigned</td>
            <td>ulong</td>
            <td>ul</td>
            <td>UInt64</td>
        </tr>
        <tr>
            <td></td>
            <td>double</td>
            <td>d</td>
            <td>Double</td>
        </tr>
      <tr>
            <td>128-bit</td>
            <td></td>
            <td>decimal</td>
            <td>m</td>
            <td>Decimal</td>
        </tr>
    </tbody>
</table>   

> **Note:** Signed means having "-" sign as well and unsigned means 0 and non-negative.   
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
> Numbers, in general, can be divided into two types: Integer type and floating-point types:   
> ![image](https://user-images.githubusercontent.com/58625165/215872124-3086dc11-42d0-401e-bcec-a144a9f2742c.png)    
>  - The int data type is also used for hexadecimal and binary numbers.     
>  - A hexadecimal number starts with 0x or 0X prefix. C# 7.2 onwards, a binary number starts with 0b or 0B.    
>  ```c#     
>  int hex = 0x2F;
>  int binary = 0b_0010_1111;
>  
>  Console.WriteLine(hex);
>  Console.WriteLine(binary); 
>  ```   
>  
>  The decimal type has more precision and a smaller range than both float and double, and so it is appropriate for financial and monetary calculations.   
>  
>  **Scientific Notation:**    
>  _Use e or E to indicate the power of 10 as exponent part of scientific notation with float, double or decimal._   
>  ```c#    
>  double d = 0.12e2;
>  Console.WriteLine(d);  // 12;
>  
>  float f = 123.45e-2f;
>  Console.WriteLine(f);  // 1.2345
>  
>  decimal m = 1.2e6m;
>  Console.WriteLine(m);// 1200000  
>  ```          
  

#### Strings in C#  
>  _The maximum size of a String object in memory is 2GB or about 1 billion characters. However, practically it will be less depending upon CPU and memory of the computer._   
>  There two ways to declare a string variable in C#. Using System.String class and using string keyword. Both are same and make no difference:    
> ```c#   
> string str1 = "Hello"; // uses string keyword
> 
> String str2 = "Hello"; // uses System.String class  
> ```   
> In C#, a string is a collection or an array of characters. So, string can be created using a char array or accessed like a char array:   
> ```c#   
> char[] chars = {'H','e','l','l','o'};
> 
> string str1 = new string(chars);  
> String str2 = new String(chars); 
> 
> foreach (char c in str1)
> {
>   Console.WriteLine(c);
> }
> 
> ```   
> **Verbatim Strings:**   
> - It is tedious to prefix \ to include every special characters.  
> - Verbatim string in C# allows a special characters and line brakes.   
> - Verbatim string can be created by prefixing @ symbol before double quotes.   
> ```c#    
> string str = @"xyzdef\rabc";
> string path = @"\\mypc\shared\project";
> string email = @"test@test.com";  
> ```   
> The @ symbol can also be used to declare a multi-line string:   
> ```c#     
> string str1 = "this is a \n" + 
>       "multi line \n" + 
>       "string";
> 
> // Verbatim string
> string str2 = @"this is a 
>       multi line 
>       string";     
> ```   
> Please note that you cannot use a backslash to allow " in a varbatim string. If you wish to include @, then use double double-quotes "" to include " in a verbatim string.    
> ```c#    
>  string text = "This is a \"string\" in C#."; // valid
>  string text = @"This is a "string." in C#."; // error
>  string text = @"This is a \"string\" in C#."; // error
>  string text = @"This is a ""string"" in C#."; // valid   
> ```   
> - Each time you concatenate strings, .NET CLR will create a new memory location for the concatenated string.    
> - So, it is recommended to use StringBuilder instead of string if you concatenate more than five strings. (know more about it in the following sections)    
> 
> **String Interpolation:**   
> - C# 6 includes a special character $ to identify an interpolated string.  
> - An interpolated string is a mixture of static string and string variable where string variables should be in {} brackets.   
> ```c#   
> string firstName = "James";
> string lastName = "Bond";
> string code = "007";
> 
> string fullName = $"Mr. {firstName} {lastName}, Code: {code}";   
> ```     
> 


#### Working with Date and Time in C#
> - The default and the lowest value of a DateTime object is January 1, 0001 00:00:00 (midnight).   
> - The maximum value can be December 31, 9999 11:59:59 P.M.   
> ```c#    
> //assigns year, month, day, hour, min, seconds, UTC timezone
> DateTime dt4 = new DateTime(2015, 12, 31, 5, 10, 20, DateTimeKind.Utc);  
> ```      
> - Setting any other value out of these ranges will result in a run-time exception.   
> 
> **Ticks:**   
> - Ticks is a date and time expressed in the number of 100-nanosecond intervals that have elapsed since January 1, 0001, at 00:00:00.000 in the Gregorian calendar.    
> ```c#    
> DateTime dt = new DateTime(636370000000000000); 
> Console.WriteLine(DateTime.MinValue.Ticks);  //min value of ticks => 3155378975999999999   
> Console.WriteLine(DateTime.MaxValue.Ticks); // max value of ticks => 0    
> ```    
> 
> **DateTime Static Fields:**   
> _The DateTime struct includes static fields, properties, and methods_:    
> ```c#    
> DateTime currentDateTime = DateTime.Now;  //returns current date and time
> DateTime todaysDate = DateTime.Today; // returns today's date
> DateTime currentDateTimeUTC = DateTime.UtcNow;// returns current UTC date and time
> 
> DateTime maxDateTimeValue = DateTime.MaxValue; // returns max value of DateTime
> DateTime minDateTimeValue = DateTime.MinValue; // returns min value of DateTime  
> ```   
> 
> **TimeSpan:**   
> _TimeSpan is a struct that is used to represent time in days, hour, minutes, seconds, and milliseconds._       
> ```c#     
> DateTime dt = new DateTime(2015, 12, 31);
>          
> TimeSpan ts = new TimeSpan(25,20,55);
>  
> DateTime newDate = dt.Add(ts);
> 
> Console.WriteLine(newDate);//1/1/2016 1:20:55 AM 
> ```    
> - Subtraction of two dates results in TimeSpan:   
> ```c#    
> DateTime dt1 = new DateTime(2015, 12, 31); 
> DateTime dt2 = new DateTime(2016, 2, 2);
> TimeSpan result = dt2.Subtract(dt1);//33.00:00:00  
> ```   
> 
> **Operators:**   
> The DateTime struct overloads +, -, ==, !=, >, <, <=, >= operators to ease out addition, subtraction, and comparison of dates:   
> ```c#   
>  DateTime dt1 = new DateTime(2015, 12, 20);
>  DateTime dt2 = new DateTime(2016, 12, 31, 5, 10, 20); 
>  TimeSpan time = new TimeSpan(10, 5, 25, 50);
>  
>  Console.WriteLine(dt2 + time); // 1/10/2017 10:36:10 AM
>  Console.WriteLine(dt2 - dt1); //377.05:10:20
>  Console.WriteLine(dt1 == dt2); //False
>  Console.WriteLine(dt1 != dt2); //True
>  Console.WriteLine(dt1 > dt2); //False
>  Console.WriteLine(dt1 < dt2); //True
>  Console.WriteLine(dt1 >= dt2); //False
>  Console.WriteLine(dt1 <= dt2);//True  
> ```   
> **Convert String to DateTime:**   
> - A valid date and time string can be converted to a DateTime object using Parse(), ParseExact(), TryParse() and TryParseExact() methods.   
> - The Parse() and ParseExact() methods will throw an exception if the specified string is not a valid representation of a date and time.   
> - So, it's recommended to use TryParse() or TryParseExact() method because they return false if a string is not valid.      
> ```c#    
> var str = "5/12/2020";
> DateTime dt;
>             
> var isValidDate = DateTime.TryParse(str, out dt);
> 
> if(isValidDate)
>   Console.WriteLine(dt);
> else
>   Console.WriteLine($"{str} is not a valid date string");   
> ```  
>     


#### Struct type in C#   
> - In C#, **_struct_** is the value type data type that represents data structures.    
> - It can contain a parameterized constructor, static constructor, constants, fields, methods, properties, indexers, operators, events, and nested types.   
> - struct can be used to hold small data values that do not require inheritance, e.g. coordinate points, key-value pairs, and complex data structure.   
> **Structure Declaration:**   
> - A structure is declared using struct keyword.   
> - The default modifier is **internal** for the struct and its members.   
> ```c#   
> struct Coordinate
> {
>   public int x;
>   public int y;
> }  
> ```   
> - A struct object can be created with or without the new operator, same as primitive type variables.    
> ```c#    
> struct Coordinate
> {
>   public int x;
>   public int y;
> }
> 
> Coordinate point = new Coordinate();
> Console.WriteLine(point.x); //output: 0  
> Console.WriteLine(point.y); //output: 0    
> ```   
> - Above, an object of the Coordinate structure is created using the new keyword. It calls the default parameterless constructor of the struct, which initializes all the members to their default value of the specified data type.   
> - If you declare a variable of struct type without using new keyword, it does not call any constructor, so all the members remain unassigned. Therefore, you must assign values to each member before accessing them, otherwise, it will give a compile-time error:      
> ```c#   
> struct Coordinate
> {
>   public int x;
>   public int y;
> }
> 
> Coordinate point;
> Console.Write(point.x); // Compile time error  
> 
> point.x = 10;
> point.y = 20;
> Console.Write(point.x); //output: 10  
> Console.Write(point.y); //output: 20     
> ```    
> 
> **Constructors in Structure:**   
> - A struct cannot contain a parameterless constructor.   
> - It can only contain parameterized constructors or a static constructor.        
> ```c#    
> struct Coordinate
> {
>   public int x;
>   public int y;
> 
>   public Coordinate(int x, int y)
>   {
>       this.x = x;
>       this.y = y;
>   }
> }
> 
> Coordinate point = new Coordinate(10, 20);
> 
> Console.WriteLine(point.x); //output: 10  
> Console.WriteLine(point.y); //output: 20   
> ```   
> **Note:**  _You must include all the members of the struct in the parameterized constructor and assign parameters to members; otherwise C# compiler will give a compile-time error if any member remains unassigned._    
> 
> **Methods and Properties in Structure:**   
> - A struct can contain properties, auto-implemented properties, methods, etc., same as classes.   
> ```c#    
> struct Coordinate
> {
>   public int x { get; set; }
>   public int y { get; set; }
> 
>   public void SetOrigin()
>   {
>       this.x = 0;
>       this.y = 0;
>   }
> }
> 
> Coordinate point = Coordinate();
> point.SetOrigin();
> 
> Console.WriteLine(point.x); //output: 0  
> Console.WriteLine(point.y); //output: 0    
> ```   
> 
> **Events in Structure:**   
> A struct can contain events to notify subscribers about some action:    
> ```c#   
> struct Coordinate
> {
>   private int _x, _y;
> 
>   public int x 
>   {
>       get{
>           return _x;
>       }
> 
>       set{
>           _x = value;
>           CoordinatesChanged(_x);
>       }
>   }
> 
>   public int y
>   {
>       get{
>           return _y;
>       }
> 
>       set{
>           _y = value;
>           CoordinatesChanged(_y);
>       }
>   }
> 
>   public event Action< int> CoordinatesChanged;
> }  
> ```   
> - The above structure contains CoordinatesChanged event, which will be raised when x or y coordinate changes.   
> The following example demonstrates the handling of the CoordinatesChanged event:_
>     
> ```c#    
> class Program
> {
>   static void Main(string[] args)
>   {
> 
>       Coordinate point = new Coordinate();
>       
>       point.CoordinatesChanged += StructEventHandler;
>       point.x = 10;
>       point.y = 20;
>   }
> 
>   static void StructEventHandler(int point)
>   {
>       Console.WriteLine("Coordinate changed to {0}", point);
>   }
> }  
> ```   
> - struct is a value type, so it is faster than a class object.   
> - Generally, structs are good for game programming.   
> - However, it is easier to transfer a class object than a struct.   
> - So do not use struct when you are passing data across the wire or to other classes.    
> - struct members cannot be specified as abstract, sealed, virtual, or protected.   
>               


#### Enum type in C#  
> - Enumeration type (enum) is used to assign constant names to a group of numeric integer values.    
> - It makes constant values more readable, for example, WeekDays.Monday is more readable then number 0 when referring to the day in a week.   
> **Enum Values:**   
> - If values are not assigned to enum members, then the compiler will assign integer values to each member starting with zero by default:   
> ```c#    
> enum WeekDays
> {
>   Monday,     // 0
>   Tuesday,    // 1
>   Wednesday,  // 2
>   Thursday,   // 3
>   Friday,     // 4
>   Saturday,   // 5
>   Sunday      // 6
> }  
> ```   
> - You can assign different values to enum member.   
> - A change in the default value of an enum member will automatically assign incremental values to the other members sequentially:    
> ```c#    
> enum Categories
> {
>   Electronics,    // 0
>   Food,           // 1
>   Automotive = 6, // 6
>   Arts,           // 7
>   BeautyCare,     // 8
>   Fashion         // 9
> }  
> ```   
> - The enum can be of any numeric data type such as byte, sbyte, short, ushort, int, uint, long, or ulong.   
> - However, an enum cannot be a string type.  
> - Specify the type after enum name as : type:    
> ```c#    
> enum Categories: byte
> {
>   Electronics = 1,  
>   Food = 5, 
>   Automotive = 6, 
>   Arts = 10, 
>   BeautyCare = 11, 
>   Fashion = 15
> }  
> ```    
>  
> **Access an Enum:**   
> An enum can be accessed using the dot syntax: enum.member:    
> enum WeekDays
> {
>   Monday, 
>   Tuesday,
>   Wednesday,
>   Thursday, 
>   Friday, 
>   Saturday,
>   Sunday 
> }
> 
> Console.WriteLine(WeekDays.Monday); // Monday
> Console.WriteLine(WeekDays.Tuesday); // Tuesday       
> Console.WriteLine(WeekDays.Wednesday); // Wednesday       
> Console.WriteLine(WeekDays.Thursday); // Thursday       
> Console.WriteLine(WeekDays.Friday); // Friday       
> Console.WriteLine(WeekDays.Saturday); // Saturday       
> Console.WriteLine(WeekDays.Sunday); // Sunday             
> 
> **Conversion:**   
> Explicit casting is required to convert from an enum type to its underlying integral type:    
> ```c#    
> enum WeekDays
> {
>   Monday, 
>   Tuesday,
>   Wednesday,
>   Thursday, 
>   Friday, 
>   Saturday,
>   Sunday 
> }
> 
> Console.WriteLine(WeekDays.Friday); //output: Friday 
> int day = (int) WeekDays.Friday; // enum to int conversion
> Console.WriteLine(day); //output: 4 
> 		
> var wd = (WeekDays) 5; // int to enum conversion
> Console.WriteLine(wd);//output: Saturday   
> ```   
> - **Note:**  enum is an abstract class.    
>           

#### StringBuilder over String in C#   
> **Problem:**  
> - In C#, the string type is immutable.  
> - It means a string cannot be changed once created.    
> - For example, a new string, "Hello World!" will occupy a memory space on the heap.   
> - Now, by changing the initial string "Hello World!" to "Hello World! from Tutorials Teacher" will create a new string object on the memory heap instead of modifying an original string at the same memory address.      
> - This behavior would hinder the performance if the original string changed multiple times by replacing, appending, removing, or inserting new strings in the original string.   
> ![image](https://user-images.githubusercontent.com/58625165/215895414-23a17fbc-3658-4e4d-933d-30fe925750cc.png)   
> 
> **Solution:**   
> - To solve this problem, C# introduced the StringBuilder in the System.Text namespace.   
> - The StringBuilder doesn't create a new object in the memory but dynamically expands memory to accommodate the modified string.   
> ![image](https://user-images.githubusercontent.com/58625165/215895607-813ddfba-16d5-4f44-a4dd-3b0b243a2cf7.png)    
> 
> **Creating a StringBuilder Object:**   
> ```c#    
> using System.Text; // include at the top
>           
> StringBuilder sb = new StringBuilder(); //string will be appended later
> //or
> StringBuilder sb = new StringBuilder("Hello World!");  
> ```    
> - Optionally, you can also specify the maximum capacity of the StringBuilder object using overloaded constructors, as shown below.    
> ```c#    
> StringBuilder sb = new StringBuilder(50); //string will be appended later
> //or
> StringBuilder sb = new StringBuilder("Hello World!", 50);  
> ```   
> - Above, C# allocates a maximum of 50 spaces sequentially on the memory heap.      
> - This capacity will automatically be doubled once it reaches the specified capacity.   
> - You can also use the capacity or length property to set or retrieve the StringBuilder object's capacity.   
> - You can iterate the using for loop to get or set a character at the specified index:    
> ```c#    
> StringBuilder sb = new StringBuilder("Hello World!");
> 
> for(int i = 0; i < sb.Length; i++)
>   Console.Write(sb[i]); // output: Hello World!  
> ```   
> 
> **Retrieve String from StringBuilder:**   
> - The StringBuilder is not the string.  
> - Use the ToString() method to retrieve a string from the StringBuilder object:       
> ```c#    
>  StringBuilder sb = new StringBuilder("Hello World!");
>  
>  var greet = sb.ToString(); //returns "Hello World!"  
> ```   
> 
> **Add/Append String to StringBuilder:**   
> - Use the Append() method to append a string at the end of the current StringBuilder object.   
> - If a StringBuilder does not contain any string yet, it will add it.   
> - The AppendLine() method append a string with the newline character at the end.   
> ```c#    
>  StringBuilder sb = new StringBuilder();
>  sb.Append("Hello ");
>  sb.AppendLine("World!");
>  sb.AppendLine("Hello C#");
>  Console.WriteLine(sb);   
> ```              
> 
> **Append Formated String to StringBuilder:**    
> - Use the AppendFormat() method to format an input string into the specified format and append it:   
> ```c#   
> StringBuilder sbAmout = new StringBuilder("Your total amount is ");
> sbAmout.AppendFormat("{0:C} ", 25);
> 
> Console.WriteLine(sbAmout);//output: Your total amount is $ 25.00    
> ```      
> 
> **Insert String into StringBuilder:**    
> - Use the Insert() method inserts a string at the specified index in the StringBuilder object:   
> ```c#    
> StringBuilder sb = new StringBuilder("Hello World!");
> sb.Insert(5," C#"); 
> 
> Console.WriteLine(sb); //output: Hello C# World!  
> ```   
> 
> **Remove String in StringBuilder:**   
> - Use the Remove() method to remove a string from the specified index and up to the specified length:    
> ```c#    
> StringBuilder sb = new StringBuilder("Hello World!",50);
> sb.Remove(6, 7);
> 
> Console.WriteLine(sb); //output: Hello   
> ```   
> 
> **Replace String in StringBuilder:**   
> - Use the Replace() method to replace all the specified string occurrences with the specified replacement string:   
> ```c#    
> StringBuilder sb = new StringBuilder("Hello World!");
> sb.Replace("World", "C#");
> 
> Console.WriteLine(sb);//output: Hello C#!  
> ```   
> - StringBuilder is mutable.   
> - StringBuilder performs faster than string when appending multiple string values.   
> - Use StringBuilder when you need to append more than three or four strings.   
>   


#### Anonymous types in C#  
> _In C#, an anonymous type is a type (class) without any name that can contain public read-only properties only._   
> - It cannot contain other members, such as fields, methods, events, etc.   
> - You create an anonymous type using the new operator with an object initializer syntax.   
> ```c#    
> var student = new { Id = 1, FirstName = "James", LastName = "Bond" };    
> ```     
> - The properties of anonymous types are read-only and cannot be initialized with a null, anonymous function, or a pointer type:   
> ```c#    
> var student = new { Id = 1, FirstName = "James", LastName = "Bond" };
> Console.WriteLine(student.Id); //output: 1
> Console.WriteLine(student.FirstName); //output: James
> Console.WriteLine(student.LastName); //output: Bond
> 
> student.Id = 2;//Error: cannot chage value
> student.FirstName = "Steve";//Error: cannot chage value   
> ```     
> - An anonymous type's property can include another anonymous type:   
> ```c#     
> var students = new[] {
>           new { Id = 1, FirstName = "James", LastName = "Bond" },
>           new { Id = 2, FirstName = "Steve", LastName = "Jobs" },
>           new { Id = 3, FirstName = "Bill", LastName = "Gates" }
>   };
> 
> ```     
> 
> - Internally, all the anonymous types are directly derived from the System.Object class.   
> - Example: Internal Name of an Anonymous Type:   
> ```c#    
>  static void Main(string[] args)
>  {
>   var student = new { Id = 1, FirstName = "James", LastName = "Bond" };
>   Console.WriteLine(student.GetType().ToString()); // Use GetType() method to see the name.   
>  }    
> ```     
>   


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
