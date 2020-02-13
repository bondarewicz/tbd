reamde.md

Create a new branch of `master` for feature-1
```
git checkout master
git checkout -b feat-1
git add -A
git commit -m "Add gh cli cmd"
gh pr create 
```

Create a new branch of `master` for feature-2
```
git checkout master
git checkout -b feat-2
git add -A
git commit -m "f2"
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

f5

the end