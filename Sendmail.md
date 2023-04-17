---  
share: true  
tag: public  
---  
```  
$ echo "Subject: sendmail test" | sendmail -v msits.marcel@gmail.com  
```  
  
To see user mail run  
```  
$ less /var/mail/$(whoami)  
```