**Starting: Order of operations**
```
git checkout -b feist-<story> origin/prj-fleetos
```
       or
```
git checkout -b feist-<story>
```
```
git branch --set-upstream-to origin/prj-fleetos
```
-------------------------------------------------------------------

**Finished: Order of operations**
```
git phabsend --squash
```
```
git pull --rebase
```
```
git push origin HEAD:prj-fleetos-next
```

-------------------------------------------------------------------

**Push to private ref:**
```
git push origin HEAD:refs/private/phabusername__as-123456
```

**Fetch from private ref:**
```
git fetch origin refs/private/phabusername__as-1234:<LOCAL_BRANCH_NAME>
```
```
git checkout <LOCAL_BRANCH_NAME>
```

**Track private branch:
```
git branch --set-upstream-to origin/private/phabusername__as-123456
```

------------------------------------------------------------------

**Delete branch:**
```
git branch -d <branch>
```

------------------------------------------------------------------

**Rebase changes onto a commit in history:
```
git rebase --onto <commit-hash>
```

**Interactive rebase (choose commits to apply)
```
git fetch && git rebase -i prj-fleetos
```

------------------------------------------------------------------

**Amend last commit:**
```
git commit --amend
```

**Update a commit message in local history:**
```
git rebase -i @~5
```
```
git commit --amend
```
```
git rebase --continue
```

**Edit specific commit contents in history:**

```
git rebase -i <commit-hash>~
```
- choose edit option
- make changes
```
git add <edited file>
```
```
git commit --amend
```
```
git rebase --continue
```

**Remove commit from history:**

```
git rebase -i
```
- choose drop option for offending commit and save

-----------------------------------------------------------------

**Check the hash of the commit we are based on**
```
git merge-base HEAD origin/prj-fleetos
```

-----------------------------------------------------------------------

**View which files changed between commits:**
```
git diff --name-only HEAD <commit>
```