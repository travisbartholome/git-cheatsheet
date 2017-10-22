# git-cheatsheet

Just a small sheet to hold all the git commands I forget on a semi-regular basis.

## Commits

- `git commit -m "Message" --amend` - Overwrites the most recent commit with a new one. Useful for minor fixes to early commits.

- `git reset --soft HEAD^` - Removes the most recent commit, but keeps changes in working tree. Useful for removing early commits.

    * Often followed by a `git push -f origin master` which forces an override of old commit that have already been pushed.
