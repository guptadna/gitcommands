Git commands
=====

***Check if ssh is already present***
```
ls -al ~/.ssh
```

***Generating the SSH keys***
```
ssh-keygen -t rsa  // will generate ~/.ssh/id_rsa.pub and linked with already

ssh-keygen -t rsa -C "workmail@gmail.com" -f "id_rsa_work"

```

**Make sure ssh agent is running**
```
eval "$(ssh-agent -s)"
```

***Register the new ssh key***
```
ssh-add ~/.ssh/id_rsa
ssh-add ~/.ssh/id_rsa_work
```

***Copy ssh key public***

```
pbcopy < ~/.ssh/id_rsa.pub
```
***Paste ssh key***

User Account --> Settings --> SSH and GPC key --> New SSH Key 

***Config***
```
cd ~/.ssh/
touch config           // Creates the file if not exists
code config            // Opens the file in VS code, use any editor
```

***Config git***

```
git config --global user.name "John Doe"
git config --global user.email johndoe@example.com

git config --list
```

**Multiple SSH Account**
```
##Office account - the default 
Host github.com
   HostName github.com
   User git
   IdentityFile ~/.ssh/id_rsa

#Personal account - rdntech14
Host rdntech14github.com
   HostName github.com
   User git
   IdentityFile ~/.ssh/id_rsa_rdntech14
```

***to access any git repo using *the default* config***

```
git clone git@github.com/<whateverusername>/<RepoName>.git
```
***to access any git repo using *rdntech14 or non default* config**

```
git clone git@<hostname defined under rdntech14 in config>/<whateverusername>/<RepoName>.git
git clone git@rdntech14github.com/rdntech14/<RepoName>.git
```


***One active SSH key in the ssh-agent at a time***

ssh-add -l will list all the SSH keys attached to the ssh-agent
```
ssh-add -D            //removes all ssh entries from the ssh-agent
ssh-add ~/.ssh/id_rsa                 // Adds the relevant ssh key

ssh-add -D
ssh-add ~/.ssh/id_rsa_work
```


***Common Error***

```
The authenticity of host 'domain.com (a.b.c.d)' can't be established.
RSA key fingerprint is XX:XX:...:XX.
Are you sure you want to continue connecting (yes/no)?
```
***Solution*** 
We need to add host key to known_hosts file. Following command add automatically.
```
ssh-keyscan -t rsa github.com >> ~/.ssh/known_hosts
```
***few basic command***

```
git reset --hard HEAD  -------Discard all local changes in working directory
git reset --hard origin/master  -------Discard all local changes in working directory
git checkout master -- set pointer to local master
```




I forked a GitHub repo thoughtbot/dotfiles to croaky/dotfiles and want to keep it updated.

Add upstream to git clone fork

git remote add upstream git@github.com:thoughtbot/dotfiles.git

Rebase local upstream/master

```
git fetch upstream
git rebase upstream/master
```

Commit local upstream to remote upstream, usually we will not have right access.

```
git checkout -b upstream upstream/master
```

Git fetch - bring changes from remote branches to local remote branches but does not impact local local( heads) branches. 

Git pull = git fetch + git merge

Git merge —> this will update local 
Copy.

Only bring remote repo changes into remote snapshots, does not effect local copies. 

```
Git fetch origin
Git fetch upstream
```

Git fetch will download changes to remote but will not uodate working copy ( safe)

Git pull will download changes to remote and update working copy also. Has to deal with merge conflicts.

******************************

```
git log
```

**How to delete last two pushed commits**

```
git reset HEAD~2 --hard
git push --force
```










612  git clone https://git.com/user/projectname.git
613  git remote -v
614  pwd
615  cd mountebank
616  git remote -v
617  git remote add upstream https://git.com/Mian/projectname.git
618  git remote -v
619  git add .
620  git commit -m "AG | my first commit"
621  git status
622  git push
623  history


git branch
git branch <branchName>
git checkout <branchName> -- set pointer to local branch
git checkout master -- set pointer to local master
git diff  --> shows changed files
git branch -d <branchName>   # to delete a branch

git add <fileName>
git rm <fileName>

git reset --hard ----- to reset staging and local copy to recent commit changes
git reset --hard HEAD  -------Discard all local changes in working directory
git reset --hard origin/master  -------Discard all local changes in working directory

git branch -r   -- To know branches on remote

git checkout --> shows the changed files

git remote -v
How to reset Git local brach with upstream or origin
**************************** Reset local master with upstream/master ****************************
git checkout master
git reset --hard upstream/master


**************************** Git process Work flow  ****************************



1) main branch
```
https://git.com/Main/projectname.git
```
2) Create a fork off main branch from git GUI

3) clone fork on local
```
git clone https://git.com/user/projectname.git
```
4) Add main branch to local master as upstream
```
git remote add upstream https://git.com/Main/projectname.git
git remote -v
```

5) Create a new branch off local master
```
git branch <featureBranch>
git checkout <featureBranch>
```

6) Update code ( fix problem or enhance functionality) in local branches and add it to stag
```
git checkout <featureBranch>
git status
git add <changedFiles>
git commit -m "Updated readme"
```

7) Checkout to master branch and Pull upstream changes to local master ( if someone has committed new changes)
```
git checkout master
git pull upstream master

or

git fetch upstream
git checkout master
git merge upstream/master

```

8) Push upstream changes to Remote Fork ( so upstream, fork master, local master can be insync)
```
git push
```

9) rebase local master with branch
```
git rebase master <featureBranch>

or

or git checkout <featureBranch>
git rebase master
```

10) push local branch to origin as new branch

```
git push -u origin <featureBranch>
```

11) Create pull request based off <featureBranch>


******************** how to update fork ****************************

```
git clone  https://git.com/user/projectname.git
cd LiftOff-ProcessEngine/
git remote add upstream https://git.com/Main/projectname.git
git remote -v
git pull upstream master
git remote -v
git push

```
******************** how to stash commands ****************************

```
git stash save "comments"
git stash list
git stash apply stash@{0}
git stash drop stash@{0}
git stash pop  # apply and drop stash at the same time

```
