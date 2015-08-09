# Cake.IIS
Cake-Build addin that extends Cake with IIS extensions

[![Build status](https://ci.appveyor.com/api/projects/status/eqvnf0dk25rqsh44?svg=true)](https://ci.appveyor.com/project/PhillipSharpe/cake-iis)

[![cakebuild.net](https://img.shields.io/badge/WWW-cakebuild.net-blue.svg)](http://cakebuild.net/)

[![Join the chat at https://gitter.im/cake-build/cake](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/cake-build/cake?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)



## Implemented functionality

* Create Website / Ftpsite
* Delete Site
* Start Site
* Stop Site
* Site Exists



* Create Applicaiton Pool
* Delete Pool
* Start Pool
* Stop Pool
* Pool Exists 
* Recycle Pool



## Referencing

Cake.IIS is available as a nuget package from the package manager console:

```csharp
Install-Package Cake.IIS
```

or directly in your build script via a cake addin:

```csharp
#addin "Cake.IIS"
```



## Usage

```csharp
#addin "Cake.IIS"


Task("ApplicationPool-Create")
    .Description("Create a ApplicationPool")
    .Does(() =>
{
    CreatePool("remote-server-name", new ApplicationPoolSettings()
    {
        Name = "Production",

        Username = "Admin",
        Password = "pass1"
    });
});

Task("ApplicationPool-Stop")
    .Description("Stops a local ApplicationPool")
    .Does(() =>
{
    StopPool("Production");
});

Task("ApplicationPool-Start")
    .Description("Starts a remote ApplicationPool")
    .Does(() =>
{
    StartPool("remote-server-name", "Production");
});



Task("Website-Create")
    .Description("Create a Website")
    .Does(() =>
{
    CreateWebsite("remote-server-name", new WebsiteSettings()
    {
        Name = "MyBlog",
        HostName = "blog.website.com",
        PhysicalPath = "C:/Websites/Blog",

        ApplicationPool = new ApplicationPoolSettings()
        {
            Name = "Production"
        }
    });
});

Task("Website-Stop")
    .Description("Stops a remote Website")
    .Does(() =>
{
    StopWebsite("remote-server-name", "MyBlog");
});

Task("Website-Start")
    .Description("Starts a local Website")
    .Does(() =>
{
    StartWebsite("MyBlog");
});


RunTarget("Website-Create");
```



## Example

A complete Cake example can be found [here](https://github.com/SharpeRAD/Cake.IIS/blob/master/test/build.cake)