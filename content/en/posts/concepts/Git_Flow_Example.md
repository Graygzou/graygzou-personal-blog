---
Title: Git Branching Flow
Description: TODO
Date: TODO
tags: ["git", "branching"]
draft: true
---

## Before even cloning the repository

## Cloning the repository

## Workflow
### Programmers
#### Master branch (mainline) `PUBLIC` `Protected`
- Description: At any time, the master branch contains a stable state of the project. 
You should be able to build from it, all tests must pass and no errors should be visible (at least crash errors or serious bugs that stop the game entirely. *Hotfix branches* are here for what's left)
- Constraints: This branch is protected. This mean, unless you have a specific role in the project, you should not be able to commit, merged, revert, etc. directly from this branch.
Only certains persons will be able to access this branch. In most cases, you should never interact with it directly anyway.
- Input branches: *Release branches* and *Hotfix branches* will be `merged` into this branch.
- Output branches: *Hotfix branch*.
#### **Development branch** (develop) `Public`
- Description: This branch replace the *Master branch* in the daily development process.
Just like the *Master branch*, you should be able to build from it, all tests must run, etc. 
But some deeper errors that hasn't been found can be discover here (we're still humans). *Hotfix branches* will take care of that.
- Constraints: Before merging any features or bugfix into this branch, you should be sure the project is stable (see above).
- Input branches: *Feature branches* and *Release branch* will be `merged` into it.
- Output branches: *Hotfix branch*.
#### **Feature branch** (feature/xxxx) `Public` 
- Description: This branch is made to work on a features of the project. Since you might not be the only one working on the feature before his final state, you should be careful of what you do. The historic of a feature should be one straight line.
- Constraints: Todo

### Artists
TODO

<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="Licence Creative Commons" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br />Ce(tte) œuvre est mise à disposition selon les termes de la <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">Licence Creative Commons Attribution - Pas d’Utilisation Commerciale - Partage dans les Mêmes Conditions 4.0 International</a>.
