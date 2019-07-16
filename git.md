# git 

#### Add all modified files
```
git add -u
```

#### Add new files
```
git add .
```

#### Add deleted files
```
git add .
```

#### Make an additional commit on the most recent one, without making a new commit
```
Make changes you want locally
git add -u
git commit --amend --no-edit
git push origin -f 4704-feature
```


#### Delete all local branches except master
```git branch | grep -v "master" | xargs git branch -D ```

#### Delete a branch 

```git branch -d the_local_branch```

#### Uncommit last commit 

```git reset --soft HEAD^```

#### Nuking a commit
```
git reset --hard HEAD~1 // last commit
git reset --hard <sha1-commit-id> //revert to a given commit
```

```
git push origin HEAD --force
```

#### Setting up Multiple Git Configs

* Setting up two ssh keys: https://gist.github.com/jexchan/2351996

* To use a particular user (Waleed-Chaudhry is the user here) for a given repo
  * Go to the repo
  * vi .git/config
  * Switch url from git@github.com:Waleed-Chaudhry/jQuery.git to git@github.com-Waleed-Chaudhry:Waleed-Chaudhry/jQuery.git
