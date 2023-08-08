#### 相关命令
```bash
systemd-analyze blame #显示开机启动项的时间, 从最慢依次列出。

#禁止启动
sudo systemctl disable xxx.service
sudo systemctl mask xxx.service # mask 这个 systemctl 命令的选项参数是比 disable 更强力。
```

#### /etc/fstab
挂载(mount)服务器上的nfs磁盘
在options那一列中加上 noauto即可, 表示不自动启动。
auto是automatic的缩写, 表示"自动"。而noauto就是not/no automatic的缩写, 表示"不自动"。
```bash
172.19.0.133:/mnt/androidstorage/NFS_RO   /mnt/nfs_ro nfs noauto,user,ro,_netdev 0 0
172.19.0.133:/mnt/androidstorage/NFS_RW   /mnt/nfs_rw nfs noauto,user,rw,_netdev 0 0
```
默认情况下(default中)是auto的, 也就是说默认情况下会在开机时自动挂载那两个nfs磁盘。

#### 
1. 在/lib/systemd/system目录下，找到NetworkManager-wait-online.service这个文件把修改等待的时间从30秒改成5秒。
   ```bash
   Environment=NM_ONLINE_TIMEOUT=5
   ```
2. 禁用etworkManager-wait-online.service
    ```bash
    sudo systemctl disable NetworkManager-wait-online.service
    #或
    sudo systemctl mask NetworkManager-wait-online.service
    ```