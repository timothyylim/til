# git 

#### Pull from upstream 

```
git pull upstream master
```

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

### Add everything except one thing
```
git add .
git reset your/file.js
```

#### Make an additional commit on the most recent one, without making a new commit
```
Make changes you want locally
git add -u
git commit --amend --no-edit
git push origin -f 4704-feature
```

#### Squash all commits into one commit
```
git checkout my_branch
git reset --soft HEAD~4
git commit
git push --force origin my_branch
```

#### Delete all local branches except master
```git branch | grep -v "master" | xargs git branch -D ```

#### Delete a branch 

```
git branch -d the_local_branch
git push -d origin the_remote_branch
```

### Rename a branch
```
git checkout <old_name>
git branch -m <new_name> // Modifies local branch
git push origin --delete <old_name> // Delete remote
git push origin -u <new_name> // Push new branch to remote
```

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

### Remove a commit inside the git log
```
git log --oneline // to view the commit id
git rebase --onto 436923f^ 436923f HEAD
git push origin HEAD:minside-dev --force
```

#### Set up multiple users:
```
git config user.name "Timothy Lim"
git config user.email "timothylim23@gmail.com"
```
* Can confirm by checking vi .git/config
```
[user]
        name = Timothy Lim
        email = timothylim23@gmail.com
```

#### Setting up Multiple Git Configs

* Setting up two ssh keys: https://gist.github.com/jexchan/2351996

* To use a particular user (Waleed-Chaudhry is the user here) for a given repo
  * Go to the repo
  * vi .git/config
  * Switch url from git@github.com:Waleed-Chaudhry/jQuery.git to git@github.com-Waleed-Chaudhry:Waleed-Chaudhry/jQuery.git
  * Or https://github.com/timothyylim/axo-minside-private to https://github.com-timothyylim/timothyylim/axo-minside-private

### Migrate a repo from bitbucket to git
```
Waleeds-MacBook-Pro:~ Waleed$ cd Code/
Waleeds-MacBook-Pro:Code Waleed$ git clone --mirror https://timothyylim@bitbucket.org/axofinans/axofinans-no-nyweb.git
Waleeds-MacBook-Pro:Code Waleed$ cd axofinans-no-nyweb/
Waleeds-MacBook-Pro:axofinans-no-nyweb Waleed$ git remote set-url --push origin https://github.com/timothyylim/axo-minside-private.git
Make sure you have given collab permissions to the user you're about to push before doing the next step
git push --mirror
Delete the repo you had, and git clone the new one
```

## Submodules

```
git submodule update --init --recursive
```

```
To remove a submodule you need to:

- Delete the relevant section from the .gitmodules file.
- Stage the .gitmodules changes git add .gitmodules
- Delete the relevant section from .git/config.
- Run git rm --cached path_to_submodule (no trailing slash).
- Run rm -rf .git/modules/path_to_submodule (no trailing slash).
- Commit git commit -m "Removed submodule <name>"
- Delete the now untracked submodule files rm -rf path_to_submodule
```

