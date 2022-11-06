# git stash

Create a git history like below where every commit changes the SAME file. (e.g Readme.md).

```
* (main) work
* work
| * (feature) Made the greatest feature
|/
* Set up mvp
* init commit
```

1. Switch you branch to `feature`, for example to review it.
2. Go grab a coffee and completly forget what you were doing. 
3. Start coding and make some changes to that SAME file.
4. Realize you are on the wrong branch. 
5. When you try to `git switch main`  you get an error message.
6. Stash your changes using `git stash`
7. Switch branches to `main` and create a new `my-feature` branch. 
8. Unstash your changes.
    - You can  using either `git stash pop` or `git stash apply`. What is the difference? 
9. Commit your changes and look at the git history graph with `git log --oneline --graph --all`.



# git reflog

With `git reflog` you can find back commits that have no branch pointing to them anymore. 

1. Set up a history like below. 

```
* (main) work
* work
| * (feature) Made the greatest feature
|/
* Set up mvp
* init commit
```

2. Rebase `feature` on top of `main`
3. Suppose you have made a mistake and you want to undo this rebase.
4. Figure out how to recover the hash of the commit that `feature` used to point to.
5. Make a branch pointing to this commit with the name `feature-recovery`.
6. Look at the resulting git history.  Can you see that a rebase does not actually move anything, but just recreates commits. 




# Bonus Exercise: Cherry pick

Set up a git history with a main branch and a released version branch. Like pseudo git log below.
```
* (main) latest work
* some recent work
* (v1, tag: v1.0.0) release 1.0.0
* MVP feature complete
* Init commit
```

Compare the following scenarios. 
1. Starting a `bugfix` branch from `main` and merging it back into both `main` and `v1` branches. 
    - Can you see the merge into `v1` also includes the changes in "latest work" and "some recent work". This might not be what you want. 
2. Starting a `bugfix` branch from `main` and merging it back into both `main`. And Cherry-picking the right commit(s) into `v1` branches. 
    - Can you pick just the merge commit or should you pick from the branch. Why or why not?
3. Starting a `bugfix` branch from `v1` and merging it back into both `main` and `v1` branches.
    - Does this work out as intended?  Contrast the resulting git history graph with the one from Scenario 1.

Which of these 3 approaches do you like best? 


# Bonus exercise: Git restore 
If you have time left you can read the documentation `git restore` and play with it or compare it to `git checkout`. 