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

```sh
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

## Undoing changes

- **Detached HEAD**
  ![](images/Screenshot%20from%202023-02-22%2008-23-39.png)
  ![](images/Screenshot%20from%202023-02-22%2008-23-53.png)
  ![](images/Screenshot%20from%202023-02-22%2008-24-22.png)
  ![](images/Screenshot%20from%202023-02-22%2008-24-50.png)
  - In detached head state we can do following things: - Stay in detached HEAD to examine the contents of the old commit. Poke around, view the files, etc - Leave and go back to wherever you were before - reattach the HEAD - Create a new branch and switch to it. You can now make and save changes, since HEAD is no longer detached.
- ![](images/Screenshot%20from%202023-02-22%2008-29-02.png)

```bash
# git checkout: Used to create branches, switch to new branches, restore files, and undo history
git checkout <commit-hash> # Detached head statte
git switch <branch-name> # Reattach the head

git checkout HEAD~1 # Previous commit
git checkout HEAD~2 # (Head - 2)th commit

git switch - # Switch to the last branch we were on

git checkout HEAD <filename> # Discard any changes in the file and make the match the content of the file at HEAD
# OR
git checkout -- <filename> # Discard any changes in the file

git restore <filename> # Discard any changes in the file and make the match the content of the file at HEAD
git restore --source <commit-hash> <file-name> # Discard any changes in the file and make the match the content of the file at the commit
git restore --staged <filename> # Remove a file from the staging area
```

- Git reset
  ![](images/Screenshot%20from%202023-02-22%2008-53-53.png)
  ![](images/Screenshot%20from%202023-02-22%2008-54-14.png)
  ![](images/Screenshot%20from%202023-02-22%2008-54-56.png)
  ![](images/Screenshot%20from%202023-02-22%2008-56-01.png)
  ![](images/Screenshot%20from%202023-02-22%2008-56-41.png)
  ![](images/Screenshot%20from%202023-02-22%2008-56-51.png)

```bash
git reset <commit-hash> # Soft reset; Removes the commits but keeps the changes
git reset --hard <commit-hash> # Hard reset; Removes the commits as well as changes
```

- Git revert
  ![](images/Screenshot%20from%202023-02-22%2008-59-44.png)
  ![](images/Screenshot%20from%202023-02-22%2009-00-06.png)
  ![](images/Screenshot%20from%202023-02-22%2009-00-15.png)
  ![](images/Screenshot%20from%202023-02-22%2009-00-25.png)
  ![](images/Screenshot%20from%202023-02-22%2009-00-35.png)
  - Both git reset and git revert help us reverse changes, but there is a significant difference when it comes to collaboration. If you want to **reverse some commits** that **other people already have on their machines**, you should **use revert**. If you want to **reverse commits that you haven't shared with others**, **use reset** and no one will ever know!

---

## GitHub

- Github is a hosting platform for git repositories. You can put your own Git repos on Github and access them from anywhere and share them with people around the world. Beyond hosting repos, Github also provides additional collaboration features that are not native to Git (but are super useful). Basically, Github helps people share and collaborate on repos.
  ![](images/Screenshot%20from%202023-02-23%2023-20-40.png)
- **Cloning**
  - Git will retrieve all the files associated with the repository and will copy them to your local machine.

```bash
git clone <repo-url>
```

- Adding remote to an existing local repo
  ![](images/Screenshot%20from%202023-02-23%2023-52-24.png)
  ![](images/Screenshot%20from%202023-02-23%2023-56-15.png)

```bash
# View remotes
git remote -v
# OR
git remote

# Adding a new remote
git remote add <name> <url> # name is just a label or alias for a particular remote

# removing a remote
git remote remove <name>

# renaming a remote
git remote rename <old-name> <new-name>
```

- Pushing
  ![](images/Screenshot%20from%202023-02-24%2000-27-11.png)
  ![](images/Screenshot%20from%202023-02-24%2000-27-43.png)

```bash
# pushing the code to remote
git push <remote> <branch>

# pushing a local branch to a different remote branch
git push <remote> <local-branch>:<remote-branch>

# setting upstream of a branch
git push -u <remote> <branch>
```

## ![](images/Screenshot%20from%202023-02-24%2000-28-55.png)

---

## Fetch and pull

![](images/Screenshot%20from%202023-02-24%2000-36-11.png)
![](images/Screenshot%20from%202023-02-24%2000-36-29.png)
![](images/Screenshot%20from%202023-02-24%2000-36-37.png)

```bash
# View remote references
git remote -r
```

![](images/Screenshot%20from%202023-02-24%2000-43-36.png)
![](images/Screenshot%20from%202023-02-24%2000-43-52.png)

- On cloning a new repo, Only the default branch is tracking the remote/default-branch
  ![](images/Screenshot%20from%202023-02-24%2000-48-43.png)

```bash
git remote -r # list all remote branches

# track a remote branch via a local branch
git switch <remote-branch-name> # makes a local branch AND sets it up to track the concerned remote branch
# OR
git checkout --track <remote>/<branch-name>
```

![](images/Screenshot%20from%202023-02-24%2000-52-27.png)

- **Fetch**
  ![](images/Screenshot%20from%202023-02-24%2001-03-51.png)
  ![](images/Screenshot%20from%202023-02-24%2001-04-19.png)
  ![](images/Screenshot%20from%202023-02-24%2001-05-21.png)

```bash
# Fetching
git fetch <remote>
git fetch <remote> <branch>
git fetch # updates the list of remote branches
```

![](images/Screenshot%20from%202023-02-24%2001-06-14.png)
![](images/Screenshot%20from%202023-02-24%2001-06-23.png)
![](images/Screenshot%20from%202023-02-24%2001-06-32.png)

- **Pulling**
  ![](images/Screenshot%20from%202023-02-24%2001-07-04.png)
  ![](images/Screenshot%20from%202023-02-24%2001-07-18.png)
  ![](images/Screenshot%20from%202023-02-24%2001-08-39.png)
  ![](images/Screenshot%20from%202023-02-24%2001-09-18.png)
  ![](images/Screenshot%20from%202023-02-24%2001-09-53.png)

```bash
# Run it from the branch where you want to merge the pulled changes
git pull <remote> <branch>
```

![](images/Screenshot%20from%202023-02-24%2001-10-09.png)

---

## Git collaboration workflows

- **Centralized workflows**
  - The simplest collaborative workflow is to have everyone work on the master branch (or main, or any other SINGLE branch).
  - Issues
    - Lots of time spent resolving conflicts and merging code, especially as team size scales up.
    - No one can work on anything without disturbing the main codebase. How do you try adding something radically different in? How do you experiment?
    - The only way to collaborate on a feature together with another teammate is to push incomplete code to master. Other teammates now have broken code...
- **Feature branches**
  ![](images/Screenshot%20from%202023-02-25%2004-45-31.png)
  ![](images/Screenshot%20from%202023-02-25%2004-44-19.png)
  ![](images/Screenshot%20from%202023-02-25%2004-44-48.png)
  - Pull requests
    ![](images/Screenshot%20from%202023-02-25%2004-46-22.png)
- The workflow
  ![](images/Screenshot%20from%202023-02-25%2004-46-52.png)
  ![](images/Screenshot%20from%202023-02-25%2004-49-54.png)
  ![](images/Screenshot%20from%202023-02-25%2004-50-56.png)
- Fork and clone: Another workflow
  ![](images/Screenshot%20from%202023-02-25%2004-51-43.png)
  ![](images/Screenshot%20from%202023-02-25%2004-52-07.png)
  ![](images/Screenshot%20from%202023-02-25%2004-53-06.png)
  ![](images/Screenshot%20from%202023-02-25%2004-53-19.png)
  ![](images/Screenshot%20from%202023-02-25%2004-53-33.png)
  ![](images/Screenshot%20from%202023-02-25%2004-54-16.png)
  ![](images/Screenshot%20from%202023-02-25%2004-54-26.png)
  ![](images/Screenshot%20from%202023-02-25%2004-55-04.png)
  ![](images/Screenshot%20from%202023-02-25%2004-55-15.png)

---

## Rebasing

![](images/Screenshot%20from%202023-02-25%2019-00-59.png)
![](images/Screenshot%20from%202023-02-25%2019-05-38.png)
![](images/Screenshot%20from%202023-02-25%2019-05-49.png)
![](images/Screenshot%20from%202023-02-25%2019-06-25.png)

```bash
# Cleaning history
git switch feature # switch to branch which is to be rebased
git rebase master # the branch on whom to rebase
```

![](images/Screenshot%20from%202023-02-25%2019-06-39.png)
![](images/Screenshot%20from%202023-02-25%2019-07-03.png)
![](images/Screenshot%20from%202023-02-26%2013-57-14.png)

![](images/Screenshot%20from%202023-02-26%2014-12-38.png)
![](images/Screenshot%20from%202023-02-26%2014-13-58.png)

```bash
# Interactive rebase
git rebase -i <commit-hash> # inplace rebasing
# eg. git rebase -i HEAD~9
```

---

## Git tags

![](images/Screenshot%20from%202023-02-26%2021-33-18.png)
![](images/Screenshot%20from%202023-02-26%2021-33-37.png)
![](images/Screenshot%20from%202023-02-26%2021-33-53.png)
![](images/Screenshot%20from%202023-02-26%2021-34-11.png)
![](images/Screenshot%20from%202023-02-26%2021-34-31.png)
![](images/Screenshot%20from%202023-02-26%2021-34-51.png)
![](images/Screenshot%20from%202023-02-26%2021-35-00.png)
![](images/Screenshot%20from%202023-02-26%2021-35-26.png)
![](images/Screenshot%20from%202023-02-26%2021-35-35.png)

```bash
git tag # List all tags
git tag -l "<pattern>" # List all tags satisfying the pattern

git checkout <tag-name> # To checkout at a particular tag

git tag <tag-name> # Create a lightweight tag, By default, Git will create the tag referring to the commit that HEAD is referencing
git tag -a <tag-name> # Create annotated tags
# OR
git tag -a <tag-name> -m <message>
# OR
git tag <tag-name> <commit-hash> # Tagging previous commits

git tag -f <tag-name> # Forcing the reuse of a used tag

git tag -d <tag-name> # Deleting a tag

# By default, the git push command doesn’t transfer tags to remote servers.
git push --tags # Transfer all of your tags to the remote server that are not already there.
```

---

## Git behind the scenes

![](images/Screenshot%20from%202023-02-26%2021-54-48.png)
![](images/Screenshot%20from%202023-02-26%2021-55-19.png)
![](images/Screenshot%20from%202023-02-26%2021-55-43.png)
![](images/Screenshot%20from%202023-02-26%2021-56-00.png)
![](images/Screenshot%20from%202023-02-26%2021-56-13.png)
![](images/Screenshot%20from%202023-02-26%2021-56-42.png)
![](images/Screenshot%20from%202023-02-26%2021-57-04.png)

- Git uses the SHA-1 algorithm
  ![](images/Screenshot%20from%202023-02-26%2023-30-53.png)
- Git hash-object
  ![](images/Screenshot%20from%202023-02-27%2000-08-38.png)

```bash
echo hello | git hash-object --stdin # Just spits out the hashed value without writing anything to .git directory
echo hello | git hash-object --stdin -w # write the content of the input in .git/objects folder
git cat-file -p <object-hash> # Takes the stored file in the .git/objects directory and converts it back to the original file; -p is for pretty print
```

![](images/Screenshot%20from%202023-02-27%2000-12-38.png)
![](images/Screenshot%20from%202023-02-27%2000-13-00.png)
![](images/Screenshot%20from%202023-02-27%2000-13-12.png)
![](images/Screenshot%20from%202023-02-27%2000-15-06.png)
![](images/Screenshot%20from%202023-02-27%2000-15-19.png)
![](images/Screenshot%20from%202023-02-27%2000-15-34.png)
![](images/Screenshot%20from%202023-02-27%2000-16-01.png)
![](images/Screenshot%20from%202023-02-27%2000-16-20.png)
![](images/Screenshot%20from%202023-02-27%2000-16-28.png)

```bash
# Viewing trees
git cat-file -p master^{tree} # master^{tree} syntax specifies the tree object that is pointed to by the tip of our master branch

git cat-file -t <commit-hash> # type of git object
```

---
