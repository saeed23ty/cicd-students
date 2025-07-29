# Git Bisect Guide

## 📌 What is `git bisect`?

`git bisect` is a Git command that helps you **find the exact commit** that introduced a bug using **binary search**.

Instead of checking each commit manually, it automatically narrows down the range of suspect commits by testing halfway between a known **good** and **bad** commit.

---

## 🧠 How It Works

You:
- Mark one commit as **bad** (where the bug exists).
- Mark one commit as **good** (where the bug didn't exist).

Git:
- Picks a commit halfway between them.
- You test that commit and mark it good or bad.
- Git continues narrowing the range until it finds the **first bad commit**.

---

## ✅ Step-by-Step Example

### 1. Start the bisect session:
```bash
git bisect start
```
2. Tell Git the current commit is bad:
```bash
git bisect bad
```
3. Tell Git a known good commit (before the bug appeared):
```
git bisect good <commit-hash>
```
Git will now checkout a commit in the middle of the good-bad range.

4. Test the code:
After Git checks out a commit:
* If the bug is present:
git bisect bad
* If the bug is NOT present:
```bash
git bisect good
```
Git will continue this process until it finds the first bad commit.

5. Finish the bisect session:
Once you’ve found the commit:
```bash
git bisect reset
```
This returns you to the original branch.

| Command                   | Description                                |
| ------------------------- | ------------------------------------------ |
| `git bisect start`        | Start a bisect session                     |
| `git bisect bad`          | Mark current commit as bad                 |
| `git bisect good <hash>`  | Mark known good commit                     |
| `git bisect reset`        | End the bisect and return to original HEAD |
| `git bisect run <script>` | Automate with a test script                |

