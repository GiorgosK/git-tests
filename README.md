# git-tests
testing git commands

## Clone repo

Choose way to clone the repo (https or ssh) https is easier but need to use your password any time you push or pull but ssh has a complicated setup so we go with https for now 

```
git clone https://github.com/GiorgosK/git-tests.git
```

Get into the project folder
```
cd git-tests
```

open project in your favorite editor
```
code .
```

VSCode has a nice integration with git and gives you nice indications of git status and changed lines (helps a lot).  To be fair other editors probably have tight git integration !!!

## Make changes, commit, push

Make changes in any file and see what files have changed
```
git status
```

Add ALL (*) changes to stage (get ready for commit)

```
git add *
```

Commit your changes
```
git commit -m 'Change to gk1.txt
```

Push all your changes to origin/master
```
git push origin master
```

## Working with branches 

What branch are you on ? 
```
git branch
```

Create new branch to work on and and move to it
```
git branch feature-2
git checkout feature-2
```

Note: Previous 2 steps can be done with one command 
```
git checkout -b feature-2
```

Check with branch you are on ? 
```
git branch
```

Make changes to an existing file or new file and commit 

```
git add *
git commit -m 'Finished feature-2'
```

Check the git log
```
git log
```

Move to master branch and the git log is different
```
git checkout master
git log
```

Merge changes from feature-2 and check log
```
git merge feature-2
git log
```

## Changing history when things go wrong

Go back 1 commits (change number for more commits)
```
git reset HEAD~1
```
It will give you back your changes but they will not be committed 

Correct the mistake and do a new commit
```
git add *
git commit -m 'Finished feature-2'
```

Push your changes to repository (assumes origin/master)
```
git push
```

## Simple merge with conflict resolution

Make a change to feature-2 and commit
```
git checkout feature-2
/// make change to a file
git add *
git commit -m 'Change to gk1.txt on feature-2'
```

Simulate another user and change the same file on another branch
```
git checkout master
/// make changes to same file as above
git add *
git commit -m 'Change to gk1.txt on feature-2'
```

Now try to merge your changes from feature-2
```
git merge feature-2
```

The merge is pending and gives you the following message
```
Auto-merging gk1.txt
CONFLICT (content): Merge conflict in gk1.txt
Automatic merge failed; fix conflicts and then commit the result.
```

Open conflicting file should look like this
```
gk 1
gk 2
gk 3 feature-2
<<<<<<< HEAD
gk 4 master
=======
gk 4 feature-2
>>>>>>> feature-2
```

Remove instructions put lines and perhaps put lines in order and save file.  The file should look like this on save

```
gk 1
gk 2
gk 3 feature-2
gk 4 master
gk 4 feature-2
```

Add file to staging (ready to commit) and continue merging and check status in between if you want (not needed)
```
git status
git add gk1.txt
git status
git merge --continue
```

Default cli editor (nano, vim, vi etc) will open up with default commit message, change message if you want and save file and exit editor

check status and log and push to origin/master

```
git status
git log
git push
```

## Pull latest changes

Go to github interface and make changes to a file.  Go to file and click pencil for editor.  After changes you can commit using the editor giving a commit message.

Go to your command line and pull the latest changes
```
git pull origin master
```

## Usual workflow of working in a team

Get latest changes from most up to date repo/branch (source of truth)
```
git pull origin master
```

Create a new branch from latest changes and move to it to start working
```
git checkout -b feature-2
```

Make your changes and commit
```
git add *
git commit -m 'Implement feature-x'
```

Push your current branch 
```
git push origin HEAD
```

Go to the github interface and create a pull request into the master branch (or any other source of truth branch the team has agreed to use)

The pull request will be handled by a different team member which will review the changes, might need to resolve conflicts and merge your change or might ask for modifications

