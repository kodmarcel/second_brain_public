---  
share: true  
tag: public  
---  
# Use different ssh keys for github  
  
[mediabiz@mediabiz-sentry ~]$ cat .ssh/config  
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
  
  
  
  
 [mediabiz@mediabiz-sentry ~]$ git clone git@github.com-streamingspecial:mediabiz-dev/streamingspecial.git