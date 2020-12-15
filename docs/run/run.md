---
id: run
title: "运行 MISA-AKMC"
sidebar_label: "运行 MISA-AKMC"
---

我们假设你已通过上述步骤完成了 MISA-AKMC 的编译构建工作，编译完成的二进制可执行文件位于 `$AKMC_PATH/build/bin/` 目录下。

## 1.运行
你可以使用 `mpirun` 命令运行并行的 MISA-AKMC 分子动力学软件。例如，在下面的示例中，使用4个 MPI 进程运行 MISA-AKMC, 并指定配置文件路径为 `$AKMC_PATH/example/config.yaml` 文件。

?> 关于配置文件的相关说明可参考[**配置项说明**](https://hpcer.pages.hpcer.dev/misa-akmc/users-manual/reference/reference/)等相关章节。

```bash
cd $AKMC_PATH/example
mpirun -n 4 ../build/bin/pmisa-kmc -c config.yaml
```
更多信息可以通过执行`$AKMC_PATH/build/bin/pmisa-kmc --help`命令查看。

```bash
$ cd $AKMC_PATH
$ build/bin/pmisa-kmc --help
  build/bin/pmisa-kmc {OPTIONS}

    This is parallel misa-kmc program.

  OPTIONS:

      -h, --help                        Display this help menu
      -c[conf], --conf=[conf]           The configure file
      -v, --version                     show version number
```

## 2.运行结果

运行完成后， example 目录中会生成名为 kmc.\*.out 的二进制文件( kmc.\*.out 为默认的输出文件名称，可在配置文件中更改)。该文件中包含各个指定时间步 dump 的所有原子信息，如原子类型、位置坐标等。