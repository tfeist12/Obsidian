### Week of 10/21/25

**To Do:**
- Make story for updating the kubectl dsp plugin.
- Review Jonathan's IP-Podd state monitoring change


-ACTIVE spec and controller restart together are a problem since we can't use an inactive fw version update to determine when to start reboot


```
$ git log --oneline -10
5076a8ea1df (HEAD -> feist-AS210224-ippoddOsdGrpc) unit tests
617c2a2ceae create osd file client and make requests
0f85ab218d6 add osd api
8628b88f567 add OSD GRPC port env var to ippodd
bda199ad667 2 GRPC Ports for ippodd
```

**Order of Ops for Ippod 1.5:**
git worktree add -b feist-AS210224-ippoddOsdGrpc /data/workspace/feist/ippoddOsdGrpc origin/prj-fleetos
git phabsend rebase D46594
git apply /tmp/britt.patch
git add .
add OSD GRPC port env var to ippodd
git cherry-pick cf13705a7f1 afac2ec95e6 27bc7723d5f c05abf57195
git phabsend pr --update D46631

