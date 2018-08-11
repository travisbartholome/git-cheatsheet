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

## Logs

- `git log -<n>` - Display the <n> most recent commits in a repository

    - E.g., `git log -3` will display the 3 most recent commits

- `git log --oneline` - Convenient one-line output for each commit

- `git log tag1..tag2` - Log all commits between the two given tags

## Remotes

- `git push [-u] origin [BRANCH-NAME]` - Used to push commits to a particular (usually new) branch.

    - Usually used for the first push after `git checkout -b [BRANCH-NAME]`.

    - `-u` sets the new remote branch as upstream for the local branch

- `git remote add origin [YOUR-REPO-URL]` - Use this to set your remote repo as origin for a local repo.

    - Typically used when you're first pushing an existing repository up to GitHub. In that case, follow it with `git push -u origin master`

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

## Stashes

- `git stash` and `git stash pop` - Store a dirty working tree and restore stored changes, respectively

- `git stash push -m "Message"` - Stash changes with a particular description
