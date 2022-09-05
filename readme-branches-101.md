# Branches demystified

# list branches
git branch

# create a dev branch
git branch dev

git branch ideas

# HEAD is a pointer to a branch, you can have one current branch

# switch to another branch (you must check in or stash pending changes)

# merge
git merge ideas

when merging git has two parents when viewing git log

git merge without second parameter gives message
fatal: No remote for the current branch.

# to merge main to ideas
git switch ideas
git merge main

# fast forward
when merging branch with no conflicts between branches git does a "fast forward" commit which just points branch you are merging to with the lastest commit hash from the other branch.

# get specific version
git checkout <hashid>

