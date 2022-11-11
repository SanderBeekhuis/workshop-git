
# Creating a merge conflict

Note: We will be working on a new empty repo. You don't need to clone this repo. 

## Initial state
1. Set up a new repo with `git init`
2. Make a file `main.py` and add a the lines below to it

```python
def add(a, b):
    return a + b

if __name__ == "__main__":
    print(add("a", "b"))
    print(add(3, 4))

```

3. Commit all changes to a commit on the default branch. 

## Setup features
Suppose we now want to add two features. 
1. Support any amount of arguments
2. Add some logging code in this function


### Feature 1: Any amount of arguments

1.  Create a branch `feature/many-arguments`
2.  Change the code to 
```python
def add(*args):
    accumulator = args[0]
    for arg in args[1:]:
        accumulator += arg
    return accumulator

if __name__ == "__main__":
    print(add("a", "b"))
    print(add(3, 4))
    print(add(1, 2, 3))

```
3. Commit this change

### Feature 2: Add logging
4. Go back to the `main` branch
5. Create a branch `feature/logging`
6. Change the code to
```python
import logging
logging.basicConfig(level=logging.INFO)


def add(a, b):
    logging.info(f"add called with {a} and {b}")
    return a + b

if __name__ == "__main__":
    print(add("a", "b"))
    print(add(3, 4))

```
7. Make a commit

### Going back to the main branch
8. Switch back to main
9. Mark the current state of the main branch with a tag `git tag main-before-merge`
10. Inspect the current state of you branches using `git log --oneline --graph --all`

It should look like this:
```
➜ git log --oneline --graph --all
* 121bce7 (feature/logging) Add basic logging
| * a4759ad (feature/many-arguments) Support multiple arguments
|/
* 28a42e2 (HEAD -> main, tag: main-before-merge) Basic add method
```


## Resolve merge conflicts using merges
Now we have completed the setup we can start merging. 

### Merge first feature
1. Now we merge the first branch with `git merge --no-ff feature/many-arguments`.  No problems so far. 

2. It is nice to inspect the current state of the branches again with `git log --oneline --graph --all`


###  Merge second feature: Merge conflict
3. But now if we try to merge the second feature using `git merge --no-ff feature/logging`
we get a merge conflict.  

4. Our edits to the method body are conflicting and git does not know how to resolve this by itself. 

### Resolve using merge conflict resolution

6. To resolve this merge conflict change the code in the editor (think a little about how you want to combine these two features)
7. Test the resulting code using `python main.py`. Is the output like you expect? 
8. Then add the file it using `git add` and finally commit using `git commit`.
9. Have another look at the commit graph using `git log --graph --oneline --all`.

## Resolve using rebase

1. Reset all merging you did using `git reset --hard main-before-merge`. 

2. It might be nice to look up what this command does exactly if you don't know it. It is one of the best ways to loose data in git if you are not careful with it.

3. Have another look at the commit graph.

4. Let's first merge `feature/many-arguments` into `main` again with `git merge --no-ff feature/many-arguments`
5. Switch to `feature/logging` and tag with `git tag logging-before-rebase`
6. Then this time let's `git rebase main`, resolve the conflicts in this process, and use `git rebase --continue` to finish the process. 
7. Have another look at the commit graph. Especially note the location of the `logging-before-rebase` tag.
8. Switch to `main` and complete the merge with `git merge --no-ff feature/logging`
9. And have a look at the resulting commit graph. Can you see the resulting history is different than in the first case? 
10. Also test the resulting code using `python main.py`


# Bonus Exercise 1: Alternative scenarios
Reset the `feature/logging` and `main` branches to their respective tags. 

Play around with some other scenarios, for example. 
- Do not use the `no-ff` flag and allow for fast-forward in merging. When will git fast-forward? 
- Change around the order of the merges around. Does this make any difference? 

# Bonus Exercise 2: Interactive rebase.  

Make a "messy" branch yourself. For example including: 
- A commit that only fixes a typo. 
- A commit that has a typo in the commit message.
- Maybe even a commit that does two separate things that could be better split into two.

Afterwards use `git rebase -i` to "clean up" this branch and make a nice git commit history. 
