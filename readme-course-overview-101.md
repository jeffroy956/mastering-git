GIT is a hashed key value pair repository

# on git bash run this command to hash a key
echo "Applie Pie" | git hash-object --stdin

SHA1 hashes

keys are hashes
values are pieces of content

Git is a persistent map

# turn directory into a git project
git init

# rename git branch from master to main
git branch -m main

# persist the apple pie content to repository
echo "Apple Pie" | git hash-object --stdin -w

# open the git repository with windows explorer when in root directory of repo
explorer .git

# get the type of a stored hash
git cat-file 23991897e13e47ed0adb91a0082c31c82fe0cbe5 -t

# pretty print the stored has
git cat-file 23991897e13e47ed0adb91a0082c31c82fe0cbe5 -p

# see whether files are tracked by git versioning
git status

# add readme.md from root
git add readme.md

# add recipes folder
git add recipes

# check status again
git status

# commit with a message
git commit -m "my first commit"

# review commit history
git log

in git the commit is also represented by a hash and you can print the commit hash with cat-file

git cat-file -p 71fff60bf40a4af808aa38d07eb23401b480ad48
# print the hash of the tree stored by commit
git cat-file -p 0b433582f019d0ff6a8def821a3701161b8f2858

# print readme.md within tree stored by commit
git cat-file -p acb81678928e96ad3b8e9541b647e59c984a54fe

# print apple_pie.txt within recipes folder
git cat-file -p 8adfdb18d903ed727e30e35a67e8a8d79822515b
git cat-file -p 124b2c537cbdf63a0c8b88d409b3b0882b9b3996
# print readme.txt
git cat-file -p 870ace5cca9a742723b62bd556cf9a87667af16c

# look at the third commit with a parent
git log
git cat-file -p 98179400c8cee4af04e78db60f9aab7c540fa1b5
# look at tree of third commit
git cat-file -p 452081db26f44b698e542226a0bfc37bd8fde7ba

# look at parent of third commit (parent is the second commit)
git cat-file -p b449950a9347da100b5e5dbe06b7bf2748c66d71

# look at parent of second commit (the first)
git cat-file -p 71fff60bf40a4af808aa38d07eb23401b480ad48

# can use just the first few digits of hash
git cat-file -p 71ff

# count objects in repository
git count-objects

# annotated tags (a label on a commit)
