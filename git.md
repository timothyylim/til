# git 

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
