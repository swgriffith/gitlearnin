# gitlearnin

## Initial Setup
https://git-scm.com/downloads

Check the current settings
```
git config --global --list
```

**Note:** You can also use --local to see the settings for a given repository, or leave it off to see ALL settings relevant to the current repository (global and local)

```
git config --global user.name "Steve Griffith"
git config --global user.email "stgriffi@microsoft.com"
```

## Setting your default editor
Many activities you do in git may pop you into an editor (ex. commits, diffs, etc). Git will use your system default editor, but you may want to change this as follows:

```
#Ex. Using Nano for linux or WSL
git config --global core.editor nano
```

## Cloning and Existing Repo
```
git clone https://github.com/swgriffith/gitlearnin.git
```

Now you have a local working copy of the repository that you cloned. You can do whatever you want with this copy, but need to be mindful of what you do if you intend to push back to **origin**. 

## What is origin?
Origin is the default name for the remote repository you cloned from. You can see your origin using the following:

```
git remote -v
```
You can rename your origin as well:

```
#git remote rename <originalName> <newName>
git remote rename origin github
git remote -v
```

**Note:** This name will be used when you interact with the remote repository for pushes.

## Branches
Branches allow you to work on various changes locally at the same time without them overlapping. To switch between branches you use **checkout**. For example, if you have 2 hot fixes you need to apply you can create a branch for each and swap back and forth between them without any conflict, until you're ready to push them to your origin.

**Note:** On your first check-in a 'master' branch is created for you automatically. **General best practice is to avoid making changes directly in master**

You create a new branch as follows:
```
git branch griffithmods
git checkout griffithmods
# or

git checkout -b griffithmods
```

You can delete a branch as follows:
```
git branch -d griffithmods
```

## Making changes
Once you've cloned a repository, created a branch and checked it out, you're ready to work. Create a new file within the cloned folder named <yourlastname.txt> and in that file enter the text 'commit1'.

This file is now in your folder, but has not been added to the repository. You can see this by trying to commit your change.

```
git commit -m "commit1" .
On branch griffithmods
Untracked files:
	griffith.txt

nothing added to commit but untracked files present

```

In order to commit this new file we need to add it to the repo:

```
git add griffith.txt
```

We're now ready to commit our change to the current branch. Every commit requires a comment be added. You can do this either in line, or git will bring up your editor to enter your commit message.

**Note:** This will commit all staged files. If you want to commit a single file you can name that file at the end of the command (ex. git commit griffith.txt). 

```
git commit -m "Added new file griffith.txt"
# or 
git commit
```

## Pushing to your remote repository (i.e. GitHub or Azure DevOps)
You can push to any remote repository you have listed when you run the following:
```
git remote -v
```

In this case we want to push our branch with it's changes up to github