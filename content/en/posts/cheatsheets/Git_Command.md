---
Title: Git Basic Commands
Description: TODO
date: 2020-04-11T18:26:10+02:00
tags: ["git"]
draft: true
---

# Useful commands
## Clone a repository
### For the first time
When you clone a repository, Git automatically adds a shortcut called origin that points back to the “parent” repository. Just run:
```
git clone git@github.com:host/path/to/repo.git    # Good ! Don't forget to add your ssh keys to your github to make it work.
or
git clone https://user@host/path/to/repo.git  # https but it's not safer than ssh.
```
#### Problems
> When I run the clone command with the ssh, I have the following error:
> ```
> fatal: Could not read from remote repository.  
> Please make sure you have the correct access rights
> and the repository exists
> ```

If you encounters problems with the ssh, do not directly go to the https ! Try adding your ssh key to your ssh agent by running:
```
$ ssh-add ~/.ssh/id_rsa  # For Mac, you need to add a -K option after the ssh-add command.
```
For more information check out this [link](https://help.github.com/en/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent).

> The historic of the project is waaaaaay too big that the cloning it takes forever.
> Plus it might fill my drive !

I you feel that you don't need the full history right now, you can use the `--depth <depth>` option in order to truncated the history.
It will create a shallow clone with the history truncated to the specified number of commits.
```
git clone --depth 5 git@github.com:host/path/to/repo.git    # history truncated with only the 5 newest commits.
```
More can be found [here](https://git-scm.com/docs/git-clone)

### For a second time
You can achieve that by running the following command :
```
git clone --reference ../path/to/root/first/repo --dissociate git@github.com:host/path/to/repo.git
```
The command use the `--dissociate` option. With this option, the new repository made will use the repository specify with the `--reference` option, to borrow objets from it, in order to reduce network transfer. Once the clone operation is done, the two repositories remain **independent** ! Either one can be deleted without impacting the other !

You can also us the `--reference` option without the `--dissociate` one. But keep in mind that it will create dependencies between the two repositories. see NOTE for the `--shared` option in this [link](https://git-scm.com/docs/git-clone).

## Create a branch
```
$ git checkout develop
$ git branch sprint-X/feature-1
$ git push --set-upstream origin sprint-X/feature-1
```

## Pulling work made on the remote 
* If we want to explicitly create a merge commit when pulling :
```git pull --no-ff```
* If you don't want to create a merge commit no matters what :
```git pull --ff-only```

Note: It's a good practice to use the option `--ff-only` without thinking and then decide if we want to merge or rebase if an error shows up.

## Rebase (instead of merge commit)
`git pull --rebase origin master`
* *Explanation(s)*: Rebasing allow to keep a cleaner history for a repository. 
* *Warning*: Use `rebase` only if the changes do not deserve a separate branch.

`git rebase --abort`
* *Explanation(s)*: Cancel a current rebase.

## Merge branches (instead of rebasing)
`git merge origin/develop`

## Checkout a branch
```
$ git fetch origin
$ git checkout sprint-X/feature-1
```

## Commiting (and pushing)
```
$ git status
$ git diff "Folder/feature-1/script.cs"`
$ git add . --all
$ git commit [-m "this is the commit message"]    # automatically call git gc --auto.
$ git push
```

## Checking the graph of the repository
```
git log --graph   // Built-in
gitk              // Additional software
```

## Acknowledgements
* [Git Clone - Git documentation](https://git-scm.com/docs/git-clone)
* [Adding ssh key to ssh agent - GitHub help](https://help.github.com/en/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
* [StackOverflow - What is the difference between `git merge` and `git merge --no-ff`?](https://stackoverflow.com/questions/9069061/what-is-the-difference-between-git-merge-and-git-merge-no-ff)

<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="Licence Creative Commons" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br />Ce(tte) œuvre est mise à disposition selon les termes de la <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">Licence Creative Commons Attribution - Pas d’Utilisation Commerciale - Partage dans les Mêmes Conditions 4.0 International</a>.
