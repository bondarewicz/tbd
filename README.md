> TODO: add simple test step and require it to pass before merging

Following workflow is inspired by [this](https://www.remotemobprogramming.org/) approach.

Repository itself is configured with [automerge](https://github.com/pascalgn/automerge-action) github action which to automate any pull requests from short lived branches into master.

## Prerequisites
- [mob](https://github.com/remotemobprogramming/mob) 
- [zsh](https://ohmyz.sh/)
- [gh cli](https://github.com/cli/cli)


## Config

`.zshrc`

```bash
export MOB_WEEK_NO=`date +%V`
export MOB_DAY=`date +%a`
export MOB_TIME=`date +%T`
export MOB_SWARM_TEAM="flock"
export MOB_USER_EMAIL=`git config user.email`
export MOB_WIP_BRANCH=$(echo "$MOB_SWARM_TEAM-w$MOB_WEEK_NO-$(echo $MOB_DAY | tr '[:upper:]' '[:lower:]')")
export MOB_WIP_COMMIT_MESSAGE="$MOB_WIP_BRANCH $MOB_TIME $MOB_USER_EMAIL"

mobs() {

  local minutes=$1

  if [ -d ".git" ]; then
    changes=$(git status --porcelain)
      if [ -z "${changes}" ]; then
		    git checkout master
        mob start $minutes
      else
        echo "you have uncommited changes"
      fi

    
  fi
}

mobd() {
  git checkout mob-session

  gh pr create
  gh pr status
  gh pr list -s all -L 3
}
```


## Example workflow

```bash
# simon begins the mob session as typist
simon$ mobs 10
# work
#...after 15 minutes...
simon$ mobn

# carola takes over as the second typist
carola$ mobs 10
# work
# after 10 minutes...

carola$ mobn

# fred takes over as the third typist
fred$ mobs 10
# work
# after few minutes the work is done...

fred$ mobd
```

## Alternative workflow

Create a new branch of `master` for feature-2
```
git checkout master
git pull --ff-only origin master
git checkout -b feat-2
git add -A
git commit -m "Add feat-2"
gh pr create
gh pr status
gh pr list -s all -L 5
```

Squash merge feat-2 into master first
```
git checkout master 
git merge --squash feat-2
git commit (esc :wq)
```

Now switch to feature-1 branch and integrate changes from `master`

```
git checkout feat-1
git rebase master
git add -A
git commit -m "f1.1"
```

Finally squash merge feat-1 into master
```
git checkout master 
git merge --squash feat-1
git commit (esc :wq)
```


Final state of master

```
* eff0037 (HEAD -> master) f1
| * 58564e2 (feat-1) f1.1
| * 06dc37b f1
|/  
* 34d577b f2
| * 931bdc4 (feat-2) f2
|/  
* 9b1bc0b init
```