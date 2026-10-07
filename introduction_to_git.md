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


## Section 2: Playing with Version History

![](/assets/commit_struct.png)

The unique identifier of a commit is known as the **commit hash**. It points to the tree which maps the files and the directory structure. The blob shows a snapshot of what the files contained at the time of the commit.

The commit hash is a **40 char** alphanumeric string. Hashes allow data sharing between repos. If two files are the same, then their hashes are the same. To check for data change in files, compare the commit hashes.

### Version History with `git log`
1. `git log` shows the latest history of all commits on the git repo.
2. `git log -N` where N is any number, shows the N most recent commits.
3. **Restricting to one file:** ``git log <file-name>`` shows the commit history of the specified file.
4. `git log -N <file-name>` shows the N most recent commits of the mentioned file.
5. `git log --since='Month Day Year'` shows the commit histpry from the specified date. Month is a 3 letter abbreviation, Day is 2 digits and Year is 4 digits.
6. **Commits between two dates:** `git log --since='Apr 2 2024' --until='Apr 11 2024'`

![](/assets/git_log_date_filters.png)

Finidng a particular commit and the files changed:
`git show <commit-hash>`

### Comparing Versions
`git diff` shows the difference between versions.

`git diff <filename>` compares the last committed version with the latest version not in the staging area. The output shows two versions of the report (A and B) where (A) is the **last version committed** and (B) is the **unstaged latest content**.

![](/assets/git%20diff%20git%20show%20-%20commit%20details.png)

The line between the two @@ symbols tells us what changed between the two versions. The -0,0 indicate that version A starts at line 0 and has 0 lines (meaning its a blank file), and the +1,74 show that version B starts at line 1 and has 74 lines. This makes sense when we look at the next part of the output.

In the next part we have green lines starting with +, this indicate the new lines added in Version B which were not in Version A. If there were lines in version A which had been moved or edited, they would be in red and started with a - sign.

`git diff --staged <filename>` compaes the last committed versio of the file with the version in the **staging area**.

`git diff <commit-hash-1> <commit-hash-2>` compares the content of two commits. This shows what changed from the first commit (hash) to the second commit (hash).

**`HEAD`** is the shortcut keyword to refer to the latest commit. All other commits can be referred to relative to the ``HEAD`` commit (easier than using hashes). ``HEAD~1`` refers to the commit 1 step below the `HEAD` commit (the second most recent commit). Likewise, `HEAD~N` is the N-th commit below the `HEAD`.

Therefore, to compare the second most recent commit with the most recent commit, use:
`git diff HEAD~1 HEAD`

### Restoring and Reverting files
Essential when there is an error in a previous commit or we want to restore a repo to the state prior to a certain previous commit.

**git revert**

`git revert` reinstates the previous versions and makes a new commit with the older versions. It restores **all files** updated in the given commit. 
This command only works on commits not on individual files.

`git revert HEAD` will undo the changes made in the most recent commit and make a new commit with the files from the previous commit (`HEAD~1`). 

By default this opens a text editor where we are prompted to enter a commit message. To SAVE the commit message press `Ctrl + 0` then `Enter`. To EXIT press `Ctrl + X`.

**git revert flags** - extra operations

`git revert --no-edit HEAD` : reverts the latest commit without opening the text editor.

`git revert -n HEAD`: reverts **without creating the new commit**, so the most recent (`HEAD`) commit is undone and all the files from the previous commit are fetched and added to the staging area.

### Reverting single files

`git checkout HEAD~1 -- <filename>` 
This command can also be used to revert a single file. 

This restores the `<filename>` to the version in the HEAD~1 commit. We can also mention specific commit hashes to restore file states from that commit.

Unstaging files:
- A single file :`git restore --staged <filename>`. 
- All files: `git restore --staged`.

Adding files to the staging area:
- `git add .` : adds all files (tracked/untraced) to the staging area for committing.
- `git add <filename>` : adds only the aprticular file to the staging area.