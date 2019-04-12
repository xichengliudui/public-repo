Log exception after nginx-ingress delete.

kubectl delete nginx-ingress control的pod， 这个节点报了以下日志， emptydir 和secret的vlome还在


Jan 25 16:45:27 node169 kubelet: E0125 16:45:27.880512    1752 kubelet_volumes.go:140] Orphaned pod "5de3b1b1-1fae-11e9-ab07-005056a25aec" found, but volume paths are still present on disk : There were a total of 1 errors similar to this. Turn up verbosity to see them.

[root@node169 volumes]# ls
kubernetes.io~empty-dir  kubernetes.io~secret
[root@node169 volumes]# cd kubernetes.io~empty-dir/
[root@node169 kubernetes.io~empty-dir]# ls
logdir
[root@node169 kubernetes.io~empty-dir]# cd logdir/
[root@node169 logdir]# ls
access.log  error.log
[root@node169 logdir]# pwd
/var/lib/kubelet/pods/5de3b1b1-1fae-11e9-ab07-005056a25aec/volumes/kubernetes.io~empty-dir/logdir
[root@node169 logdir]# docker ps -a | grep nginx 
901a732d7d7a        deploy.bocloud/abcsys/nginx:1.13-alpine     "nginx -g 'daemon of…"   5 hours ago         Up 5 hours                                     nginx-proxy

---

[root@node170 volumes]# tail -f /var/log/messages

Jan 28 15:47:33 node170 kubelet: E0128 15:47:33.225022    2311 kubelet_volumes.go:140] Orphaned pod "07823c14-22cc-11e9-bb14-005056a25aec" found, but volume paths are still present on disk : There were a total of 1 errors similar to this. Turn up verbosity to see them.

Jan 28 15:47:35 node170 kubelet: E0128 15:47:35.196657    2311 kubelet_volumes.go:140] Orphaned pod "07823c14-22cc-11e9-bb14-005056a25aec" found, but volume paths are still present on disk : There were a total of 1 errors similar to this. Turn up verbosity to see them.

Jan 28 15:47:36 node170 kubelet: E0128 15:47:36.517866    2311 fsHandler.go:121] failed to collect filesystem stats - rootDiskErr: du command failed on /var/lib/docker/overlay2/1a2be3aeee2e6f9130c92d304b50f2cf3328527247e8363ca04d326295adc159/diff with output stdout: , stderr: du: cannot access ‘/var/lib/docker/overlay2/1a2be3aeee2e6f9130c92d304b50f2cf3328527247e8363ca04d326295adc159/diff’: No such file or directory

Jan 28 15:47:36 node170 kubelet: - exit status 1, rootInodeErr: cmd [ionice -c3 nice -n 19 find /var/lib/docker/overlay2/1a2be3aeee2e6f9130c92d304b50f2cf3328527247e8363ca04d326295adc159/diff -xdev -printf .] failed. stderr: find: ‘/var/lib/docker/overlay2/1a2be3aeee2e6f9130c92d304b50f2cf3328527247e8363ca04d326295adc159/diff’: No such file or directory

Jan 28 15:47:36 node170 kubelet: ; err: exit status 1, extraDiskErr: du command failed on /var/lib/docker/containers/921eaca1c35ebe33906b63889e1ba9910a92aaac9a91b48b4df21b345c9037db with output stdout: , stderr: du: cannot access ‘/var/lib/docker/containers/921eaca1c35ebe33906b63889e1ba9910a92aaac9a91b48b4df21b345c9037db’: No such file or directory

Jan 28 15:47:36 node170 kubelet: - exit status 1

Jan 28 15:47:37 node170 kubelet: E0128 15:47:37.193882    2311 kubelet_volumes.go:140] Orphaned pod "07823c14-22cc-11e9-bb14-005056a25aec" found, but volume paths are still present on disk : There were a total of 1 errors similar to this. Turn up verbosity to see them.

Jan 28 15:47:39 node170 kubelet: E0128 15:47:39.210671    2311 kubelet_volumes.go:140] Orphaned pod "07823c14-22cc-11e9-bb14-005056a25aec" found, but volume paths are still present on disk : There were a total of 1 errors similar to this. Turn up verbosity to see them.

Jan 28 15:47:41 node170 kubelet: E0128 15:47:41.195791    2311 kubelet_volumes.go:140] Orphaned pod "07823c14-22cc-11e9-bb14-005056a25aec" found, but volume paths are still present on disk : There were a total of 1 errors similar to this. Turn up verbosity to see them.

Jan 28 15:47:43 node170 kubelet: E0128 15:47:43.231678    2311 kubelet_volumes.go:140] Orphaned pod "07823c14-22cc-11e9-bb14-005056a25aec" found, but volume paths are still present on disk : There were a total of 1 errors similar to this. Turn up verbosity to see them.

Jan 28 15:47:45 node170 kubelet: E0128 15:47:45.200953    2311 kubelet_volumes.go:140] Orphaned pod "07823c14-22cc-11e9-bb14-005056a25aec" found, but volume paths are still present on disk : There were a total of 1 errors similar to this. Turn up verbosity to see them.

Jan 28 15:47:47 node170 kubelet: E0128 15:47:47.208932    2311 kubelet_volumes.go:140] Orphaned pod "07823c14-22cc-11e9-bb14-005056a25aec" found, but volume paths are still present on disk : There were a total of 1 errors similar to this. Turn up verbosity to see them.

