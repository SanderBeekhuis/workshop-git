---
marp: true
---

# Git Gud!
## New and less well-known commands

By Sander Beekhuis

---
# switch and restore
- New in git 2.23 (2019)
- Replace Checkout
- `git switch` to change branches
    - `git switch -c` to create a branch
- `git restore` to change file contents

---
# `stash`
- `git stash` allows you to store non-commited changes

---

# reflog

- `git reflog` stores previously checked out commits 
- life-saver if you somehow lost your last branch pointer


---
# cherry-pick
- `git cherry-pick` allows you to pick over just one commit without merging
- Use sparingly, there is no link between the commits
- Example use case: backporting fixes to maintenance branches

<!-- But starting your branch at the right spot may be better -->
---

# closing notes

- git status on command line
- aliases 



