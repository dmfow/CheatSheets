## Start a repo/project (start using git in a directory structure)
#### Make git in you current directory
```
cd ./where_you_want_it
git init
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

#### Check status of files in the project
```
# Display the list of changed files together with the files that are yet to be staged or committed
git status

# Add files to your project for git to keep track of
git add <temp.txt>
# OR
git add <File name> command
  
# Commit (Save) files to your project - (Don't forget to save the file to the disk first)
git commit -m “Message for the commit here”
# OR
git commit –m “Message for the commit here”
# OR
git commit -am “Message for the commit here” command

# Upload to your git/gitlab/github server
git push command
# OR
git push origin <master>
```


#### User info (eg for push and pull)
```
git config --local user.email youremail@example.com
# OR (to use the same for all repos/projects --global)
git config --global user.email youremail@example.com
```

