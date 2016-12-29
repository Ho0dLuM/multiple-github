# Managing Multiple Github Accounts

This post will guide you through setting up and managing multiple Github accounts from one computer. We will be configuring and using ssh to accomplish this.

> _Note: This tutorial is for Unix and Linux users._

## Set Up SSH Keys
Let's say we are setting up these two Github accounts for _WORK_ and _PERSONAL_.

We will need to create our two SSH keys, and save them each to a separate file:

> _Note: The names for the files in the following block do not have to be WORK or PERSONAL, the names can whatever you want them to be. Just remember to substitute the names when you are following along._

```
1. $ cd ~/.ssh
   * If no .ssh file exists in your /home directory, go ahead and create that directory with:
     $ take .ssh (Mac)
     $ mkdir .ssh && cd .ssh (Linux)
2. When you're prompted to "Enter a file in which to save the key" use the same name as during the command, WORK or PERSONAL.
3. When you're prompted to "Enter a password", this is to protect the private key that is generated. Press enter to skip (not recommended) or choose a password. If you try to access that private ssh key it will prompt you for the password you chose when you created it (Do not share your Private Key).
4. $ ssh-keygen -t rsa -b 4096 -C WORK
5. $ ssh-keygen -t rsa -b 4096 -C PERSONAL
```
The above commands will create the following files in the .ssh folder:

* WORK
* WORK.pub
* PERSONAL
* PERSONAL.pub

Open the WORK.pub and PERSONAL.pub files in a text editor.

## Add the keys to your Github accounts:

1. Sign in to one of the accounts
2. Navigate to your account settings
3. Click on "SSH and GPG keys"
4. You will see two boxes "SSH Keys" and "GPG Keys", both boxes will have buttons in the upper right,  click on "New SSH key"
5. Give your key a title so you know which computer you are referencing.
6. Copy the file contents from WORK.pub or PERSONAL.pub into the space labeled "Key" on Github.
7. Repeat steps 1 - 6 for the other Github account, using the other ssh key.

## Create configuration file to manage the separate ssh keys

> _Note: You will need to be inside the .ssh directory._

__Create Config File__

```
1. $ touch config
2. open config file in a text editor
```

__Edit Config File__

```
#PERSONAL account
Host github.com-PERSONAL
  HostName github.com
  User git
  IdentityFile ~/.ssh/PERSONAL

#WORK account
Host github.com-WORK
  HostName github.com-WORK
  User git
  IdentityFile ~/.ssh/WORK
```

This is how your config file inside the .ssh directory should look.
