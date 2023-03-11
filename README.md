# Git: Get to know the commands
---

## 1. Main Commands

Create Users:
```
git config --global user.name "Marcelo Ribas"
git config --global user.email "marcelo.pachione@icloud.com"
```

Create Folder:
```
mkdir <folder name>
```

Check Status:
Check if there is something new to be committed, and other infos. If the folder you are in still is not a git repo, it tell you also “this is not a git repo”

```
git status
```

Create a Git Repository:
Enter in the folder you want to turn into a git repo and init it =D
```
git init
```

List content of a folder:
```
ls
-- use the -a to show hidden folders
ls -a
```

## 2. First Commit:
First create a .txt or .md file in the folder (manually on the folder or via VIM).
Then add it to the staging area and list of file to be commited, it is not commited to Git yet!

```
git add <file name>
```

Finally commit, adding a -m as comment parameter

```
git commit -m "My first commit"
```

## 3. Staging
Add multiple files to staging.

Before you send something to the external source or to the be latest version of it locally.

```
git add --all
--or
git add .
```

Unstaging

```
git reset HEAD <file name>
```

## 4. Commiting folder

* Git does not track folders
* to track a folder, you must track a file inside it, an can ben an empty file

```
---create folder
mkdir temp
---create an empty file called gitkeep
touch temp/.gitkeep
--- now can add it an commit
```

## 5. Removing file or folder
Remove file

```
rm <file name>
```

Remove folder
```
rm -rf -- <folder name>
```

After this, need to also add to staging and also commit.

Delete is also a git action.

## 6. Ignore file or folder
Lets say I have a private file on a folder:
```
mkdir private
touch private/config.txt
```

After this, if run git status, it will say to git add config.txt If I want my config folder not to be included in any commit or add, for some reason, just need to create a .gitignore file and add the file or folder name inside it.

```
-- create the file
vim .gitignore
```

Add the file name or folder inside the git ignore and save it.
Now run git status, and the folders and files inside gitignore will no longer asked to be git add`.

## 7. Branch
* So far, just used the master branch
* Usually we don’t do that, we create a local or test branch
* Is basically like create a copy of the other repository and start in the copy Create a new branch

```
git checkout -b feature/table
```

Now you can start developing changes in your files in a different branch.
You can add theses changes and commit them, without changing the master.
To change between branches:

```
-- back to master
git checkout master
-- go to branch again
git checkout feature/table
```

## 8. Fast Foward Merge Branches
After working in a branch, you may want to discard de work:

```
git branch -D feature/table
```

Mostly, you’d want to merge it in the master/main branch:

* Move to the branch you want the changes to be merged in
* Run merge specifying the branch to merge to the branch you just moved in

```
git checkout master
git merge feature/table
```

If you take a look on git log, it will show a fast foward merge.
It is when the branch you copied to the new branch have not changed since.
When the branch you copied changed, your development branch and that branch are no longe compatible, it leads us to advanced merging.

## 9. Rebase Commit
In case you have the same scenario as before (master changed while working in branch) you can rebuild the branch to be updated with the newest version of your master, and thus have a FAST FORWARD merge:

```
-- go into the branch 
git checkout mybranch/name
-- rebase the branch according to your master
git rebase master
```

Now, when you git add, git commit and git merge, you will have a fast forward merge.

## 9. Merge Conflicts
Conflicts happen in 2 sittuations:

* Merge a branch where the same line you changed in the branch, was also changed in the master after your branch
* Trying to rebase a branch with master, but the same line changed in branch was also changed in the master. It will throw an error where you can’t work anymore, then:
* Abort the rebase or merge

```
git merge --abort
--or
git rebase --abort
```

* Open the file causing the conflict in the master
* you will see the head notation (master) and the branch changed

```
<<<<<<<< HEAD
    original
=============
    Original!
>>>>>>>> Branch
```

* Fix it in the file
* It can be usedul to use an IDE like VS Code to help compare and decide which adjustment to do
* After adjusting the conflict, do a git add, commit and merge!

## 10. Push
```
git add .
git commit -m "your comment"
git push origin master
```

## 11. Delete Branches
```
// delete branch locally
git branch -d localBranchName
// delete branch remotely
git push origin --delete remoteBranchName
// check available branches
git branch
```

## 12 . Clean Changes befores — clean untracked items git
```
git clean -f -d
```