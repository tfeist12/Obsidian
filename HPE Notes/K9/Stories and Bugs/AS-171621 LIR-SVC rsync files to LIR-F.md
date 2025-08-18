**Notes:**
We are not calling the grpc api for this story
Don’t know the lir-data primary hostname so assume that is just being passed in
modify nimos/release_tgz -> generate receipe

**Questions:**
Should I completely replace CopyFilesLirF() with an rsync function for this story
Do the generate release squash fs changes impact install release

```
rsync -av /root/tmp.fos.1865387926/fleetos-1699336246553088~git9df56ef70aa097-dbg/FleetOS-files/ rsync://172-26-122-12.lir-data.cm.svc:873/lir-data/lir-f/0.0.4870.0-1699336704976714
```