---  
share: true  
tag: public  
---  
# How to specify the private SSH-key to use when executing shell command on Git?  
#### [stackoverflow.com](https://stackoverflow.com/questions/4565700/how-to-specify-the-private-ssh-key-to-use-when-executing-shell-command-on-git)  
  
Most of the answers given here do not explain the details for the most basic usage.  
  
After you have setup a server (in this case a `linux` server) in the cloud, you connect to it using ssh from the terminal.  
  
From your computer, add the private key `dyson-ubuntu-vm.pem` which is given to you by your cloud services provider such as Azure, AWS etc to your .ssh configuration on your local machine like this:  
  
Copy the `.pem` file to the `/home/ssenyonjo/.ssh` folder, then open `/home/ssenyonjo/.ssh/config` file and add the following entry:  
  
    Host 20.85.213.44  
      HostName 20.85.213.44  
      User Dyson  
      IdentityFile /home/ssenyonjo/.ssh/dyson-ubuntu-vm.pem  
      IdentitiesOnly yes  
      
      
  
Now from your terminal, access the cloud linux server like so:  
  
    ssh Dyson@20.85.213.44  
      
  
When that works, create a git project on the cloud server like so:  
  
    Dyson@dyson-ubuntu-vm:~/projects$ git init --bare s2  
      
  
Now come back to your local machine and clone that empty repository like so:  
  
    ssenyonjo@ssenyonjo-pc:~/Projects/mastering-git$ git clone ssh://Dyson@20.85.213.44/home/Dyson/projects/s2  
      
  
If you see an error that looks something like: `fatal: Could not read from remote repository`, It means you're accessing the wrong folder. Ensure you have outlined the right path from the root to the created repository.  
  
If you dont want to setup a config file but want to access the ssh server that requires a key, you can use below command:  
  
    GIT_SSH_COMMAND='ssh -i ~/Projects/aws/keys/aws_ubuntu.pem'  git clone ssh://ubuntu@15.207.99.158/home/ubuntu/projects/mastering-git/rand   
      
  
You can export the command to continue using it for other tasks like `git push` and `git pull`  
  
    export GIT_SSH_COMMAND='ssh -i ~/Projects/aws/keys/aws_ubuntu.pem'  
      
  
See: [https://stackoverflow.com/a/29754018/10030693](https://stackoverflow.com/a/29754018/10030693)  
  
* * *  
  
#### Page 2  
  
If you're like me, you can:  
  
*   Keep your ssh keys organized  
      
*   Keep your git clone commands simple  
      
*   Handle any number of keys for any number of repositories.  
      
*   Reduce your ssh key maintenance.  
      
  
I keep my keys in my `~/.ssh/keys` directory.  
  
I prefer convention over configuration.  
  
I think code is law; the simpler it is, the better.  
  
**STEP 1 - Create Alias**  
  
Add this alias to your shell: `alias git-clone='GIT_SSH=ssh_wrapper git clone'`  
  
**STEP 2 - Create Script**  
  
Add this **ssh\_wrapper** script to your PATH:  
  
    #!/bin/bash  
    # Filename: ssh_wrapper  
      
    if [ -z ${SSH_KEY} ]; then  
        SSH_KEY='github.com/l3x'  # <= Default key  
    fi  
    SSH_KEY="~/.ssh/keys/${SSH_KEY}/id_rsa"  
    ssh -i "${SSH_KEY}" "$@"  
      
  
**EXAMPLES**  
  
Use github.com/l3x key:  
  
    KEY=github.com/l3x git-clone https://github.com/l3x/learn-fp-go  
      
  
The following example also uses the **github.com/l3x** key (by default):  
  
    git-clone https://github.com/l3x/learn-fp-go  
      
  
Use bitbucket.org/lsheehan key:  
  
    KEY=bitbucket.org/lsheehan git-clone git@bitbucket.org:dave_andersen/exchange.git  
      
  
**NOTES**  
  
Change the default SSH\_KEY in the ssh\_wrapper script to what you use most of the time. That way, you don't need to use the KEY variable most of the time.  
  
You may think, "Hey! That's a lot going on with an alias, a script and some directory of keys," but for me it's convention. Nearly all my workstations (and servers for that matter) are configured similarly.  
  
My goal here is to simplify the commands that I execute regularly.  
  
My conventions, e.g., Bash scripts, aliases, etc., create a consistent environment and helps me keep things simple.  
  
KISS and names matter.  
  
For more design tips check out _Chapter 4 SOLID Design in Go_ from my book: [https://www.amazon.com/Learning-Functional-Programming-Lex-Sheehan-ebook/dp/B0725B8MYW](https://rads.stackoverflow.com/amzn/click/com/B0725B8MYW)  
  
Hope that helps. - Lex  
  
---  
  
Clipped on Monday, January 9, 2023, 10:40 AM