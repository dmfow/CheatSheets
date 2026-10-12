#### Start a branch
```
# Start a new branch
git checkout -b refactor-startup
```

###### NOTE !!!
git checkout has two main modes:
A. Switch branches, with git checkout <branch>
B. Restore a different version of a file, for example with git checkout <commit> <filename> or git checkout <filename>

#### See which branch your on and handling commits
```
# Check which branch you're on. The current branch has an asterisk * refactor-startup.
  git branch
  git branch --show-current

# Handling commits, will be done on the current branch
  git add .
  git commit -m "message"

# push first time on the new branch
  git push origin refactor-startup

  # if  "no target (origin)" error means refactor-startup doesn't have an upstream set yet.
  # First time, you need to tell it where to go
  # The -u (short for --set-upstream) remembers the mapping. After that, plain git push works every time:
  git push -u origin refactor-startup

# To push on the branch your on
  git push
```


