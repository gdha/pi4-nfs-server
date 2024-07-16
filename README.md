# pi4-nfs-server
A NFS Server container image working with longhorn (inside kubernetes)

* Directory docker-nfs-server/ content is to create the container image with `build.sh`
* Directory kubernetes/ content is to create the NFS pod in our k3s cluster

```bash
$ kubectl logs -n nfs-server nfs-server-f48df7cdc-b7trm
Displaying /etc/exports contents:
/exports *(rw,fsid=0,async,no_subtree_check,no_auth_nlm,insecure,no_root_squash)

Starting rpcbind...
Displaying rpcbind status...
   program version netid     address                service    owner
    100000    4    tcp6      ::.0.111               -          superuser
    100000    3    tcp6      ::.0.111               -          superuser
    100000    4    udp6      ::.0.111               -          superuser
    100000    3    udp6      ::.0.111               -          superuser
    100000    4    tcp       0.0.0.0.0.111          -          superuser
    100000    3    tcp       0.0.0.0.0.111          -          superuser
    100000    2    tcp       0.0.0.0.0.111          -          superuser
    100000    4    udp       0.0.0.0.0.111          -          superuser
    100000    3    udp       0.0.0.0.0.111          -          superuser
    100000    2    udp       0.0.0.0.0.111          -          superuser
    100000    4    local     /var/run/rpcbind.sock  -          superuser
    100000    3    local     /var/run/rpcbind.sock  -          superuser
Starting NFS in the background...
rpc.nfsd: knfsd is currently down
rpc.nfsd: Writing version string to kernel: -2 +3
rpc.nfsd: Created AF_INET TCP socket.
rpc.nfsd: Created AF_INET6 TCP socket.
Exporting File System...
exporting *:/exports
/exports      	<world>
Starting Mountd in the background...These
Startup successful.
```
