---
id: reference
title: "配置项说明"
sidebar_label: "配置项说明"
---

MISA-AKMC 使用 [yaml](https://yaml.org) 格式作为配置文件的格式

## 1.示例

以下展示了 MISA-AKMC 配置文件的部分示例：
```yaml
# This is the config file of parallel kMC program.
# file format: yaml, see https://yaml.org for mor e details.
# config template file writen by <a href='mailto:genshenchu@gmail.com'>genshen</a>"

title: "parallel kMC configure file"
version: "0.1.0"

box:
  size: [80, 80, 80]
  lattice_const: 2.85532   # lattice constance
  cutoff_radius: 5.6

create: # how the simulation box is created.
  random:
    enable: true
    va_count: 1   # vacancy number, not percent.
    alloy:
      Fe: 9598
      Cu: 134
      Mn: 134
      Ni: 134
      FeFe: 0 # pair number of [110] dumbbell.
      FeCu: 0
      FeMn: 0
      FeNi: 0
      CuCu: 0
      CuNi: 0
      CuMn: 0
      NiNi: 0
      NiMn: 0
      MnMn: 0
  pipe: # if create_box is set to false or not set, then pipe will be used.
    enable: false
    input_box: last_frame.xyz # pipe from MD.
  restart:
    enable: false
    file_path: 1072.xyz

seeds:
  seeds_file: "" # used for setting different seed for each MPI rank (todo)
  create_types: 100565 # if 0 is set, random device will be used.
  create_vacancy: 16650
  event_selection: 563264
  time_inc: 594689

simulation:
  temperature: 673  # unit: K
  physics_time: 8e4  # physics time limit.
  steps_limit: 1000 # limit of kMC steps.
  attempt_freq: 6e12 #  unit:  1/s
  isgenr: false
  dpasm1: 3e-9 # dpa per second, unit: dpa/s

output:
  dump:
    interval: 100 # dump system lattice information.
    file_path: "kmc.{}.out"
  logs:
    interval: 10 # if zero is set, it means no log.
    logs_file: "" # if it is empty, log to /dev/console
```

## 2.使用配置文件
你可以在运行 MISA-AKMC 程序时，通过命令行参数配置文件路径，程序可以读取配置文件，以进行后续模拟，例如：

```bash
mpirun -n 4 /path/of/pmisa-akmc -c /path/of/config.yaml
```
或者：
```bash
mpirun -n 4 /path/of/pmisa-akmc --conf=/path/of/config.yaml
```