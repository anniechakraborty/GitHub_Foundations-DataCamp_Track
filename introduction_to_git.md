# Introduction to Git
Notes from the DataCamp track on [GitHub Foundations](https://app.datacamp.com/learn/skill-tracks/github-foundations). This markdown contains notes form the first course Introduction to Git.

## Section 1: Introduction

**Shell Navigation**
Basic shell commands for navigating between different directories.
```bash
pwd                 # print current directory
cd <folder-name>    # moves to the directory with the mentioned folder-name
ls -l               # lists all files and sub-directories within the mentioned directory
```

**Important Git commands**

Creating new git repos and checking `git status`
![](/assets/Screenshot%202026-10-06%20013458.png)

**Basic Git commands cheat sheet**
```bash
git --version               # show the installed git version
git config --global user.name "Your Name"       # set the name attached to your commits
git config --global user.email "you@email.com"  # set the email attached to your commits

git init                    # turn the current folder into a git repo (creates a hidden .git folder)
git status                  # show which files are new, modified, staged, or committed
git add <file>              # stage a specific file, ready for the next commit
git add .                   # stage all changes in the current folder
git commit -m "message"     # save the staged changes as a commit, with a short description
git log                     # show the commit history (hash, author, date, message)
git log --oneline           # compact history, one line per commit
git diff                    # show unstaged changes (edited but not yet staged)
git diff --staged           # show staged changes (what will go into the next commit)
git show <commit-hash>      # show the details and changes of one commit
```

**How they fit together**
1. Edit files in the working directory.
2. `git add` moves the changes to the staging area.
3. `git commit` saves the staged snapshot to the repo history.
4. `git status` and `git log` check where things stand at any point.

<!-- **Two common undo commands**
```bash
git restore <file>          # discard unstaged changes to a file (can't be undone)
git restore --staged <file> # unstage a file but keep your edits
``` -->


## Section 2: Version History

![](/assets/commit_struct.png)

The unique identifier of a commit is known as the **commit hash**. It points to the tree which maps the files and the directory structure. The blob shows a snapshot of what the files contained at the time of the commit.

The commit hash is a **40 char** alphanumeric string. Hashes allow data sharing between repos. If two files are the same, then their hashes are the same. To check for data change in files, compare the commit hashes.

**Version History with `git log`**
1. `git log` shows the latest history of all commits on the git repo.
2. `git log -N` where N is any number, shows the N most recent commits.
3. **Restricting to one file:** ``git log <file-name>`` shows the commit history of the specified file.
4. `git log -N <file-name>` shows the N most recent commits of the mentioned file.
5. `git log --since='Month Day Year'` shows the commit histpry from the specified date. Month is a 3 letter abbreviation, Day is 2 digits and Year is 4 digits.
6. **Commits between two dates:** `git log --since='Apr 2 2024' --until='Apr 11 2024'`

![](/assets/git_log_date_filters.png)

Finidng a particular commit and the files changed:
`git show <commit-hash>`

**Comparing Versions**


**Restoring and Reverting files**