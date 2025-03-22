```sh
$ ceph mon dump
epoch 2
fsid 91fb2e11-d9b5-43ca-929f-d02033c1f837
last_changed 2025-03-20T22:14:27.881784+0900
created 2025-02-19T19:50:43.403633+0900
min_mon_release 19 (squid)
election_strategy: 1
0: [v2:192.168.11.201:3300/0,v1:192.168.11.201:6789/0] mon.pve201
1: [v2:192.168.11.202:3300/0,v1:192.168.11.202:6789/0] mon.pve202
dumped monmap epoch 2
```

```sh
$ ceph auth get-key client.admin
AQCDt7VnFGO/AhAAovHNIghR6LVlmw392IGU/w==
```

```sh
$ ceph status
  cluster:
    id:     91fb2e11-d9b5-43ca-929f-d02033c1f837
    health: HEALTH_OK
 
  services:
    mon: 2 daemons, quorum pve201,pve202 (age 41h)
    mgr: pve201(active, since 10d)
    mds: 1/1 daemons up, 2 standby
    osd: 3 osds: 3 up (since 10d), 3 in (since 4w)
 
  data:
    volumes: 1/1 healthy
    pools:   5 pools, 129 pgs
    objects: 564 objects, 2.1 GiB
    usage:   6.5 GiB used, 935 GiB / 942 GiB avail
    pgs:     129 active+clean
```
