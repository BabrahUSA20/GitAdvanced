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

### 8.Cherry-Picking Commits:
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

GIT-LOG --GRAPH:

git log --graph :is a command-line tool that creates a graphical representation of your commit history in the terminal.
STEPS:
1)git log --oneline --graph --all --decorate

Definition of each:
--oneline: Shows each commit as a single line (shorter and easier to read).
--graph: Displays a graphical tree of commits.
--all: Shows commits from all branches.
--decorate: Labels branches, tags, and other references.

NB:
The asterisks (*) represent individual commits.
The vertical bars (|) show the branching structure.
You can see which branch each commit is on, and the commit history will be shown in a graph format, which makes it much easier to understand branching and merging.

WORKING:
Uruyanges-iMac:GitAdvanced gymuruyange$ git log --oneline --graph --all --decorate
* 835f55f (HEAD -> main) updation
* 10c61ea Implemented test 5
| * c90d85c (ft/branch) Implemented test 5
|/  
* 193d133 readme
* 9c7dd10 read me
* cd6741b updating the readme
* 5dc6e0c readme update
* 338bdcb Readme updates
* 3ab9c65 Create third and fourth files
| * 9586864 (origin/main, origin/HEAD) readme update
| * 789ef4e Readme updates
| * 97dab47 create forth file
| * a98524e create third file
|/  
* 903a7c0 create second file
* 33e0109 chore: Create initial file
* de20020 Initial commit
Uruyanges-iMac:GitAdvanced gymuruyange$ 


GRAPHICAL GIT CLIENT:
If you prefer GUI-based tools, there are several graphical Git clients that offer a more intuitive interface to visualize your commit history. Here are a few popular ones:


 A. GitKraken:

Platform: Cross-platform (Windows, macOS, Linux)
Features:
Graphical commit history: Shows branches, merges, and rebases visually.
Drag-and-drop: You can easily perform Git operations (merge, rebase, checkout) by dragging and dropping commits.
Task management: Integrated issue tracking and task management.

B. Sourcetree:

Platform: Windows, macOS
Features:
Clean and easy-to-read commit graph: Visualize all your commits, branches, and merges.
Multiple repository support: You can manage several repositories at once.
Branching and merging made easy: A simple interface for managing branches and resolving conflicts.

C. Git GUI (by Git):

Platform: Cross-platform (Windows, macOS, Linux)
Features:
Simple interface: Git GUI is lightweight and offers a simple way to view commit history and perform common Git operations.
Visual diff viewer: See changes between commits, branches, and files.

D. Visual Studio Code (VSCode) with Git Graph Extension:
Platform: Cross-platform (Windows, macOS, Linux)
Features:
Integrated Git graph: The Git Graph extension adds a commit history graph to VSCode’s interface.
Easy to use: You can navigate between branches, commits, and even perform actions like merges and rebases directly in the editor.



REMINDER  😘:
Why Use These Tools?

Clarity: Viewing your commit history as a graph helps you see the structure of your project, making it easier to understand how branches and merges interact.
Efficiency: You can quickly spot issues, such as unmerged branches or redundant commits.
Better Collaboration: In team environments, visual tools help everyone stay on the same page, especially when dealing with complex branching and merging workflows.
```

### 10. Understanding Reflogs (Bonus):

```bash
Reflogs track Git operation history. Research about git reflog to learn how you can navigate back to previous states in your repository if needed.

# SOLUTION:
git reflog is a powerful Git command that allows you to track and view the history of all changes to the references in your repository (such as branches, HEAD, and remotes). It records every action that moves or modifies the HEAD and branch pointers — even if those changes are temporary or seem to be "lost" after a rebase, reset, or checkout.

Why is git reflog useful?

1. Undoing Mistakes: If you accidentally make changes (e.g., an unwanted git reset or git checkout), git reflog allows you to go back to any previous state of the repository.
2. Recovering Lost Commits: If you think you've "lost" a commit, like after a "git reset --hard", you can often recover it using "git reflog".
3. Tracking Actions: It gives you a log of every Git operation that moves HEAD — things like "git checkout", "git commit", "git rebase", etc.

STEP:
1) git reflog: (To see your reflog history)

WORKING: 
Uruyanges-iMac:GitAdvanced gymuruyange$ git reflow
git: 'reflow' is not a git command. See 'git --help'.

The most similar command is
        reflog
Uruyanges-iMac:GitAdvanced gymuruyange$ git reflog
6a91b3e (HEAD -> main) HEAD@{0}: pull: Merge made by the 'ort' strategy.
ac7429e HEAD@{1}: commit: merging
ab15e4b HEAD@{2}: reset: moving to HEAD@{5}
8344081 (origin/main, origin/HEAD) HEAD@{3}: reset: moving to HEAD
8344081 (origin/main, origin/HEAD) HEAD@{4}: rebase (finish): returning to refs/heads/main
8344081 (origin/main, origin/HEAD) HEAD@{5}: rebase (pick): babrah's file to study reflog with reset
eeb2508 HEAD@{6}: rebase (pick): updation
f21bf53 HEAD@{7}: rebase (pick): updation
ab15e4b HEAD@{8}: rebase (pick): Implemented test 5
9274122 HEAD@{9}: rebase (pick): readme
6798bd5 HEAD@{10}: rebase (pick): read me
0dc1ee9 HEAD@{11}: rebase (pick): updating the readme
9586864 HEAD@{12}: rebase (start): checkout origin/main
d3889c6 HEAD@{13}: reset: moving to HEAD
d3889c6 HEAD@{14}: checkout: moving from d3889c626d35f0a42c99cc51ee87bb436386cf11 to main
Uruyanges-iMac:GitAdvanced gymuruyange$ git reset --hard HEAD@{3}
HEAD is now at 8344081 babrah's file to study reflog with reset
Uruyanges-iMac:GitAdvanced gymuruyange$ git reset --hard HEAD@{0}
HEAD is now at 8344081 babrah's file to study reflog with reset
Uruyanges-iMac:GitAdvanced gymuruyange$ git reflog
8344081 (HEAD -> main, origin/main, origin/HEAD) HEAD@{0}: reset: moving to HEAD@{0}
8344081 (HEAD -> main, origin/main, origin/HEAD) HEAD@{1}: reset: moving to HEAD@{3}
6a91b3e HEAD@{2}: pull: Merge made by the 'ort' strategy.
ac7429e HEAD@{3}: commit: merging
ab15e4b HEAD@{4}: reset: moving to HEAD@{5}
8344081 (HEAD -> main, origin/main, origin/HEAD) HEAD@{5}: reset: moving to HEAD
8344081 (HEAD -> main, origin/main, origin/HEAD) HEAD@{6}: rebase (finish): returning to refs/heads/main
8344081 (HEAD -> main, origin/main, origin/HEAD) HEAD@{7}: rebase (pick): babrah's file to study reflog with reset
eeb2508 HEAD@{8}: rebase (pick): updation
f21bf53 HEAD@{9}: rebase (pick): updation
ab15e4b HEAD@{10}: rebase (pick): Implemented test 5
9274122 HEAD@{11}: rebase (pick): readme
6798bd5 HEAD@{12}: rebase (pick): read me
0dc1ee9 HEAD@{13}: rebase (pick): updating the readme
9586864 HEAD@{14}: rebase (start): checkout origin/main
d3889c6 HEAD@{15}: reset: moving to HEAD
d3889c6 HEAD@{16}: checkout: moving from d3889c626d35f0a42c99cc51ee87bb436386cf11 to main

```

# Challenges:  Part 2: Branching Basics (10 Challenges)
### 1.Feature Branch Creation:
```bash
Imagine working on a new feature named ft/new-feature. Let's establish a dedicated branch for it.
Challenge: Create a new branch named ft/new-feature and switch to that branch.

 # Solution:
STEPS:
They are different ways of doing that

WAY 1:
1) git checkout -b "branch-name" (THIS CREATE AND SIMPLE SWITCH TO THAT NEW BRANCH)

WORKING:
Uruyanges-iMac:GitAdvanced gymuruyange$ git checkout -b ft/new-feature
Switched to a new branch 'ft/new-feature'
Uruyanges-iMac:GitAdvanced gymuruyange$

WAY 2:
1) git branch  -M "branch-name" (THIS CREATE AND SIMPLE SWITCH TO THAT NEW BRANCH)
WORKING:
Uruyanges-iMac:GitAdvanced gymuruyange$ git branch -M babrah
Uruyanges-iMac:GitAdvanced gymuruyange$ git branch
* babrah
  ft/branch
  main
```

 ### 2.Working on the Feature Branch:
 ```bash
 Create a new file named feature.txt in this branch and add some content to it.
Commit these changes with a descriptive message like "Implemented core functionality for new feature".

#SOLUTION:
STEPS: 
1) touch feature.txt (also add the content dynamic)
2)git status
3)git add feature.txt
4)git commit -m "Implemented core functionality for new feature"

WORKING:
Uruyanges-iMac:GitAdvanced gymuruyange$ git checkout -b ft/new-feature
Switched to a new branch 'ft/new-feature'
Uruyanges-iMac:GitAdvanced gymuruyange$ echo "This is feature contet" > feature.txt
Uruyanges-iMac:GitAdvanced gymuruyange$ git status
On branch ft/new-feature
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        feature.txt

nothing added to commit but untracked files present (use "git add" to track)
Uruyanges-iMac:GitAdvanced gymuruyange$ git add feature.txt
Uruyanges-iMac:GitAdvanced gymuruyange$ git commit -m "Implemented core functionality for new feature"
[ft/new-feature 337fc4d] Implemented core functionality for new feature
 1 file changed, 1 insertion(+)
 create mode 100644 feature.txt

 ```
 ### 3. Switching Back and Making More Changes:
 ```bash
 It's common to switch between branches during development.
Challenge: Switch back to the main branch (previously master) and create a new file named readme.txt with some introductory content.
 Commit these changes with a message like "Updated project readme".

 # SOLUTION:
 STEPS:
1) git checkout main
2) echo "This is readme content" > readme.txt
3) git status
4) git add readme.txt
5) git commit -m "Updated project readme"

 WORKING:
 Uruyanges-iMac:GitAdvanced gymuruyange$ git switch main
Switched to branch 'main'
Your branch is ahead of 'origin/main' by 2 commits.
  (use "git push" to publish your local commits)
Uruyanges-iMac:GitAdvanced gymuruyange$ echo "This is readme content" > readme.txt
Uruyanges-iMac:GitAdvanced gymuruyange$ git status
On branch main
Your branch is ahead of 'origin/main' by 2 commits.
  (use "git push" to publish your local commits)

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        readme.txt

nothing added to commit but untracked files present (use "git add" to track)
Uruyanges-iMac:GitAdvanced gymuruyange$ git add  readme.txt
Uruyanges-iMac:GitAdvanced gymuruyange$ git commit -m "Updated project readme"
[main b3a343d] Updated project readme
 1 file changed, 1 insertion(+)
 create mode 100644 readme.txt
Uruyanges-iMac:GitAdvanced gymuruyange$ 
 ```

 ### 4. Local vs. Remote Branches:
 ```bash
So far, we've been working with local branches that exist on your machine. Research the concept of remote branches, which are copies of your local branches stored on a Git hosting platform like GitHub. 
Learn how to push your local branches to remote repositories and pull changes from them to keep your local and remote repositories in sync.


# SOLUTION 
Local vs. Remote Branches:

Local branches only exist on your computer. They’re private to you until you push them somewhere remote.
Remote branches are versions of your branches stored on a Git hosting service (like GitHub, GitLab, Bitbucket). 

They let your teammates access and collaborate on the same code.

How to Push a Local Branch to a Remote Repository:

Create a local branch (if you haven’t already):
->git checkout -b feature-branch

Make your changes and commit:
->git add .
->git commit -m "Add new feature"

Push your branch to the remote repo:
->git push origin feature-branch

origin is the default name of your remote repo. feature-branch is the name of your branch.
How to Pull Changes from a Remote Repository:

Fetch the latest changes (without merging):
->git fetch origin

Pull and merge changes:
If you want to get the latest changes and automatically merge them:
->git pull origin feature-branch

Keeping Local and Remote Branches in Sync:

When you push, you’re sending your local changes to the remote.
When you pull, you’re getting changes from the remote and merging them into your local branch.
Fetch only updates your local knowledge of the remote — it doesn’t change your working directory.
Checking Remote Branches:
To see all remote branches:
->git branch -r

To see both local and remote:
->git branch -a

```

### 5.Branch Deletion:
```bash
After merging or completing work on a feature branch, it's good practice to remove it.

#SOLUTION
You can delete a local branch using:
--> git branch -d <branch-name>

    WORKING:
    rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)
$ git checkout -b ft/new-feature
Switched to a new branch 'ft/new-feature'

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (ft/new-feature)
$ echo "This is feature contet" > feature.txt

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (ft/new-feature)
$ git add .
warning: in the working copy of 'feature.txt', LF will be replaced by CRLF the next time Git touches it

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (ft/new-feature)
$ git  git commit -m "Implemented core functionality for new feature"
git: 'git' is not a git command. See 'git --help'.

The most similar command is
        init

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (ft/new-feature)
$  git commit -m "Implemented core functionality for new feature"
[ft/new-feature 8effe58] Implemented core functionality for new feature
 2 files changed, 52 insertions(+), 4 deletions(-)
 create mode 100644 feature.txt

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (ft/new-feature)
$ git switch main
Switched to branch 'main'
Your branch is ahead of 'origin/main' by 3 commits.
  (use "git push" to publish your local commits)

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)
$ git log --oneline ft/new-feature
8effe58 (ft/new-feature) Implemented core functionality for new feature
803e0f8 (HEAD -> main) Merge branch 'main' of https://github.com/BabrahUSA20/GitAdvanced
65e7f17 staging
cde43f7 (origin/main, origin/HEAD) pushng readme on git
b3a343d Updated project readme
0772d4f updating the readme
2145b61 read me
452efd0 hi
2f70beb read to update it

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)
$ git cherry-pick 8effe58
[main 6a7fa8b] Implemented core functionality for new feature
 Date: Mon Mar 3 11:26:01 2025 +0200
 2 files changed, 52 insertions(+), 4 deletions(-)
 create mode 100644 feature.txt

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)
$ git log --oneline 
6a7fa8b (HEAD -> main) Implemented core functionality for new feature
803e0f8 Merge branch 'main' of https://github.com/BabrahUSA20/GitAdvanced
65e7f17 staging
cde43f7 (origin/main, origin/HEAD) pushng readme on git
b3a343d Updated project readme
0772d4f updating the readme
2145b61 read me
452efd0 hi
2f70beb read to update it

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)
$ git branch -d ft/new-feature
error: the branch 'ft/new-feature' is not fully merged
hint: If you are sure you want to delete it, run 'git branch -D ft/new-feature'
hint: Disable this message with "git config advice.forceDeleteBranch false"

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)
$ git branch -D ft/new-feature
Deleted branch ft/new-feature (was 8effe58).

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)
$ git log --oneline
6a7fa8b (HEAD -> main) Implemented core functionality for new feature
803e0f8 Merge branch 'main' of https://github.com/BabrahUSA20/GitAdvanced
65e7f17 staging
cde43f7 (origin/main, origin/HEAD) pushng readme on git
b3a343d Updated project readme
0772d4f updating the readme
2145b61 read me
452efd0 hi
2f70beb read to update it

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)
$ git branch
* main

```
### 6.Creating a Branch from a Commit:

```bash
You can also create a branch from a specific commit in your history.
Challenge: Use git checkout -b ft/new-branch-from-commit commit-hash (adjust the commit hash as needed) to create a new branch named ft/new-branch-from-commit starting from the commit two positions back in your history. learn more here

SOOLUTION:
STEPS:
1)git log --oneline to get the commit hashes of your previous commits
2) git checkout -b ft/new-branch-from-commit(new branch-name ) 803e0f8 (commit-hash you gate the one after the first 2 positions back).

WORKING:
rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)
$ git log --oneline
7a7d225 (HEAD -> main) staging the readme
6a7fa8b Implemented core functionality for new feature
803e0f8 Merge branch 'main' of https://github.com/BabrahUSA20/GitAdvanced
65e7f17 staging
cde43f7 (origin/main, origin/HEAD) pushng readme on git
b3a343d Updated project readme
0772d4f updating the readme
2145b61 read me
452efd0 hi
2f70beb read to update it
e20f6ec hello
3e04410 merging
eeb2508 updation

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)
$ git checkout -b ft/new-branch-from-commit 803e0f8
Switched to a new branch 'ft/new-branch-from-commit'

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (ft/new-branch-from-commit)
$ git branch 
* ft/new-branch-from-commit
  main

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (ft/new-branch-from-commit)
$ git switch main
Switched to branch 'main'
Your branch is ahead of 'origin/main' by 5 commits.
  (use "git push" to publish your local commits)

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)
$

```
### 7.Branch Merging:
```bash
Now that you've completed work on your feature branch, it's time to integrate it into main.
Challenge: Merge the ft/new-branch-from-commit branch into the main branch. Address any merge conflicts that might arise

# SOLUTION:
STEPS:
1) git checkout main
2)git merge ft/new-branch-from-commit
3)Handle any merge conflicts (if they pop up):
If Git shows a merge conflict message, don’t worry — it just means two branches changed the same part of a file. Git will mark the conflict like this:

<<<<<<< HEAD
Changes from the main branch
=======
Changes from the feature branch
>>>>>>> ft/new-branch-from-commit

Open the file and decide which version (or combination) you want to keep.
After resolving, stage the changes:

git add conflicted-file.js
Then continue the merge:
-->git commit

(Optional) Clean up the feature branch:
If you’re done with the feature branch and it’s been merged, you can delete it:
-->git branch -d ft/new-branch-from-commit

And if it’s on the remote too:
-->git push origin --delete ft/new-branch-from-commit

Push the updated main branch to remote:
Let’s get those changes up on GitHub (or whatever remote you’re using):
-->git push origin main



WORKING:
rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)
$ git merge ft/new-branch-from-commit
Already up to date.

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)
$ 
```
### 8.Branch Rebasing:
```bash
Rebasing is another method to integrate changes from a feature branch. It rewrites your branch history by incorporating its commits on top of the latest commit in the target branch (main in our case).
Challenge: Try rebasing the ft/new-branch-from-commit branch onto the main branch. Remember, rebasing rewrites history, so use it with caution, especially in shared repositories. learn more about rebasing here

#SOLUTION:
STEPS :
1) git checkout ft/new-branch-from-commit (any branch you want to rebase)
2) git rebase main (this simply copy the things in main into that active branch you are in)
3)Handle any merge conflicts (if needed): git will show you the conflict markers like this:

<<<<<<< HEAD
Changes from the main branch
=======
Changes from the feature branch
>>>>>>> ft/new-branch-from-commit

4)Manually edit the file, keeping the changes you want. After resolving conflicts, stage the changes:
5) Finish the rebase:
Once all conflicts (if any) are resolved, Git will complete the rebase and move your feature branch commits on top of main
6)git rebase --continue
7)git push origin ft/new-branch-from-commit --force if you want to force push the changes to the remote branch

WORKING: 
rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)
$ git checkout ft/new-branch-from-commit
Switched to branch 'ft/new-branch-from-commit'

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (ft/new-branch-from-commit)
$ git rebase main
Successfully rebased and updated refs/heads/ft/new-branch-from-commit.

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (ft/new-branch-from-commit)
$ git push origin -u ft/new-branch-from-commit
Enumerating objects: 29, done.
Counting objects: 100% (29/29), done.
Delta compression using up to 8 threads
Compressing objects: 100% (22/22), done.
Writing objects: 100% (23/23), 10.60 KiB | 775.00 KiB/s, done.
Total 23 (delta 14), reused 0 (delta 0), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (14/14), completed with 2 local objects.
remote:
remote: Create a pull request for 'ft/new-branch-from-commit' on GitHub by visiting:
remote:      https://github.com/BabrahUSA20/GitAdvanced/pull/new/ft/new-branch-from-commit
remote:
To https://github.com/BabrahUSA20/GitAdvanced.git
 * [new branch]      ft/new-branch-from-commit -> ft/new-branch-from-commit
branch 'ft/new-branch-from-commit' set up to track 'origin/ft/new-branch-from-commit'.

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (ft/new-branch-from-commit)
$

```
### 9. Renaming Branches:
```bash
Branch names can sometimes evolve. Let's rename ft/new-branch-from-commit to a more descriptive name.
Challenge: Use git branch -m ft/new-branch-from-commit ft/improved-branch-name to rename your branch.

# SOLUTION:
STEPS:
1) Make you are in the branch you want to rename
2) git switch <branch-name you want to rename>
3)Rename the branch: git branch -m <new-branch-name>

WORKING:
rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)
$ git branch
  draft
  ft/new-branch-from-commit
* main

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)
$ git switch ft/new-branch-from-commit
Switched to branch 'ft/new-branch-from-commit'
Your branch is up to date with 'origin/ft/new-branch-from-commit'.

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (ft/new-branch-from-commit)
$ git branch -m ft/improved-branch-name

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (ft/improved-branch-name)
$ git push origin ft/improved-branch-name
Total 0 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
remote: 
remote: Create a pull request for 'ft/improved-branch-name' on GitHub by visiting:
remote:      https://github.com/BabrahUSA20/GitAdvanced/pull/new/ft/improved-branch-name
remote:
To https://github.com/BabrahUSA20/GitAdvanced.git
 * [new branch]   

```

### 10.Checking Out Detached HEAD:
```bash
In specific situations, you might need to detach HEAD from your current branch. Research git checkout <commit-hash> (replace with the desired commit hash) to understand this concept.

# SOLUTION:
STEPS:
1)git log --oneline
2) git checkout <commit hash> eg git checkout e4f5g6
3)Explore or make changes:You can look at files, test code, or even make changes — just know these changes won’t belong to any branch unless you save them.
4)Saving changes while in detached HEAD: if you made the change and want to commit them :
-->git checkout -b new-branch-from-detached
5) then get  back to your main branch: git checkout main


TO DELETE THE DETACHED HEAD: 
["you  can simple move to that main and write git reset --hard"]
1)git status (you will see something like this: HEAD is now at e4f5g6) 
2) leave the detached HEAD: git checkout main
3) you can save the change before leaving by : if you have made the change and you want to save them : git checkout -b new-branch-name

 (Optional) Discard changes:
4) git reset --hard 


# Challenges:  Part 3: Advanced Workflows (10+ Challenges)
### 1.Stashing Changes:
```bash
Imagine you're working on some changes in the main branch but need to attend to something urgent. You don't want to lose your uncommitted work.
Challenge: Stash your current changes in the main branch using git stash.

#SOLUTION:
STASHING : Stashing is perfect for exactly this kind of situation — when you need to put your current work aside without committing it! 

When you stash your changes, Git temporarily saves them away on a stack. You can then come back to your work when you're ready. by : git stash pop to remove from the stack and apply the changes. 

STEPS:
1) git status (you will see something like this: Changes not staged for commit
2) git stash it will hold the commit of the last that commmit but also you can
stash with your commit message.:
-->git stash push -m "WIP: Working on new feature"
3) git stash list : (if you want to see the stash list)
4)when you want to get back to your work you do :
-->git stash apply
-->git stash pop

NB: 
 Drop a stash without applying: git stash drop stash@{0}
If you want to clear everything in the stash: git stash clear


WORKING: 
rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)
$ git status
On branch main
Your branch is up to date with 'origin/main'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)
$ git stash
Saved working directory and index state WIP on main: 06f1d6d part 2 readme Update

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)
$ git stash push -m "WIP: Working on new feature"
No local changes to save

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)
$ git stash list
stash@{0}: WIP on main: 06f1d6d part 2 readme Update

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)
$ git stash apply
On branch main
Your branch is up to date with 'origin/main'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)
$ git stash pop
error: Your local changes to the following files would be overwritten by merge:
        README.md
Please commit your changes or stash them before you merge.
Aborting
On branch main
Your branch is up to date with 'origin/main'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")
The stash entry is kept in case you need it again.

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)
$ $ git stash push -m "WIP: Working on new feature"
bash: $: command not found

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)
$ git stash push -m "WIP: Working on new feature"
Saved working directory and index state On main: WIP: Working on new feature

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)
$ git stash pop
On branch main
Your branch is up to date with 'origin/main'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")
Dropped refs/stash@{0} (f3a00290f98efa38b341ac55a69c06dfd85d9437)

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)

```

### 3.Retrieving Stashed Changes:
```bash
Later, when you're ready to resume working on those stashed changes, you can retrieve them.
Challenge: Apply the most recent stash back onto the main branch using git stash pop.

#SOLUTION:

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)
$ git stash pop
error: Your local changes to the following files would be overwritten by merge:
        README.md
Please commit your changes or stash them before you merge.
Aborting
On branch main
Your branch is up to date with 'origin/main'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")
The stash entry is kept in case you need it again.

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)
$ $ git stash push -m "WIP: Working on new feature"
bash: $: command not found

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)
$ git stash push -m "WIP: Working on new feature"
Saved working directory and index state On main: WIP: Working on new feature

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)
$ git stash pop
On branch main
Your branch is up to date with 'origin/main'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")
Dropped refs/stash@{0} (f3a00290f98efa38b341ac55a69c06dfd85d9437)

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)
$

```
### 3.Branch Merging Conflicts (Continued):
```bash
Merge conflicts can arise when the same lines of code are modified in both branches being merged.
Challenge: Simulate a merge conflict scenario (you can create conflicting changes in a file on both main and a new feature branch). Then, try merging again and resolve the conflicts manually using your text editor.

SOLUTION:
rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)
$ git status
On branch main
Your branch is ahead of 'origin/main' by 1 commit.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)
$ git branch
  draft
  ft/improved-branch-name
* main

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)
$ git switch draft
Switched to branch 'draft'
Your branch and 'origin/main' have diverged,
and have 1 and 4 different commits each, respectively.
  (use "git pull" if you want to integrate the remote branch with yours)

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (draft)
$ gut pull 
bash: gut: command not found

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (draft)
$ git pull
Auto-merging draft.md
CONFLICT (add/add): Merge conflict in draft.md
Automatic merge failed; fix conflicts and then commit the result.

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (draft|MERGING)
$ git status
On branch draft
Your branch and 'origin/main' have diverged,
and have 1 and 4 different commits each, respectively.
  (use "git pull" if you want to integrate the remote branch with yours)

You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Changes to be committed:
        modified:   README.md

Unmerged paths:
  (use "git add <file>..." to mark resolution)
        both added:      draft.md

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   README.md


rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (draft|MERGING)
$ git merge
error: Merging is not possible because you have unmerged files.
hint: Fix them up in the work tree, and then use 'git add/rm <file>'
hint: as appropriate to mark resolution and make a commit.
fatal: Exiting because of an unresolved conflict.

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (draft|MERGING)
$ git add .

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (draft|MERGING)
$ git commit "merging in both files"
fatal: cannot do a partial commit during a merge.

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (draft|MERGING)
$ git status
On branch draft
Your branch and 'origin/main' have diverged,
and have 1 and 4 different commits each, respectively.
  (use "git pull" if you want to integrate the remote branch with yours)

All conflicts fixed but you are still merging.
  (use "git commit" to conclude merge)

Changes to be committed:
        modified:   README.md
        modified:   draft.md


rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (draft|MERGING)
$ git switch draft

```
### 4. Resolving Merge Conflicts with a Merge Tool:
```bash
Explore using a merge tool like git mergetool to help you visualize and resolve merge conflicts more efficiently.

#SOLUTION:
You can also set VS Code to be your default merge tool in Git, so it opens automatically when you use git mergetool.
1)Set VS Code as the default merge tool: git config --global merge.tool vscode
2)Configure VS Code's merge tool options: git config --global mergetool.vscode.cmd "code --wait $MERGED"
3)Run git mergetool:
When you have a conflict and want to use VS Code’s merge tool, just run:

->git mergetool

WORKING:
rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)
$ git config --global merge.tool vscode

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)
$ 

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)
$ git config --global mergetool.vscode.cmd "code --wait $MERGED"

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)
$ git switch draft 
Switched to branch 'draft'
Your branch and 'origin/main' have diverged,
and have 3 and 4 different commits each, respectively.
  (use "git pull" if you want to integrate the remote branch with yours)

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (draft)
$ git mergetool
No files need merging

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (draft)
$ git switch main
Switched to branch 'main'
Your branch is ahead of 'origin/main' by 2 commits.
  (use "git push" to publish your local commits)

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)
$

```
### 5.Understanding Detached HEAD State:
```bash
Detached HEAD refers to a state where your working directory is not associated with any specific branch. Research the implications and how to recover from this state using commands like git checkout <branch-name>.

What is Detached HEAD?
Normally, Git’s HEAD points to the latest commit on your current branch (e.g., main, develop, or any feature branch). When you checkout a branch, HEAD is pointing to that branch.


# SOLUTION:
However, when you checkout a specific commit (not a branch), Git detaches HEAD. This means HEAD no longer points to a branch, but instead to a specific commit. You’re still working with the same files and changes, but they’re not tied to any branch until you decide to create one.


Why does it happen?
It happens when you checkout a commit hash instead of a branch:
-->git checkout <commit-hash>

For example: git checkout e4f5g6d

Now, Git is in a detached HEAD state because HEAD is pointing directly to that commit, not a branch.

Implications of Detached HEAD:
==============================

1) You’re not on a branch: Changes you make won’t be associated with any branch unless you explicitly create a new branch from this state.

2)Any commits are "lost": If you make new commits while in a detached HEAD state and switch branches later, those commits could be lost. You can still access them if you remember the commit hash, but they aren’t tied to any branch.

3) Perfect for temporary exploration:Detached HEAD is useful when you want to explore previous commits, test something, or build off a specific commit without affecting your current branches.

Recovering from Detached HEAD State:
1. Switching back to an existing branch:
N-->git checkout main

2. Create a new branch from the detached HEAD:
If you want to keep the changes you made in the detached HEAD state, you can create a new branch from where HEAD is pointing:
-->git checkout -b new-branch-name


3. Discard changes in detached HEAD:
If you decide you no longer need any changes from the detached HEAD state, you can discard them:
-->git reset --hard

This will revert any uncommitted changes in the working directory, and you can switch back to your branch:
-->git checkout main

Key Commands:

Check current status:
-->git status
This will show if you're in a detached HEAD state.

Switch to a branch:
-->git switch <branch-name>

Create a new branch from detached HEAD:
-->git checkout -b <new-branch-name>

Return to the previous branch:
-->git checkout -

```


### 6.Ignoring Files/Directories:
```bash
You might have files or directories you don't want to track in Git. Create a .gitignore file to specify these exclusions.
Challenge: Add a pattern like /tmp to your .gitignore file to exclude all temporary files and directories from version control. more about ignoring files here


# SOLUTION:
gitignore is a simple text file that lists patterns for files and directories to ignore in Git.

STEPS:
1. Create a .gitignore File
To start, you can create a .gitignore file in the root of your Git repository.
-->touch .gitignore :(Alternatively, you can manually create the file using a text editor, like VS Code.)

2. Edit the .gitignore File
The .gitignore file is where you specify which files or directories Git should ignore. You can list specific files, file types, or entire directories. Each pattern you add to this file tells Git to exclude those files from tracking.

Here are some examples of what you might put in the .gitignore file:

Ignore specific files:
secrets.txt
This will ignore the file secrets.txt.

Ignore all files of a certain type:
-->*.log
This will ignore all files ending with .log.


Ignore a specific directory:
node_modules/
This will ignore the node_modules directory and its contents.

Ignore all files and directories except one specific file:

*
!important-file.txt
[This will ignore everything in the repository except for important-file.txt.]

Ignore files by pattern:
-->*.bak
This will ignore any file ending with .bak.

Ignore files in a specific directory:
-->build/*
This will ignore everything in the build directory.

Ignore OS and IDE specific files:
It’s common to ignore files generated by your operating system or IDE. Here’s an example for macOS and Visual Studio Code:

.DS_Store
.vscode/

3. Apply .gitignore to Already Tracked Files
If you have already tracked files that are now in .gitignore, Git will continue to track them unless you remove them from the repository. To stop tracking files that are already being tracked, you’ll need to run:

git rm --cached <file>

For example:
git rm --cached secrets.txt
This will remove the file from Git’s tracking, but not delete it from your working directory. It will be ignored moving forward.

4. Check Status
After updating your .gitignore, run:

git status
This will show you any files that are still being tracked or ignored, and you can verify that the right files are excluded.

5. Commit the .gitignore File
Once you've configured .gitignore, make sure to commit it to your repository so others working on the project will have the same ignore rules:

git add .gitignore
git commit -m "Add .gitignore to exclude unwanted files"
git push


WORKING:
rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)
$ mkdir tmp

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)
$ touch tmp/temp-file.txt

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)
$ git status
On branch main
Your branch is ahead of 'origin/main' by 3 commits.
  (use "git push" to publish your local commits)

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        .gitignore
        tmp/

nothing added to commit but untracked files present (use "git add" to track)

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)
$ git add .gitignore

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)
$ git commit -m "Add /tmp to .gitignore to exclude temporary files"
[main 96f427b] Add /tmp to .gitignore to exclude temporary files
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 .gitignore

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)
$ git status
On branch main
Your branch is ahead of 'origin/main' by 4 commits.
  (use "git push" to publish your local commits)

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   .gitignore

no changes added to commit (use "git add" and/or "git commit -a")

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)
$ git add .gitignore

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)
$ git commit -m "Add /tmp to .gitignore to exclude temporary files"
[main dd7b3cf] Add /tmp to .gitignore to exclude temporary files
 1 file changed, 1 insertion(+)

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)
$ git push
Enumerating objects: 16, done.
Counting objects: 100% (16/16), done.
Delta compression using up to 8 threads
Compressing objects: 100% (13/13), done.
Writing objects: 100% (14/14), 5.35 KiB | 498.00 KiB/s, done.
Total 14 (delta 8), reused 0 (delta 0), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (8/8), completed with 2 local objects.
To https://github.com/BabrahUSA20/GitAdvanced.git
   06f1d6d..dd7b3cf  main -> main

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)


```

### 7.Working with Tags:
```bash
Tags act like bookmarks in your Git history. Create a tag to mark a specific point in your development.
Challenge: Use git tag v1.0 to create a tag named v1.0 on the current commit in your main branch. git tags


# SOLUTION:
["ags make a point as a specific point in Git history. Tags are used to mark a commit stage as relevant. We can tag a commit for future reference. Primarily, it is used to mark a project's initial point like v1.1."]


A tag in Git is like a bookmark or a snapshot of a specific commit — usually used to mark important points in your project’s history, like releases (v1.0, v2.1).

Why use tags?

Mark versions: Tagging stable releases like v1.0, v2.0-beta.
Easier navigation: Quickly return to a specific point in the project’s history.
Deployment references: Use tags to deploy specific versions of your code.

STEPS:
1)first check out the branch you want your tag tobe: git checkout main
2)create a new tag: git tag v1.0 or "git tag -a v1.0 -m "Version 1.0 release" (with a commit message).
3) verify the tag: git show v1.0 (to see the details of the tag)"
4) push the tag to the remote repository: git push origin v1.0 (it is always pushed separately to avoid accidentally pushing a tag to the wrong branch).
5)


Git List Tag
We can list the available tags in our repository. There are three options that are available to list the tags in the repository. They are as follows:

git tag:
["It is the most generally used option to list all the available tags from the repository. It is used as:"]

git show :
["It's a specific command used to display the details of a particular tag
syntax: git show <tagname>"]

git tag -l ".*":
["It is also a specific command-line tool. It displays the available tags using wild card pattern. Suppose we have ten tags as v1.0, v1.1, v1.2 up to v1.10. Then, we can list all v pattern using tag pattern v. it is used as:"]

["syntax:$ git tag -l "<pattern>.*"  like :$ git tag -l "pro*"  "] it will list all tags starting with 'pro'".




WORKING:
rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)
$ git tag v1.0

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)
$ git tag
v1.0

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)
$ git tag -a v1.0 -m "Version 1.0 release"
fatal: tag 'v1.0' already exists

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)
$ git tag -d v1.0
Deleted tag 'v1.0' (was d3939af)

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)
$ git tag -a v1.0 -m "am creating Version 1.0 release which is a tag"

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)
$ git tag
v1.0

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)
$ git show v1.0
tag v1.0
Tagger: Your Name <you@example.com>
Date:   Tue Mar 4 12:32:56 2025 +0200

am creating Version 1.0 release which is a tag

commit d3939af9d7d1bbb38d7e8cfae6456bb60cac8e0d (HEAD -> main, tag: v1.0)
Author: Your Name <you@example.com>
Date:   Tue Mar 4 12:25:26 2025 +0200

    readme update

diff --git a/README.md b/README.md

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)
$ git push origin v1.0
Enumerating objects: 6, done.
Counting objects: 100% (6/6), done.
Delta compression using up to 8 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (4/4), 453 bytes | 151.00 KiB/s, done.
Total 4 (delta 2), reused 0 (delta 0), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
To https://github.com/BabrahUSA20/GitAdvanced.git
 * [new tag]         v1.0 -> v1.0

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)
$
```

### 8.Listing and Deleting Tags:
```bash
Challenge: Use git tag to list all existing tags. Then, use git tag -d <tag-name> to delete a specific tag (replace <tag-name> with the actual tag you want to remove).

# SOLUTION:
TO DELETE TAGS:
1) git tag -d <tagname> (to delete a local tag)
2) DELETE A TAG FROM REMOTE REPO: git push origin :refs/tags/<tagname> (to delete a remote tag)
EG:git push origin --delete v1.0

WORKING:

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)
$ git tag v1.0

rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)
$ git tag
v1.0
rurmi@Babrah MINGW64 ~/Documents/CLONING WEBSITES/GitAdvanced (main)
$ git tag -d v1.0
Deleted tag 'v1.0' (was d3939af)
```

### 9.Pushing Local Work to Remote Repositories:
```bash
Once you're happy with your local changes and branches, it's time to share them with others.
Challenge: Assuming you've set up a remote repository on a Git hosting platform (like GitHub), push the changes with the actual branch you want to push to push your local branch to the remote repository.

# SOLUTION:
STEPS:
1)check the branch you want to push: git branch or git checkout feature-branch
2)git status
3)git add .
4)git commit -m "Your commit message"
5)git push origin <branch-name> or 
if it is your first time pushing to the remote repository: git push -u origin <branch-name> or git push --set-upstream origin feature-branch

6) after that you can simply  use : git push


WORKING:


 ```

### 10.Pulling Changes from Remote Repositories:
```bash
Collaboration often involves pulling changes from the remote repository made by others.
Challenge: Navigate to Github and make some changes inside your README file that you created on your main branch and in your local environment use git pull origin <branch-name> (replace <branch-name> with the actual branch you want to pull) to fetch changes from the remote repository's main branch and merge them into your local main branch. Address any merge conflicts that might arise.

# SOLUTION:
STEPS:
1) I am adding this content dynamically
2) am mackinng the change that i will be commiting directlt to the main branch

WORKING:

```

