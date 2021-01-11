# Mount a remote VM as a shared disk

## Conf for remote server

Install necessary kernel NFS

    apt-get install nfs-kernel-server

Mark the server as exportable (viewable by other server) by editing

    nano /etc/exports

Mark a folder as export and allow which IP has access. Possible to use `*` fully or partially

    /path/to/share xx.xx.xx.*(rw,sync,no_subtree_check,no_root_squash)

`no_root_squash` Allow to run commands as root from other server

Save configuration

    exportfs -ra



## Conf for current server

Create a shared folder to mount on

    mkdir /sharedvm

Mount using NFS system [remoteIP:/location/]

    mount -t nfs xx.xx.xx.xx:/path/to/share /sharedvm

If we want drive is mount automatically on next reboot

    nano /etc/fstab

    xx.xx.xx.xx:/path/to/share /sharedvm nfs defaults 0 0
