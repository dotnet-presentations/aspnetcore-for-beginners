The tutorial below is based on [*"Get started with ASP.NET Core Razor Pages in Visual Studio Code"*](https://docs.microsoft.com/en-us/aspnet/core/tutorials/razor-pages-vsc/razor-pages-start) from docs.microsoft.com.

### Prerequisites
* .NET Core SDK 2.1 
*  Visual Studio Code
* Tutorial 1- Create a Razor Page application

## Add a data model
In this section, we are adding classes to manage movies in a database.
- Add a folder named Models
- Add a class to Models folder named Movie.cs
![](images\Models.PNG)

#### Add the code below to Movie.cs
```
using System;

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
#### Add a database context class
Create a new class named `MovieContext.cs` in the Models folder. database context aka `DbContext` is a class provided by Entity Framework to establish connection to database.
```
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
The code above creates a `DbSet`  property for the entity set. An entity set typically corresponds to a database table, and entity corresponds to a row in the table.

#### Add a connection string.

Open the `appsettings.json` file.
```
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
#### Register the database context
Open Startup.cs file and add the code below to the ConfigureServices method.
```
 public void ConfigureServices(IServiceCollection services)
        {
            services.AddDbContext<MovieContext>(options => options.UseSqlite(Configuration.GetConnectionString("MovieContext")));
            services.AddMvc();
        }
```
Add the following using statements `using RazorPagesMovie.Models` and `using Microsoft.EntityFrameworkCore`.