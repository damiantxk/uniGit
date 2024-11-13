# Git Cheat Sheet

## Initializing a Repository
- **Initialize a new Git repository**:  
  ```bash
  git init
  ```
- **Stop tracking Git repository**:  
  ```bash
  rm -rf .git  # removes the .git directory
  ```

## Viewing Changes
- **See the current status of files (modified/untracked)**:  
  ```bash
  git status
  ```
- **See differences between changes**:  
  ```bash
  git diff
  ```

## .gitignore
- **Create a `.gitignore` file** to list files/folders you want Git to ignore.

## Three Stages in Git
1. **Working Directory**: Contains untracked or modified files.
2. **Staging Area**: Organize files to commit in batches.
3. **.git Directory**: Stores repository metadata and history.

## Staging Changes
- **Add all files to the staging area**:  
  ```bash
  git add -A
  ```
- **See what is staged**:  
  ```bash
  git status
  ```
- **Remove a specific file from staging area**:  
  ```bash
  git reset <file.js>
  ```
- **Remove all files from staging area**:  
  ```bash
  git reset
  ```

## Committing Changes
- **Commit changes with a message**:  
  ```bash
  git commit -m "Message"
  ```
- **Check commit log**:  
  ```bash
  git log
  ```

## Tracking an Existing Repository
- **Clone an existing repository**:  
  ```bash
  git clone <url> <directory_path>  # use . for the current directory
  ```
- **List remote repositories**:  
  ```bash
  git remote -v
  ```

## Branches
- **List all branches (local and remote)**:  
  ```bash
  git branch -a
  ```
- **Create a new branch**:  
  ```bash
  git branch <branch-name>
  ```
- **Switch to a branch**:  
  ```bash
  git checkout <branch-name>
  ```
- **Create and switch to a new branch**:  
  ```bash
  git checkout -b <branch-name>
  ```
- **Delete a branch locally**:  
  ```bash
  git branch -d <branch-name>
  ```
- **Delete a branch on the remote**:  
  ```bash
  git push origin --delete <branch-name>
  ```

## Pushing and Pulling Changes
- **Pull latest changes from a branch**:  
  ```bash
  git pull origin <branch>
  ```
- **Push changes to remote repository**:  
  ```bash
  git push origin <branch>
  ```
- **Associate local branch with remote branch (first time only)**:  
  ```bash
  git push -u origin <branch-name>
  ```

## Merging Branches
- **Switch to master branch**:  
  ```bash
  git checkout master
  ```
- **Merge another branch into the current branch**:  
  ```bash
  git merge <branch-name>
  ```
- **Push merged changes to remote**:  
  ```bash
  git push origin master
  ```
- **Check if a branch has been merged**:  
  ```bash
  git branch --merged
  ```

## Example Workflow -- Impt
1. **Create and switch to a new branch**:  
   ```bash
   git branch <branch-name>
   git checkout <branch-name>
   ```
2. **Make changes, then stage and commit**:  
   ```bash
   git add -A
   git commit -m "Description"
   ```
3. **Push branch to remote and set tracking**:  
   ```bash
   git push -u origin <branch-name>
   ```
4. **Ensure master branch is up-to-date**:  
   ```bash
   git checkout master
   git pull origin master
   ```
5. **Merge branch into master**:  
   ```bash
   git merge <branch-name>
   git push origin master
   ```
6. **Delete the branch locally and remotely if no longer needed**:  
   ```bash
   git branch -d <branch-name>
   git push origin --delete <branch-name>
   ```

## Making and Unstaging Changes
- **Stage changes** (after modifying `file.js`):  
  ```bash
  git add file.js
  ```
- **Unstage changes** (if you decide not to commit yet):  
  ```bash
  git restore --staged file.js
  ```

## Restoring Deleted Files
- **Restore a file accidentally deleted**:  
  ```bash
  git restore file.js
  ```

## Viewing Commit History
- **View all changes made in each commit**:  
  ```bash
  git log -p  # -p shows the diff for each commit
  ```

## Going Back to a Previous Commit
- **Revert to an earlier commit**:  
  ```bash
  git reset <commit-code>  # <commit-code> is the commit hash from git log
  ```

## Rebasing Commits
Git rebase is used to reapply commits on top of another base tip, typically to clean up or reorganize commit history.

### Interactive Rebase from the Root Commit
- **Start an interactive rebase from the first commit**:  
  ```bash
  git rebase -i --root
  ```

### Rebase from a Specific Commit
- **Start an interactive rebase from a specific commit onward**:  
  ```bash
  git rebase -i <commit-code>
  ```

### Rebase to Update with a Remote Branch
- **Reapply commits on top of the latest changes in `origin/master`**:  
  ```bash
  git rebase origin/master
  ```

### Rebase Options in Interactive Mode
When running `git rebase -i`, you’ll enter a text editor with a list of commits and options to manage them:
- **Pick**: Keeps the commit as-is.
- **Edit**: Allows you to make changes to the commit, including its message or staged content.
- **Squash (s)**: Combines this commit with the one directly before it.
- **Fixup (f)**: Similar to `squash`, but discards the commit message.
- **Drop**: Removes the commit from history entirely.

## Example Rebase Workflow
1. **Start an interactive rebase** (for the last 3 commits):  
   ```bash
   git rebase -i HEAD~3
   ```
2. **Choose options (`pick`, `edit`, `squash`, etc.) for each commit** and save.
3. **If you chose `edit`, make changes and re-commit**:  
   ```bash
   git add <file.js>
   git commit --amend
   git rebase --continue
   ```
4. **If conflicts arise, resolve them**:
   - Add changes:  
     ```bash
     git add <file.js>
     ```
   - Continue rebasing:  
     ```bash
     git rebase --continue
     ```

## Example Workflow for Fixing Commit History
1. **Check commit history**:  
   ```bash
   git log
   ```
2. **Rebase interactively to organize commits**:  
   ```bash
   git rebase -i HEAD~4  # for the last 4 commits
   ```
3. **Combine or remove commits as needed** using `squash`, `edit`, or `drop` options.
4. **Complete the rebase**:  
   Resolve conflicts if needed, then run:  
   ```bash
   git rebase --continue
   ```

--- 

To make sure code is up to date,
 git checkout main
 git pull
 git checkout YOUR_BRANCH_HERE
 git rebase main

