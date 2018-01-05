# git-cheatsheet

Just a small sheet to hold the Git commands I forget on a semi-regular basis.

## Commits

- `git commit -m "Message" --amend` - Overwrites the most recent commit with a new one. Useful for minor fixes to early commits.

- `git reset --soft HEAD^` - Removes the most recent commit, but keeps changes in working tree. Useful for removing early commits.

    - Often followed by `git push -f origin master` which forces an override of an early commit that has already been pushed.

- `git commit -m "Commit title" -m "Commit description..."` - Shorthand/hackish way to add a long commit description

## Logs

- `git log -<n>` - Display the <n> most recent commits in a repository

    - E.g., `git log -3` will display the 3 most recent commits

- `git log --oneline` - Convenient one-line output for each commit

- `git log tag1..tag2` - Log all commits between the two given tags

## Remotes

- `git push origin [BRANCH-NAME]` - Used to push commits to a particular (usually new) branch.

    - Usually used for the first push after `git checkout -b [BRANCH-NAME]`.

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
