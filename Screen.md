---  
share: true  
tag: public  
---  
# Screen  
   
It is a good practice to start screen sessions with descriptive names so you can easily remember which process is running in the session. To create a new session with a session name, run the following command  
  
```  
screen -S name  
```  
  
You can view all the current screens in your VM by doing ls  
  
```  
screen -ls  
```  
  
 To detach from the current screen session you can press ‘**Ctrl-A’** and **‘Ctrl-D’**. All screen sessions will still be active and you can re-attach to them at any time later.  
  
To re-attach/restore to a session which you had detached from, simply run the following command  
  
```  
screen -r name  
```  
  
  
 **‘Ctrl-A’** and **‘?’**  to see help  
  
![Pasted image 20230401082340.png](./resources/Software/images/Pasted%20image%2020230401082340.png)