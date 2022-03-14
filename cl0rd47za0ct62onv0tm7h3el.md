## Home git server

Probably you use [git](https://git-scm.com/) repository hosted by [Github](https://github.com/), [GitLab](https://about.gitlab.com/) or another third-party service.

In some cases like privacy, speed,  you would like to host a git server at home, and I'm not talking about GitHub Enterprise ;) A simple solution like [Gitea](https://gitea.io/en-us/) or [OneDev](https://code.onedev.io/) exists and will provide "GitHub like" experience.

But in my opinion for single user/home lab, they are overkill. As it turns out to have git server you only need git and ssh. I'll show a simple setup of a home git server that will work great, of course without WebUI, PR, Actions, stars and social aspects,  just a plain repository server.

## Hardware/platform

For my server, I use [NanoPi NEO3](https://www.friendlyelec.com/index.php?route=product/product&path=69&product_id=279) SBC connected to my LAN with [DietPi](https://dietpi.com/) running just git and OpenSSH. 

DietPi is based on Debian/Ubuntu but this tutorial will be distribution agnostic and should work as long git and ssh server are there.

## Setup

First login to your remote machine over SSH, from now on all commands are executed on a remote machine that will be git server.

### Let's configure Git as a new shell

```
sudo echo `which git-shell` >> /etc/shells
```

`git-shell` is a limited shell that will be used for our new user as he doesn't need many privileges on this machine. 

Your list of shells should look something like this now:

```
$ cat /etc/shells 
# /etc/shells: valid login shells
/bin/sh
/bin/bash
/usr/bin/bash
/bin/rbash
/usr/bin/rbash
/bin/dash
/usr/bin/dash
/usr/bin/git-shell

```

### Create new user

```
sudo useradd -r -m -U -d /home/git -s /usr/bin/git-shell git
```

A new user will be created, with `git-shell` as shell and `/home/git` as home directory. No password was set as the login will be possible only using the ssh keys.

### Setup new user

Usually, on this point, you will do `su - git` and do the configuration as git user, but since `git-shell` was used we can't do it and need to use sudo a few more times.

```
sudo cd /home/git
sudo rm -rvf .*
sudo mkdir .ssh && chmod 700 .ssh
sudo touch .ssh/authorized_keys && chmod 600 .ssh/authorized_keys
sudo chown -R git:git /home/git
```

Now we need to copy our public ssh key from the client machine to `.ssh/authoized_keys` to make this setup usable. This can be done using `vim /home/git/.ssh/authorized_keys` and pasting public keys, more keys can be added in separate lines to provide collaboration or use different keys from different client machines.

`/home/git/` directory at this stage.
``` 
root@nanopi3h1:/home/git# ls -lRa
.:
total 12
drwxr-xr-x 3 git  git  4096 Mar 14 18:07 .
drwxr-xr-x 4 root root 4096 Mar 14 17:57 ..
drwx------ 2 git  git  4096 Mar 14 18:14 .ssh

./.ssh:
total 12
drwx------ 2 git git 4096 Mar 14 18:14 .
drwxr-xr-x 3 git git 4096 Mar 14 18:07 ..
-rw------- 1 git git  107 Mar 14 18:14 authorized_keys
```

### More setup

Now we need a way to create new repositories.

```
sudo mkdir /home/git/git-shell-commands 
sudo mkdir /home/git/repo

sudo ln -s /home/git/repo /repo
chown -R git:git /home/git/repo
```

This will create two directories. `/home/git/git-shell-commands` will be used to store additional git commands. `/home/git/repo` will be used to store repositories. I also created a symbolic link with the name `/repo` just for convenience. 

###  Repository creation command

Use `vim /home/git/git-shell-commands/newrepo` to create new file

```
#!/bin/sh
mkdir -p /repo/$1
cd /repo/$1
git init --bare
```

At the end execute to make this script executable.

```
chmod +x /home/git/git-shell-commands/newrepo
chown -R git:git /home/git/repo
```

This is a very, very short version of the script that will create a new repository. Please check out this repository to get better scripts.

%[https://github.com/git-utilities/git-shell-commands]


### Repository creation

At this point in time, your server should be ready for your first repository. Usually this means that you need to log in with *git* user to your server and execute the following commands:

```
ssh git@gitserver 
$ cd /repo
$ mkdir project.git
$ cd project.git
$ git init --bare
Initialized empty Git repository in /repo/project.git/
```

But as we use `git-sell` this will not work ;) and it should stay that way. 

The only command that needs to be executed to create a new repository, and made from the client workstation is this one:

```
ssh git@gitserver newrepo testrepo.git
Initialized empty Git repository in /repo/testrepo.git/
```

Simple one line, as ssh keys are used there is no need to use the password for login in. This way remote repositories can be created in a simple and elegant way.

```
❯ git clone git@gitserver:/repo/testrepo.git
Klonowanie do „testrepo”...
warning: Wygląda na to, że sklonowano puste repozytorium.

❯ cd testrepo/
❯ touch README.md
❯ git add --all
❯ git commit -m "initial commit"
[master (zapis-korzeń) 35ac541] initial commit
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 README.md

❯ git push
Wymienianie obiektów: 3, gotowe.
Zliczanie obiektów: 100% (3/3), gotowe.
Zapisywanie obiektów: 100% (3/3), 223 bajty | 223.00 KiB/s, gotowe.
Razem 3 (delty 0), użyte ponownie 0 (delty 0), paczki użyte ponownie 0
To gitserver:/repo/testrepo.git
 * [new branch]      master -> master

❯ 

```

Will clone this repository to the client machine

### Final word

This is a simple and convenient setup for the home git repository. 

Some additional steps like adding `no-port-forwarding,no-X11-forwarding,no-agent-forwarding,no-pty` to `.ssh/authorized_keys` or limit clients/useres that can actually connect to this server will be grate idea. 


## Classic way of settings thing up

You can search for `git server setup` and get a lot of tutorials on how to setup one. I started some time ago with this one [https://git-scm.com/book/en/v2/Git-on-the-Server-Setting-Up-the-Server](https://git-scm.com/book/en/v2/Git-on-the-Server-Setting-Up-the-Server). Nice and clean setup with some additional steps. It evolved a little bit by changing the way the user is created and started right away with `git-shell`.



## Links

- https://git-scm.com/book/en/v2/Git-on-the-Server-Setting-Up-the-Server
- https://git-scm.com/docs/git-init
- https://github.com/git-utilities/git-shell-commands
























