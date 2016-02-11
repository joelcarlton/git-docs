# Git Commands

## All commands should be executed from the parent of the associated repository.

---

### Configuration

---

#### Set user specific information for local repository only

```shell
git config user.name "First Last"
git config user.email "First.Last@domain.com"
```

#### Set user specific information all repositories

```shell
git config --global user.name "First Last"
git config --global user.email "First.Last@domain.com"
```

#### Force git to set group write permissions

```shell
git config --add core.sharedRepository group
```

#### Force git to accept self signed certificates

```shell
git config --global http.sslVerify false
```

#### Ignore posix changes inside repo:

```shell
git config core.fileMode false
```

---

## Learning Version Control With Git

---

### How to get help
```shell
git command --help
```

---
### Inspecting local changes, staging, and committing
---
##### Show list of added, modified, and deleted files that have or haven't been tracked by git
```shell
git status
```
##### Add files that will be committed
```shell
git add file file file
```
##### Remove files from the commit
```shell
git rm file file file
```
##### Status should now reflect changes
```shell
git status
```
##### Commit with comment
```shell
git commit -m "Comment"
```
##### Status should now not show changes from before the commit
```shell
git status
```

---
### Commit history
---

##### Viewing commit history
```shell
git log
```
##### View files changed
```shell
git log --status
```
##### View files changed with diff
```shell
git log -p
```

---
### Ignoring files for everyones repositories
---

##### Specific path
```shell
echo "folder/file.ext" >> .gitignore
```
##### All files with name
```shell
echo "file.ext" >> .gitignore
```
##### All file extensions
```shell
echo "*.ext" >> .gitignore
```
##### All files within folder
```shell
echo "folder/folder/*" >> .gitignore
```
##### Ignoring files for only your repository
```shell
echo "file.ext" >> .git/info/exclude
```

---
### Branching
---

##### Create new branch
```shell
git branch branchName
```
##### List all branches
```shell
git branch -v
```
##### Switch working branch
```shell
git checkout branchName
```

---
### Merging
---

##### Switch to the branch receiving the merge
```shell
git checkout master
```
##### Merge other branch into master
```shell
git merge branchName
```

---
### Merge conflicts
---

##### Switch to the receiving branch
```shell
git checkout master
```
##### Resolve conflict after merge
```shell
git merge branchName
```
### With text editor
##### Check status to see which files have conflicts
```shell
git status
```
##### Edit the file, save, and add for commit
```shell
git add file.ext
```
### With merge tool
##### Run git command to open all conflicts up in configured tool
```shell
git mergetool
```
##### Commit the changes
```shell
git commit
```
##### Attempt another merge
```shell
git merge branchName
```
##### Reverting a merge
```shell
git merge --abort
```

---
### Stashing
---

##### Temporality move all local, uncommitted progress to side
```shell
git stash
```
##### List items in stash
```shell
git stash list
```
##### Restoring stash to go back to previous working state
```shell
git stash apply stash@{0}
```
##### Delete stash after restoration or after it is no longer necessary
```shell
git stash drop stash@{0}
```
##### Delete most recent stash
```shell
git stash pop
```

---
### Undoing things
---

##### Remove a staged file
```shell
git reset HEAD file
```
##### Edit the message of last commit
```shell
git log
git commit --amend -m "Message"
git log
```
##### Add additional files
```shell
git status
git add file.ext
git commit --amend -m "Message"
git status
git log
```
##### Reverting a file to the last commit
```shell
git status
git checkout HEAD file.ext
git status
```
##### Discard all local changes
```shell
git status
git reset --hard HEAD
git status
```
##### Discard all local changes
```shell
git checkout -- .
```
##### Revert a commit (ex: 1234abcd, first 8 from commit uid)
```shell
show log
git show 1234abcd
git revert 1234abcd
git log
git log -p
```
##### Reset a commit (ex: 1234abcd, first 8 from commit uid)
```shell
git reset --hard 1234abcd
git log
```

---
### Tags
---

##### Show a list of tags
```shell
git tag
```
##### Create a tag of current branch (ex: 1.0.1)
```shell
git tag 1.0.1
```
##### Create an annotated tag
```shell
git tag -a 1.0.1 -m "Message"
```
##### Show which commit is using that tag
```shell
git show 1.0.1
```
##### Tag an older commit (ex: 1234abcd, first 8 from commit uid)
```shell
git tag -a 1.0.1 1234abcd -m "Message"
```
##### Remove a tag
```shell
git tag -d 1.0.1
```

---
### Working with Remotes
---

#### Adding remotes
##### List remote servers
```shell
git remotes -v
```
##### Connect one or more additional remote servers to local repo
```shell
git remote add origin http://domain/namespace/repo.git
```

---
### Pushing
---

##### Publishing a local branch on the remote origin for the first time (-u add tracking)
```shell
git push -u origin branchName
```
##### Verify branches (ex: -vva, show tracking)
```shell
git branch -vva
```
##### Pushing once the origin is being tracked
```shell
git push
```

---
### Fetching and Pulling
---

##### Fetch pulls information on changes
```shell
git fetch origin
```
##### Pull pulls information and integrates changes in local repo
```shell
git pull origin master
```
##### Prune local references to remotes that no longer exist 
```shell
git fetch -vp origin
```
##### If the branch has tracking enabled
```shell
git pull
```
##### Creating a local brach from a remote branch
```shell
git checkout --track origin/branchName
```

---
### Rebase
---

### Rebasing is like a merge but removes all merge history and rewrites the commits so it looks like all the commits were created on a single branch. 
#### (Warning: Never rebase commits AFTER they have  been pushed. Other developers will not be able to base their work off of it. Only use rebase on local commits BEFORE they are pushed.)
##### Switch to receiving branch
```shell
git checkout master
```
##### Rebase with branch to merge
```shell
git rebase branchName
```

---

### Branch Manipulation 

---

#### Overwrite a branch on the local machine with the branch on the master.
##### Good for when things change on your local system but you don't want to keep the changes.

```shell
git fetch --all
git reset --hard origin/master
```

##### To save the local changes into a new branch before overwrite run:

```shell
git checkout master
git branch new-branch-to-save-current-commits
git fetch --all
git reset --hard origin/master
```

#### Create new repository from existing files

```shell
git init
git add .
git commit -m "Fresh Upload"
git remote add origin http://domain/namespace/repo.git
git push origin master
```

---

### Gitlabs instructions for creating and cloning repositories

---

##### Git global setup

```shell
git config --global user.name "First Last"
git config --global user.email "First.Last@domain.com"
git config --add core.sharedRepository group
```

##### Create a new repository

```shell
git clone http://domain/namespace/repo.git
git clone git@domain:namespace/repo.git
```

##### Ignore self signed certificates
```shell
git -c http.sslVerify=false https://domain/namespace/repo.git
GIT_SSL_NO_VERIFY=true git clone https://domain/namespace/repo.git
```

```shell
cd repo
touch README.md
git add README.md
git commit -m "add README"
git push -u origin master
```

##### Existing folder or Git repository

```shell
cd folder
git init
git remote add origin http://domain/namespace/repo.git
git push -u origin master
```

---

### Bashrc scripts to make life easier

---

```shell
function gitacp() {
    git add .
    git commit -a -m "$1"
    git push
}

function gitfrc() {
    BRANCH=`git branch | grep "*" | awk '{print $2}'`
    echo "Overwriting $BRANCH"
    git fetch --all
    git reset --hard origin/$BRANCH
    git clean -dn
    git clean -dfx
    git pull
}

export GIT_SSL_NO_VERFY='false'   #This will set it so that ALL Clone commands ignore the ssl verification... use with care.

```

##### Usage:

```shell
gitacp “These are new changes”
gitfrc
```

---

### Advanced (Can Be Very Dangerous)

---

##### Permanently remove file or folders from all commits and branches

```shell
git gc
git count-objects -v

git filter-branch -f --tree-filter 'rm -rf folder/folder/*' HEAD

git for-each-ref --format='delete %(refname)' refs/original | git update-ref --stdin
git reflog expire --expire=now --all
git gc --prune=now

rm -Rf .git/refs/original
rm -Rf .git/logs
git prune --expire now

git gc
git count-objects -v

git push origin --force --tags
git push origin --force --all
```
