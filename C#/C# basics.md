#### Difference between C# and .NET    
> - C# is a programming language. 
> - .NET is a framework for building applications on Windows (not limited to C#, also can be used with F#, VB.NET etc.,)  
> - .NET consists of 2 components: 
>         1) CLR, 
>         2) Class Library   

#### CLR   
>![image](https://user-images.githubusercontent.com/58625165/215612777-1f271850-5e65-49f4-b2b1-e94513316d28.png)    
> Microsoft took the same approach as Java, and have same mechanism in .NET. It compiles C# code into IL Code (Intermediate Language), which is independent of the machine. Now, the it has to be converted into Native code (which is done by CLR, and the process of converting IL code-> Native code is called Just-in-time compilation).   

#### Architecture of .NET applications  
> ![image](https://user-images.githubusercontent.com/58625165/215613813-effaa0f3-5f8c-4428-ac59-87e015ec7347.png)   
> **Classes** are building blocks of a .NET application.    
> **Namespace:**  - it's a container for related classes for 

#### Variables and Constants  
> ![image](https://user-images.githubusercontent.com/58625165/215615958-775ccd8a-af2b-40c0-928a-5224957db8dc.png)    
> ```c#    
>    float number = 1.2f;   // note here we have added "f" and 
>    decimal number = 1.2m; //  "m" as suffix for float and decimal values.     
> ```   

#### Overflowing  
> ```c#    
>     byte number = 255; //255 is the largest value which can be stored in a byte variable.  
>     number = number + 1;   // 0     
> ```    
> to resolve this we can use "checked":   
> ```c#    
>     checked  
>     {     
>       byte number = 255;   
>       number = number + 1;  
>     }    
> ```   
