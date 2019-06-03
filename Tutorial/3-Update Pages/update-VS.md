The tutorial below is based on [*"Get started with Razor Pages in ASP.NET Core"*](https://docs.microsoft.com/en-us/aspnet/core/tutorials/razor-pages/razor-pages-start) from docs.microsoft.com.

### Prerequisites
*  [Visual Studio 2019](https://visualstudio.microsoft.com/downloads/?wt.mc_id=adw-brand&gclid=Cj0KCQjwqYfWBRDPARIsABjQRYwLe3b9dJMixA98s8nS8QfuNBKGsiRVRXzB93fe4E27LGK5KLrGcnYaAgdREALw_wcB)
* In the Visual Studio Installer, install the following workloads:
    * ASP.NET and web development
    * .NET Core cross-platform development
* Tutorial 2- [Add a Model](../2-Add%20a%20model/Addamodel-VS.md)
* Tutorial 3- [Update Page](../3-Update%20Pages/update-VS.md)

## Update generated Pages

![](images/CurrentPage.PNG)

In this quick tutorial we are going to learn how to update the generated pages. For example, suppose we want to remove the time from the release date.

* Open Models/Movie.cs

### Replace Movie.cs with the following

```csharp
using System;
namespace RazorPagesMovie.Models
{
    public class Movie
    {
        public int ID { get; set; }
        public string Title { get; set; }

        [Display(Name = "Release Date")]
        [DataType(DataType.Date)]
        public DateTime ReleaseDate { get; set; }
        public string Genre { get; set; }

        [Column(TypeName = "decimal(18, 2)")]
        public decimal Price { get; set; }
    }
}
```

* Right click on a red line > Quick Actions and Refactorings

![](images/refactor_VS.png)

* Select `using System.ComponentModel.DataAnnotations;`

![](images/using_annotations_VS.png)

* Right click on the remaining red line > Quick Actions and Refactorings on the [Column] attribute and select using `System.ComponentModel.DataAnnotations.Schema;`
* Press F5 to run the app and see the changes.

![](images/NewPage.PNG)

**NEXT TUTORIAL** - [Adding search](../4-Add%20Search/SearchPage-VS.md)
