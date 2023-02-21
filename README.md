# Git

## Configuring git

- Need to set the name and email of the user

```bash
git config --global user.name "<name>"
git config --global user.email "<email-id>"
```

---

## Introduction

- Repositories
  ![](images/Screenshot%20from%202023-02-15%2023-17-29.png)

- Basic commands

```bash
# Creating a git repository, At the top level folder containing the project
git init
# Checking the status for git repository
git status
# See the logs
git log
# or
git log --oneline
```

- Adding
  ![](images/Screenshot%20from%202023-02-15%2023-34-15.png)

```bash
git add file1 file2
# or
git add . # stage all changes at once
```

- Commiting
  ![](images/Screenshot%20from%202023-02-15%2023-16-57.png)

```bash
git commit -m "<inline-message>"
```

- Git workflow
  ![](images/Screenshot%20from%202023-02-15%2023-33-00.png)

---

## Working with git

- Amending commits: Redoing the **previous** commit

```bash
git commit -m "commit-msg"
git add file1
git commit --amend # modifies the prev commit to include file1
```

- Writing commit messages: Follow present tense imperative style eg. Add feature 1
- Atomic commits
  ![](images/Screenshot%20from%202023-02-16%2022-45-08.png)
- Ignoring files: .gitignore
  ![](images/Screenshot%20from%202023-02-16%2022-46-05.png)
  ![](images/Screenshot%20from%202023-02-16%2022-46-23.png)

---

## Git branching

- Stucture of git commits
  ![](images/Screenshot%20from%202023-02-16%2023-28-07.png)
- Branches: Useful for segregating multiple contexts
  ![](images/Screenshot%20from%202023-02-16%2023-29-33.png)
  ![](images/Screenshot%20from%202023-02-16%2023-31-26.png)
- Head
  - Head points to a Branch reference and a Branch reference points to a commit
    ![](images/Screenshot%20from%202023-02-16%2023-34-44.png)
- Viewing all branches
  ![](images/Screenshot%20from%202023-02-16%2023-38-49.png)

```bash
git branch
git branch -v # to view more info
```

- Creating a new branch
  ![](images/Screenshot%20from%202023-02-16%2023-39-42.png)
  ![](images/Screenshot%20from%202023-02-16%2023-50-37.png)

```bash
git branch <branch-name>
```

![](images/Screenshot%20from%202023-02-16%2023-40-35.png)

- Switching branches
  ![](images/Screenshot%20from%202023-02-16%2023-43-10.png)
  ![](images/Screenshot%20from%202023-02-16%2023-47-17.png)

```bash
git switch <branch-name> # newer
# or
git checkout <branch-name> #older

# switch to new branch while also creating it
git switch -c <branch-name>
```

_Note: Untracked files follow the head to wherever it goes while if we have some changes in tracked files and we try to switch branches then git gives us an error_

- Deleting branch
  - Switch to some other branch as cannot delete the branch at which we are currently checked out

```bash
git branch -d <branch-name>
# or
git branch -D <branch-name> #delete a branch which is not fully merged; Shortcut for -df (--delete --force)
```

- Renaming branch
  - Switch to branch you want to rename

```bash
git branch -m <new-branch-name>
```

- Merging branches
  - We merge branches, not specific commits
  - We always merge to the current HEAD branch
  - To merge a branch into another
    - Switch to branch you want to merge the changes into (receiving branch)
    - use `git merge <branch-name>` to merge
      ![](images/Screenshot%20from%202023-02-20%2022-33-34.png)
      ![](images/Screenshot%20from%202023-02-20%2022-34-52.png)
  - **Fast forward merge (Catch up)**
    ![](images/Screenshot%20from%202023-02-20%2022-40-08.png)
    ![](images/Screenshot%20from%202023-02-20%2022-40-35.png)
  - **Merge commits**
    - They have multiple parents
      ![](images/Screenshot%20from%202023-02-20%2022-59-30.png)
      ![](images/Screenshot%20from%202023-02-20%2022-59-37.png)
      ![](images/Screenshot%20from%202023-02-20%2022-59-44.png)
      ![](images/Screenshot%20from%202023-02-20%2022-59-48.png)
  - **Merge conflicts**
    ![](images/Screenshot%20from%202023-02-20%2023-06-32.png)
    ![](images/Screenshot%20from%202023-02-20%2023-06-59.png)
    - Conflict markers: Git changes the contents of your files to indicate the conflicts that it wants you to resolve by adding some markers
      ![](images/Screenshot%20from%202023-02-20%2023-10-15.png)
      ![](images/Screenshot%20from%202023-02-20%2023-11-01.png)
    - Resolving conflicts
      ![](images/Screenshot%20from%202023-02-20%2023-12-14.png)

---

## Git Diff

![](images/Screenshot%20from%202023-02-21%2000-34-51.png)
![](images/Screenshot%20from%202023-02-21%2000-38-06.png)

```bash
git diff #shows changes between the staging area and working directory
```

![](images/Screenshot%20from%202023-02-21%2001-12-00.png)
![](images/Screenshot%20from%202023-02-21%2001-12-53.png)
![](images/Screenshot%20from%202023-02-21%2001-13-06.png)
![](images/Screenshot%20from%202023-02-21%2001-13-20.png)
![](images/Screenshot%20from%202023-02-21%2001-13-28.png)
![](images/Screenshot%20from%202023-02-21%2001-13-43.png)
![](images/Screenshot%20from%202023-02-21%2001-13-52.png)
![](images/Screenshot%20from%202023-02-21%2001-14-04.png)
![](images/Screenshot%20from%202023-02-21%2001-14-12.png)

```bash
git diff HEAD #lists all changes in the working directory since the last commit; staged + unstaged changes

git diff --staged #shows diff between the staging area and the last commit; "Show me what will be included in my commit if I run git commit right now"
# OR
git diff --cached

# diff-ing particular files
git diff HEAD <filename>
# OR
git diff --staged <filename>

# diff-ing branches
git diff branch1..branch2

# diff-ing commits
git diff commit1..commit2
```

---

## Stashing

- Switching from one branch to another:
  - If there are conflicting changes then we would get error on switching
  - Else the changes follow us to the new branch
    ![](images/Screenshot%20from%202023-02-22%2001-01-28.png)
    ![](images/Screenshot%20from%202023-02-22%2001-02-56.png)

```bash
git stash list # View the list of stashes

git stash
# OR
git stash save # Saves all the uncommited changes to the stash; Doesn't includes the untracked files

git stash -u # Saves all the uncommited files including the untracked files to stash

git stash pop # Removes the most recently stashed changes in your stash and re-apply them to your working copy.

git stash apply # applies whatever is in the stash to the current branch without deleting it from the stash
# OR
git stash apply <stash-name> # Applies a particular stash

git stash clear # Deletes all the stashes
# OR
git stash drop <stash-name> # Deletes a particular stash
```

![](images/Screenshot%20from%202023-02-22%2001-05-14.png)
![](images/Screenshot%20from%202023-02-22%2001-06-42.png)
![](images/Screenshot%20from%202023-02-22%2001-06-58.png)
![](images/Screenshot%20from%202023-02-22%2001-07-21.png)
![](images/Screenshot%20from%202023-02-22%2001-09-38.png)

---
