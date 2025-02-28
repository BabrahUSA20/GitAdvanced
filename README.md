# GitAdvanced

# Challenges:  Part 1: Refining Git History (10 Challenges)

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

### 2. Editing Commit History:
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

### 3. Keeping History Tidy - Squashing Commits:
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
 

 ### 4. Splitting a Commit:

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

 ### 5. Advanced Squashing:
```bash
Let's explore more complex squashing. Can you combine the last two commits ("Create third file" and "Create fourth file") into a single commit named "Create third and fourth files"?
Challenge: Utilize interactive rebasing with the squash command to achieve this advanced squash. Check step 4

# SOLUTION
STEPS:
1)git log --oneline
2)git rebase -i HEAD~5 (JUST THE LIMIT NUMBER OF LINES YOU NEED TO EDIT)
3)I replaced the fourth one where is pick to squach and i save and quit  (only that no additional edit)
4)It  will immitiately prompt me a editing page and delete the message i needed and write my one commit message wanted and :wq
5) if successful I saw "[detached HEAD abc5678] Create third and fourth files
Successfully rebased and updated refs/heads/main.]"
6) Verification  : git log --oneline
7)git push --force

#WORKING :  
Uruyanges-iMac:GitAdvanced gymuruyange$ git log --oneline
9586864 (HEAD -> main, origin/main, origin/HEAD) readme update
789ef4e Readme updates
97dab47 create forth file
a98524e create third file
903a7c0 create second file
33e0109 chore: Create initial file
de20020 Initial commit
Uruyanges-iMac:GitAdvanced gymuruyange$ git rebase -i HEAD~5
Successfully rebased and updated refs/heads/main.
Uruyanges-iMac:GitAdvanced gymuruyange$ git rebase -i HEAD~5
[detached HEAD 3ab9c65] Create third and fourth files
 Date: Wed Feb 26 13:45:18 2025 +0200
 2 files changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 test3.md
 create mode 100644 test4.md
Successfully rebased and updated refs/heads/main.
Uruyanges-iMac:GitAdvanced gymuruyange$ git log --oneline
5dc6e0c (HEAD -> main) readme update
338bdcb Readme updates
3ab9c65 Create third and fourth files
903a7c0 create second file
33e0109 chore: Create initial file
de20020 Initial commit
```

### 6. Dropping a Commit:
```bash
We all make mistakes. Imagine needing to completely remove an unwanted commit from your history.

Create a new file named unwanted.txt add some changes and commit it with a message like "Unwanted commit".

Challenge: Use git rebase -i to identify and remove the "Unwanted commit" commit, cleaning up your history. learn more about dropping commits 


 SOLUTION:
Dropping a commmit: when you remove (drop) a commit using git rebase -i, the changes from that commit do not go back to the staging area or your working directory. They’re completely deleted from history, as if the commit never happened.

STEPS:
1) git log --oneline
2) touch unwanted.txt
3) Added the message dynamicly or you can simply do echo "This is an unwanted file" > unwanted.txt
4) add and commit with (unwanted)
5)git log --oneline
6) git rebase -i HEAD~1 ( the limit where that commit you want to drop)
7) where i the pick replace it with drop or d 
8) :wq
9) for git log --oneline (you will see that the whole file will be droed) ---> to 
If you wanted to keep the changes but remove the commit, you’d use a soft reset instead: git reset --soft HEAD~1
Or, if you wanted the changes back in your working directory (unstaged):git reset HEAD~1

# WORKING:

Uruyanges-iMac:GitAdvanced gymuruyange$ touch unwanted.txt
Uruyanges-iMac:GitAdvanced gymuruyange$ git add .
Uruyanges-iMac:GitAdvanced gymuruyange$ git commit -m "Unwanted commit"
[main 96764ce] Unwanted commit
 1 file changed, 1 insertion(+)
 create mode 100644 unwanted.txt
Uruyanges-iMac:GitAdvanced gymuruyange$ git log --oneline
96764ce (HEAD -> main) Unwanted commit
5969311 read me
5dc6e0c readme update
338bdcb Readme updates
3ab9c65 Create third and fourth files
903a7c0 create second file
33e0109 chore: Create initial file
de20020 Initial commit
Uruyanges-iMac:GitAdvanced gymuruyange$ git rebase -i HEAD~1
Successfully rebased and updated refs/heads/main.
Uruyanges-iMac:GitAdvanced gymuruyange$ git log --oneline
5969311 (HEAD -> main) read me
5dc6e0c readme update
338bdcb Readme updates
3ab9c65 Create third and fourth files
903a7c0 create second file
33e0109 chore: Create initial file
de20020 Initial commit
Uruyanges-iMac:GitAdvanced gymuruyange$ 

```
### 7. Reordering Commits:
``` bash
Delve deeper into git rebase -i. Can you rearrange commits within your history using this command? learn more about ordering commits


# SOLUTION:
STEPS:
1) git log or git log --oneline
2)git rebase -i HEAD~3
3) put the curse where you want to reorder press "dd" to cut and move on that spot and press "p" to paste
4):wq
if successful you will see "Successfully rebased and updated refs/heads/main."


WORKING:
Uruyanges-iMac:GitAdvanced gymuruyange$ git log --oneline
5969311 (HEAD -> main) read me
5dc6e0c readme update
338bdcb Readme updates
3ab9c65 Create third and fourth files
903a7c0 create second file
33e0109 chore: Create initial file
de20020 Initial commit
Uruyanges-iMac:GitAdvanced gymuruyange$ git rebase -i HEAD~6
Uruyanges-iMac:GitAdvanced gymuruyange$ git status
Author: Babrah <usanasebabrah35@gmail.com>
Uruyanges-iMac:GitAdvanced gymuruyange$ git rebase -i HEAD~3
[For here i putted the curse where i want to cut and pressed "dd" and : pressed "p" where i want to past]
Successfully rebased and updated refs/heads/main.
```

### 8.Cherry-Picking Commits:
```bash 
Create a branch, call it ft/branch, and add a new file named test5.md with some content. Commit these changes with a message like "Implemented test 5".
Imagine you only desire a specific commit from ft/branch. Research and use git cherry-pick to selectively bring that commit into your current branch which is main.
learn more about cherry-pick


# SOLUTION:
git cherry-pick is a powerful Git command that lets you selectively apply a specific commit from one branch into another
without merging the entire branch.

this  is simple copy that file and the commit message but (it will be a new commit with a different commit hash) to the specific target branch and also remain in original branch also with the commit message.

STEPS:
1) git checkout -b ft/branch
2)echo "This is test 5" > test5.md
3) git add test5.md
4) git commit -m "Implemented test 5"
5)git checkout main or <target branch>
6) git log --oneline ft/branch
7) git cherry-pick abc1234 or <its hash code>
8) you can verify by git log --oneline

WORKING:
Uruyanges-iMac:GitAdvanced gymuruyange$ git checkout -b ft/branch
Switched to a new branch 'ft/branch'
Uruyanges-iMac:GitAdvanced gymuruyange$ echo "This is test 5" > test5.md
Uruyanges-iMac:GitAdvanced gymuruyange$ git add test5.md
Uruyanges-iMac:GitAdvanced gymuruyange$ git commit -m "Implemented test 5"
[ft/branch c90d85c] Implemented test 5
 1 file changed, 1 insertion(+)
 create mode 100644 test5.md
Uruyanges-iMac:GitAdvanced gymuruyange$ git checkout main
Switched to branch 'main'
Your branch and 'origin/main' have diverged,
and have 6 and 4 different commits each, respectively.
  (use "git pull" to merge the remote branch into yours)
Uruyanges-iMac:GitAdvanced gymuruyange$ git log --oneline ft/branch
c90d85c (ft/branch) Implemented test 5
193d133 (HEAD -> main) readme
9c7dd10 read me
cd6741b updating the readme
5dc6e0c readme update
338bdcb Readme updates
3ab9c65 Create third and fourth files
903a7c0 create second file
33e0109 chore: Create initial file
de20020 Initial commit
Uruyanges-iMac:GitAdvanced gymuruyange$ git cherry-pick c90d85c 
[main 10c61ea] Implemented test 5
 Date: Fri Feb 28 12:14:18 2025 +0200
 1 file changed, 1 insertion(+)
 create mode 100644 test5.md
Uruyanges-iMac:GitAdvanced gymuruyange$ git log --oneline
10c61ea (HEAD -> main) Implemented test 5
193d133 readme
9c7dd10 read me
cd6741b updating the readme
5dc6e0c readme update
338bdcb Readme updates
3ab9c65 Create third and fourth files
903a7c0 create second file
33e0109 chore: Create initial file
de20020 Initial commit

```

### 9. Visualizing Commit History (Bonus):
```bash
Tools like git log --graph or a graphical Git client can help visualize your commit history. Explore these tools for a clearer understanding of your workflow.

# SOLUTION:
Visualizing your commit history can make it much easier to understand your workflow, see the relationships between branches, and track changes over time.
STEPS:




WORKING

```




