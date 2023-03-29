---  
share: true  
tag: public  
---  
# How do I run multiple background commands in bash in a single line?  
#### [stackoverflow.com](https://stackoverflow.com/questions/14612371/how-do-i-run-multiple-background-commands-in-bash-in-a-single-line)  
  
I normally run multiple commands with something like this:  
  
    sleep 2 && sleep 3  
      
  
or  
  
    sleep 2 ; sleep 3  
      
  
but what if I want to run them both in the background from one command line command?  
  
    sleep 2 & && sleep 3 &  
      
  
doesn't work. And neither does replacing `&&` with `;`  
  
Is there a way to do it?  
  
1  
  
---  
  
Exactly how do you want them to run? If you want them to be started in the _background_ and run **sequentially**, you would do something like this:  
  
```  
{ sleep 2; sleep 3; } &  
```  
  
If you want `sleep 3` to run only if `sleep 2` succeeds, then:  
  
```  
sleep 2 && sleep 3 &  
```  
  
If, on the other hand, you would like them to run in **parallel** in the _background_, you can instead do this:  
  
```  
sleep 2 & sleep 3 &  
```  
  
And the two techniques could be combined, such as:  
  
```  
{ sleep 2; echo first finished; } & { sleep 3; echo second finished; } &  
```  
  
Bash being bash, there's often a multitude of different techniques to accomplish the same task, although sometimes with subtle differences between them.  
  
  
  
Clipped on Wednesday, September 28, 2022 at 12:24 PM