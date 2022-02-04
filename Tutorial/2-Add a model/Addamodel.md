# Add a data model in Visual Studio Code

The following tutorial is based on [*"Get started with ASP.NET Core Razor Pages in Visual Studio Code"*](https://docs.microsoft.com/aspnet/core/tutorials/razor-pages-vsc/razor-pages-start) from docs.microsoft.com.

## Prerequisites

* [.NET 6 SDK](https://dotnet.microsoft.com/download/dotnet/6.0)
* [Visual Studio Code](https://code.visualstudio.com/?wt.mc_id=adw-brand&gclid=Cj0KCQjwqYfWBRDPARIsABjQRYwLe3b9dJMixA98s8nS8QfuNBKGsiRVRXzB93fe4E27LGK5KLrGcnYaAgdREALw_wcB)
* Tutorial 1- [Create a Razor Page application](../1-Create%20a%20Razor%20Page/Create-a-Razorpage.md)
  
## Add a data model

In this section, you're adding classes to manage movies in a database.

1. Add a folder named **Models**.
1. Add a class to the `Models` folder named `Movie.cs`.

    ![](images/Models.PNG)

1. Add the following code to the `Movie.cs` file:

    ``` cs
    namespace RazorPagesMovie.Models;
        
    public class Movie
    {
        public int ID { get; set; }
        public string? Title { get; set; }
        public DateTime ReleaseDate { get; set; }
        public string? Genre { get; set; }
        public decimal Price { get; set; }
    }
    ```

## Add Entity Framework NuGet Packages

In the command line, run the following commands (you can open a new Terminal in VS Code via **Terminal** > **New Terminal**) :

 ```console
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design
dotnet add package Microsoft.EntityFrameworkCore.Sqlite
dotnet add package Microsoft.EntityFrameworkCore.SqlServer
dotnet add package Microsoft.EntityFrameworkCore.Design
dotnet restore
```

## Add a database context class


1. Add a folder named **Data**.

1. Create a new class named `RazorPagesMovieContext.cs` in the Models folder. 

The database context, or `DbContext`, is a class provided by Entity Framework to facilitate database interactions.

``` cs
using Microsoft.EntityFrameworkCore;
using RazorPagesModel.Models;

namespace RazorPagesMovie.Data;

public class RazorPagesMovieContext : DbContext 
{
    public RazorPagesMovieContext(DbContextOptions<RazorPagesMovieContext> options) 
        : base(options) 
    {
    }

    public DbSet<Movie> Movie => Set<Movie>();
}
```

The previous code creates a `DbSet` property for the entity set. An entity set typically corresponds to a database table, and an entity corresponds to a row in the table.

### Add a connection string

Open the `appsettings.json` file and add the `RazorPagesMovieContext` connection string as shown below.

``` json
{
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft.AspNetCore": "Warning"
    }
  },
  "AllowHosts": "*",
  "ConnectionStrings": {
    "RazorPagesMovieContext": "Data Source=MvcMovie.db"
  }
}
```

### Register the database context

1. Open the `Program.cs` file.
2. Add the following using directive at the top of the file.

   ```cs
   using RazorPagesMovie.Data;
   ```

3. Add the following code under `builder.Services.AddRazorPages();`:

    ``` cs
    var connectionString = builder.Configuration.GetConnectionString("RazorPagesMovieContext");
    builder.Services.AddSqlite<RazorPagesMovieContext>(connectionString);
    ```

## Perform initial migration

Save all files in the project. To run commands to create and manage migrations, you need to install the `dotnet ef` tool. Do that with the following command in the terminal (you can open a terminal inside of Visual Studio for Mac by right clicking on the project and selecting **Open in Terminal**).

```console
dotnet tool install --global dotnet-ef
```

> Tip:
> If `dotnet-ef` is already installed, you can update it with `dotnet tool update --global dotnet-ef`.

For more information, see [Entity Framework Core tools reference - .NET Core CLI](https://docs.microsoft.com/ef/core/cli/dotnet).

In the terminal, run the following commands in the project directory:

 ```console
dotnet ef migrations add InitialCreate
dotnet ef database update
```

Commands Explained

| Command       |Description       |
| ------------- |-------------|
| ` add package`    | installs the tools needed |
| `ef migrations add InitialCreate`     | generates code to create the initial database schema based on the model specified in 'RazorPagesMovieContext.cs'. `InitialCreate` is the name of the migrations. |  
|`ef database update` | creates the database      |

## Scaffold the movie model

Install the `aspnet-codegenerator` global tool by running the following command:

 ```console
dotnet tool install --global dotnet-aspnet-codegenerator
```

> Tip:
> If `dotnet-aspnet-codegenerator` is already installed, you can update it with `dotnet tool update --global dotnet-aspnet-codegenerator`.

> Note:
> You may need to close and reopen the console window to be able to use this tool.

Run the the following commands:

*On Windows*

`dotnet aspnet-codegenerator razorpage -m Movie -dc RazorPagesMovieContext -udl -outDir Pages\Movies --referenceScriptLibraries`

*On Mac and Linux*

`dotnet aspnet-codegenerator razorpage -m Movie -dc RazorPagesMovieContext -udl -outDir Pages/Movies --referenceScriptLibraries`

## Test your app

1. Run the app by typing the `dotnet run` command on the terminal.
1. Launch a browser and go to `http://localhost:<port number>/movies`.

    ![](images/moviespage.PNG)

1. Create a new entry

    ![](images/createnew.PNG)

    It works!

    ![](images/newentry.PNG)

1. Test Edit, Details and Delete links.

**Extra light read 7 minutes**: If you want to read more on pages you just created, see the [Part 3, scaffolded Razor Pages in ASP.NET Core](https://docs.microsoft.com/aspnet/core/tutorials/razor-pages-vsc/page) article.

**NEXT TUTORIAL** :[Modifying generated pages](../3-Update%20Pages/update.md)
