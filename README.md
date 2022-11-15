Changed by Main
Changed by Main2
Workflow test
1. set up branch A
2. set up branch B
3. set up branch C

Change last commit in C
drop duplicate commits

How to identify duplicate commits?

same commmit message but different sha code,
the orginal commit should be dropped and pick up the new one

```bash
git checkout --theirs changed/files
```

# merge conflict
```
git rebase --continue

```
