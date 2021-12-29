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


<h2>#Table of results with mdraid without limits</h2>

| Command                                                               | etalon without raid                                | raid0                                             | raid5                                             | raid5-status-failed                               |
|-----------------------------------------------------------------------|----------------------------------------------------|---------------------------------------------------|---------------------------------------------------|---------------------------------------------------|
| pgbench -h 127.0.0.1 -p 5432 -U postgres -i -s 150 benchmark          | done in 24.46 s                                    | done in 23.62 s                                   | done in 32.87 s                                   | done in 56.83 s                                   |
| pgbench -h 127.0.0.1 -p 5432 -U postgres -i -s 15000 benchmark        | done in 2374.99 s                                  | done in 2386.01 s                                 | done in 3258.05 s                                 | done in 3252.54 s                                 |
| pgbench -h 127.0.0.1 -p 5432 -U postgres  -T 90 -j 2 benchmark        | number of transactions actually processed: 99878   | number of transactions actually processed: 96676  | number of transactions actually processed: 67668  | number of transactions actually processed: 70750  |
| pgbench -h 127.0.0.1 -p 5432 -U postgres -T 30 -j 2 -S -c 4 benchmark | number of transactions actually processed: 1596150 | number of transactions actually processed: 849168 | number of transactions actually processed: 713059 | number of transactions actually processed: 783608 |

<h2>#Table of results with lvmraid (custom limits)</h2>

| Command (custom settings)                                             | etalon without raid | raid0                                             | raid5                                             |
|-----------------------------------------------------------------------|---------------------|---------------------------------------------------|---------------------------------------------------|
| pgbench -h 127.0.0.1 -p 5432 -U postgres -i -s 150 benchmark          | done in 37.98 s     | done in 55.01 s                                   | done in 57.30 s                                   |
| pgbench -h 127.0.0.1 -p 5432 -U postgres -i -s 15000 benchmark        |                     | done in 3741.85 s                                 | done in 4394.09 s                                 |
| pgbench -h 127.0.0.1 -p 5432 -U postgres  -T 90 -j 2 benchmark        |                     | number of transactions actually processed: 64999  | number of transactions actually processed: 31419  |
| pgbench -h 127.0.0.1 -p 5432 -U postgres -T 30 -j 2 -S -c 4 benchmark |                     | number of transactions actually processed: 291017 | number of transactions actually processed: 195523 |