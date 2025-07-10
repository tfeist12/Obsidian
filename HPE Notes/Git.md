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
-```
git fetch origin refs/private/phabusername__as-1234:<LOCAL_BRANCH_NAME>
-```
-```
-git checkout <LOCAL_BRANCH_NAME>