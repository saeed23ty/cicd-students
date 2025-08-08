## Git bisect
The `bisect` command is for quickly finding where a problem or change was introduced in a range of commits in Git by implementing an automated binary search. Starting from an initial range specified between a known bad revision and a known good revision. Most commonly, this is used for debugging a problem.

### Description

Imagine you have a bug in your code, and:

- You know it works in an old commit (e.g. 2 months ago).

- You know it is broken now (e.g. today).

git bisect walks you through the middle commits and asks you at each step:
"Is it good here?" or "Is it bad?"

Depending on your answer, it keeps cutting the commit range in half.

It repeats this process until it finds **the exact commit** that introduced the issue.

The syntax for cherry-pick is as follows:
```bash
git bisect [subcommand] [options]
```
### What happens under the hood
- **Binary Search Logic:** Git calculates the midpoint of the commit range, checks it out, and repeats—cutting down the possible commits quickly.

- **Metadata Tracking:** Git stores bisect progress and results in internal state files like `.git/BISECT_LOG` and `refs/bisect/*`, tracking what’s been tested and what’s left.

- **Efficiency:** Instead of testing N commits, you typically test around 1 + log₂(N) commits—binary search drastically reduces effort.

### Step-by-step example
Create a new repo with 7 commits and introduce a "bug" in one commit then use git bisect to find that commit:
#### Step 1. Set up the repo:
```bash 
mkdir bisect-test && cd bisect-test
git init
```
#### Step 2. Add good commits:
```bash 
echo "1" > test.txt
git add test.txt
git commit -m "Commit 1: Initial good value"

echo "2" > test.txt
git commit -am "Commit 2: Still good"

echo "3" > test.txt
git commit -am "Commit 3: Still good"
```
#### Step 3. Introduce a bug:
```bash 
echo "BUG" > test.txt
git commit -am "Commit 4: Bug introduced"
```
#### Step 4. Add more bad commits:
```bash
echo "BUG 2" > test.txt
git commit -am "Commit 5: Still broken"

echo "BUG 3" > test.txt
git commit -am "Commit 6: Still broken"
```
Now **git log --oneline** shows:
```bash 
<hash6> Commit 6: Still broken
<hash5> Commit 5: Still broken
<hash4> Commit 4: Bug introduced
<hash3> Commit 3: Still good
<hash2> Commit 2: Still good
<hash1> Commit 1: Initial good value
```
#### Step 5. Use `git bisect`:
```bash
git bisect start
git bisect bad                # current HEAD is bad
git bisect good HEAD~5        # commit 1 is known to be good
```
Git will checkout the middle commit (e.g. commit 4).
Now test it:
```bash
cat test.txt
```
If it contains **'BUG"**, then:
```bash
git bisect bad
```
Otherwise:
```bash
git bisect good
```
Repeat until you get:
```bash
<hash> is the first bad commit
```
Finally to clean up the bisection state and return to the original HEAD, issue the following command:
```bash 
git bisect reset
```

### Automating with `git bisect run`

To save time and avoid manual testing, you can automate git bisect using a script. Here’s how that works:

Write a test script that:

- Exits with status 0 if the commit is good.

- Exits with non-zero if the commit is bad.

- Optionally, exits with 125 to skip untestable commit

#### Example use case:
#### 1. Make a test script **test.sh**:
```bash
#!/bin/bash

# Fail if "BUG" is found in the file
if grep -q "BUG" test.txt; then
  exit 1
else
  exit 0
fi
```
Make it executable:
```bash
chmod +x test.sh
```
#### 2. Run bisect with automation:
```bash
git bisect start
git bisect bad
git bisect good HEAD~5
git bisect run ./test.sh
```
Git will test each commit automatically using your script until it finds the problematic commit.
When it's done, run:
```bash 
git bisect reset
```


