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


<h2>#Сustom limits for pgbench</h2>
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
