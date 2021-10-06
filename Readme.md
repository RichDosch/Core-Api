# Readme information on the C# Solution/Project

This is a .NET Core 5.0 Solution/Project build using Visual Studio Community 2019

this project will use Docker because Docker provides contain capabilities that make it easier for developers and
publishing to different environments.

this project also uses Swagger as a helper for development only. Swagger will NOT be utilized in a production environment.
however, you can also use Postman to test the API when published to other environments.

## Write a c# restful controller that:

1. Consumes a OwnerModel consisting of:
   a. companyId (Guid), 
   b. ownerId (Guid), 
   c. Owner Name (string), 
   d. owner percentage (double).  
   
2. The controller should:
   a. add the owner to a dictionary of owners.  
   b. should update the owner percentage and name if existing or create a new owner, 
   c. not allow the total owner percentages to exceed 100%. 
   d. NOTE: Did NOT create a method that would update the percentages based on company Id
   
3. the dictionary stores the owners is in a static/singleton class that is called OwnerRespository. 

   --- Singleton using Dependency Injection ---
   defined by the model with an Interface for List<OwnerRespository> and within the startup and then
   the List is injected into the controller

4. Pay careful attention to error conditions and make sure to verify all input.  

   --- Error Conditions ---
   using ProblemDetails or RFC 7807 to log all problem conditions
   also using a filter "HttpGlobalExceptionFilter" that will log all HttpContext errors so that code is not littered
     with try...catch...finally. This is helpful from a security point of view as it logs all errors but reports
	 back to the consumer BadRequests - do not want to provide too much information to a bad actor who is attempting
	 to hack the service

   --- Verify all input ---
   common class checking for injection on strings as well as applying encoding on strings if needed

5. write unit test conditions using xUnit: RichardDosch.Service.Test

   To run the tests perform the following steps:

   1. Right click on the Test project file and from the menu, select either "Run Tests" or "Test Debug"
