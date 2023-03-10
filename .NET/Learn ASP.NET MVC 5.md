### Basics    
##### 1. Overview of MVC Architecture 
> 1. MVC stands for Model, View and Controller.
> 2. Model represents the data
> 3. View is the User Interface.
> 4. Controller is the request handler.   


##### 2. ASP.NET MVC Framework Version History   
> Microsoft had introduced ASP.NET MVC in .NET 3.5.   
> Microsoft made ASP.NET MVC framework open-source in April 2009.

##### 3. Create First MVC App   
> press F5 to run the project in debug mode  
> Ctrl + F5 to run the project without debugging   
> MVC 5 project includes JavaScript and CSS files of bootstrap 3.0 by default   


##### 4. MVC Folder Structure   
> ![image](https://user-images.githubusercontent.com/58625165/214932488-6b272848-7b02-4a32-8f5b-2ad71357c6bb.png)   
> **1. App_Data:**   The App_Data folder can contain application data files like LocalDB, .mdf files, XML files, and other data related files. IIS will never serve files from App_Data folder.   
> **2. App_Start:**   The App_Start folder can contain class files that will be executed when the application starts. Typically, these would be config files like AuthConfig.cs, BundleConfig.cs, FilterConfig.cs, RouteConfig.cs etc. MVC 5 includes BundleConfig.cs, FilterConfig.cs and RouteConfig.cs by default. We will see the significance of these files later.   
> **3. Content:**   The Content folder contains static files like CSS files, images, and icons files. MVC 5 application includes bootstrap.css, bootstrap.min.css, and Site.css by default.   
> **4. Controllers:**    A Controller handles users' request and returns a response. MVC requires the name of all controller files to end with "Controller". You will learn about the controller in the next section.   
> **5. fonts:**  The Fonts folder contains custom font files for your application.   
> **6. Models:**  The Models folder contains model class files. Typically model class includes public properties, which will be used by the application to hold and manipulate application data.   
> **7. Scripts:**  The Scripts folder contains JavaScript or VBScript files for the application. MVC 5 includes javascript files for bootstrap, jquery 1.10, and modernizer by default.   
> **8. Views:**  Typically view file is a .cshtml file where you write HTML and C# or VB.NET code. The Views folder includes a separate folder for each controller. For example, all the .cshtml files, which will be rendered by HomeController will be in View > Home folder. The Shared folder under the View folder contains all the views shared among different controllers e.g., layout files.    
> **9. Global.asax:**  Global.asax file allows you to write code that runs in response to application-level events, such as Application_BeginRequest, application_start, application_error, session_start, session_end, etc.   
> **10. Packages.config:**  Packages.config file is managed by NuGet to track what packages and versions you have installed in the application.   
> **11. Web.config:**    Web.config file contains application-level configurations.   

##### 5. Routing in ASP.NET MVC   
> In the ASP.NET Web Forms application, every URL must match with a specific .aspx file.   
> e.g., a URL http://domain/studentsinfo.aspx must match with the file studentsinfo.aspx that contains code and markup for rendering a response to the browser.   
> _ASP.NET introduced Routing to eliminate the needs of mapping each URL with a physical file._   
> Route defines the URL pattern and handler information. All the configured routes of an application stored in RouteTable and will be used by the Routing engine to determine appropriate handler class or file for an incoming request.   
> The following figure illustrates the Routing process.   
> ![image](https://user-images.githubusercontent.com/58625165/214934605-5e0369ad-968f-49f0-b55c-2e268a4f8e33.png)   

> **Configure a Route:**     
> he following figure illustrates how to configure a route in the RouteConfig class:       
> ![image](https://user-images.githubusercontent.com/58625165/214935031-76eb27f4-aa60-43df-8e0c-0ea7d2b70a7f.png)    

> **URL Pattern:**    
> ![image](https://user-images.githubusercontent.com/58625165/214935544-dab418ef-74e3-4d5e-b100-d2028353608f.png)    

> **Multiple Routes:**   
> You can also configure a custom route using the MapRoute extension method.    
> You need to provide at least two parameters in MapRoute, route name, and URL pattern. The Defaults parameter is optional.    
> ```c#      
>     public class RouteConfig
> {
>    public static void RegisterRoutes(RouteCollection routes)
>    {
>        routes.IgnoreRoute("{resource}.axd/{* pathInfo}");
>
>        routes.MapRoute(
>            name: "Student",
>            url: "students/{id}",
>            defaults: new { controller = "Student", action = "Index"}
>        );
>
>        routes.MapRoute(
>            name: "Default",
>            url: "{controller}/{action}/{id}",
>            defaults: new { controller = "Home", action = "Index", id = UrlParameter.Optional }
>        );
>    }
> } 
> ```   
> The following shows how different URLs will be mapped to the Student route with Student(as a Controller), Index(as an Action), and 123(as an Id):      
> http://localhost/student/123	  
> http://localhost/student/index/123	  
> http://localhost/student?Id=123	   

> **Route Constraints:**   
> You can also apply restrictions on the value of the parameter by configuring route constraints. For example, the following route applies a limitation on the id parameter that the id's value must be numeric:    
> ```c#    
> routes.MapRoute(
>  name: "Student",
>  url: "student/{id}/{name}/{standardId}",
>  defaults: new { controller = "Student", action = "Index", id = UrlParameter.Optional, name = UrlParameter.Optional, standardId = UrlParameter.Optional },
>  constraints: new { id = @"\d+" }
> );   
> ```     
> _So if you give non-numeric value for id parameter, then that request will be handled by another route or, if there are no matching routes, then "The resource could not be found" error will be thrown._    

> **Register Routes:**   
> Now, after configuring all the routes in the RouteConfig class, you need to register it in the Application_Start() event in the Global.asax so that it includes all your routes into the RouteTable:    
> ```c#     
>   public class MvcApplication : System.Web.HttpApplication
> {
>   protected void Application_Start()
>   {
>       RouteConfig.RegisterRoutes(RouteTable.Routes);
>   }
> }
> ```   
> The following figure illustrate Route registration process:    
> ![image](https://user-images.githubusercontent.com/58625165/214937926-0efcee94-80a8-480c-a7e6-14ffe5c4b9c4.png)   
> So, Route must be registered in Application_Start event in Global.ascx.cs file.   
> 

##### 6. Razor Syntax     
> **Inline expression:**   @Variable_Name   
> 
> **Multi-statement Code block:**  @{ ... }   
> 
> **Display Text from Code Block:**   Use @: or < text>/< text> to display texts within code block:    
> ```c#   
>  @{
>   var date = DateTime.Now.ToShortDateString();
>   string message = "Hello World!";
>   @:Today's date is: @date <br />
>   @message                               
> }
> ```   
> ![image](https://user-images.githubusercontent.com/58625165/214968951-79c2e439-4ab8-44df-9ae1-baa0688d73fe.png)    
> Display text using < text> within a code block, as shown below:   
> ```c#    
>  @{
>   var date = DateTime.Now.ToShortDateString();
>   string message = "Hello World!";
>   <text>Today's date is:</text> @date <br />
>   @message                               
> }
> ```   
> ![image](https://user-images.githubusercontent.com/58625165/214969080-5a4af4f9-a645-4f7f-b45d-9c7273c94a2b.png)   
> 
> **if-else condition:**   
> Write if-else condition starting with @ symbol. The if-else code block must be enclosed in braces { }, even for a single statement:   
> ```c#    
>  @if(DateTime.IsLeapYear(DateTime.Now.Year) )
> {
>   @DateTime.Now.Year @:is a leap year.
> }
> else { 
>   @DateTime.Now.Year @:is not a leap year.
> }
> ```     
> 
> **for loop:**   
> ```c#     
>  @for (int i = 0; i < 5; i++) { 
>   @i.ToString() <br />
> }
> ```    
> 
> **Model:**   
> Use @model to use model object anywhere in the view:   
> ```c#   
>  @model Student
> 
> <h2>Student Detail:</h2>
> <ul>
>   <li>Student Id: @Model.StudentId</li>
>   <li>Student Name: @Model.StudentName</li>
>   <li>Age: @Model.Age</li>
> </ul>  
> ```   
> 
> **Declare Variables:**   
> Declare a variable in a code block enclosed in brackets and then use those variables inside HTML with @ symbol:    
> ```c#     
>  @{ 
>   string str = "";
>  
>   if(1 > 0)
>   {
>       str = "Hello World!";
>   }
>  }
>  
>  <p>@str</p>
> ```    
> 

 
##### 7. Filters in ASP.NET MVC   


##### 8. ActionFilter Attributes
##### 9. What is Bundling in ASP.NET MVC?   
##### 10. ScriptBundle  
##### 11. StyleBundle  
##### 12. Area in ASP.NET MVC  
##### 13. ASP.NET MVC Learning Resources   

### Create HTML Controls in MVC
##### 1. What is HTML Helper?    
> The difference between calling the HtmlHelper methods and using an HTML tags is that the HtmlHelper method is designed to make it easy to bind to view data or model data  
| Extension Method | Strongly Typed Method | Html Control | 
| ---------------- | --------------------- | ------------ |
| Html.ActionLink() |	NA | <a></a> |
| Html.TextBox() | Html.TextBoxFor() | < input type="textbox"> |
| Html.TextArea() | Html.TextAreaFor( | < input type="textarea"> |
| Html.CheckBox() | Html.CheckBoxFor() | < input type="checkbox"> |
| Html.RadioButton() | Html.RadioButtonFor() | < input type="radio"> |
| Html.DropDownList() | Html.DropDownListFor() | < select> <option> </select> |
| Html.ListBox() | Html.ListBoxFor() | multi-select list box: < select> |
| Html.Hidden() | Html.HiddenFor() | < input type="hidden"> |
| Html.Password() | Html.PasswordFor() | < input type="password"> |
| Html.Display() | Html.DisplayFor() | HTML text: "" |
| Html.Label() | Html.LabelFor() | < label> |
| Html.Editor() | Html.EditorFor() | Generates Html controls based on data type of specified model property e.g. textbox for string property, numeric field for int, double or other numeric type. |  
> 


##### 2. Create TextBox    
> two extension methods: TextBox(), TextBoxFor<TModel, TProperty>()   
> It is recommended to use the generic TextBoxFor<TModel, TProperty>() method, which is less error prons and performs fast.   
> 
> **Html.TextBoxFor():**   
> The TextBoxFor<TModel, TProperty>() is the generic extension method that creates <input type="text"> control.      
> The first type parameter is for the model class, and second type parameter is for the property.   
> ```c#     
>  @model Student
>  
>  @Html.TextBoxFor(m => m.StudentName)  
> ```   
> In the above example, the lambda expression m => m.StudentName specifies the StudentName property to bind with a textbox.   
> It generates an input text element with id and name attributes, as shown below:   
> ![image](https://user-images.githubusercontent.com/58625165/214980798-64626dda-f5d8-4f7d-a8c9-de7aefa85c8f.png)    
> The following example renders a textbox with the class attribute:   
> ```c#   
>  @model Student
>  
>  @Html.TextBoxFor(m => m.StudentName, new { @class = "form-control" })   
> ```   
>  ![image](https://user-images.githubusercontent.com/58625165/214980912-067e5dde-6f01-4524-942f-e92acb84b5fd.png)   
>  
>  **Html.TextBox():**  
>  The TextBox() method is a loosely typed method because the name parameter is a string.  
>  ```c#    
>  @model Student
>  
>  @Html.TextBox("StudentName")     
>  ```   
>  ![image](https://user-images.githubusercontent.com/58625165/214981297-85a928c5-5228-4c6d-9482-aac2e74737f4.png)    
>    
  
    

##### 3. Create TextArea  
> TextArea() and TextAreaFor<TModel, TProperty>()   
> By default, it creates a textarea with rows=2 and cols=20.   
> ```c#   
>  @model Student
>  
>  @Html.TextArea("Description", "This is dummy description.", new { @class = "form-control" })    
> ```   
> HTML Result:  
> ```html   
>  <textarea class="form-control" id="Description" name="Description" rows="2"cols="20">This is dummy description.</textarea>      
> ```        
> 


##### 4. Create CheckBox   
> ```c#    
>  @model Student
>  
>  @Html.CheckBoxFor(m => m.isActive)  
> ```   
> ![image](https://user-images.githubusercontent.com/58625165/215164660-f5ff72bc-6bf7-40bc-b727-5f66305125e4.png)   
> Notice that it has generated an additional hidden field with the same name and value=false.   
> When you submit a form with a checkbox, the value is posted only if a checkbox is checked.    
> So, if you leave the checkbox unchecked, then nothing will be sent to the server.   
> Sometimes, you would want false to be sent to the server.   
> Because, an hidden input has the same name, it will send false to the server if checkbox is unchecked.   
> 
> **Html.CheckBox():**   
> The Html.CheckBox() is a loosely typed method which generates a <input type="checkbox" > with the specified name, isChecked boolean, and HTML attributes.   
> ```c#    
> @Html.CheckBox("isActive", true)     
> ```    
> ![image](https://user-images.githubusercontent.com/58625165/215166627-2c484bd1-0463-440d-85c4-199fe6e90b6b.png)    
>  
   

##### 5. Create Radio Button    
>  **Html.RadioButtonFor():**   
> ```c#   
>  @model Student
>  
>  @Html.RadioButtonFor(m => m.Gender,"Male")
>  @Html.RadioButtonFor(m => m.Gender,"Female")       
> ```     
> ![image](https://user-images.githubusercontent.com/58625165/215166945-87338ea5-b62c-4047-a028-69d80569f7a0.png)    
> 
> **RadioButton():**  
> ```c#    
>  Male:   @Html.RadioButton("Gender","Male")  
>  Female: @Html.RadioButton("Gender","Female")    
> ```   
> ![image](https://user-images.githubusercontent.com/58625165/215167270-d09cf7e3-712e-4cf9-9d12-6a3aa1f21413.png)   
> 


##### 6. Create DropDownList     
> **Html.DropDownListFor():**   
> ```c#    
> @using MyMVCApp.Models
> 
> @model Student
> 
> @Html.DropDownListFor(m => m.StudentGender, 
>             new SelectList(Enum.GetValues(typeof(Gender))), 
>             "Select Gender")  
> ```      
> ![image](https://user-images.githubusercontent.com/58625165/215167513-3073dbc6-7549-424c-9cd2-9fe61d32dd31.png)   
> 

##### 7. Create Hidden field  
##### 8. Create Password field  
##### 9. Create Display field  
##### 10. Create Label  
##### 11. Create Editor field  

### Model, View, & Controller    
##### 1. Controllers in ASP.NET MVC      
> The Controller is a class, derived from the base class System.Web.Mvc.Controller  
> Controller class contains public methods called **Action methods**.    
> **Role:**   Controller and its action method handles incoming browser requests, retrieves necessary model data and returns appropriate responses.   
> **FYI:** _MVC will throw "The resource cannot be found" error when you do not append "Controller" to the controller class name._       
> **Note:**  _Scaffolding is an automatic code generation framework for ASP.NET web applications. Scaffolding reduces the time taken to develop a controller, view, etc. in the MVC framework. You can develop a customized scaffolding template using T4 templates as per your architecture and coding standards._    
> You can create a custom scaffolding template also.    
> 

##### 2. Action Methods in Controller     
> All the public methods of the Controller class are called Action methods. They are like any other normal methods with the following restrictions:    
> 1. Action Method must be public. It cannot be private or protected.  
> 2. Action method cannot be overloaded.    
> 3. Action method cannot be a static method.    
> The following illustrates the Index() action method in the StudentController class:       
> ![image](https://user-images.githubusercontent.com/58625165/214940323-d59fc6d3-ef88-429c-996c-5cfd309188d1.png)   

> **ActionResult:**      
> MVC framework includes various Result classes, which can be returned from an action method.   
> The result classes represent different types of responses, such as HTML, file, string, JSON, javascript, etc.   
> The following table lists all the result classes available in ASP.NET MVC:    
>   
| Result Class  | Description   | Base Controller Method | 
| ------------- | ------------- | ---------------------- |
| ViewResult  |  Represents HTML and markup. | View() |
| EmptyResult  |  Represents No response. |  |  
| ContentResult | Represents string literal. | Content() |
| FileContentResult/ FilePathResult/ FileStreamResult | Represents the content of a file. | File() | 
| JavaScriptResult | Represent a JavaScript script. | JavaScript() |
| JsonResult | Represent JSON that can be used in AJAX. | Json() |
| RedirectResult | Represents a redirection to a new URL. | Redirect() |
| RedirectToRouteResult | Represent another action of same or other controller. | RedirectToRoute() |
| PartialViewResult | Returns HTML from Partial view. | PartialView() |
| HttpUnauthorizedResult | Returns HTTP 403 status. |  |
>
>**Note:**  The ActionResult class is a base class of all the above result classes, so it can be the return type of action method that returns any result listed above.   

> **Action Method Parameters:**   
> Every action methods can have input parameters as normal methods.   
> Action Parameters can be primitive data type or complex type parameters, as shown below.    
> ```c#     
> [HttpPost]
> public ActionResult Edit(Student std)
> {
>   // update student to the database
>   
>   return RedirectToAction("Index");
> }
> 
> [HttpDelete]
> public ActionResult Delete(int id)
> {
>   // delete student from the database whose id matches with specified id
> 
>   return RedirectToAction("Index");
> }
> ```     
> **Note:**  The Action method can include Nullable type parameters.   


##### 3. Action Selector Attributes    
> Action selector is the attribute that can be applied to the action methods.  
> It helps the routing engine to select the correct action method to handle a particular request.  
> MVC 5 includes the following action selector attributes:    
> 1. ActionName   
> 2. NonAction   
> 3. ActionVerbs   

> **1. ActionName:**    
> ```c#     
> public class StudentController : Controller
> {
>   public StudentController()
>   {
>   }
>      
>   [ActionName("Find")]
>   public ActionResult GetById(int id)
>   {
>       // get student from the database 
>       return View();
>   }
> }
> ```   
> Note, above we have applied ActioName("find") attribute to the GetById() action method.   
> So now, the action method name is Find instead of the GetById. So now, it will be invoked on http://localhost/student/find/1 request instead of http://localhost/student/getbyid/1 request.   

> **2. NonAction:**   
> Use the NonAction attribute when you want public method in a controller but do not want to treat it as an action method.  
> In the following example, the Index() method is an action method, but the GetStudent() is not an action method:   
> ```c#    
>     public class StudentController : Controller
> {
>   public string Index()
>   {
>           return "This is Index action method of StudentController";
>   }
>  
>   [NonAction]
>   public Student GetStudent(int id)
>   {
>       return studentList.Where(s => s.StudentId == id).FirstOrDefault();
>   }
> }  
> ```   

> **3. ActionVerbs: HttpGet, HttpPost, HttpPut:**   
> The ActionVerbs selector is to handle different type of Http requests.  
> Includes: HttpGet, HttpPost, HttpPut, HttpDelete, HttpOptions, and HttpPatch      
> You can apply **one or more action verbs** to an action method to handle different HTTP requests.   
> If you don't apply any action verbs to an action method, then it will handle HttpGet request by default.    
> The following table lists the usage of HTTP methods:   
> 
| Http method |	Usage | 
| ----------- | ----- |   
| GET |	To retrieve the information from the server. Parameters will be appended in the query string. |
| POST |	To create a new resource. |
| PUT	| To update an existing resource. |
| HEAD	| Identical to GET except that server do not return the message body. |
| OPTIONS	| It represents a request for information about the communication options supported by the web server. |
| DELETE	| To delete an existing resource. |
| PATCH	| To full or partial update the resource. |
> The following example shows how to handle different types of HTTP requests in the Controller using ActionVerbs:    
> ```c#   
> public class StudentController : Controller
> {
>   public ActionResult Index() // handles GET requests by default
>   {
>       return View();
>   }
> 
>   [HttpPost]
>   public ActionResult PostAction() // handles POST requests by default
>   {
>       return View("Index");
>   }
> 
> 
>   [HttpPut]
>   public ActionResult PutAction() // handles PUT requests by default
>   {
>       return View("Index");
>   }
> 
>   [HttpDelete]
>   public ActionResult DeleteAction() // handles DELETE requests by default
>   {
>       return View("Index");
>   }
> 
>   [HttpHead]
>   public ActionResult HeadAction() // handles HEAD requests by default
>   {
>       return View("Index");
>   }
>      
>   [HttpOptions]
>   public ActionResult OptionsAction() // handles OPTION requests by default
>   {
>       return View("Index");
>   }
>      
>   [HttpPatch]
>   public ActionResult PatchAction() // handles PATCH requests by default
>   {
>       return View("Index");
>   }
> }
> ```   
> You can also apply multiple action verbs using the **AcceptVerbs** attribute, as shown below:    
> ```c#     
>   [AcceptVerbs(HttpVerbs.Post | HttpVerbs.Get)]
> public ActionResult GetAndPostAction()
> {
>   return RedirectToAction("Index");
> }  
> ```   
>       

##### 4. Model in MVC    
> The model classes represents domain-specific data and business logic in the MVC application.    
> It represents the shape of the data as public properties and business logic as methods.   

> **Adding a Model Class:**    
> ```c#    
> public class Student
> {
>   public int StudentId { get; set; }
>   public string StudentName { get; set;  }
>   public int Age { get; set;  }
> }
> ```   
> We have added **public properties** for Id, Name, and Age, as shown above.   
> The model class can be used **in the view to populate the data**, as well as **sending data to the controller**.    
>            

##### 5. View in MVC    
> A controller can have one or more action methods, and each action method can return a different view.  
> In short, a controller can render one or more views. So, for easy maintenance, the MVC framework requires a separate sub-folder for each controller with the same name as a controller, under the Views folder.    
> For example, all the views rendered from the HomeController will resides in the Views > Home folder. In the same way, views for StudentController will resides in Views > Student folder, as shown below.   
> ![image](https://user-images.githubusercontent.com/58625165/214950463-e1688c36-232f-4ad3-be71-9953e5bf1c20.png)    
> **Note:** The **Shared** folder contains views, layout views, and partial views, which will be shared among multiple controllers.   

##### 6. Razor View Syntax   
> **Razor View Engine:**     
> Microsoft introduced the razor view engine to compile a view with a mix of HTML tags and server-side code.   
> The special syntax for razor view maximizes the speed of writing code by minimizing the number of characters and keystrokes required when writing a view.   
> The razor view uses @ character to include the server-side code instead of the traditional <% %> of ASP.   
> ASP.NET MVC supports the following types of razor view files:   
| File extension | Description |
| -------------- | ----------- | 
| .cshtml	| C# Razor view. Supports C# code with html tags. |
| .vbhtml	| Visual Basic Razor view. Supports Visual Basic code with html tags. |
| .aspx	| ASP.Net web form |
| .ascx	| ASP.NET web control |     
> ![image](https://user-images.githubusercontent.com/58625165/214954036-a8dce8c1-10ed-466a-886d-cad430fb7988.png)   
> **Note:** Every view in the ASP.NET MVC is derived from WebViewPage class included in System.Web.Mvc namespace.   
> 


##### 9. Binding Model to View & Controller   
> The model binding refers to converting the HTTP request data (from the query string or form collection) to an action method parameters.   
> These parameters can be of primitive type or complex type.   

 > **Binding to Primitive Type:**   
 > For example, the query string parameters of an HTTP request http://localhost/Student/Edit?id=1&name=John would map to id and name parameters of the following Edit() action method.   
 > ```c#    
 >  public ActionResult Edit(int id, string name)
>  {            
>   // do something here
>           
>   return View();
>  }
 > ```

> **Binding to Complex Type:**    
> ```c#    
> public class Student
> {
>   public int StudentId { get; set; }
>   public string StudentName { get; set; }
>   public int Age { get; set; }
>   public Standard standard { get; set; }
> }
> 
> public class Standard
> {
>   public int StandardId { get; set; }
>   public string StandardName { get; set; }
> }  
> ```   
> Now, you can create an action method which includes the Student type parameter.   
> In the following example, Edit action method (HttpPost) includes Student type parameter:    
> ```c#    
>  [HttpPost]
>  public ActionResult Edit(Student std)
>  {
>   var id = std.StudentId;
>   var name = std.StudentName;
>   var age = std.Age;
>   var standardName = std.standard.StandardName;
>  
>   //update database here..
>  
>   return RedirectToAction("Index");
>  } 
> ```   
> Thus, the MVC framework will automatically map Form collection values to the Student type parameter when the form submits an HTTP POST request to the Edit() action method, as shown below:   
> ![image](https://user-images.githubusercontent.com/58625165/214963149-c7234c61-5a3c-44a2-ac69-28100de73e8c.png)    

> **FormCollection:**   
> You can also include the FormCollection type parameter in the action method instead of a complex type to retrieve all the values from view form fields, as shown below:    
> ![image](https://user-images.githubusercontent.com/58625165/214963367-f9c490e4-b831-4452-af96-3e311ed3bba4.png)    

> **Bind Attribute:**   
> ASP.NET MVC framework also enables you to specify which properties of a model class you want to bind.  
> The [Bind] attribute will let you specify the exact properties of a model should include or exclude in binding.   
> In the following example, the Edit() action method will only bind StudentId and StudentName properties of the Student model class:     
> ```c#    
>  [HttpPost]
>  public ActionResult Edit([Bind(Include = "StudentId, StudentName")] Student std)
>  {
>   var name = std.StudentName;
>             
>   //write code to update student 
>           
>   return RedirectToAction("Index");
>  }         
> ```   
> 
> You can also exclude the properties, as shown below:   
> 
> ```c#    
>  [HttpPost]
> public ActionResult Edit([Bind(Exclude = "Age")] Student std)
> {
>   var name = std.StudentName;
>          
>   //write code to update student 
>           
>   return RedirectToAction("Index");
> } 
> ```   
> Model binding is a two-step process.   
> First, it collects values from the incoming HTTP request.      
> Second, it populates primitive type or a complex type with these values.      
> Value providers are responsible for collecting values from requests, and Model Binders are responsible for populating values.    
> ![image](https://user-images.githubusercontent.com/58625165/214964437-2f99daf2-26cc-4292-81e7-196f7206ccf2.png)    
>      


##### 10. Create View To Edit Data     
> The following figure describes how the edit functionality would work in ASP.NET MVC application:    
> ![image](https://user-images.githubusercontent.com/58625165/214966663-f7722573-15fd-4d37-8087-5e69cb02d488.png)    
> The above figure illustrates the following steps:   
> 1. The user clicks on the Edit link in the student list view, which will send the HttpGET request http://localhost/student/edit/{Id} with corresponding Id parameter in the query string. This request will be handled by the HttpGET action method Edit(). (by default action method handles the HttpGET request if no attribute specified)   
> 2. The HttpGet action method Edit() will fetch student data from the database, based on the supplied Id parameter and render the Edit view with that particular Student data.   
> 3. The user can edit the data and click on the Save button in the Edit view. The Save button will send a HttpPOST request http://localhost/Student/Edit with the Form data collection.   
> 4. The HttpPOST Edit action method in StudentController will finally update the data into the database and render an Index page with the refreshed data using the RedirectToAction method as a fourth step.    
> 


##### 11. What is Layout View?    
> - An application may contain a specific UI portion that remains the same throughout the application, such as header, left navigation bar, right bar, or footer section. 
> - ASP.NET MVC introduced a Layout view which contains these common UI portions so that we don't have to write the same code in every page.
> - 


##### 12. Create Layout View in ASP.NET MVC  
##### 13. What is Partial View?  
##### 14. What is a ViewBag?  
##### 15. What is ViewData?  
##### 16. What is TempData?  
##### 17. Implement Validations in ASP.NET MVC Form  
##### 18. Use Validationsummary to Display Error Summary  
##### 19. Exception Handling in ASP.NET MVC  


### ASP.NET MVC Articles   
##### 1. Redirect from HTTP to HTTPS in ASP.NET
##### 2. Redirect non-www to www domain in ASP.NET   
##### 3. Build e-commerce application on .NET Framework   
##### 4. How to create a custom filter in ASP.NET MVC?  
##### 5. How to use we.config customErrors in ASP.NET MVC?   
##### 6. How to display a custom error page with error code using httpErrors in ASP.NET MVC?  
##### 7. Difference between Html.Partial() and Html.RenderPartial() in ASP.NET MVC  
##### 8. Difference between Html.RenderBody() and Html.RenderSection() in ASP.NET MVC
##### 9. What is RouteData in ASP.NET MVC?  
##### 10. How to set image path in StyleBundle?  
##### 11. How to pre-compile razor view in ASP.NET MVC?  
##### 12. How to enable bundling and minification in ASP.NET MVC?  
##### 13. How to enable client side validation in ASP.NET MVC?  
##### 14. How to display an error message using ValidationSummary in ASP.NET MVC?   
##### 15. How to define a custom action selector in ASP.NET MVC?   
##### 16. How to bind a model to a partial view in ASP.NET MVC?  
##### 17. View in ASP.NET MVC   
