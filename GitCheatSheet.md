## Git Cheat Sheet

### SETUP

Configuring user information used across all local repositories:

    git config --global user.name “[firstname lastname]” 

Set a name that is identifiable for credit when review version history.

`git config --global user.email “[valid-email]”` 

Set an email address that will be associated with each history marker.

    git config --global color.ui auto 

Set automatic command line coloring for Git for easy reviewing.

### SETUP & INIT

Configuring user information, initializing and cloning repositories:

    git init 

Initialize an existing directory as a Git repository.

    git clone [url] 

Retrieve an entire repository from a hosted location via URL.


### INSPECT & COMPARE 

Examining logs, diffs and object information:

    git log 

Show the commit history for the currently active branch.

    git log branchB..branchA 

Show the commits on branchA that are not on branchB.

    git log --follow [file] 

Show the commits that changed file, even across renames.

    git diff branchB...branchA 

Show the diff of what is in branchA that is not in branchB.

    git show [SHA] 

Show any object in Git in human-readable format.

### TRACKING PATH CHANGES 

Versioning file removes and path changes:

    git rm [file] 

Delete the file from project and stage the removal for commit.

    git mv [existing-path] [new-path] 

Change an existing file path and stage the move.

    git log --stat -M 

Show all commit logs with indication of any paths that moved.


### STAGE & SNAPSHOT 

Working with snapshots and the Git staging area git status show modified files in working directory, staged for your next commit :

    git add [file] 

Add a file as it looks now to your next commit (stage).

    git reset [file] 

Unstage a file while retaining the changes in working directory.

    git diff 

Diff of what is changed but not staged.

    git diff --staged 

Diff of what is staged but not yet commited.

    git commit -m “[descriptive message]” 

Commit your staged content as a new commit snapshot.

    git cherry-pick <commit-hash>

Cherry picking in Git means to choose a commit from one branch and apply it onto another. This is in contrast with other ways such as  `merge`  and  `rebase`  which normally apply many commits onto another branch.

### BRANCH & MERGE 

Isolating work in branches, changing context, and integrating changes:

    git branch 

List your branches. A * will appear next to the currently active branch.

    git branch [branch-name] 

Create a new branch at the current commit.

    git checkout 

Switch to another branch and check it out into your working directory.

    git merge [branch] 

Merge the specified branch’s history into the current one.

    git log 

Show all commits in the current branch’s history.


### TEMPORARY COMMITS 

Temporarily store modified, tracked files in order to change branches :

    git stash 

Save modified and staged changes.

    git stash list 

List stack-order of stashed file changes.

    git stash pop 

Write working from top of stash stack.

    git stash drop 

Discard the changes from top of stash stack.
