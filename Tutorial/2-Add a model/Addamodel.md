# Add a model in Visual Studio Code

The following tutorial is based on [*"Get started with ASP.NET Core Razor Pages in Visual Studio Code"*](https://docs.microsoft.com/aspnet/core/tutorials/razor-pages-vsc/razor-pages-start) from docs.microsoft.com.

## Prerequisites

* [.NET 6 SDK](https://dotnet.microsoft.com/download/dotnet/6.0)
* [Visual Studio Code](https://code.visualstudio.com/?wt.mc_id=adw-brand&gclid=Cj0KCQjwqYfWBRDPARIsABjQRYwLe3b9dJMixA98s8nS8QfuNBKGsiRVRXzB93fe4E27LGK5KLrGcnYaAgdREALw_wcB)
* Tutorial 1- [Create a Razor Page application](../1-Create%20a%20Razor%20Page/Create-a-Razorpage.md)
  
## Add a data model

In this section, you are adding classes to manage movies in a database.

1. Add a folder named Models.
1. Add a class to the `Models` folder named `Movie.cs`.

    ![](images/Models.PNG)

1. Add the following code to the `Movie.cs` file:

    ``` cs
    namespace RazorPagesMovie.Models
    {
        public class Movie
        {
            public int ID { get; set; }
            public string Title { get; set; }
            public DateTime ReleaseDate { get; set; }
            public string Genre { get; set; }
            public decimal Price { get; set; }
        }
    }
    ```

## Add a database context class

Create a new class named `MovieContext.cs` in the Models folder. The database context, or `DbContext`, is a class provided by Entity Framework to facilitate database interactions.

``` cs
using Microsoft.EntityFrameworkCore;

namespace RazorPagesMovie.Models
{
    public class MovieContext : DbContext
    {
        public MovieContext(DbContextOptions<MovieContext> options)
                : base(options)
        {
        }

        public DbSet<Movie> Movie { get; set; }
    }
}
```

The previous code creates a `DbSet` property for the entity set. An entity set typically corresponds to a database table, and an entity corresponds to a row in the table.

### Add a connection string

Open the `appsettings.json` file and add the `MovieContext` connection string as shown below.

``` json
{
  "Logging": {
    "IncludeScopes": false,
    "LogLevel": {
      "Default": "Warning"
    }
  },
  "ConnectionStrings": {
    "MovieContext": "Data Source=MvcMovie.db"
  }
}
```

### Register the database context

1. Open the `Startup.cs` file and add the following code to the `ConfigureServices` method:

    ``` cs
    public void ConfigureServices(IServiceCollection services)
    {
        services.Configure<CookiePolicyOptions>(options =>
        {
            // This lambda determines whether user consent for non-essential cookies is needed for a given request.
            options.CheckConsentNeeded = context => true;
            options.MinimumSameSitePolicy = SameSiteMode.None;
        });
    
        services.AddDbContext<MovieContext>(options => options.UseSqlite(Configuration.GetConnectionString("MovieContext")));
        services.AddMvc().AddMvcOptions(opt => opt.EnableEndpointRouting = false);
    }
    ```

1. Add the following using statements: `using RazorPagesMovie.Models` and `using Microsoft.EntityFrameworkCore`.

## Add scaffold tooling and perform initial migration

In the command line, run the following commands:

 ```console
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design
dotnet add package Microsoft.EntityFrameworkCore.Sqlite
dotnet restore
dotnet ef migrations add InitialCreate
dotnet ef database update
```

Commands Explained

| Command       |Description       |
| ------------- |-------------|
| ` add package`    | installs the tools needed |
| `ef migrations add InitialCreate`     | generates code to create the initial database schema based on the model specified in 'MovieContext.cs'. `InitialCreate` is the name of the migrations. |  
|`ef database update` | creates the database      |

### Scaffold the movie model

Install the `aspnet-codegenerator` global tool by running the following command:

 ```console
dotnet tool install --global dotnet-aspnet-codegenerator
```

> Note: You need to close and reopen the console window to be able to use this tool.

Run the the following commands:

*On Windows*

`dotnet aspnet-codegenerator razorpage -m Movie -dc MovieContext -udl -outDir Pages\Movies --referenceScriptLibraries`

*On Mac and Linux*

`dotnet aspnet-codegenerator razorpage -m Movie -dc MovieContext -udl -outDir Pages/Movies --referenceScriptLibraries`

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
