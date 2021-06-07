---
id: config-ref
title: "配置项说明"
sidebar_label: "配置项说明"
---

## 配置项说明
配置文件的示例见 `$SLKMC_PATH/example/config.yaml`, 其中配置文件的各个字段如下，你也可以根据你的需求修改各选项的值。

###	基本配置
基本配置指定模拟的基本信息，如空间信息(晶格点数、截断半径等)，体系创建等配置。

- `box`  
说明：指定模拟的基本信息，如box大小、截断半径等;  

- `box.size`  
类型: Unsigned Long 数组, 长度: 3;  
说明：模拟盒子大小，分别为x、y、z三个维度上的尺寸；单位为晶格常数;

- `box.lattice_const`  
类型: Double;  
单位: 埃, Å;  
说明: 晶格常数;  

- `box.cutoff_radius`  
类型: Double;  
说明: 截断半径系数;   截断半径系数乘以晶格常数等于实际的截断半径长度;  

###	模拟体系创建
- `create`  
说明：指定模拟初始化时创建模拟体系的相关参数;  

- `create.random`  
说明：随机创建模拟体系的相关参数

- `create.random.enable`  
类型：Boolean;  
说明：true表示程序初始化时，按照给定参数随机创建原子；false表示读入已有的原子信息以创建原子;  

- `create.random.va_count`  
类型：Unsigned Long;  
说明：模拟体系中空位的数目

- `create.random.alloy`  
说明：合金元素的相关配置; 该部分仅create.random.enable 为 true 时有效;  

- `create.random.alloy.Fe`
类型：Unsigned Int;  
说明：创建合金时，合金中Fe原子的数目;  

- `create.random.alloy.Cu`  
类型：Unsigned Int;  
说明：创建合金时，合金中Cu原子的数目;  

- `create.random.alloy.Mn`  
类型：Unsigned Int;  
说明：创建合金时，合金中Mn原子的数目;  

- `create.random.alloy.FeFe`  
类型：Unsigned Int;  
说明：创建合金时，合金中FeFe[110]间隙对的数目;  

- `create.random.alloy.FeCu`  
类型：Unsigned Int;  
说明：创建合金时，合金中FeCu[110]间隙对的数目;  

- `create.random.alloy.FeMn`  
类型：Unsigned Int;  
说明：创建合金时，合金中FeMn[110]间隙对的数目;  

- `create.random.alloy.FeNi`  
类型：Unsigned Int;  
说明：创建合金时，合金中FeNi[110]间隙对的数目;  

- `create.random.alloy.CuCu`  
类型：Unsigned Int;  
说明：创建合金时，合金中CuCu[110]间隙对的数目;  

- `create.random.alloy.CuNi`  
类型：Unsigned Int;  
说明：创建合金时，合金中CuNi[110]间隙对的数目;  

- `create.random.alloy.CuMn`  
类型：Unsigned Int;  
说明：创建合金时，合金中CuMn[110]间隙对的数目;  

- `create.random.alloy.NiNi`  
类型：Unsigned Int;  
说明：创建合金时，合金中NiNi[110]间隙对的数目;  

- `create.random.alloy.NiMn`  
类型：Unsigned Int;  
说明：创建合金时，合金中NiMn[110]间隙对的数目;  

- `create.random.alloy.MnMn`  
类型：Unsigned Int;  
说明：创建合金时，合金中MnMn[110]间隙对的数目;  

- `create.pipe`  
说明：读入已有的原子信息的相关参数；

- `create.pipe.enable`  
类型：Boolean;  
说明：当且仅当 create.random.enable 为 false 时启用，true 表示使用读入已有的原子信息创建原子；

- `create.pipe.input_box`  
类型：String;  
说明：如果 create.random.enable 为 false 且 create.pipe.enable 为 true, 该项指定读取文件路径;  

###	随机数种子与模拟条件
- `seeds`  
说明：指定随机数种子信息;  

- `seeds.seeds_file`  
类型：String;  
说明：通过读入随机数种子文件，对每个 MPI rank 设置不同的随机数;  

- `seeds.create_vancancy`  
类型：Unsigned Int32;  
说明：创建空位信息的随机数种子;  

- `seeds.event_selection`  
类型：Unsigned Int32;  
说明：选择反应事件的随机数种子;  

- `seeds.time_inc`  
类型：Unsigned Int32;  
说明：确定反应事件事件增量的随机数种子;  

- `simulation`  
说明：指定模拟的条件;  

- `simulation.temperature`  
类型：Double;  
说明：体系的温度，单位为 K;  

- `simulation.physics_time`  
类型：Double;  
说明：模拟的物理时间;  

- `simulation.steps_limit`  
类型：Unsigned Long;  
说明：模拟的最大时间步;  

- `simulation.attempt_freq`  
类型：Double;  
说明：体系的尝试频率;  

- `simulation.dpasm1`  
类型：Double;  
说明：每秒 dpa, 单位 dpa/s

###	输出及日志
- `output`  
说明：输出相关配置;  

- `output.dump`  
说明：预设的体系 dump 配置，包括 dump 文件名、输出模拟等配置;  

- `output.dump.interval`  
类型：Unsigned Long;  
说明：指定每隔一定时间步 dump 体系的点阵信息;  

- `output.dump.file_path`  
类型：String;  
说明：指定 dump 文件的路径;  

- `output.logs`  
说明：程序日志, 可以选择输出到标准输出或者文件;  

- `output.logs.interval`  
类型：Unsigned Long;  
说明：指定每隔一定时间步输出系统的热力学信息，包括体系温度、能量等;  

- `output.logs.logs_file`  
类型：String;  
说明：如果日志输出模式为file, 该选项指定文件路径，如果此项为空日志输出至 /dev/console;  
