**rsync examples:**
- Receive on LIR-Svc pod: 
```
rsync -rdt rsync://172.26.58.11:873/share/lir-f/0.0.4870.0-1696632362269999/install-control.yaml /tmp
```
- Send from LIR-Data pod:
```
	- rsync -av /var/opt/hpe/containers/lir/* rsync://172.26.121.150:873/lir-data/
```
	or
```
	- rsync -av /var/opt/hpe/containers/lir/* rsync://172-26-121-149.lir-data.cm.svc.cluster.local:873/lir-data/
```

[https://serverfault.com/questions/305764/rsync-permissions-from-one-server-to-another-mkdir-permission-denied-13](https://serverfault.com/questions/305764/rsync-permissions-from-one-server-to-another-mkdir-permission-denied-13)

**access individual pods:**
172-26-58-43.lir-data.cm.svc.cluster.local
172-26-58-43.lir-data-headless.cm.svc.cluster.local

**grpcurl examples:**
```
grpcurl -plaintext lir-data.cm.svc.cluster.local:31322 lir.Service/Rsync
```
```
grpcurl -d '{"dst_pod_hostname":"172-26-58-43.lir-data.cm.svc.cluster.local"}' -plaintext lir-data.cm.svc.cluster.local:31322 lir.Service/Rsync
```

**10/23:**
`find /var/opt/hpe/containers/lir | sort | sha256sum
24c48d0a4b9e4493dcbd45fbc2dc88f2c6d9e26eb983bae8351e77067cf465dc  - c0n0
24c48d0a4b9e4493dcbd45fbc2dc88f2c6d9e26eb983bae8351e77067cf465dc  - c0n1

make config map for the rsyncd.conf so we can configure shared directory and port of rsync daemon
create file from config map using volume mount

**10/24:**
Unit Tests:
	basic replication
	file count
	size
	file removal