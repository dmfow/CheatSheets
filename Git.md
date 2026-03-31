## Start a repo/project (start using git in a directory structure)
#### Make git in you current directory
```
cd ./where_you_want_it
git init

# Undo init
cd ./where_you_want_it
rm -rf .git
```

#### Make git in you current empty directory
```
cd ./where_you_want_it
git init [project name]
```


#### Get a "repo" from a servre
```
cd ./where_you_want_it
git clone https://....the webaddress_and_dir
# OR
git clone username@host:/path/to/repository
# OR
git clone /path/to/repository
```

## Use git

#### Make a .gitignore file
```
# In your application root where you did "git init".
# Edit a file (or create) .gitignore (first example line is to skip sqlite3 databases, second is to skip a library)
*.sqlite3
src/__pycache__/

```

#### Check status of files in the project
```
# Display the list of changed files together with the files that are yet to be staged or committed
git status

# Add files to your project for git to keep track of
git add <temp.txt>
# OR
git add <File name> command

# undo what you have added
git reset
```

#### Connect local repos to remote repos (One Time)
```
git config --global user.email "email"
git config --global user.name "name"
git remote add origin <host-or-remoteURL, incl port and path>
# If you got it wrong
git remote rm <name-of-the-repository, ex origin>
```

#### Commit your changes (add, delete, reset etc)
```
# Commit (Save) files to your project - (Don't forget to save the file to the disk first)
git commit -m “Message for the commit here”
# OR
git commit –m “Message for the commit here”
# OR
git commit -am “Message for the commit here” command

# Upload to your git/gitlab/github server (<master> is the name of the master)
git push command
# OR
git push origin <master>

# Merge everything on the remote repo to your local repo
git pull

```


#### User info (eg for push and pull)
```
git config --local user.email youremail@example.com
# OR (to use the same for all repos/projects --global)
git config --global user.email youremail@example.com
```

#### Make a new branch
```
command git checkout -b <branch-name>
```

#### Switch from one branch to another
```
git checkout <branch-name>
```
#### List branches
```
git branch
# Delete branch
git branch –d <branch-name>
```

#### Merge a branch into the active one
```
git merge <branch-name>
```
  
  


## Delete a connection between local repo and a remote repo
```
git remote rm <name-of-the-repository>
```



  
