---
Title: "Git Cheat Sheet"
Description: TODO
date: 2020-04-11T18:26:10+02:00
tags: ["raspberry-pi", "git", "troubleshootings"]
draft: true
---

# How to set a central repository in Git

### Background story
TODO ?

## Getting started
In the folder you want your central repository run :
```
$ git clone --mirror git@github.com:host/path/to/repo.git   # Create a bare repository from which you can update the origin one.
```
In the folder where you will make a local copy or the central repository and start working, run this command :
```
$ git clone <username>@<server-adress>:/path/to/central/repo.git   # Clone a copy from the central repository.
```
Basically, this will make a ssh connection with the server and apply the git command which is `git clone` in that case.

And you're good to go !

## Command on the bare repository
When you commit a lot of changed in your central repository and you're happy about the historic, you can run the following command:
```
$ git remote update
```

## Setting up the client repository
Since you make an ssh connection every time you execute a git command, you will enter your server password a lot of times, aka
```
$ git push
<username>@<server-address>'s password: 
``` 
If you're fine with that, don't bother with this section. But if you find it annoying you can solve it.

##### Share a passphrase with the server
In order to avoid entering your password, you will have to generate a passphrase.
But if you do not have one yet, this can be done using the following command.
```
$ ssh-keygen -t rsa -b 2048
```
Follow the prompted instructions it's recommanded to use a passphrase and not leave it empty.

Once you've done it, you have to share it with the server.
You can do that with :
```
$ ssh-copy-id <username>@<server-address>
```
You will have to enter your password in order to log in the server.
You can then log in the server and check the authorized_keys to see if the new one is added :
```
$ ssh '<username>@<server-address>'
$ cat .ssh/authorized_keys
```
##### Use `ssh-agent` to store the passphrase for us
If you entered a passphrase in the `ssh-keygen` step, you should have the same problem that before.
But instead of a password, it's now a passphrase that is required !

So we did not went far on our problem.

But luckily for us, there is a deamon that can helps us with passphrase : `ssh-agent`
You can make sure your agent is running with (it will start it it if not already running) :
```
$ eval `ssh-agent -s`         # Start the ssh-agent
Agent pid 7716
```
You only have to run the following command :
```
$ ssh-add path/to/key
```
It will prompt you to enter your passphrase.    And just like with the password, **you're done** ! 🎉

You can make a test and run `ssh '<username>@<server-address>''` to test if it works.  
You should, in theory, not have to enter any passwords or passphrase !

*Note*: You can also run the below commands to make sure the `ssh-agent` has the right identities:
```
$ ssh-add -l
$ ssh-add -L
```

### Remove a ssh key added
You might have add a ssh key that wasn't the one you wanted to use for that server.
To fix your mistake, you can remove the desired key in the file `known_hosts` and `authorized_keys` with:
```
sed -i 'Xd' <filename>      # remove the `X` th line from the file.
```

### Useful commands
* You can check information about the remote url you can run the following command
```
git config --get remote.origin.url    # Return the remote url
git remote show origin                # Show the full output about remote stuff
```

* You have a lot of control on the `ssh-agent`. You can for example specify the lifetime of identities it hold with
```
$ ssh-agent -t 1d   # the agent will remember identities for a day
$ ssh-add -t 1D     # the agent will remember identities for a day
```

## Using [Fork](https://fork.dev/)
This can be also be accomplished quite easily with Fork git client.
All you have to do is :
1. `File` > `Configure SSH Keys...`
2. In the dropdown menu, select the keys you want to use for this repository. You can also generate a new one if you wish.
3. When making a server command, you will have a prompt to emter your passphrase.
4. Once enter, you should be able to make other server commands without worrying about it again.


## Aknowledgements
* [ ] [git clone command - Git docs](https://git-scm.com/docs/git-clone)
* [ ] [remote url - StackOverflow](https://stackoverflow.com/questions/4089430/how-can-i-determine-the-url-that-a-local-git-repository-was-originally-cloned-fr)

* [ ] [ - serverfault.com](https://serverfault.com/questions/241588/how-to-automate-ssh-login-with-password)