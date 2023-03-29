---  
share: true  
tag: public  
---  
# Regex to fix slovenian commas  
  
    Popravi vse s/z.  
~~~  
z ([t,s,h,š,k,f,c,p,č]) replace-> s \1 s ([^t,s,h,š,k,f,c,p,č]) replace-> z \1  
~~~  
    dodaj vse nujne vejice  
~~~  
([^,]) (ki|ko|ker|da|če) replace ->\1, \2   
~~~