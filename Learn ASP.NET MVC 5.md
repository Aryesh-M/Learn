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
##### 2. Action Methods in Controller  
##### 3. Action Selector Attributes  
##### 4. HttpGet, HttpPost, HttpPut  
##### 5. Model in MVC  
##### 6. View in MVC  
##### 7. Razor View Syntax  
##### 8. Integrate Model, View & Controller  
##### 9. Binding Model to View & Controller  
##### 10. Create View To Edit Data  
##### 11. What is Layout View?   
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
