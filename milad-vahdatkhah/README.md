# 🔍 Git Debugging Tools: `git bisect` & `git cherry-pick`

Welcome! This document explains two powerful Git commands:

- 🪓 `git bisect` — to find bugs using binary search
- 🍒 `git cherry-pick` — to apply individual commits from one branch to another

---

## 🪓 `git bisect`: Find the Commit that Broke Things

### 💡 What is it?

`git bisect` helps you **automatically find the commit that introduced a bug** using **binary search**. This is much faster than checking each commit manually.

---

### 🛠️ How It Works

1. Start bisect:
   ```bash
   git bisect start
   ```

2. Mark the current (bad) commit:
   ```bash
   git bisect bad
   ```

3. Mark a previous (good) commit where everything worked:
   ```bash
   git bisect good <commit-hash>
   ```

Git will now **checkout a commit halfway** between the good and bad commits.

4. Test that commit:
   - If it's **good**:
     ```bash
     git bisect good
     ```
   - If it's **bad**:
     ```bash
     git bisect bad
     ```

Repeat this until Git finds the exact commit that introduced the bug.

---

### ✅ Example
```bash
git bisect start
git bisect bad  # current broken commit
git bisect good abc123  # known good commit
# Test → if okay:
git bisect good
# Test → if broken:
git bisect bad
```

After Git identifies the bad commit:

```bash
git bisect reset  # to return to your original branch
```

---

## 🍒 `git cherry-pick`: Apply Specific Commits

### 💡 What is it?

`git cherry-pick` allows you to **apply a specific commit from one branch into another**, without merging the entire branch.

---

### 📌 Use Cases

- You fixed a bug in `dev` and want to apply it to `main`
- You want to reuse a feature from another feature branch
- You want to backport a fix to an older release branch

---

### 🛠️ How It Works

```bash
git cherry-pick <commit-hash>
```

This applies the changes from that commit to your current branch.

---

### ✅ Example

```bash
# Switch to the branch you want to apply the commit to
git checkout main

# Apply a commit from 'dev' branch
git cherry-pick 9fceb02
```

If there's a conflict, Git will prompt you to resolve it. After fixing:

```bash
git add .
git cherry-pick --continue
```

---

### 🔁 Multiple Commits

To cherry-pick a range:
```bash
git cherry-pick abc123..def456
```

To pick multiple, non-sequential commits:
```bash
git cherry-pick abc123 def456 ghi789
```

---

## 🧠 Tips

- `git bisect` is great for **debugging regressions**.
- `git cherry-pick` is great for **porting features or fixes** between branches.
- Always test cherry-picked commits — context matters! 🍽️

---

## 📚 Resources

- [Git Bisect Docs](https://git-scm.com/docs/git-bisect)
- [Git Cherry-pick Docs](https://git-scm.com/docs/git-cherry-pick)

---

Happy Git-ing! 🧑‍💻🚀
