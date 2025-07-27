iWhat is git cherry-pick?
git cherry-pick is a Git command used to apply a specific commit from one branch onto another.

It’s like saying:

“I want just this commit from that branch — not the whole branch — and I want to apply it here.”

Step-by-Step Example
1. Find the commit hash you want:
You can find it with:
```bash
git log
```
2. Run cherry-pick:
```bash
git cherry-pick abc1234
```
This applies the changes from commit abc1234 to your current branch as a new commit.

## Example Workflow
You’re on the feature branch and want to apply a fix from main.
```bash
git checkout feature
git cherry-pick abc1234
```
Now the changes from abc1234 (which may have been made in main) are in your feature branch.


