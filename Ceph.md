
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


# configure (in the config file) the crush-failure-domain to impact how the data is spread
# Choose to survive from outage of: osd, host, rack. Example, survive 1 server/host outage:
crush-failure-domain=host

# K and M
# K: data chunks, M: coding chunks
# Sustain loss of 2 OSD (M = 2), Spread over 5 OSD => K = 3, as K+M=5 (the 5 OSD spread)

# Overhead
# The overhead factor (space amplification) of an erasure-coded pool is (k+m) / k
	m=1	m=2	m=3	m=4	m=5	m=6	m=7	m=8	m=9	m=10	m=11
k=1	2.00	3.00	4.00	5.00	6.00	7.00	8.00	9.00	10.00	11.00	12.00
k=2	1.50	2.00	2.50	3.00	3.50	4.00	4.50	5.00	5.50	6.00	6.50
k=3	1.33	1.67	2.00	2.33	2.67	3.00	3.33	3.67	4.00	4.33	4.67
k=4	1.25	1.50	1.75	2.00	2.25	2.50	2.75	3.00	3.25	3.50	3.75
k=5	1.20	1.40	1.60	1.80	2.00	2.20	2.40	2.60	2.80	3.00	3.20
k=6	1.16	1.33	1.50	1.66	1.83	2.00	2.17	2.33	2.50	2.66	2.83
k=7	1.14	1.29	1.43	1.58	1.71	1.86	2.00	2.14	2.29	2.43	2.58
k=8	1.13	1.25	1.38	1.50	1.63	1.75	1.88	2.00	2.13	2.25	2.38
k=9	1.11	1.22	1.33	1.44	1.56	1.67	1.78	1.88	2.00	2.11	2.22
k=10	1.10	1.20	1.30	1.40	1.50	1.60	1.70	1.80	1.90	2.00	2.10
k=11	1.09	1.18	1.27	1.36	1.45	1.54	1.63	1.72	1.82	1.91	2.00

```


