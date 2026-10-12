#### Start a branch
```
# Start a new branch
git checkout -b refactor-startup
```

#### NOTE !!!
git checkout has two main modes:
A. Switch branches, with git checkout <branch>
B. Restore a different version of a file, for example with git checkout <commit> <filename> or git checkout <filename>
 
```
# Check which branch you're on. The current branch has an asterisk * refactor-startup.
  git branch
  git branch --show-current
# Handling commits and push  
  git add .
  git commit -m "message"
  git push origin refactor-startup
```


