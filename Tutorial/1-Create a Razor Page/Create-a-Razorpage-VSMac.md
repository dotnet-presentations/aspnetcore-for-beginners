# Create a Razor Pages web app in Visual Studio for Mac

The following tutorial is based on [*"Get started with Razor Pages in ASP.NET Core"*](https://docs.microsoft.com/aspnet/core/tutorials/razor-pages/razor-pages-start) from docs.microsoft.com.

## Prerequisites

* [Visual Studio 2022 for Mac Preview](https://visualstudio.microsoft.com/vs/mac/preview/?wt.mc_id=adw-brand&gclid=Cj0KCQjwqYfWBRDPARIsABjQRYwLe3b9dJMixA98s8nS8QfuNBKGsiRVRXzB93fe4E27LGK5KLrGcnYaAgdREALw_wcB)
* In the Visual Studio for Mac Installer, install the .NET Core target.

## Create a Razor web app

* From the Visual Studio for Mac File menu, select New Solution.
* Create a new `ASP.NET Core Web Application` with  **Web and Console > ASP.NET Core > Web Application**. Name the project `RazorPagesMovie`.

![](images/newproject-vsmac.png)

* Select .NET 6.0 in the dropdown, and keep the other defaults.

![](images/createwebapp-vsmac.png)

* Name the project RazorPagesMovie.

![](images/nameproject-vsmac.png)

The template creates a starter project.

![](images/projectfiles-vsmac.png)

* Run the application with **Debug** > **Start Without Debugging**.
* If you see a dialog box for invalid certificate, select **Run** to install the ASP.NET Core debug certificate.

![](images/razor-page.png)

## Project files and folders explained

The following table lists the files and folders associated in the project.

| Name                     | Description                                                                                         |
| ------------------------ |-----------------------------------------------------------------------------------------------------|
| *wwwroot/*               | Contains all the static files. For example CSS, images, and so on.                                  |
| *Pages/*                 | Contains Razor Pages and supporting files. Each Razor page is a pair of files:<br/>- A *.cshtml* file that contains markup with C# code using Razor syntax.<br/>- A *.cshtml.cs* `PageModel` class file that defines page handler methods and data used to render the page.                                                                                        |
| *RazorPagesMovie.csproj* | Contains configuration metadata for the project, such as dependencies.                              |
| *Program.cs*             | Serves as the app's managed entry point and configures app behavior, such as routing between pages. |

**NEXT TUTORIAL:** [Adding a Model](../2-Add%20a%20model/Addamodel-VSMac.md)
