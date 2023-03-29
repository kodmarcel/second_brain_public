---  
share: true  
tag: public  
---  
# Iptables  
  
sudo iptables -I INPUT -p all -s 71.211.139.49 -j ACCEPT  
sudo iptables -I INPUT 13 -p all -s 76.131.117.75 -j ACCEPT -m comment --comment "Ryan's machine"  
sudo ^Ctables -I INPUT -p tcp -s "213.250.28.226" --dport 1433 -j ACCEPT -m comment --comment "windows server access to DB for alteryx"  
sudo iptables -I INPUT -p tcp -m tcp --dport 8091 -j ACCEPT -m comment --comment "api server - open port 8091"  
sudo iptables -I INPUT -p tcp -m tcp --dport 9090 -j ACCEPT -m comment --comment "cockpit - open port 9090"  
