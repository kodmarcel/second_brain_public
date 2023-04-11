---  
share: true  
tag: public  
---  
# Use different ssh keys for github  
  
If you need to use different ssh keys, because for example you use different deploy keys for each project you can set them up in the .ssh/config file like this:  
```  
Host github.com-streamingscrapper  
 HostName github.com  
 User git  
 AddKeysToAgent yes  
 IdentityFile ~/.ssh/id_rsa  
Host github.com-imdb  
 HostName github.com  
 User git  
 AddKeysToAgent yes  
 IdentityFile ~/.ssh/id_ed25519  
Host github.com-suite  
 HostName github.com  
 User git  
 AddKeysToAgent yes  
 IdentityFile ~/.ssh/automatching_suite_deploy_key  
Host github.com-streamingspecial  
 HostName github.com  
 User git  
 AddKeysToAgent yes  
 IdentityFile ~/.ssh/streamingspecial_deploy_key  
```  
  
Then you can access github repositories by changing the host name in url like this  
```  
 [mediabiz@mediabiz-sentry ~]$ git clone git@github.com-streamingspecial:mediabiz-dev/streamingspecial.git  
 ```  
 