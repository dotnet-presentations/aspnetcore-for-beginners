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

#### Add the Entity Framework tools 

- Install the   `Microsoft.EntityFrameworkCore.Tools.DotNet` package to `DotNetCliToolReference` in RazorPagesMovie.csproj.

```
<Project Sdk="Microsoft.NET.Sdk.Web">
  <PropertyGroup>
    <TargetFramework>netcoreapp2.0</TargetFramework>
  </PropertyGroup>
  <ItemGroup>
    <PackageReference Include="Microsoft.AspNetCore.All" Version="2.0.3" />
    <PackageReference Include="Microsoft.VisualStudio.Web.CodeGeneration.Design" Version="2.0.2" />
  </ItemGroup>
  <ItemGroup>
    <DotNetCliToolReference Include="Microsoft.VisualStudio.Web.CodeGeneration.Tools" Version="2.0.2" />
    <DotNetCliToolReference Include="Microsoft.EntityFrameworkCore.Tools.DotNet" Version="2.0.1" />
  </ItemGroup>
</Project>

```
#### Add scaffold tooling and perform initial migration

In the command line run the following commands
```
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design
dotnet restore
dotnet ef migrations add InitialCreate
dotnet ef database update
```
Commands Explained 
| Command       |    Description       | 
| ------------- |:-------------:|
| ` add package`    | installs the tools needed |
| `ef migrations add InitialCreate`     | generates code to create the initial database schema based on the model specified in 'MovieContenxt.cs'.`InitialCreate` is the name of the migrations. |  
|`ef database update` | creates the database      | 

#### Scaffold the movie model

Run the commands below 

*On Windows*

`dotnet aspnet-codegenerator razorpage -m Movie -dc MovieContext -udl -outDir Pages\Movies --referenceScriptLibraries`

*On Mac and Linux*

`dotnet aspnet-codegenerator razorpage -m Movie -dc MovieContext -udl -outDir Pages/Movies --referenceScriptLibraries`
#### Test your app
- Run the app `dotnet run`
- Launch a browser and go to `http://localhost:5000/movies`

![](images\moviespage.PNG)
- create a new entry

![](images\createnew.PNG)

- It works!
![](images\newentry.PNG.PNG)
- Test to se Edit, Details and delete

To learn more on the pages created in this tutorial read [this post](https://docs.microsoft.com/en-us/aspnet/core/tutorials/razor-pages-vsc/page)
