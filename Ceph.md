
https://access.redhat.com/documentation/zh-tw/red_hat_ceph_storage/5/html/administration_guide/monitoring-a-ceph-storage-cluster


#### Ceph service
```
systemctl --type=service | grep Ceph
systemctl status ceph-mgr.target
systemctl status ceph-mon.target
systemctl status ceph-osd.target

sudo ceph -s
sudo ceph -w
sudo ceph status
sudo ceph df

```


#### Monitor
```
sudo ceph mon stat
sudo ceph mon dump

ceph quorum_status -f json-pretty
ceph daemon mon.pm1 help
ceph daemon mon.pm1 mon_status

# Different way to see the status
# Check filename with
ls /var/run/ceph/ceph- + TAB
  # eg ceph-osd.0.asok
ceph daemon /var/run/ceph/ceph-osd.0.asok status
```

#### OSD
```
ceph osd stat
ceph osd dump
sudo ceph osd df
```

#### PG
```
ceph pg dump
ceph pg map 128
ceph pg stat
```



#### PGs per OSD
```
# Past this as one command in the shell to get PGs per OSD
ceph pg dump | awk '
BEGIN { IGNORECASE = 1 }
 /^PG_STAT/ { col=1; while($col!="UP") {col++}; col++ }
 /^[0-9a-f]+\.[0-9a-f]+/ { match($0,/^[0-9a-f]+/); pool=substr($0, RSTART, RLENGTH); poollist[pool]=0;
 up=$col; i=0; RSTART=0; RLENGTH=0; delete osds; while(match(up,/[0-9]+/)>0) { osds[++i]=substr(up,RSTART,RLENGTH); up = substr(up, RSTART+RLENGTH) }
 for(i in osds) {array[osds[i],pool]++; osdlist[osds[i]];}
}
END {
 printf("\n");
 printf("pool :\t"); for (i in poollist) printf("%s\t",i); printf("| SUM \n");
 for (i in poollist) printf("--------"); printf("----------------\n");
 for (i in osdlist) { printf("osd.%i\t", i); sum=0;
   for (j in poollist) { printf("%i\t", array[i,j]); sum+=array[i,j]; sumpool[j]+=array[i,j] }; printf("| %i\n",sum) }
 for (i in poollist) printf("--------"); printf("----------------\n");
 printf("SUM :\t"); for (i in poollist) printf("%s\t",sumpool[i]); printf("|\n");
}'

```


#### Reboot a ceph cluster
It take more than below. This is a start
https://access.redhat.com/documentation/zh-tw/red_hat_ceph_storage/5/html/administration_guide/understanding-process-management-for-ceph#powering-down-and-rebooting-a-red-hat-ceph-storage-cluster_admin
```

If you use the Ceph File System (CephFS), bring down the CephFS cluster: 
eph fs set cephfs max_mds 1
ceph fs fail cephfs
ceph status
ceph fs set cephfs joinable false

ceph osd set noout
ceph osd set norecover
ceph osd set norebalance
ceph osd set nobackfill
ceph osd set nodown
ceph osd set pause

# If the MDS and Ceph Object Gateway nodes are on their own dedicated nodes, power them off.

# Shut down the OSD nodes one by one
systemctl stop ceph-499829b4-832f-11eb-8d6d-001a4a000635@osd.2.service

# Shut down the monitor nodes one by one:
systemctl stop ceph-499829b4-832f-11eb-8d6d-001a4a000635@mon.host01.service

# Reboot

systemctl start ceph-499829b4-832f-11eb-8d6d-001a4a000635@mon.host01.service

systemctl start ceph-499829b4-832f-11eb-8d6d-001a4a000635@osd.2.service

sudo ceph -s

ceph osd unset noout
ceph osd unset norecover
ceph osd unset norebalance
ceph osd unset nobackfill
ceph osd unset nodown
ceph osd unset pause

# If you use the Ceph File System (CephFS), bring the CephFS cluster back up by setting the joinable flag to true
ceph fs set cephfs joinable true


```


#### erasure encoding
```
# List profiles
ceph osd erasure-code-profile ls
# Display profile settings (replace {name} with your profile name)
ceph osd erasure-code-profile get {name}

# Display profile settings of the default profile
ceph osd erasure-code-profile get default

```


