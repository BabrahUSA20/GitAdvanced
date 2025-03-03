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