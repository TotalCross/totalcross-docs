---
description: Understand our git workflow
---

# Branch workflow

## Types

There are some types of branches in our repository, they are:

* **Feature**: used to implement new features. Can be started from an issue. Started at the source of the problem \(commit\) from the source version. The prefix is `feature-`;
* **Fix**: used to fix bugs and code smells. Can be started from an issue. Started at the source of the problem \(commit\) from the source version. Fix takes precedence over the feature and should be resolved quickly and has the same process. The prefix is `fix-`;
* **Hotfix**: special branches for cases of emergency corrections, are used to quickly patch production releases. The prefix is `hotfix-`;
* **Develop**: **WIP**
* **Master**: **WIP**

## **Rebase before merge**

In summary:

1. Open branch `feature-x`;
2. `develop`does not stop production ;
3. Finish `feature-x`;
4. Rebase `feature-x` into `develop`;
5. Test integration;
6. Merge request \(delete the branch\).

The reasons for this are: 

* Anticipate integration;
* Maintain a more linear history;
* Commit squash situation \(compile multiples commits in an unique commit\).

