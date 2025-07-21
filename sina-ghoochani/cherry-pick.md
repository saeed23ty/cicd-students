# Git Cherry Pick

**Git Cherry Pick** is a command that allows you to apply changes introduced by one or more specific commits from another branch onto your current branch.

---

## Concept

Imagine you have a commit on a feature branch that fixes a bug or adds a useful change, and you want to apply just that specific commit to your main branch without merging the entire feature branch.  
`git cherry-pick` lets you "pick" those commits and apply them on top of your current branch.

---

## Use Cases

- Apply a specific bug fix or feature from one branch to another without merging all changes.  
- Selectively transfer commits to keep your history clean.  
- Quickly patch the main branch with changes from a development branch.

---

## Basic Usage

```bash
# Switch to the branch where you want to apply the commit(s)
git checkout main

# Apply a single commit by its hash
git cherry-pick <commit-hash>

# Apply multiple commits by specifying their hashes
git cherry-pick <commit1> <commit2> <commit3>

# Apply a range of commits (from commit1’s parent up to commit5)
git cherry-pick <commit1>^..<commit5>

