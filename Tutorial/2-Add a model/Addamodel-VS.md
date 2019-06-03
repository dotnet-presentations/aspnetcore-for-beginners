The tutorial below is based on [*"Get started with Razor Pages in ASP.NET Core"*](https://docs.microsoft.com/en-us/aspnet/core/tutorials/razor-pages/razor-pages-start) from docs.microsoft.com.

### Prerequisites
*  [Visual Studio 2019](https://visualstudio.microsoft.com/downloads/?wt.mc_id=adw-brand&gclid=Cj0KCQjwqYfWBRDPARIsABjQRYwLe3b9dJMixA98s8nS8QfuNBKGsiRVRXzB93fe4E27LGK5KLrGcnYaAgdREALw_wcB)
* In the Visual Studio Installer, install the following workloads:
    * ASP.NET and web development
    * .NET Core cross-platform development
* Tutorial 1- [Create a Razor Page application](../1-Create%20a%20Razor%20Page/Create-a-Razorpage-VS.md)

## Add a data model
In this section, we are adding classes to manage movies in a database.

* In Solution Explorer, right-click the RazorPagesMovie project > Add > New Folder. Name the folder Models.
* Right click the Models folder. Select Add > Class. Name the class `Movie`.

#### Add the code below to Movie.cs

```csharp
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

## Scaffold a Context class

* In Solution Explorer, right click on the Pages folder > Add > New Folder.
* Name the folder Movies
* In Solution Explorer, right click on the Pages/Movies folder > Add > New Scaffolded Item.
  
![](images/add_scaffold_VS.png)

* In the Add Scaffold dialog, select Razor Pages using Entity Framework (CRUD) > Add.
  
![](images/scaffold_dialog_VS.png)

### In the Add Razor Pages using Entity Framework (CRUD) dialog:

![](images/add_razor_VS.png)

* In the Model class drop down, select Movie (RazorPagesMovie.Models).
* In the Data context class row, select the + (plus) sign and set the name as RazorPagesMovie.Models.MovieContext.
* In the Data context class drop down, select RazorPagesMovie.Models.MovieContext.
* Select Add.

The generated code from the scaffold process creates the following files:

* Pages/Movies/
    * Create
    * Delete
    * Details
    * Edit
    * Index
* Data/MovieContext.cs: Class that includes a `DbSet` property for the entity set. An entity set typically corresponds to a database table, and entity corresponds to a row in the table.

The scaffold process also modifies existing files:

* Startup.cs: Created a DB context and registered it with the dependency injection container
* appsettings.json: The connection string used to connect to a local database is added.

#### Perform initial migration

* From the Tools menu, select NuGet Package Manager > Package Manager Console.

![](images/pmc_VS.png)

* In the Package Manager Console enter the following commands:

```
Add-Migration Initial
Update-Database
```

#### Test your app
* Press F5 to run the app
* Append /movies to the URL in the browser: http://localhost:port/movies

![](images/moviespage.PNG)

* Create a new entry with the Create link

![](images/createnew.PNG)

* It works!

![](images/newentry.PNG)

* Test the Edit, Details and Delete links
  
If you get a SQL exception, verify you have run migrations and updated the database.

**Extra light read 7 minutes**: If you want to read more on pages we just created [click here for more information](https://docs.microsoft.com/en-us/aspnet/core/tutorials/razor-pages/page).

**NEXT TUTORIAL** - [Modifying generated pages](../3-Update%20Pages/update-VS.md)
