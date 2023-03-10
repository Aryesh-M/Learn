#### Controllers   
> ![image](https://user-images.githubusercontent.com/58625165/214377336-fa3c689d-818f-45f7-89e4-680451c27a40.png)    
> **So, how are the URL's mapped to Controller Action Methods?**    
> _The answert is ASP.NET Routing. Notice that in Global.asax we have RegisterRoutes()._   
> ![image](https://user-images.githubusercontent.com/58625165/214377838-f03e4e49-f9ca-4ba2-b535-940a33516004.png)    
> For Example, http://localhost/MVCDemo/home/index/10?name=Pragim   
> ASP.NET MVC will automatically pass any query string or from post parameters named "name" to "index" action method when it is invoked.   
> ```c#     
>   public string Index(string id, string name)    
>   {      
>         return "The value of Id= " + id + " and Name = " + name;    
>   }       
> ```    
> ```c#      
>   public string Index(string id)    
>   {      
>         return "The value of Id= " + id + " and Name = " + Request.QueryString["name"];    
>   }       
> ```   

#### Views  
> **ViewBag & ViewData** is a mechanism to pass data from controller to view    
> **Note:**  To pass data from controller to a view, it's always a good practice to use strongly typed view models   
> We use **"@"** symbol to switch between **html and C# code**     
> ```csharp    
>       public ActionResult Index(string id, string name)   
>       {      
>         ViewBag.Countries = new List< string >()    
>         {    
>           "India",    
>           "US",    
>           "UK",      
>           "Canada"              
>         }       
>       };    
>      return View();     
> ```      
>```csharp    
>      @{     
>           ViewBag.Title = "Countries List";     
>      }         
>      < h2>Countries List</h2>    
>      < ul>  
>         @foreach (string strCountry in ViewBag.Countries)   
>         {   
>             < li>@strCountry </li>
>         }    
>      </ul>  
>```  


#### ViewData and ViewBag      
![image](https://user-images.githubusercontent.com/58625165/214386118-e7469d2c-f5ce-4fc6-980b-7a5f56a96dc6.png)     
> Both **ViewData** and **ViewBag** are used to pass data from a **controller** to a **view**. ViewData is a dictionary of objects that are stored and retrived using strings as keys.    
> ![image](https://user-images.githubusercontent.com/58625165/214386349-db8adf18-b0d8-4f09-a8db-3bf66f82e6af.png)    
> ![image](https://user-images.githubusercontent.com/58625165/214386372-025310e3-8e3e-40c7-a41f-a1cbaee4700e.png)    
> **ViewBag** uses the dynamic feature that was introduced into C# 4. It allows an object to have properties dynamically added to it.    
> 
> **Both ViewData & ViewBag does not provide compile time error checking.** For example, if you miss-spell keys or property names, you wouldn't get any compile time error. You get to know about the error only at runtime. Internally ViewBag properties are stored as name/value pairs in the ViewData dictionary.    
> 
> To pass data from controller to a view, **It's always a good practice to use strongly typed view models** over ViewBag & ViewData. Strongly typed view models provide compile time error checking.   
> 


#### Models   
![image](https://user-images.githubusercontent.com/58625165/214391018-df9a3016-a4e8-4021-944c-a70031d63fde.png)   
> **We want to retrieve an employee information from tblEmployee** table and display it as shown below:    
> ![image](https://user-images.githubusercontent.com/58625165/214391141-c08bc6c8-d8ec-4f27-a096-315f08627f63.png)     
> The controller responds to URL request, gets data from a model and hands it over to the view. The view then renders the data. Model can be entities or business objects.    
> 


#### Data access in MVC using entity framework      
> **The controller responds to URL request,** gets data from a model and hands it over to the view. The view then renders the data. Model can be entities or business objects.   
> We will focus on **retrieving data from a database table tblEmployee using entity framework**. In a later video, we will discuss using business objects as our model.  
> **Step 1:**  Install entity framework using nuget package manager   
> **Step 2:**  Add EmployeeContext.cs class file to the Models folder   
> **Step 3:**  Add a connection string, to the web.config file, in the root directory   
> **Step 4:**  Map "Employee" model class to the database table, tblEmployee using "Table" attribute   
> **Step 5:**  Make the required changes to "Details()" action method in "EmployeeController"    
> ```csharp    
>         public ActionResult Details(int id)    
>         {    
>             EmployeeContext employeeContext = new EmployeeContext();    
>             Employee employee = employeeContext.Employees.Single(x=>x.EmployeeId == id);   
>             return View(employee);   
>         }        
> ```    
> **Step 6:**  Paste the following code in **Application_Start()** function, in **Global.asax** file. Existing databases do not need, database initializer so it can be turned off.   
> ```csharp   
>       Database.SetInitializer<MvcApplication1.Models.EmployeeContext>(null);      
> ```       
>


#### Generate hyperlinks using actionlink HTML helper    
> ```c#    
>     public ActionResult Index()   
>     {   
>         EmployeeContext employeeContext = new EmployeeContext();   
>         List< Employee> employees = employeeContext.Employees.ToList();  
>         return View(employees);   
>     }       
> ```


#### Working with multiple tables in MVC     
#### Using business objects as model in MVC     
#### Creating a view to insert data 
#### FormCollection     
#### Mapping ASP.NET request data to controller action simple parameter types    
#### Updatemodel function  
#### Difference between updatemodel and tryupdatemodel    
#### Editing a model    
#### Updating a model  
#### Unintendent updates    
#### Preventing unintendent updates    
#### Including and Excluding properties from model binding using bind attribute  
#### Including and Excluding properties from model binding using interfaces    
#### Why deleting database records using get request is bad    
#### Deleting database records using post request in MVC  
#### Insert update delete in MVC using entity framework     
#### Customizing the autogenerated index view     
#### Customizing the autogenerated create view
#### Customizing the autogenerated edit view   
#### Using data transfer object as the model in MVC   
#### View engines in ASP.NET MVC  
#### Using custom view engines with ASP.NET MVC    
#### How does a controller find a view in MVC    
#### HTML helpers in MVC   
#### Generating a dropdownlist control in MVC using HTML helpers      
#### How to set an item selected when an ASP.NET MVC dropdownlist is loaded    
#### Difference between HTML TextBox and HTML TextBoxFor    
#### Generating a radiobuttonlist control in MVC using HTML helpers     
#### CheckBoxList in ASP.NET MVC     
#### ListBox in ASP.NET MVC  
#### Using displayname, displayformat, scaffoldcolumn attributes in ASP.NET MVC     
#### Using datatype and datacolumn attribute     
#### Opening a page in new browser window in ASP.NET MVC   
#### HiddenInput and readonly attributes in MVC    
#### Display and edit templated helpers in ASP.NET MVC    
#### Customize display and edit templates in ASP.NET MVC   
#### Accessing model metadata from custom templated helpers     
#### Display images    
#### Custom HTML helpers 
#### HTML encoding     
#### Detect errors in views at compile time     
#### Advantages of using strongly typed views   
#### Partial views    
#### Difference between HTML.partial and HTML.renderpartial     
#### T4 templates in ASP.NET MVC  
#### What is cross site scripting attack    
#### How to prevent cross site scripting attack     
#### Razor views   
#### Layout view     
#### ViewStart in ASP.NET MVC        
#### Named section in layout files in MVC   
#### Implementing search functionality in ASP.NET MVC     
#### Implement paging in ASP.NET MVC     
#### Implement sorting in ASP.NET MVC   
#### Deleting multiple rows in MVC    
#### Check uncheck all checkboxes with another single checkbox using jquery     
#### Action selector in MVC   
#### What is the use of NonAction attribute in MVC     
#### Action files in MVC     
#### Authorize and AllowAnonymous action filters in MVC   
#### childactiononly attribute in MVC     
#### HandleError attribute in MVC     
#### OutputCache attribute in MVC  
#### CacheProfile in MVC     
#### RequireHttps attribute in MVC    
#### ValidateInput attribute in MVC    
#### Custom action filters in ASP.NET MVC     
#### Different types of ActionResult in ASP.NET MVC     
#### Areas in ASP.NET MVC   
#### StringLength attribute in ASP.NET MVC     
#### Range attribute in ASP.NET MVC     
#### Creating custom validation attribute in ASP.NET MVC   
#### RegularExpression attribute in ASP.NET MVC       
#### Compare attribute in ASP.NET MVC     
#### Enable client side validation in ASP.NET MVC   
#### ValidationSummary in ASP.NET MVC     
#### What is Unobstrusive JavaScript    
#### Unostrusive validtion in ASP.NET MVC   
#### Remote validation in ASP.NET MVC     
#### Remote validation in MVC when javascript is disabled    
#### Create a custom remote attribute and override IsValid() method   
#### Ajax with ASP.NET MVC        
#### What is Ajax and why should we use it     
#### Providing visual feedback using LoadingElementId AjaxOption   
#### OnBegin, OnComplete, OnSuccess, and OnFailure properties of AjaxOptions class     
#### LoadingElementDuration property of AjaxOptions class      
#### Implement autocomplete textbox functionality in MVC   
#### What is JavaScript minification     
#### What is CDN Content Delivery Network     
#### What if CDN is down  
