---  
share: true  
tag: public  
---  
# Add user  
  
#!/bin/bash  
sudo adduser $1  
sudo passwd $1  
sudo passwd -u $1   
sudo  -u $1 mkdir /home/$1/.ssh  
sudo  -u $1 vim /home/$1/.ssh/authorized_keys  
sudo  -u $1 chmod 700 /home/$1/.ssh  
sudo  -u $1 chmod 600 /home/$1/.ssh/authorized_keys