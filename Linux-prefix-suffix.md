---  
share: true  
tag: public  
---  
# Linux prefix-suffix  
  
```  
$ prefix="hell"  
$ suffix="ld"  
$ string="hello-world"  
$ foo=${string#"$prefix"}  
$ foo=${foo%"$suffix"}  
$ echo "${foo}"  
o-wor  
```