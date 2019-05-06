What is GIT ?
It is a version control System - It wont solve everything but you need to layer processes on top of that , like
  - Branching rules 
  - Code review rules
  - README.md
  - License for the code

It's just a directory with a hidden .git file that tracks all the files in the directory.

# Terminologies

- **DAG** - git stores history of files as a direct acyclic graph of commit hashes
- **Repository** - Directory with files being tracked by git
- **Commit** - Snapshot in time of how your work of the commit tree. Multiple commits happen. 
- **Diff** -  Moving from one commit to another.(Subversion only stores Diff , GIT stores Commits. What is the clever stuff git uses to compress and store so much information.)
- **Branch** -  My version , their version . 2 histories moving along
- **Merge** - Merging 2 histories together.
- **Fork** - get your own version by forking and cloning a remote repository.
- 
# Ways to start
1. Creating a new project
2. Cloning an existing project


# Cloning an existing project
Any system or any server that you have ssh access to can act as the remote repository
Copy the entire Repo (Remote) down to your local machine (clone).i.e you have a copy of the entire history of the repo.

#### Check which version of git
```sh
$ git version
git version 2.17.2 (Apple Git-113)
```
#### Check where git is installed
```sh
$ which git
```
#### Cloning a repository

```sh
$ git clone https://github.com/raywenderlich/rwTODOs.git
Cloning into 'rwTODOs'...
remote: Enumerating objects: 49, done.
remote: Total 49 (delta 0), reused 0 (delta 0), pack-reused 49
Unpacking objects: 100% (49/49), done.
```
#### Forking a repository
```sh
$ git clone https://github.com/kripashetty/rwTODOs.git
Cloning into 'rwTODOs'…
remote: Enumerating objects: 49, done.
remote: Total 49 (delta 0), reused 0 (delta 0), pack-reused 49
Unpacking objects: 100% (49/49), done.
```

#### Check the remote for the repo you just cloned.
```sh
$ cd rwTODOs/
$ git remote -v
origin https://github.com/kripashetty/rwTODOs.git (fetch)
origin https://github.com/kripashetty/rwTODOs.git (push)
```
# Creating a new Repository
```sh
$ mkdir myToDos
$ cd myToDos/
$ git init
Initialized empty Git repository in /.../.git/
$ ls -al
total 0
drwxr-xr-x  3 shetty kripa  BCGCOM\Domain Users   96 May  3 14:46 .
drwxr-xr-x  4 shetty kripa  BCGCOM\Domain Users  128 May  3 14:45 ..
drwxr-xr-x  9 shetty kripa  BCGCOM\Domain Users  288 May  3 14:46 .git
it is good hygine to create a License
$ mkdir myToDos
$ cd myToDos/
$ git init
Initialized empty Git repository in /.../.git/
$ ls -al
total 0
drwxr-xr-x  3 shetty kripa  BCGCOM\Domain Users   96 May  3 14:46 .
drwxr-xr-x  4 shetty kripa  BCGCOM\Domain Users  128 May  3 14:45 ..
drwxr-xr-x  9 shetty kripa  BCGCOM\Domain Users  288 May  3 14:46 .git

```
It is good hygine to create a License, use the below link to choose a Licence
https://medium.com/r/?url=https%3A%2F%2Fchoosealicense.com and add the license text to the new LICENSE file

```
$ vim LICENSE
```
Check Status
```
$ git status
On branch master
No commits yet
Untracked files:
(use "git add <file>…" to include in what will be committed)
LICENSE
nothing added to commit but untracked files present (use "git add" to track)
```

Add the file to the staging area asking git to start tracking it.
```
$ git add LICENSE
$ git status
On branch master
No commits yet
Changes to be committed:
(use "git rm - cached <file>…" to unstage)
new file: LICENSE
````

Now add commit the file giving a high level commit message to help
````

$ git commit
hint: Waiting for your editor to close the file…
Committing the License
# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# On branch master
#
# Initial commit
#
# Changes to be committed:
# new file: LICENSE
````
After commiting , check if there is anything left to commit
```
$ git status
On branch master
nothing to commit, working tree clean
```
Check the last commit with the commit message
```
$ git log
commit fd5490d345dba984a670970769a84e2e3c4a0a59 (HEAD -> master)
Author: Kripa Shetty <abc@gmail.com>
Date: Fri May 3 14:55:26 2019 +0200
Committing the License
````
Changing configuration values per repo or globally
```
$ git config - list
credential.helper=osxkeychain
filter.lfs.clean=git-lfs clean - %f
filter.lfs.smudge=git-lfs smudge - %f
filter.lfs.process=git-lfs filter-process
filter.lfs.required=true
user.name=Kripa Shetty
user.email=abc@gmail.com
core.repositoryformatversion=0
core.filemode=true
core.bare=false
core.logallrefupdates=true
core.ignorecase=true
core.precomposeunicode=true
```
To change user name
```
$ git config user.name Kripa
Check the changes
$ git config - list
credential.helper=osxkeychain
filter.lfs.clean=git-lfs clean - %f
filter.lfs.smudge=git-lfs smudge - %f
filter.lfs.process=git-lfs filter-process
filter.lfs.required=true
user.name=Kripa Shetty
user.email=abc@gmail.com
core.repositoryformatversion=0
core.filemode=true
core.bare=false
core.logallrefupdates=true
core.ignorecase=true
core.precomposeunicode=true
user.name=Kripa
```
You see 2 entries for user.name , one for local and one for global.
Checking local config values 
```
$ git config - local - list
core.repositoryformatversion=0
core.filemode=true
core.bare=false
core.logallrefupdates=true
core.ignorecase=true
core.precomposeunicode=true
user.name=Kripa
```
Checking global config values
```

$ git config - global - list
filter.lfs.clean=git-lfs clean - %f
filter.lfs.smudge=git-lfs smudge - %f
filter.lfs.process=git-lfs filter-process
filter.lfs.required=true
user.name=Kripa Shetty
user.email=abc@gmail.com
````

TLDR; Create the README.md file following the same steps as for the License file. 
Checking the log, notice the change in the user name between the last commit and the previous to last commit.

```
$ git log
commit bca987506696c2796c47433efba500d9d63225b1 (HEAD -> master)
Author: Kripa <abc@gmail.com>
Date: Fri May 3 15:12:38 2019 +0200
adding a README file
commit fd5490d345dba984a670970769a84e2e3c4a0a59
Author: Kripa Shetty <abc@gmail.com>
Date: Fri May 3 14:55:26 2019 +0200
Committing the License
```









## Mastering Git Tutorial
All data is stored in a Blob store as a key value.
Commit is a tre represention all the files in a directory
When u commit , 
Each file -> calculate the SHA-1 hash -> uses it as the key and value is the compressed version of the file.
Branches are cheap to create
<< TBD - Understand this >>
# Merging
- If the same line of code is edited in two branches then git cannot resolve this conflict.
Command to show three way diff, so you know what the common ancestor parent was and the changes from the other 2 brnaches. So you can manually choose what to keep and then delete the rest.
```sh
$ git config merge.conflictstyle diff3
```
To use xcode mergetool
```sh
$ git config merge.tool opendiff
$ git mergetool
```
git mergetool will invoke the merge tool. Use the action options from the dropdown to decide what to keep. Save and quit.
Delete and .orig files and commit the merged.
# Stashing
```
$ git stash
```
```
$ git stash list
stash@{0}: On master: Tools version
stash@{1}: On master: Adding base styling
`````
Stash on the top of the stash stack gets applied but stays on the Stash stack.
```
$ git stash apply 
`````
Second item on the Stash stack gets applied but stays in the Stash stack.
```
$ git stash apply stash@{1}
`````
To view the difference with the stash on the top of the stash stack 
```
$ git stash show -p
diff - git a/.tools-version b/.tools-version
index 7b378be..de28578 100644
 - - a/.tools-version
+++ b/.tools-version
@@ -1 +1 @@
-1.8.4
\ No newline at end of file
+1.7.6
`````
To view the 2nd element on the stack
```
$ git stash show@{1}
`````
To see the difference with the 2nd stash item
````
 git stash show stash@{1} -p
`````
Remove the top of the stack stash
```
git stash pop
`````
Remove the 2nd stashed item from the stack and apply.
```
git stash pop stash@{1}
`````
Give a custom label to your stash
```
git stash push -m 'Label to this stash'
`````
Apply a stash
````
$ git stash apply
````
Revert an stash which was applied
````
$ git stash show -p stash{0} | git apply -R
````
There can be merge conflicts when you pop and appl a stash list item.
Resolve the conflicts as usual but you will notice the stash item does not get deleted from the list. To manually delete the Stash item
````
git stash drop stash@{1}
````
# Aliases
Way of taking a long git command and shortening it.
Its a version of the system wide aliases but localized to git.
```
git config alias.stash-ua '!gitstash show -p | git apply -R'
````
You need to include the !git to indicate that is is a terminal command so that you can use the pipe operator.
Where does this change get saved ? 
In the .git folder there is a config file which has an alias section.
This is a local alias.
````
cat config 
[core]
 repositoryformatversion = 0
 filemode = true
 bare = false
 logallrefupdates = true
 ignorecase = true
 precomposeunicode = true
[branch "master"]
[merge]
 conflictstyle = diff3
 tool = opendiff
[alias]
 stash-ua = !gitstash show -p | git apply -R
````
Creating a Global alias
````
$ git config - global alias.gl 'log - oneline - decorate - graph - all'
````
Where does this live?
Inside your global git config file
````
$ cat ~/.gitconfig 
[filter "lfs"]
 clean = git-lfs clean - %f
 smudge = git-lfs smudge - %f
 process = git-lfs filter-process
 required = true
[user]
 name = Kripa Shetty
 email = kripashetty@gmail.com
[core]
 excludesfile = /Users/shetty_kripa/.gitignore_global
[alias]
 gl = log - oneline - decorate - graph - all
````
# Rebase
powerful concept within git 
alternative to merge
You will be re writing the history on the branch that you are rebasing off of!!!
General rule : dont rebase a brancg that is shared.
When you merge : 
Local - your branch, branch you started on 
Remote - their branch, branch that you are merging into local
You sit on the local branch and merge the remote branch into the local branch
When you Rebase - switching the concepts around.
Local - You are positioned on end of the branch that you are rebasing on top of.
Remote - Replay the commits of the branch that is yours.
eg: rebasing xValidator(your branch) onto wValidator(Some other branch that you originally branched out of)
checkout wValidator and then run the commands
````
git rebase xValidator
`````
Resolve conflicts if any. 
check the status , if nothing is there to commit use the skip command to move on , if there is something to commit use the continue command which is like a commit.
````
git rebase - skip
`````
````
git rebase - continue
`````
# Interactive Rebase
```´
git rebase -i <commitHash of a common ancestor>
`````
Puts you in the interactive mode. File is self explanatory.
Git will go over each of the listed commits and performs the action you have at the start of each commit.


# Git Ignore after the fact
- If the file is in the index then even if you add it to the gitignore file , git will still track it 
- Remove it from the index
- delete it from git 
-
````
$ git update-index - assume-unchanged <fileName>
`````
To check the files int he git index 
````
git ls-files -v
````
The files that is is not tracking , those that it assumes unchanged has a lowercase letter at the beginning
````
git ls-files -v | grep '^[[:lower:]]'
````
To start tracking again.
````
$ git update-index - no-assume-unchanged <fileName>
`````
To make a more global solution , make git remove this file from staging but keeps it in the working directory. But the file still stays in the history
`````
git rm - cached <fileName>
`````
# Cherry picking
Stealing a commit from another branch and adding it to your branch.
Cherry picking will add the commit at the end of your branch.
`````
git cherry-pick <Commit hash to pick>
`````
# Filter branch
WARNING : do this only when you have not shared this branch.
Allows you to programmatically alter history
- remove a secrets file that was accidently committed to master.
- Tree Filter
- EN Filter 
- Commit filter
```
git filter-branch -f - commit-filter '<some bash script to rename the commiter names >'
````
- Index filter - changing each of the staging area
````
git filter-branch - index-filter 'git rm - cached - ignore-unmatch - <FileName>' - prune-empty HEAD
````
prune empty removes the empty branch 
HEAD runs the command on HEAD
Check history of the file
````
git log - <FileName>
```
You should see no history.
# Undo some mess
- Reset - similiar to checkout
 - soft ->
 - mixed -> updated staging , leaves working directory
 - hard -> updates both staging and working directory
```
git reset - hard HEAD
````
Set the HEad to the secondlast commit and remove the last commit
```
git reset - hard HEAD^
````
Undoing reset actions
Look at ref logs , persists the changes zou make
`````
git reflogs
`````
`````
git checkout HEAD@{1}
`````
This results in Detached Head. But zou get the commit back
To move the HEAD to the
`````
git checkout temp
`````
`````
git checkout temp
`````
`````
git reset - hard HEAD@{4}
`````
reset will move master to that particular commit 
Then delete the temp branch
-Revert
Reverting the most reset commit
````
git revert HEAD 
````
Revert the revert, 
````
git revert HEAD 
````


# Tools 
gitk 
git gui


Source tree - atlassian
gitup.co
git hooks
git lfs
submodules subtrees
