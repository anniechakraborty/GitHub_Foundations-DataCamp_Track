

## Section 1: Working with branches

### Listing branches

`git branch` lists all local branches in the repo. In the listed output, the branch with `*` in the beginning is the current branch we are in.

`git branch -r` lists only the remote-tracking branches (e.g. `origin/main`).

`git branch -a` lists all branches: local branches as well as remote-tracking branches.

### Creating and switching branches

`git branch <branch-name>` creates a new branch (does not switch to it).

`git switch <branch-name>` switches to the mentioned branch.

`git switch -c <branch-name>` creates a new branch and switches to it in one step.

(The older equivalents are `git checkout <branch-name>` to switch and `git checkout -b <branch-name>` to create and switch.)

### Fetching a branch from remote

`git fetch` downloads the latest branches and commits from the remote without changing any of our local branches. After fetching, `git branch -a` shows the new remote branches.

`git fetch origin <branch-name>` fetches only that specific branch from the remote `origin`.

To start working on a remote branch locally, switch to it by name. Git creates a local branch that tracks the remote one:

```
git switch <branch-name>
```

### Pushing and pulling a branch

`git push origin <branch-name>` pushes the local branch to the remote.

`git push -u origin <branch-name>` does the same and sets the upstream, so later we can just use `git push` / `git pull` from that branch.

`git pull origin <branch-name>` fetches the branch from the remote and merges it into the current branch (`git pull` = `git fetch` + `git merge`).

### Renaming and Deleting branches

`git branch -m <old branch name> <new branch name>` renames the branch.

`git branch -d <branch name>` deletes the specified branch. **NOTE:** Then branch must be merged to the main branch before deletion. Gives an output confirming the deletion and the last commit hash on the branch.

To delete a branch which has NOT been merged, run `git branch -D <branch name>`. The `-D` flag 
