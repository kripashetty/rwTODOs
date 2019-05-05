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
