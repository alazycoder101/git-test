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

```
git rebase -i C # rebase based on C for B
git rebase -i C # again to drop the duplicate commits
```


# Git structure
## References

`git show-ref` - List references in a local repository

## Directed acyclic graph
https://en.wikipedia.org/wiki/Directed_acyclic_graph
## Pack files

https://codewords.recurse.com/issues/three/unpacking-git-packfiles
```bash
❯ git rev-parse HEAD:README.md
8b137891791fe96927ad78e64b0aad7bded08bdc
```
```
git pack-objects

git cat-file -p OBJECT-HASH

ruby -rzlib -e 'print Zlib::Inflate.new.inflate(STDIN.read)' < OBJECT_FILE

git cat-file commit refs/tags/testtag^{} >expected &&
git for-each-ref --format="%(*raw)" refs/tags/testtag

git rev-parse refs/mytrees/first | git cat-file --batch >expected &&
git for-each-ref --format="%(objectname) %(objecttype) %(objectsize)%(raw)" refs/mytrees/first


git rev-list --all > /tmp/all-obj.txt
git cat-file --batch-check </tmp/all-obj.txt

# hash SHA1
echo "Hello Sarah" | git hash-object --stdin

echo "Hello Sarah" | git hash-object -w --stdin

# list blobs

git rev-list --objects --all | git cat-file --batch-check='%(objectname) %(objecttype) %(rest)' | grep '^[^ ]* blob' | cut -d" " -f1,3-

git cat-file --batch-all-objects --batch-check
```

* Blob: This object as we have seen above stores the original content.
* Tree: This object is used to store directories present in our project.
* Commit: This object is created whenever a commit is made and abstracts all the information for that particular commit.


Tree object
* BLOB identifiers
* Path names
* Metadata of all files in that directory

# Rebase

Rebasing alters a sequence of commits. It moves or relocates a sequence of commits from current branch to the target branch. By default, the commits from the current branch that are not already on the other branch are rebased. Rebasing technique allows us to keep a linear history.


```
git log --oneline --all --graph

```

* Working area
* Staging area
* Repository

# reset

* Soft: move HEAD to commit only
* Mixed
* Hard

## hard
When performing a hard reset, git will copy the commit snapshot into the working area as well as the staging area. 

## Mixed
Mixed reset copies the snapshot from the repository to the staging area only

## Soft
When we perform a soft reset the commit snapshot is not copied to the staging area or to the working area. It will just move the HEAD explicitly to the commit. All changes in the working area and staging area will stay intact.

# Rerere
```bash
git config --global rerere.enabled true
```
References
---
1. https://www.tutorialspoint.com/how-to-undo-a-faulty-merge-with-reset-command-in-git
2. https://eagain.net/articles/git-for-computer-scientists/
3. https://git-scm.com/book/zh/v2/Git-%E5%B7%A5%E5%85%B7-%E9%AB%98%E7%BA%A7%E5%90%88%E5%B9%B6#_advanced_merging
4. https://www.tutorialspoint.com/explain-blob-object-and-tree-object-in-git
