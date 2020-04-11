---
Title: "Git Cheat Sheet"
Description: TODO
date: 2020-04-11T18:26:10+02:00
tags: ["git"]
draft: true
---

# Cheat Sheet GitHub

## Git LFS
*Git* can work fine with 3D games out of the box. However the main caveat here is that versioning large (>5 MB) media files can be a problem over the long term as your commit history bloats.
Maybe use *DropBox* for art assets.

## Regular Branching
 * **Development branch** (also called ‘develop’) : This is your main development branch where all the others branches (e.g. feature branches) will be merging into this branch.
 * **Production branch** (also called ‘master’) : This branch represents the latest released / deployed codebase. Only updated by merging other branches into it.
 * **Feature branches** (also prefixed with ‘feature/’) : When you start work on anything non-trivial, you create a *feature branch*. When finished, you’ll merge this branch back into the development branch.
 * **Release branches** (also prefixed with ‘release/’) : When you’re about to package a new release, you create a *release branch* from the development branch. You can commit to it during your preparation for a release, and when it’s ready to be deployed, you merge it into both the development branch and the master branch.
 * **Hotfix branches** (also prefixed with ‘hotfix/’) : If you need to patch the latest release without picking up new features from the development branch, you can create a *hotfix branch* from the latest deployed code in master. Once you’ve made your changes, the hotfix branch is then merged back into both the master branch and the development branch.

## Unity Project : Github Settings
For versions of Unity 3D v4.3 and up:

* (Skip this step in v4.5 and up) Enable External option in Unity → Preferences → Packages → Repository.
* Open the Edit menu and pick Project Settings → Editor:
  * Switch Version Control Mode to Visible Meta Files.
  * Switch Asset Serialization Mode to Force Text. (By default already)
* Save the scene and project from File menu.

## Unreal Project : Github Settings
TODO

## Acknowledgements
Based on the following blog posts :
* [StackOverflow - How to use git for unity3d source control](https://stackoverflow.com/questions/18225126/how-to-use-git-for-unity3d-source-control/18225479#18225479)
* [Setting up Git Source Control in Editor](https://wiki.unrealengine.com/index.php?title=Git_source_control_(Tutorial)#Setting_up_Git_Source_Control_in_Editor)
* [Blog - Smart branching with sourcetree and git flow](https://blog.sourcetreeapp.com/2012/08/01/smart-branching-with-sourcetree-and-git-flow/)
* [Blog - A successful git branching model](https://nvie.com/posts/a-successful-git-branching-model/)
* [Atlassian - Comparing Workflows](https://www.atlassian.com/git/tutorials/comparing-workflows#!workflow-feature-branch)
* [GitHub - Git LFS](https://github.com/git-lfs/git-lfs/tree/master/docs?utm_source=gitlfs_site&utm_medium=docs_link&utm_campaign=gitlfs)
* [Unity Manuel - EditorManager](https://docs.unity3d.com/Manual/class-EditorManager.html)

<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="Licence Creative Commons" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br />Ce(tte) œuvre est mise à disposition selon les termes de la <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">Licence Creative Commons Attribution - Pas d’Utilisation Commerciale - Partage dans les Mêmes Conditions 4.0 International</a>.
