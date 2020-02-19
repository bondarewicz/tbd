Any pull request is auto-merged 


TODO: add simple test step and require it to pass before merging

Create a new mob-session branch of `master` for wip

```
mobs
...work here...
mobn
mobd
```

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

```bash

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
```

```bash
mobd() {
  git checkout mob-session

  gh pr create
  gh pr status
  gh pr list -s all -L 3
}
```