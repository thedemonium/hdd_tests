# hdd_tests
Comparison of disks NVME vs SSD

#NVME Disks
/dev/disk/by-id/nvme-SAMSUNG_MZQLB3T8HALS-00007_S438NC0R504906 
/dev/disk/by-id/nvme-SAMSUNG_MZQLB3T8HALS-00007_S438NC0R504914 
/dev/disk/by-id/nvme-SAMSUNG_MZQLB3T8HALS-00007_S438NC0R504919 
/dev/disk/by-id/nvme-SAMSUNG_MZQLB3T8HALS-00007_S438NC0R504920 
/dev/disk/by-id/nvme-SAMSUNG_MZQLB3T8HALS-00007_S438NC0R504923 

#SSD Disks
/dev/disk/by-id/ata-Samsung_SSD_860_PRO_4TB_S5G9NC0R700213H
/dev/disk/by-id/ata-Samsung_SSD_860_PRO_4TB_S5G9NC0R700290W
/dev/disk/by-id/ata-Samsung_SSD_860_PRO_4TB_S5G9NC0R700292B
/dev/disk/by-id/ata-Samsung_SSD_860_PRO_4TB_S5G9NC0R700584R

#FIO Settings Test random read/writes
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
