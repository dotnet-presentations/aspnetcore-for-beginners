The tutorial below is based on [*"Get started with Razor Pages in ASP.NET Core"*](https://docs.microsoft.com/en-us/aspnet/core/tutorials/razor-pages/razor-pages-start) from docs.microsoft.com.

### Prerequisites
*  [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?wt.mc_id=adw-brand&gclid=Cj0KCQjwqYfWBRDPARIsABjQRYwLe3b9dJMixA98s8nS8QfuNBKGsiRVRXzB93fe4E27LGK5KLrGcnYaAgdREALw_wcB)
* In the Visual Studio Installer, install the following workloads:
    * ASP.NET and web development
    * .NET Core cross-platform development

## Create a Razor web app

* From the Visual Studio File menu, select New > Project.
* Create a new ASP.NET Core Web Application. Name the project RazorPagesMovie.

![](images/newproject.png)

* Select ASP.NET Core 2.1 in the dropdown, and then select Web Application.

![](images/createwebapp.png)

The Visual Studio template creates a starter project.

![](images/projectfiles-vs.png)

* Press F5 to run the app to view the project with the default template.

![](images/razor-page.png)

#### Project Files and Folders explained

The following table lists the files and folders associated in the project.

| Files or Folders       | Purpose        |
| ------------- |-------------|
| wwwroot      | Contains all the static files. For example CSS, images etc. | 
| Pages     | This folder contains the pages for our application.      |    
| Startup.cs | Configures services  we use in our application. For example adding user authentication through Microsoft, Google or Facebook account.   |
| Program.cs | Host our ASP.NET Core application.*The host is responsible for app startup and lifetime management*     |  

**NEXT TUTORIAL** - [Adding a Model](../2-Add%20a%20model/Addamodel-VS.md)
