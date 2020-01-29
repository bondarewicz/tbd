reamde.md

Create a new branch of `master` for feature-1
```
git checkout master
git checkout -b feat-1
git add -A
git commit -m "f1"
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
```