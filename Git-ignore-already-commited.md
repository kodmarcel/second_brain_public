---  
share: true  
tag: public  
---  
[stack overflow](https://stackoverflow.com/questions/25436312/gitignore-not-working)  
  
To untrack a single file that has already been added/initialized to your repository, i.e., stop tracking the file but not delete it from your system use: `git rm --cached filename`  
  
To untrack every file that is now in your `.gitignore`:  
  
First commit any outstanding code changes, and then, run this command:  
  
```  
git rm -r --cached .  
```  
  
This removes any changed files from the index(staging area), then just run:  
  
```  
git add .  
```  
  
Commit it:  
  
```  
git commit -m ".gitignore is now working"  
```