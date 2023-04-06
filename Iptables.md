---  
share: true  
tag: public  
---  
# Iptables  
This should work on rocky linux (probably other distributions as well)  
  
To list rules with line numbers so you can delete them  
```  
sudo iptables --list --line-numbers  
```  
To delete  rule at line number inside a specific chain (INPUT in this case)  
```  
sudo iptables -D INPUT 14  
```  
To insert a new rule at a specific place (Here we have several examples of rules. Run only one not all of them)  
```  
sudo iptables -I INPUT 13 -p all -s 76.131.117.75 -j ACCEPT -m comment --comment "Ryan's machine" # This opens all ports for specific ip  
  
sudo iptables -I INPUT -p tcp -s "213.250.28.226" --dport 1433 -j ACCEPT -m comment --comment "windows server access to DB for alteryx" # This oppens a specific port to the specific IP  
```  
To make changes persistent  
```  
sudo service iptables save  
```  
  
  
  
