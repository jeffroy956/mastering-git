# sample
simple text documents for testing git commands

hello, local commit here

# get last 2 entries
git log -2

# after 1 local commit show that local main branch is pointing to a different ref than the remote
git show-ref main

# now push local to remote
git push
git show-ref main

# force a push, ignoring the remote changes
git push -f

# use git fetch to get remote changes and merge with local changes of there is a conflicts

you fetch and merge, then you push
git fetch
git merge
git push


you pull, then you push
pull = fetch and merge
git pull
git push

# rebasing with a remote

change in dev branch
# create a new branch locally and then add to remote
https://stackoverflow.com/questions/2765421/how-do-i-push-a-new-local-branch-to-a-remote-git-repository-and-track-it-too
Edit files, add and commit. Then push with the -u (short for --set-upstream) option:

git branch dev
git switch dev
make changes
git push -u origin dev

# never rebase shared repository commits, rebase locally

# fork clones a project from someone else to my github

you can configure two remotes when you want to use a project as your base and then

have an upstream (original author) and origin (my fork)

