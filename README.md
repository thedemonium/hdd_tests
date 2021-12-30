<h1>Comparison of disks NVME vs SSD</h1>

<h2>#NVME Disks</h2>

- /dev/disk/by-id/nvme-SAMSUNG_MZQLB3T8HALS-00007_S438NC0R504906 
- /dev/disk/by-id/nvme-SAMSUNG_MZQLB3T8HALS-00007_S438NC0R504914 
- /dev/disk/by-id/nvme-SAMSUNG_MZQLB3T8HALS-00007_S438NC0R504919 
- /dev/disk/by-id/nvme-SAMSUNG_MZQLB3T8HALS-00007_S438NC0R504920 
- /dev/disk/by-id/nvme-SAMSUNG_MZQLB3T8HALS-00007_S438NC0R504923 


<h2>#SSD Disks</h2>

- /dev/disk/by-id/ata-Samsung_SSD_860_PRO_4TB_S5G9NC0R700213H
- /dev/disk/by-id/ata-Samsung_SSD_860_PRO_4TB_S5G9NC0R700290W
- /dev/disk/by-id/ata-Samsung_SSD_860_PRO_4TB_S5G9NC0R700292B
- /dev/disk/by-id/ata-Samsung_SSD_860_PRO_4TB_S5G9NC0R700584R


<h2>#FIO Settings Test random read/writes</h2>

<code>
[global]
bs=4K
iodepth=16
direct=1
numjobs=4
group_reporting
time_based

[random_rw]
rw=randrw
size=50G
</code>



<h2>#Table of results with mdraid (custom limits)</h2>

| Command (custom settings)                                             | etalon without raid                               | raid1                                             | raid5 |
|-----------------------------------------------------------------------|---------------------------------------------------|---------------------------------------------------|-------|
| pgbench -h 127.0.0.1 -p 5432 -U postgres -i -s 150 benchmark          | done in 30.33 s                                   | done in 40.91 s                                   |       |
| pgbench -h 127.0.0.1 -p 5432 -U postgres -i -s 15000 benchmark        | done in 3825.46 s                                 | done in 3902.66 s                                 |       |
| pgbench -h 127.0.0.1 -p 5432 -U postgres  -T 90 -j 2 benchmark        | number of transactions actually processed: 42564  | number of transactions actually processed: 71177  |       |
| pgbench -h 127.0.0.1 -p 5432 -U postgres -T 30 -j 2 -S -c 4 benchmark | number of transactions actually processed: 205240 | number of transactions actually processed: 556360 |       |

<h2>#Table of results with mdraid without limits</h2>

| Command (default settings)                                                                | etalon without raid                                | raid1                                             | raid5                                             | raid5-status-failed                               |
|-----------------------------------------------------------------------|----------------------------------------------------|---------------------------------------------------|---------------------------------------------------|---------------------------------------------------|
| pgbench -h 127.0.0.1 -p 5432 -U postgres -i -s 150 benchmark          | done in 24.46 s                                    | done in 23.62 s                                   | done in 32.87 s                                   | done in 56.83 s                                   |
| pgbench -h 127.0.0.1 -p 5432 -U postgres -i -s 15000 benchmark        | done in 2374.99 s                                  | done in 2386.01 s                                 | done in 3258.05 s                                 | done in 3252.54 s                                 |
| pgbench -h 127.0.0.1 -p 5432 -U postgres  -T 90 -j 2 benchmark        | number of transactions actually processed: 99878   | number of transactions actually processed: 96676  | number of transactions actually processed: 67668  | number of transactions actually processed: 70750  |
| pgbench -h 127.0.0.1 -p 5432 -U postgres -T 30 -j 2 -S -c 4 benchmark | number of transactions actually processed: 1596150 | number of transactions actually processed: 849168 | number of transactions actually processed: 713059 | number of transactions actually processed: 783608 |

<h2>#Table of results with lvmraid (custom limits)</h2>

| Command (custom settings)                                             | etalon without raid                               | raid1                                             | raid5                                             |
|-----------------------------------------------------------------------|---------------------------------------------------|---------------------------------------------------|---------------------------------------------------|
| pgbench -h 127.0.0.1 -p 5432 -U postgres -i -s 150 benchmark          | done in 37.98 s                                   | done in 55.01 s                                   | done in 57.30 s                                   |
| pgbench -h 127.0.0.1 -p 5432 -U postgres -i -s 15000 benchmark        | done in 3506.52 s                                 | done in 3741.85 s                                 | done in 4394.09 s                                 |
| pgbench -h 127.0.0.1 -p 5432 -U postgres  -T 90 -j 2 benchmark        | number of transactions actually processed: 42783  | number of transactions actually processed: 64999  | number of transactions actually processed: 31419  |
| pgbench -h 127.0.0.1 -p 5432 -U postgres -T 30 -j 2 -S -c 4 benchmark | number of transactions actually processed: 382540 | number of transactions actually processed: 291017 | number of transactions actually processed: 195523 |

<h2>#Table of results with lvmraid (default settings)</h2>

| Command (default settings)                                            | etalon without raid                               | raid1                                             | raid5                                             |
|-----------------------------------------------------------------------|---------------------------------------------------|---------------------------------------------------|---------------------------------------------------|
| pgbench -h 127.0.0.1 -p 5432 -U postgres -i -s 150 benchmark          | done in 37.53 s                                   | done in 46.31 s                                   | done in 52.31 s                                   |
| pgbench -h 127.0.0.1 -p 5432 -U postgres -i -s 15000 benchmark        | done in 4122.66 s                                 | done in 2262.67 s                                 | done in 2941.22 s                                 |
| pgbench -h 127.0.0.1 -p 5432 -U postgres  -T 90 -j 2 benchmark        | number of transactions actually processed: 39174  | number of transactions actually processed: 104473 | number of transactions actually processed: 66207  |
| pgbench -h 127.0.0.1 -p 5432 -U postgres -T 30 -j 2 -S -c 4 benchmark | number of transactions actually processed: 310658 | number of transactions actually processed: 709422 | number of transactions actually processed: 705175 |

<h2>#Сustom limits</h2>
Container:

<br>  limits.cpu: "4"
<br>  limits.memory: 16GB

Postgres:

<br>  shared_buffers = 8GB
<br>  #huge_pages = try
<br>  work_mem = 32MB
<br>  maintenance_work_mem = 1GB
<br>  dynamic_shared_memory_type = posix
<br>  wal_level = replica
<br>  max_wal_senders = 3
<br>  checkpoint_timeout = 1200
<br>  wal_compression = on
<br>  max_wal_size = 8GB
<br>  min_wal_size = 80MB
