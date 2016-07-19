
# Git

### stash changes to a file
```shell
git stash save feature    # stash files
git stash show -p > patch # save to a file
git apply patchfile       # open changes on another pc
```

### remove file from commit
```shell
# removes file from ALL COMMITS
git filter-branch --tree-filter 'rm -f my_file' HEAD
# removes file from ALL COMMITS
git filter-branch --index-filter \
    'git rm --cached --ignore-unmatch path/to/mylarge_50mb_file' \
    --tag-name-filter cat -- --all
# removes old references and forces push
rm -Rf .git/refs/original       
git gc --aggressive --prune=now
git push --force
```

### ignore a file just locally

You can add files and directories to the file `.git/info/exclude` like you do inside a `.gitignore`.

If you already have unstaged changes you must run the following after editing your ignore-patterns:
 
```shell
git update-index --assume-unchanged [<file>...]
```
