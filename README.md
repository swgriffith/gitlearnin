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

In this case we want to push our branch with it's changes up to github, so we'll run the following and when prompted enter our github credentials. 

**Note 1:** We'll come back to the credentials discussion, but use login and password for now.
**Note 2:** If you're not a collaborator on a remote repository, you cannot push to it. You will get an error.

```
#git push <remotename> <branchname>
git push github griffithmods
```

Now go take a look at your remote repository (i.e. GitHub or Azure DevOps) and see if your new branch is available in the branches list.

## Credentials
Entering your UserID and password may be a bit tedious on every remote repository push. Fortunately there are a few options to solve this pain.

1. Use credential manager
2. Use an SSH Key pair for authentication and SSH cloning instead of HTTPS cloning


### Using Credential Manager

### Using an SSG Key Pair
By generating an SSH key pair by using a tool like ssh-keygen, you can share your public key with your remote (i.e. GitHub or Azure DevOps). This key pair can be generated with or without a passphrase, although with is recommended. If you pull via the SSH endpoint rather than via the HTTPS endpoint, when you push git will attempt to use your ssh key to authenticate with the remote. If you've added your public key then you'll be able to push without entering a user ID and Password.

Using ssh-keygen from Linux, Mac or Windows Subsystem for Linux should look like the following. Again, entering a passphrase is recommended.

```
ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/home/steve/.ssh/id_rsa):
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /home/steve/.ssh/id_rsa3.
Your public key has been saved in /home/steve/.ssh/id_rsa3.pub.
The key fingerprint is:
SHA256:ubvUzxiRQd9Sj076+ZUv23GD5Af0bvagTah4mf5dsZ0 steve@griffith
The key's randomart image is:
+---[RSA 2048]----+
|          .   .  |
|         . . o o |
|          . o.+ .|
|         . o.=.  |
|        S o .o.o |
|         o .oo+.*|
|        o oo.o=E=|
|       . o+* ===B|
|        +++.= +o=|
+----[SHA256]-----+
```

The above process will create a new folder under /home/<username>/.ssh which contains the following files:

* **id_rsa** - File containing your private key
* **id_rsa.pub** - File containing your public key
* **known_hosts** - File tracking connections you've made to various hosts and which ssh-key was used


Grab the full contents of the id_rsa.pub files either opening the file or using cat on linux.

```
cat ~/.ssh/id_rsa.pub
ssh-rsa AAAA<BUNCH OF TEXT I REMOVED>EYM2Xj steve@griffith
```

Got do your remote repository, and add the ssh key for your user.

1. GitHub - You can find this by clicking on your user profile and going to 'Settings -> SSH and PGP Keys'
2. Azure DevOps - You can find this by clicking on your user profile and going to 'Security -> SSH Public Keys'

In either case you'll want to come up with a name for your key that represents where you're using it from (ex. Azure Cloud Shell, Windows PC, etc)

Once saved, you can now use the SSH endpoint for git clone and ssh for pushing to git remotes without user ID and password.
