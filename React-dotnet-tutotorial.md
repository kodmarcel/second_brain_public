---  
share: true  
tag: public  
---  
# react_dotnet_tutotorial  
[youtube video](https://www.youtube.com/watch?v=2Ayfi7OJhBI)  
  
  
Also tried to follow this one:  
[official tutorial](https://docs.microsoft.com/en-us/visualstudio/javascript/tutorial-asp-net-core-with-react?view=vs-2022)  
  
but it is made for visual studio which creates most of structure for you so i went with the youtube video.  
  
  
First i setup the vscode [vsode dotnet react setup](./vsode-dotnet-react-setup.md)   
  
then i have problems with dotnet run not finding the framework  
  
got error:  
  
```  
You must install or update .NET to run this application.  
  
App: /home/marcel/Documents/Active/vertical_fintech/technology_tutorial/bin/Debug/net6.0/technology_tutorial  
Architecture: x64  
Framework: 'Microsoft.AspNetCore.App', version '6.0.0' (x64)  
.NET location: /usr/share/dotnet  
  
No frameworks were found.  
  
Learn about framework resolution:  
https://aka.ms/dotnet/app-launch-failed  
  
To install missing framework, download:  
https://aka.ms/dotnet-core-applaunch?framework=Microsoft.AspNetCore.App&framework_version=6.0.0&arch=x64&rid=arch-x64  
```  
  
  
  
> This is caused because the runtime is shipped as a separate package in Arch. You just need to make sure you have the aspnet-runtime package installed as well.   
> -- <cite>[arch_wiki](https://wiki.archlinux.org/title/.NET#It_was_not_possible_to_find_any_compatible_framework_version)</cite>  
  
