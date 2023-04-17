---  
share: true  
tag: public  
---  
To check current limit run:  
```  
    ulimit -a  
```  
And check number of open files  
  
To modify it put  
```  
ulimit -n 24000  
```  
in the bash script that runs your program