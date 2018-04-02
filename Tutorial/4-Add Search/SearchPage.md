The tutorial below is based on [*"Get started with ASP.NET Core Razor Pages in Visual Studio Code"*](https://docs.microsoft.com/en-us/aspnet/core/tutorials/razor-pages-vsc/razor-pages-start) from docs.microsoft.com.

### Prerequisites
* .NET Core SDK 2.1 
*  Visual Studio Code
* Tutorial 1- Create a Razor Page application
* Tutorial 2- Add a Model
* Tutorial 3 - Update Page

## Adding Search to a page 

In this quick tutorial we are going to search to the Index Page. By the end of this tutorial you can search by genre and name.

- Update the Index page's `OnGetAsync` method

*Add code below to Movies/Index.cshtml*
```
@{
    Layout = "_Layout";
}
```
*Then edit the Movies/Index.cshtml.cs*
```
public async Task OnGetAsync(string searchString)
{
    var movies = from m in _context.Movie
                 select m;

    if (!String.IsNullOrEmpty(searchString))
    {
        movies = movies.Where(s => s.Title.Contains(searchString));
    }

    Movie = await movies.ToListAsync();
}
```
**Test search string**
- Run your application 
- Append the query string to the end `?searchString=Wrinkle`