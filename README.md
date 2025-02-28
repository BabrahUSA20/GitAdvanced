# GitAdvanced

# Challenges:
## Part 1: Refining Git History (10 Challenges)

 ### 1. Missing File Fix:
 ```bash


Run git status and git log to assess the current state of your repository.
From the status you will see that you forgot to add test4.md in the last commit.
Challenge: Recover from this error by staging/adding test4.md and amending the commit message with an appropriate description.

# SOLUTION
1. I attauched the fille 4 test files and latter i committed the 3 latter i did 
    i) git status ==> to see the status of my files
    ii) git log ==> to track the history of my commits
    ii): By the solution I add * and then committed teh remainded one.

```

## 2. Editing Commit History:
```bash
It's crucial to maintain accurate commit messages. Modify the message from "Create another file" to "Create second file".
Challenge: Utilize interactive rebasing (git rebase -i HEAD~2) to edit the commit message and ensure clarity. learn more about git rebase here.



# SOLUTION 
    i) is one of Git’s most powerful and flexible commands — it’s used to rewrite the commit history in a way that keeps it cleaner and more linear
Common git rebase commands:

git rebase main — Reapply your branch’s changes on top of main.
git rebase -i HEAD~3 — Interactive rebase of the last 3 commits (squash, reorder, edit).
git rebase --continue — Finish the rebase after resolving conflicts.
git rebase --abort — Cancel the rebase and go back to the original state.

HOW I DID :
0) git log
1) git rebase -i HEAD~2 (for edditing last 2 commits )  --> .) you  will see thing like:
pick <commit-hash> Commit message 1
pick <commit-hash> Commit message 2

-->Change pick to edit next to the commits where you want to edit the comments.  then save and close the editor then stage the files by git add  then git rebase --continue then git push --force

2) git commit --amend -m "Create second file"
3)git rebase --continue
4)git push origin your-branch-name --force

```

## 3. Keeping History Tidy - Squashing Commits:
 ```bash
Squashing combines multiple commits into a single one. Let's merge "Create second file" into "Create initial file" for a cleaner history.
Challenge: Use interactive rebasing with the squash command to achieve this. learn more about squash here


# SOLUTION 

Squashing commits is a great way to clean up your commit history by combining multiple smaller commits into a single, more meaningful commit.

Steps to Squash Commits Using Git Interactive Rebase:
1) git log --oneline : to see the range of commits are when you going to squash
2) you interact the rebase by  git rebase -i HEAD~2
3) the one you want to squash where is pick put it squash then :wq the you will be able to eddit the comments
then you will see the commit message like this "Create initial file and second file"
4) git log --online
5) you shoukd see a single commit representing both changes eg: ghi9012 Create initial file and second file
6)git push --force

```
 

 ## 4. Splitting a Commit:

```bash
Imagine "Create third and fourth files" describes too much at once. Separate them for better tracking with two different commit messages: "Create Third File" and "Create fourth file".
Challenge: Leverage git reset to separate the files into individual commits with distinct messages. learn more about splitting commits

# SOLUTION 
Splitting a commit is a useful technique when you've committed multiple changes that should be tracked separately.

Steps to Split a Commit Using git reset:
1) git log --oneline : To identify the commit to use git reset
2)git reset --soft HEAD~1 : Just to give the last limitted to be reseted
3)git reset when you do that it wil go under staging stage and then add and commit each 
then do git log --online the  push 

```

 ## 5. Advanced Squashing:

```bash
Let's explore more complex squashing. Can you combine the last two commits ("Create third file" and "Create fourth file") into a single commit named "Create third and fourth files"?
Challenge: Utilize interactive rebasing with the squash command to achieve this advanced squash. Check step 4

# SOLUTION


```


