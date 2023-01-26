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


##### 6. Filters in ASP.NET MVC
##### 7. ActionFilter Attributes
##### 8. What is Bundling in ASP.NET MVC?   
##### 9. ScriptBundle  
##### 10. StyleBundle  
##### 11. Area in ASP.NET MVC  
##### 12. ASP.NET MVC Learning Resources   

### Create HTML Controls in MVC
##### 1. What is HTML Helper?  
##### 2. Create TextBox  
##### 3. Create TextArea  
##### 4. Create CheckBox  
##### 5. Create Radio Button   
##### 6. Create DropDownList  
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
##### 6. Razor View Syntax  
##### 7. Integrate Model, View & Controller  
##### 8. Binding Model to View & Controller  
##### 9. Create View To Edit Data  
##### 10. What is Layout View?   
##### 11. Create Layout View in ASP.NET MVC  
##### 12. What is Partial View?  
##### 13. What is a ViewBag?  
##### 14. What is ViewData?  
##### 15. What is TempData?  
##### 16. Implement Validations in ASP.NET MVC Form  
##### 17. Use Validationsummary to Display Error Summary  
##### 18. Exception Handling in ASP.NET MVC  


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
