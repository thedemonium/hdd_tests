#New tests

<h2>#Table of results with mdraid (default settings)</h2>

| Command (mdraid, default settings)                                                                   | etalon without raid | raid1       | raid5     |
|------------------------------------------------------------------------------------------------------|---------------------|-------------|-----------|
| pgbench -h 127.0.0.1 -p 5432 -U postgres -i -s 15000 benchmark                                       | 2350.69 s           | 2451.61 s   | 2963.67 s |
| max TPS iostat во время выполнения "pgbench -h 127.0.0.1 -p 5432 -U postgres  -T 90 -j 4 -c 4 benchmark"    | 82057               | 75027       | 48928     |
| average TPS iostat во время выполнения "pgbench -h 127.0.0.1 -p 5432 -U postgres -T 90 -j 4 -c 4 benchmark" | 9439,166667         | 8425,958333 | 6250      |

<h2>#Table of results with mdraid (custom settings)</h2>

| Command (mdraid, custom settings)                                                                    | etalon without raid | raid1     | raid5       |
|------------------------------------------------------------------------------------------------------|---------------------|-----------|-------------|
| pgbench -h 127.0.0.1 -p 5432 -U postgres -i -s 15000 benchmark                                       | 3697.39 s           | 3830.03 s | 3961.66 s   |
| max TPS iostat во время выполнения "pgbench -h 127.0.0.1 -p 5432 -U postgres  -T 90 -j 4 -c 4 benchmark"    | 6997                | 5060      | 6336        |
| average TPS iostat во время выполнения "pgbench -h 127.0.0.1 -p 5432 -U postgres -T 90 -j 4 -c 4 benchmark" | 6266,583333         | 4449,625  | 5815,208333 |

<h2>#Table of results with lvmraid (default settings)</h2>

| Command (lvmraid, default settings)                                                                         | etalon without raid | raid1       | raid5     |
|-------------------------------------------------------------------------------------------------------------|---------------------|-------------|-----------|
| pgbench -h 127.0.0.1 -p 5432 -U postgres -i -s 15000 benchmark                                              | 2415.00 s           | 2328.45 s   | 2975.07 s |
| max TPS iostat во время выполнения "pgbench -h 127.0.0.1 -p 5432 -U postgres  -T 90 -j 4 -c 4 benchmark"    | 77311               | 81477       | 25 809    |
| average TPS iostat во время выполнения "pgbench -h 127.0.0.1 -p 5432 -U postgres -T 90 -j 4 -c 4 benchmark" | 7996,958333         | 8256,347826 | 3 876     |

<h2>#Table of results with lvmraid (custom settings)</h2>

| Command (lvmraid, custom settings)                                                                          | etalon without raid | raid1       | raid5       |
|-------------------------------------------------------------------------------------------------------------|---------------------|-------------|-------------|
| pgbench -h 127.0.0.1 -p 5432 -U postgres -i -s 15000 benchmark                                              | 3829.98 s           | 3560.77 s   | 4303.23 s   |
| max TPS iostat во время выполнения "pgbench -h 127.0.0.1 -p 5432 -U postgres  -T 90 -j 4 -c 4 benchmark"    | 5936                | 4810        | 3 185       |
| average TPS iostat во время выполнения "pgbench -h 127.0.0.1 -p 5432 -U postgres -T 90 -j 4 -c 4 benchmark" | 5280,333333         | 4604,956522 | 2910,956522 |