# Git Bisect

**Git Bisect** is a powerful debugging tool that helps you find the specific commit that introduced a bug by using binary search.

---

## Concept

When you notice a bug in your codebase but don’t know which commit caused it, `git bisect` helps you pinpoint the exact commit by:

1. Marking a known **good** commit (where the bug did not exist).
2. Marking a known **bad** commit (where the bug exists).
3. Git then checks out the commit halfway between the good and bad commits.
4. You test this commit:
   - If the bug is present, mark it as **bad**.
   - If the bug is absent, mark it as **good**.
5. Git repeats this process, narrowing down the commits until it finds the exact commit that introduced the bug.

---

## Basic Usage

```bash
# Start bisect with known bad commit (usually HEAD)
git bisect start

# Mark the current commit as bad (bug present)
git bisect bad

# Mark a known good commit (bug absent)
git bisect good <good_commit_hash>

# Git will checkout a commit halfway between good and bad.
# Test the code, then mark the commit as good or bad:
git bisect good    # if bug absent
git bisect bad     # if bug present

# Repeat until git finds the culprit commit.

# When done, reset bisect session:
git bisect reset
