# git-cheatsheet

Just a small sheet to hold the Git commands I forget on a semi-regular basis.

## Commits

- `git commit -m "Message" --amend` - Overwrites the most recent commit with a new one. Useful for minor fixes to early commits.

- `git reset --soft HEAD^` - Removes the most recent commit, but keeps changes in working tree. Useful for removing early commits.

    - Often followed by `git push -f origin master` which forces an override of an early commit that has already been pushed.

- `git commit -m "Commit title" -m "Commit description..."` - Shorthand/hackish way to add a long commit description

- `git commit -m "Message" -e` - Edit extended commit message in the terminal editor

- `git add -p` - Add hunks of a file at a time, interactively

- `git checkout [FILENAME]` - Reset/revert a single modified file to the version stored at HEAD

    - (Used for uncommitted changes in your working tree)

    - Use `git checkout -- [FILENAME]` if the filename is the same as a branch name

## Branches

- `git checkout -b [BRANCHNAME]` - Create a new branch off of your currently checked-out branch.

- `git checkout --track [REMOTE]/[BRANCH]` - Checkout a branch from the specified remote.

    - For example, it might be something like `git checkout --track origin/add-formatting`

## Logs

- `git log -<n>` - Display the <n> most recent commits in a repository

    - E.g., `git log -3` will display the 3 most recent commits
    
- `git reflog` - Shows the history of actions on a repository (commits, merges, checkouts, etc.)

    - Useful if you need to find a place to which you can reset (in order to revert an unwanted change). For that use case, you'd find the hashcode of the event/state that you wanted to restore in the reflog, then use `git reset --hard [HASHCODE]` to do a **hard revert** back to that state.
    
- `git log --graph --decorate --pretty=oneline --abbrev-commit` - Generate a history graph for the repo

- `git log --oneline` - Convenient one-line output for each commit

- `git log tag1..tag2` - Log all commits between the two given tags

## Extensive history editing

Foreword: it's probably best to avoid extensive history editing on branches that other people might be working on (i.e., if anyone branched or forked off of `branchA`, avoid rebasing `branchA`).

- `git rebase -i HEAD~<n>` - Probably the easiest general-purpose way to adjust commit history on the current branch. Follow the instructions in the edit file to adjust history as desired by changing the type of each commit. Note that commits can be reordered and will be replayed from top to bottom.

    - Example: to squash the last 5 commits into one, you could use `git rebase -i HEAD~5`; in the editor, change the command for the last 4 commits to `squash` (or `s`) instead of `pick`.
    
    - Could also use a hash instead of `HEAD~<n>`, to jump to a specific point in the reflog

## Remotes

- `git push [-u] origin [BRANCH-NAME]` - Used to push commits to a particular (usually new) branch on the `origin` remote.

    - Usually used for the first push after `git checkout -b [BRANCH-NAME]`.

    - `-u` sets the new remote branch as upstream for the local branch

- `git remote add origin [YOUR-REPO-URL]` - Use this to set your remote repo as origin for a local repo.

    - Typically used when you're first pushing an existing repository up to GitHub (or another remote). In that case, follow it with `git push -u origin master`

- `git remote add upstream [BASE-REPO-URL]` - Use this if you forked someone else's repo. Set their fork (the main repo) as upstream.

- `git pull --rebase upstream master` - Use this to bring your local fork up to date with upstream before making new changes.

    - Note that you need to set the main repo as upstream before doing this. Use `git remote add upstream [BASE-REPO-URL]`

## Tagging

- `git tag -a v1.0 -m "Tag message"` - Tags the version specified (in this case, 1.0)

    - Also signs and includes a short message

- `git tag` - When run without arguments, just lists all existing tags

- `git push origin --tags` - Push tags to remote (by default, tags aren't included in pushes)

- `git log tag1..tag2` - Log all commits between the two given tags

## Merging

- `git merge --continue` - Continue a merge after resolving conflicts

- `git merge --abort` - If a merge goes horribly wrong, this should cleanly revert to the pre-merge state.

### Merge conlict resolution process

This describes a typical process that one might follow to resolve merge conflicts.
If you're trying to merge a local branch into master, but you're getting conflicts, try following this process with your local/working branch as `BASE` and master as `PULL_IN_BRANCH`, then pushing the resulting merge commit.
You should then be able to continue/perform the merge on the remote repo.

1. `git checkout [BASE]` - Switch to the branch that you want to serve as a base for the merge (often master, or your current working branch)

2. `git merge [PULL_IN_BRANCH]` - Merge `[PULL_IN_BRANCH]` into the current checked-out branch (`[BASE]`)

3. In the case of conflicts, use `git status` to see conflicted files

4. Resolve conflicts in a text editor

5. `git add .` to stage resolved conflicts

6. `git merge --continue` to continue/complete the merge

## Stashes

- `git stash` and `git stash pop` - Store a dirty working tree and restore stored changes, respectively

- `git stash push -m "Message"` - Stash changes with a particular description

- `git stash list` - Show all items currently stored in the stash
