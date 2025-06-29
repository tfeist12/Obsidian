**Vim:
- Delete to the end of the line = shift-d
- Search and replace globally `:/%s/<stringToReplace>/<replacementString>/g`
	g = all instances on a line
- Capitalize = ~

**Command Line:
- Ctrl-A = go to beginning of line
- Ctrl-E = go to end of line

**Kubernetes:
- If container is failing and you'd like to see logs: `/var/log/pods/<namespace>_<pod_name>_<uuid>/<container_name>`
- Check auth permissions: `kubectl auth can-i -n cm --list --as=system:serviceaccount:cm:lir-svc`

**Storage:
	`df -Th
	`du -sh