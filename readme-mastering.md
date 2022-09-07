# four areas of git
working area, index, repository, and the stash
# three main areas
working area, index, repository

# make a repository, change master to main
git init
# "move" branch to rename master to main
git branch -m main
git branch --move main

# git index
the index is staging area files are added to when you use "git add"
"git diff" compares working area to the index
"git diff --cached" compares working area to the repository

"git commit" migrates changes from the index to repository
"git add" stages changes in the index

# clone the repo from training
git clone https://github.com/nusco/cookbook

# list remote branches
git branch -r

# cleanup untracked files
force is required if git configuration requireForce is not set to false
git clean --force

# checkout
moves the head references, changes the current commit

# see the differences between lisa and main
git diff lisa main

# switch branch to lisa and get latest version of lisa to working area
git checkout lisa

checkout is similar to switch

# unstage file with remove
git rm --cached copyright
git rm --force copyright

# renaming files
git automatically figures out renames
rename file on file system
then use git add to re-add files and check status to see rename
or use git mv to move file directly

git mv menu.txt menu.md
git reset --hard

# command that move branch
commit - creates a new commit and changes current branch to point to new commmit
merge - creates a new commit and changes current branch to point to new commmit
rebase - creates a new commit by copying existing commmit and points the current branch to point at one of the new commits
pull - gets new commmits from remote

# git reset
reset remove the current branch and optionally copies data from the repository to the other areas
--hard working area and index matches the "reset commit"
--mixed is default option, working area left alone, index matches the "reset commit"
--soft moves the repository commit pointer of current branch but does not change the index or working area files


# undo the squids commmit, reset to specific hash in git log
git reset --hard 704182

# reset to HEAD
mixed reset, leave working area alone:
git reset HEAD
hard reset, nuke working area:
git reset --hard HEAD

# stash, like a shelfset
first make changes and add to index

git stash --include-untracked

show the stashes available
git stash list

can specify stash ID or take most recent stash by default with apply
git stash apply

or take stash by id
git stash apply stash@{2}

clear out stashes
git stash clear

drop specific stash
git stash drop stash@{2}

# resolving conflicts
create a tomato branch
git branch tomato
git checkout tomato
then add guacamole.txt, commit to repo

git checkout main
then add guacamole.txt, commit to repo

now merge, you have a conflict
git merge tomato

see the differences
cat recipes/guacamole.txt

show the merge hash
cat .git/MERGE_HEAD

show the merge
git show 62f8f

view the merge with vim
vim recipes/guacamole.txt

# rollback one staged change
change two files
stage everything changed with
git add .

git status

unstage menu.txt changes in the index
git reset HEAD menu.txt

revert menu.txt to repository menu.txt
git checkout HEAD menu.txt

# committing parts of a file

create and checkout hunk branch
modify menu.txt, insert line at beginning and add to end
git diff

git add --patch menu.txt

this is small file so it only makes 1 "hunk"

? will give you help on the options
use the s option to split into smaller "hunks"

changes between working area and index
git diff

changes between index and repo
git diff --cached

commands with a "patch" option
add
checkout
stash
reset

# switch and restore
these two features split checkout into two granular commands

switch moves to a different branch
restore recovers an earlier commmit by hash

restore a staged file to repository
make changes to menu.txt and stage with git add
then
git restore --staged menu.txt
to undo changes in working area use restore like this:
git restore menu.txt

# git history

# visualize log with branch graph, color highlight, one line per commit

git log --graph --decorate --oneline

git show HEAD

# show parent of head
git show HEAD^

# show parent of parent of head
git show HEAD^^

# show 5th commit of head x
git show HEAD~5

# second parent of the second commit before head
git show HEAD~2^2

# show back in time
git show HEAD@{"1 month ago"}
git show HEAD@{"1 year ago"}

# git blame
git blame recipes/apple_pie.txt

git show 007ff

# show difference between current commit and commit 2 earlier
git diff HEAD HEAD~2


git diff nogood main

# show change details of each commit
git log --patch

# only show commits that match search string apples
git log --grep apples --oneline

git log -Gapples --patch

# show previous 3 commits, one console line per commmit
git log -3 --oneline

# show range of 5 commmits ago to parent of head
git log HEAD~5..HEAD^ --oneline

# two prior parents to current HEAD
git log HEAD^^..HEAD
# reverse shows nothing
git log HEAD..HEAD^^
show version history oldest -> newest

# go from newgood to main and show all the new commits that you see
# what commits are in main but not nogood?  should we merge?
git log nogood..main --oneline

git log main..nogood --oneline

# history: fixing mistakes

# changing the latest commit by amending the latest commit
git commit --amend -m "amending caesar salad commit"

# change older commits
git blame menu.txt
git log --graph --oneline --decorate

add new cheesecake file and commit

git log --graph --oneline --decorate

git rebase --interactive 5720fdf

git rebase --continue
this lets you know of conflicts
resolve conflicts then 

git rebase --continue

# took a number of merge fixes, see what log looks like
git log --graph --oneline --decorate

interactive rebase is most useful for cleaning up my local smaller commits

# recover hashes of abandoned objects, rebases gone wrong

git reflog HEAD

git show  HEAD@{60}

you can branch at old tag to keep pre-rebase changes from getting garbage collected

git reflog refs/heads/main

# rewriting large chunks of history

in case we added a huge file by accident or we committed password!

git filter-branch is deprecated

# focus on fixing menu.txt

# make course7 folder and clone history again
git clone https://github.com/nusco/cookbook
# rename master to main
git branch --move main

# filter-repo with invert-paths removes single file from repo and everything else is retained

git filter-repo --path menu.txt --invert-paths

# using filter-repo on windows on git bash
1. installed latest version of python
2. copied git_filter_repo.py from C:\Python310\Lib\site-packages to C:\Program Files\Git\mingw64\libexec\git-core
3. renamed git_filter_repo.py to git-filter-repo.py
4. edited git-filter-repo.py, changed python3 to python in first line of script

# now to use from windows you need to do this:
git filter-repo.py --path menu.txt --invert-paths --force

git log --graph --oneline --decorate

# create my own repository so I don't lose my notes:
git clone https://github.com/jeffroy956/mastering-git

# rename master remote to main
git branch --move main
git push -u origin main

https://dev.to/rhymu/git-renaming-the-master-branch-137b

#  reverting commits
git checkout lisa
git log --graph --decorate --oneline

5720fdf commit added cheesecake without recipe, let's revert

we could use an interactive rebase but that is heavy weight
# git revert rolls back old commit with a new commit that is exactly the opposite of the original commit while keeping all version histroy

git revert 5720fdf

git show 1d2799
git cat-file 1d2799 -t
git cat-file 1d2799 -p

revert does not mean "undo"
"reset" is closes git operation to and undo

# last moves
trying out rebase
rebase second change