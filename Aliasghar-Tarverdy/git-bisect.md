## Git bisect command ##
**git bisect is a command in Git that helps you find the commit that introduced a bug or caused a regression in your codebase. It uses a binary search algorithm to efficiently narrow down the range of commits that needs to be tested.**

**By marking specific commits as “good” or “bad”, git bisect automatically selects the next commit for testing until it identifies the exact commit that introduced the issue. This process helps identify the faulty commit more quickly and efficiently, enabling developers to pinpoint and fix the problem more effectively.**

**What is git bisect?**
**git bisect is a Git command that helps you find the specific commit that introduced a bug or problem in your codebase.**
**It works like a binary search algorithm — fast and efficient — especially when you don’t know exactly when the bug appeared.**

**Why use it?**
**Imagine your project was working fine last week, but now something’s broken. You’ve made dozens (or hundreds) of commits since then.
You don’t want to check each one manually, right?**

**That’s where git bisect helps:**
**It automatically checks commits between a “good” and a “bad” state and helps you find the exact commit that broke the code.**

make empty repository
```bash
git init git-bisect
```
change directory to git repository
```bash
cd git-bisect
```
write some message like this
```bash
echo 'echo "Hello World!"' >> app.sh
```
add file 
```bash
git add app.sh 
```
write some commit message
```bash
git commit -m "add Hello World! to app.sh file"
```
repeat these steps several times
```bash
echo 'echo "Hi World!"' >> app.sh
```
add and commit sametime like this
```bash
git commit -am "add Hi World! to app.sh file"
```
```bash
echo 'echo "ok!"' >> app.sh
```
```bash
git commit -am "add Ok! to app.sh file"
```
add some error to the file like this
```bash
echo 'echo $((1/0))' >> app.sh
```
```bash
git commit -am "add some error! to app.sh file"
```
```bash
echo 'echo "some message after making error"' >> app.sh
```
```bash
git commit -am "add some message after error! to app.sh file"
```
git execute permission to file
```bash
chmod +x app.sh 
```
now if you run script you will see error in line 4
```bash
./app.sh
```
**now imagin you dont know which line of your script has bug so in this situation bisect can help us**

start bisect process
```bash
git bisect start 
```
**in bisect process you should define endpoint as bad bisect and startpoint as good bisect**

make last commit to bad bisect 
```bash
git bisect bad 
```
now we need to make one of the commit as good bisect, one of the commit we sure about it our script was working without any error or problem! in this scenario we made first commit as good bisect.
```bash
git bisect good c4ec9e1
```
**in this step we need to run our script frequently, if script was successful we made it good bisect if script had error we made it bad bisect**

lets run our script
```bash
./app.sh
```
as you can see our script was run without any problem so we will make it good bisect this commit
```bash
git bisect good 
```
again run our script
as you can see our script has error in this commit so we will make it bad bisect
```bash
git bisect bad
```
**So now in this step you know in which commit your app or script has error or problem and bisect work has done**

to end bisect process
```bash
git bisect reset
```
