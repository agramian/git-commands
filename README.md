# Git commands
Useful Git commands reference

*TODO: formatting, organize, index/TOC*

### basic
`git add [files]`

`git commit -m [message]`

`git push`

`git diff [filename]`

`git diff`

`git status`

`git rm [files]`

`git reset --hard origin/mybranch`

### fetch/pull all remote branches
`git fetch origin; git branch -a; git pull --all;`

OR

`git fetch origin --depth=10000 $(git ls-remote -h -t origin); git pull --all;`


### removed untracked files from current branch
`git clean -f`

If you want to also remove directories, run `git clean -f -d` or `git clean -fd`

If you just want to remove ignored files, run `git clean -f -X` or `git clean -fX`

If you want to remove ignored as well as non-ignored files, run `git clean -f -x` or `git clean -fx`

### resolve merge conflicts
`git checkout --[theirs|ours]  [file]`

`git add [file]`

`git merge --strategy-option theirs`

`git reset HEAD^ -- [file]`

`git commit --amend`

`git push origin HEAD --force`

`git rebase -i HEAD~2`

### make chagnes
`git push origin HEAD --force`

### undo rebase
`git reflog`

`git reset --hard HEAD@{5}`

### specify upstream repository
```
git remote -v
git remote add upstream https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git
git remote -v
git fetch upstream
git checkout master
git merge upstream/master
```

### delete local branch
```
git branch -d the_local_branch
git push origin :the_remote_branch
```

### remove branches no longer on remote
```git fetch -p && for branch in `git branch -vv | awk '{print $1,$4}' | grep 'gone]' | awk '{print $1}'`; do git branch -D $branch; done```

### store/unstore uncommitted changes
`git stash`

`git stash pop`

### stash untracked files
`git stash -u`

### print current revision
`git rev-parse HEAD`

### get submodule revisions
`git submodule status`

### rebase from root
`git rebase -i --root`

### change upstream remote repo
```
git remote rm upstream
git remote add origin [NEW_UPSTREAM_URL]
```

### modify author for commits
https://help.github.com/articles/changing-author-info/

### remove history before a certain commit
```
echo "<NEW-ROOT-SHA1>" > .git/info/grafts`
# to check
git log
# to make permanent
git filter-branch -- --all
```

### get rid of local commits
`git reset --hard origin/[branch]`

### set git user for repository
```
cd path/to/local/repo
git config user.email "your_email@example.com"
```

### change repo url
`open .git/config`

### create a branch from another branch 
`git checkout -b myFeature dev`

### create branch from current bracnh
`git checkout -b myFeature`

### squashing a feature commit before merging to master
```
git checkout -b new-feature master
[make commits, do work,...]
git checkout -b new-feature-candidate new-feature
git rebase -i master
[mark all commits except first one with ‘s’ for squash]
[modify the commit message]
[ :wq to save the file]
git checkout master
git merge new-feature-candidate
```
### rebase preserve merge commits
`git rebase --preserve-merges`

### patching
```
# create patch file from last commit on current branch
git format-patch -1 HEAD
# check for error before applying patch 
git apply --check file.patch
# show stats regarding patch to be applied
git apply --stat file.patch
# amend patch
git am < file.patch
# just apply the patch normally
git apply mypatch.patch
# if there are issues applied the patch run with -3 argument to initiate 3-way merge
# and allow resolving conflicts using a tool like kdiff
git am -3 < file.patch
```

### undo a merge
```
# find the commit to revert to
git log
# reset to that commit
git reset --hard commit_sha
# force push
git push origin HEAD --force
```

### Resolving merge conflicts
```
git config --global mergetool.kdiff3.path /Applications/kdiff3.app/Contents/MacOS/kdiff3
git mergetool -t kdiff3
```

### remove .orig files
`git clean -f`

`git reset --hard origin/master`

`git rebase --edit-todo`

### squash merge
`git merge --squash`

### diff branches
Display what is in branc_2 but not in branch_1
`git diff branch_1..branch_2`

Display what is in branch_1 XOR branch_2 (either branch_1 or branch_2 but not both)
*So git b1...b2 is equal to git b2...b1*
`git diff branch_1...branch_2` 

### commit ID of the original base, which you can then pass to git rebase
`git merge-base feature master`

### rebase and merge branch
```
git checkout feature
git checkout -b temporary-branch
git rebase -i master
# clean up/edit the history
# ‘<,’>s/pick/squash
git checkout master
git merge temporary-branch
```

### remove all files/dirs matching anything in .gitignore
Use `git clean -xdn` to perform a dry run and see what will be removed.

Then use `git clean -xdf` to execute it.

### new project initial commits
```
git checkout --orphan <branchname>`
git commit --allow-empty -m "initial commit"
git push -u origin <branchname>
```

### permanently authenticate git repositories
`git config credential.helper store`

### Undo latest commit
git reset HEAD~

