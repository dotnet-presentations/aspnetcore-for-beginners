The tutorial below is based on [*"Get started with ASP.NET Core Razor Pages in Visual Studio Code"*](https://docs.microsoft.com/en-us/aspnet/core/tutorials/razor-pages-vsc/razor-pages-start) from docs.microsoft.com.

### Prerequisites
* .NET Core SDK 2.1 
*  Visual Studio Code
* Tutorial 1- Create a Razor Page application
* Tutorial 2- Add a Model

## Update generated Pages

![](https://github.com/dotnet-presentations/aspnetcore-for-beginners/blob/master/Tutorial/3-Upate%20Pages/images/CurrentPage.PNG)

In this quick tutorial we are going to learn how to update the generated pages. For example suppose we want to remove the time from the release date.

- Open Models/Movie.cs `using System.ComponentModel.DataAnnotations;` and following [data annotations](https://docs.microsoft.com/en-us/aspnet/mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6) `[Display(Name = "Release Date")]` and `[DataType(DataType.Date)]`.

```
using System;
using System.ComponentModel.DataAnnotations;

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
        public decimal Price { get; set; }
    }
}
```
- run the app to see the update `dotnet run`
![](images\NewPage.PNG)
