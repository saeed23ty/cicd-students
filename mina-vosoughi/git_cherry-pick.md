## Git cherry-pick
### What is `cherry-pick` in Git?
`git cherry-pick` is a Git command that The idea with this operation
is to be able to selectively choose an individual or group of commits from within one branch and
apply them to another branch. It’s like “picking” just one or several cherries (commit) from the history rather than merging or rebasing all changes.

The syntax for cherry-pick is as follows:
```bash
git cherry-pick [options] [commit]
```
`git cherry-pick` supports options that dictate how the introduced commits are
handled. This includes the following:

**-x:** This option adds a standardized message to the commit of the form *"cherry picked
from commit ..."* to specify the commit that introduces the incoming change.

**--edit:** This allows you to edit the commit message for the incoming changes.

**--no-commit:** You may wish to integrate changes from a specific commit without
creating a corresponding commit. The **--no-commit command** integrates changes from a
commit without creating a commit.

**--mainline [parent_number]:** Since a parent commit possesses two parents, running
a `cherry-pick` against a merge commit requires that a parent is specified. The given parent is compared to the merge tree of the merge commit and the resulting difference is introduced into the branch where `git cherry-pick` is invoked from.

 ### Description 
 Suppose you have this situation:
 ```
 A---B---C---D  (feature-branch)
     \
      E---F---G  (main)
```
Let’s say commit `C` on `feature-branch` is a bug fix you want in `main`, but you don’t want all the other changes from `feature-branch`.
With `git cherry-pick`, you can just grab commit `C` and add it to `main`!

### What happens under the hood
- Git takes the the difference, or *diff* in Git terms, introduced by the picked commit and applies it as a new commit on your current branch.
- The commit message will be copied (you can edit it if you want).
- The commit will have a new hash (because it’s a new object in the branch’s history).

### Step-by-step Example
#### 1. Find the commit hash
Use: 
```bash
git log
```
Copy the hash for the commit you want to pick (e.g., `C`).

#### 2. The branch you want to apply the commit to (for example, `main`)
```bash
git checkout main
```
#### 3. Cherry-pick the commit
```bash
git cherry-pick <commit-hash>
```
For example:
```bash
git cherry-pick 1234abcd
```
#### 4.Resolve conflicts (if any)
If there’s a conflict, Git will stop and let you fix it. After fixing, do:
```bash
git add .
git cherry-pick --continue
```
#### 5.Push your changes
```bash
git push
```


