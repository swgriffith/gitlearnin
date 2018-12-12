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

