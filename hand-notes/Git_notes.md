# Git Notes

| Command | Description | Example |
| --- | --- | --- |
| `git status` | Shows which files are in the staging area | |
| `git log ` | View log of projects's overall history (log entries are shown with most recent first) | |
| | Git automatically shows 1 screen of output at a time (use `spacebar` to go down a page or `q` key to quit) | |
| `git log path` | View a specific file's history | |
| `git show firstfewcharofhash` | View details of a specific commit | |
| | (`firstfewcharofhash`) : Identifies a specific commit | |
| `git annotate file` | Shows who made the last changes to each line of a file and when | |
| | No. of different hashes = No. of different sets of changes made to file | |
| `git rm filename` | Delete file | |
| `git clean -n` | Shows list of files that are in the repository but whose history Git is not currently tracking | | 
| `git clean -f` | Delete files shown in `git clean -n` | |
| | *** Use carefully because it only works on untracked files (i.e. history not saved) so deleting = gone for good | |

## Creating a new repository

| Command | Description | Example |
| --- | --- | --- |
| `git init project-name` | Create new repository for new project | |
| `git init path/to/project` | Turn an existing project into a Git repo | |

## System settings (`git config`)

| `git config` | Command | | | Example |
| --- | --- | --- | --- | --- |
| | `--list` | | See settings for: | |
| | | `--system` | Every user on computer | `git config --list --system` |
| | | `--global` | Every one of your projects | |
| | | `--local` | One specific project | |
| | | | Note: Each level overrides the one above it (order of precedence) | |
| | `-- global setting.name setting.value` | | Change a configuration value for all your projects on a particular computer with setting's name and value in appropriate values | Examples of `setting.name`: `user.name` (for name), `user.email` (for email) |


## Committing changes to a Git repo
1. Add 1 or more files to staging area
    - `git add filename`
2. Commit everything in staging area
    - `git commit -m "message"`
    - `git commit`

## `git diff`

| Command | Description | Example |
| --- | --- | --- |
| `git diff` | Shows all changes in the repo | |
| `git diff filename` | Compare file as it is currently to what you have last saved | |
| 
| `git diff directory` | Shows changes to files in the specified directory | |
| `git diff -r HEAD path/to/file` | Compare file's current state to changes in staging area | |
| `git diff ID1..ID2` | Shows changes between 2 commits| | s
| `@@` | **Output**: Tells where changes are made | |

## `git checkout` and `git reset`

| Command | Description | Example |
| --- | --- | --- |
| `git checkout --filename` | Undo changes to staged files or discard changes that have not yet been staged | |
| | Note: Use this command carefully, once you discard the changes, they are gone forever | |
| `git checkout oldfilehash filename` | Restore an old version of a file | |
| `git checkout --dir` | Restore files that have been unstaged in directory (from `git reset HEAD dir`) | |
| `git reset HEAD filename` | Undo/unstage changes that have been staged | |
| | This does not restore file to state it was before you started making changes | | 
| | Resets file to the state last staged | |
| `git reset HEAD dir` | Unstage any files from directory that have been staged | |

## Branches

| Command | Description | Example |
| --- | --- | --- |
| `git branch` | Lists all the branches in a repository | |
| | Branch currently in will have a (`*`) beside its name | |
| | By default, every Git repo will have a branch called `master` | |
| `git diff branch1..branch2` | Shows the difference between 2 branches | |
| `git checkout branch-name` | Switch to another branch | | 
| | Only possible if all changes have been committed |
| `git checkout -b branchname` | Creates a new branch | |
| | Creates branch and switches you to it | |
| | Contents of new branch are identical to contents to original | |
| | Changes made now will only affect new branch | |
| `git merge source dest` | Merge source into destination | |
| | Changes made to source branch will be incorporated into destination branch | |
| | If changes don't overlap, result is a new commit in `dest` branch that includes everything in `src` branch
| `git push -u <remote> <branch>` | Push branch to remote repo (not done by default) | |
| `git status` | See conflicts |

## Flags (`--flag`) and others

| Command | Description | Example |
| --- | --- | --- |
| `-r` | Compare to a particular revision | | 
| `HEAD` | Most recent commit | |
| `HEAD~1` | Refers to 2nd most recent commit | |
| `HEAD~2` | Refers to 3rd most recent commit etc | |
| `.` | Current working directory | |

