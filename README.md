hive-testbench
==============

fork from hortonworks,修改了部分地方，以适配hive 3.0以上的版本

TPCDS基准测试
========


环境信息
=============

* Hadoop 3.1.1(理论上3.0以上的版本都可以，本次由于环境限制，测试版本3.1.1)
* Apache Hive 3.1.0(理论上3.0以上版本都可以，本次测试版本3.1.0)
* Between 15 minutes and 2 days to generate data (depending on the Scale Factor you choose and available hardware).
* If you plan to generate 1TB or more of data, using Apache Hive 13+ to generate the data is STRONGLY suggested.

环境构建
=================

All of these steps should be carried out on your Hadoop cluster.

- Step 1: 准备 

  需要```gcc```支持


- Step 2: 编译 

```bash
./tpcds-build.sh
```

- Step 3: 初始化生成数据 


  The scripts ```tpcds-setup.sh``` and ```tpch-setup.sh``` generate and load data for TPC-DS and TPC-H, respectively. General usage is ```tpcds-setup.sh scale_factor [directory]``` or ```tpch-setup.sh scale_factor [directory]```

例子:
```bash
# 生成100G数据，格式为parquet，路径为/parquet
FORMAT=parquet ./tpcds-setup.sh 100  /parquet
```


- Step 6: 测试 

```bash
cd hive-testbench
perl runSuite.pl tpcds 100 <format> 
```

- Step 7: 查看结果

```bash
# 对应sql结果保存在query<n>.sql.log
cd sample-queries-tpcds
tail -100 query1.sql.log
```

