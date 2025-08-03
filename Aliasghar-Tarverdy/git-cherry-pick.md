## Git cherry-pick command ##
**With the "cherry-pick" command, Git allows you to integrate selected, individual commits from any branch into your current HEAD branch.**

**The reason why you should use cherry-pick rarely is that it easily creates "duplicate" commits: when you integrate a commit into your HEAD branch using cherry-pick, Git has to create a new commit with the exact same contents. It is, however, a completely new commit object with its own, new SHA identifier.**

make empty repository
```bash
git init cherry-pick
```
change directory to git repository
```bash
cd cherry-pick/
```
make some files
```bash
touch f1
```
add to git can track it
```bash
git add f1
```
commit message to add it to stage
```bash
git commit -m "add f1 file on master branch"
```
do this steps again
```bash
touch f2
```
```bash
git add f2
```
```bash
git commit -m "add f2 file on master branch"
```
one more time
```bash
touch f3
```
```bash
git add f3
```
```bash
git commit -m "add f3 file on master branch"
```
now make new branch with feature name and change current branch to feature
```bash
git checkout -b feature
```
make some files on feature branch
```bash
touch f4
```
```bash
git add f4
```
```bash
git commit -m  "add f4 file on feature branch"
```
```bash
touch f5
```
```bash
git add f5
```
```bash
git commit -m  "add f5 file on feature branch"
```
```bash
touch f6
```
```bash
git add f6
```
```bash
git commit -m  "add f6 file on feature branch"
```
now run follow command
```bash
git log --oneline --graph 
```
copy one of the commit id of the feature branch

switch to master branch
```bash
git checkout master
```
run cherry-pick command like this with commit ip you copied
```bash
git cherry-pick b50de7c
```
```bash
git log --oneline --graph
```
now as you can see the commit message with file with different commit id copied in master branch

switch to feature branch
```bash
git checkout feature
```
copied one of the commit message from feature branch as follow step
```bash
git log --oneline --graph
```
switch to master branch
```bash
git checkout master
```
run cherry-pick command like this with commit ip you copied with new commit message when its copying to master branch
```bash
git cherry-pick f1d9843 -e 
```
for sure everything is fun run this command 
```bash
git log --oneline --graph 
```
its done!
