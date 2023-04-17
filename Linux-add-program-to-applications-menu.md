---  
share: true  
tag: public  
---  
put   
application.dekstop  
under  
`~/.local/share/applications/`  
with content  
```  
[Desktop Entry]  
Type=Application  
Encoding=UTF-8  
Name=Application Name  
Comment=Application description  
Icon=/path/to/icon.xpm  
Exec=/path/to/application/executable  
Terminal=false  
Categories=Tags;Describing;Application  
```  
  
also do not forget to have the application itself executable  
  
tested on Fedora 6.1