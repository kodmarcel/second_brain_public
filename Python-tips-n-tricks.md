---  
share: true  
tag: public  
---  
# Python tips n tricks  
  
## Reimport a module  
~~~  
import importlib  
import foo #import the module here, so that it can be reloaded.  
importlib.reload(foo)  
~~~