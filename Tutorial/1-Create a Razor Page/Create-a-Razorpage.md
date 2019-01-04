The tutorial below is based on [*"Get started with ASP.NET Core Razor Pages in Visual Studio Code"*](https://docs.microsoft.com/en-us/aspnet/core/tutorials/razor-pages-vsc/razor-pages-start) from docs.microsoft.com.

### Prerequisites
* [.NET Core SDK 2.2](https://www.microsoft.com/net/download/) 
*  [Visual Studio Code](https://code.visualstudio.com/?wt.mc_id=adw-brand&gclid=Cj0KCQjwqYfWBRDPARIsABjQRYwLe3b9dJMixA98s8nS8QfuNBKGsiRVRXzB93fe4E27LGK5KLrGcnYaAgdREALw_wcB)

## Create a Razor web app

Enter commands below in the terminal
```
dotnet new razor -o RazorPagesMovie
cd RazorPagesMovie
dotnet run
```
Open a browser and browse to https://localhost:5001/ to view the application.

![](images/razor-page.png)

#### Open project in VS Code

- Shut down your application using `Ctrl+C`.
- Open your project in VS Code using one of the following options 
    - select File > Open Folder, and then select the RazorPagesMovie folder
    - or enter the following command in the terminal `code .`
- Click Yes to the prompt *"Required assets to build and debug are missing from 'RazorPagesMovie'. Add them?"*

![](images/Openinginvscode.PNG)

#### Project Files and Folders explained
| Files or Folders       | Purpose        |
| ------------- | ------------- |
| wwwroot      | Contains all the static files. For example CSS, images etc. | 
| Pages     | This folder contains the pages for our application.      |    
| Startup.cs | Configures services  we use in our application. For example adding user authentication through Microsoft, Google or Facebook account.   |
| Program.cs | Host our ASP.NET Core application.*The host is responsible for app startup and lifetime management*     |  

**NEXT TUTORIAL** - [Adding a Model](../2-Add%20a%20model/Addamodel.md)
