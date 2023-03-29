---  
share: true  
tag: public  
---  
# Linux_rename  
~~~  
# Rename all *.txt to *.text  
for file in *.txt; do   
    mv -- "$file" "${file%.txt}.text"  
done  
~~~  
