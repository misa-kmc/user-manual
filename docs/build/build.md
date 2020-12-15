---
id: build
title: "编译构建"
sidebar_label: "编译"
---

MISA-AKMC 使用 CMake 工具进行编译构建，关于如何使用 CMake 工具可以参考[相关文档](https://cmake.org/cmake/help/v3.0/index.html)。在开始进行构建之前，请确保你已完成编译环境的配置。

## 1. 使用 CMake 工具编译

```bash
cd $AKMC_PATH
cmake -B ./build -H./ -DCMAKE_BUILD_TYPE=Release
cmake --build ./build
```

执行上述步骤后，编译完成的可执行文件 misa-kmc 以及 pmisa-kmc 以及相关的测试程序均置于 `$AKMC_PATH/build/bin` 目录

## 2. 构建选项

如果你需要将编译完成的二进制文件安装至指定目录，可使用以下命令进行构建并安装：

```bash
cd $AKMC_PATH
cmake -B./build -H./ -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=/your/desirable/path/ 
cmake --build ./build
cmake --build ./build --target install # install
```

在执行 cmake 命令的时候，可以指定 CMake 构建工具内置的参数，详细的参数列表可以参考[相关文档](https://cmake.org/cmake/help/v3.0/manual/cmake-variables.7.html)，还可以使用以下参数：

| 参数                       | 取值                    | 默认值 | 说明                               |
| -------------------------- | ----------------------- | ------ | ---------------------------------- |
| KMC_OpenMP_ENABLE_FLAG     | ON/OFF                  | OFF    | 是否使用 OpenMP 构建               |
| KMC_MPI_ENABLE_FLAG        | ON/OFF                  | ON     | 是否使用 MPI 构建                  |
| KMC_TEST_BUILD_ENABLE_FLAG | ON/OFF                  | ON     | 是否构建 test (单元测试)           |
| KMC_TEST_MPI_ENABLE_FLAG   | ON/OFF                  | ON     | 是否在测试中启用 MPI               |
| EAM_POT_ENABLE_FLAG        | ON/OFF                  | OFF    | 是否启用使用电子势能来计算系统能量 |
| KMC_RAND                   | LCG/MT/STC/xoshiro/REAL | MT     | 随机数生成器                       |

注：其中 KMC_RAND 中的取值代表着如下方法

| 选项    | 方法                                    |
| ------- | --------------------------------------- |
| LCG     | linear congruential                     |
| MT      | mersenne twister                        |
| STC     | subtract with carry                     |
| xoshiro | http://xoshiro.di.unimi.it              |
| REAL    | real random number privided by linux OS |

例如，如果你不希望构建单元测试，可以使用如下命令进行构建：

```bash
cd $AKMC_PATH
cmake -B ./build -H./ -DKMC_TEST_BUILD_ENABLE_FLAG=OFF
cmake --build ./build
```

