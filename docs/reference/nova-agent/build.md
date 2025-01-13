# trace-agent 构建


## 概述

目前有支持两种方式构建, 分别对应两种不同的集成第三方库的方式.
1. `package`模式. 这种模式下需要预编译安装第三方库, 该库会默认安装到`.build/install`目录下.
2. `module`模式. 这种模式下会直接从源码编译第三方库, 每次编译的耗时比较长.

同时为了方便构建, 可以使用`CMakePresets.json`文件保存构建参数, 不需要在命令行手动设置参数.

## 环境要求

- CMake >= 3.8
- 编译器需要支持 C++17

### 使用docker构建

这里有一个预编译好的docker镜像, 你可以使用该镜像构建项目.

```shell
docker pull aronic/cppdev:latest
```


## 1. package模式
`package`模式是默认安装模式, 不需要额外设置参数.
1. 首先需要预编译第三方库. 如果已经安装过, 可以跳过这一步. 重复执行脚步不会引起重复安装. Docker镜像里面已经安装好了第三方库, 可以直接跳过这一步.
```shell
./build_third_party.sh
```

1. 为当前shell设置环境变量, 使得cmake能够找到第三方库.
```shell
source setup_env.sh
```

1. 使用cmake构建项目.
```shell
mkdir build
cmake -S . -B build \
      -DCMAKE_BUILD_TYPE=Release \
      -DTHIRD_PARTY_INSTALL_DIR="${THIRD_PARTY_INSTALL_DIR}" \
      -DCMAKE_MODULE_PATH="${THIRD_PARTY_INSTALL_DIR}/lib/cmake;${THIRD_PARTY_INSTALL_DIR}/lib64/cmake" \
      -DCMAKE_PREFIX_PATH=${THIRD_PARTY_INSTALL_DIR} \
      -DOPENSSL_ROOT_DIR=${THIRD_PARTY_INSTALL_DIR} \
      -DOPENSSL_INCLUDE_DIR=${THIRD_PARTY_INSTALL_DIR}/include \
      -DOPENSSL_CRYPTO_LIBRARY=${THIRD_PARTY_INSTALL_DIR}/lib/libcrypto.a \
      -DOPENSSL_SSL_LIBRARY=${THIRD_PARTY_INSTALL_DIR}/lib/libssl.a
cmake --build . --target nova-agent
```

## 2. `module`模式

module 模式下会集成第三方的CMakeLists.txt文件, 从源码编译第三方库. 这种方式编译时间会比较长. 不推荐这种方式.
当前的module模式有编译问题. 请使用package模式.


## CMakeList.txt 参数说明

### Debug模式
使用 `CMAKE_BUILD_TYPE=Debug` 指定为Debug模式, 在Debug模式下支撑如下的参数.

- `SANITIZER_TYPE` 指定使用的Sanitizer类型. 可选值为 `none`, `address`, `leak`, `thread`, `undefined`. 默认值为 `none`.
- `ENABLE_IWYU` 指定是否启用include-what-you-use工具. 可选值为 `ON`, `OFF`. 默认值为 `OFF`.


### Release 模式
使用 `CMAKE_BUILD_TYPE=Release` 指定为Release模式. Release 发布的二进制携带Debug信息, 但是不会启用Sanitizer. 同时绝大多数第三方库是静态链接的.


## 使用CMakePresets.json

如果你的CMake版本支持CMakePresets.json, 可以直接使用该文件构建项目.
CMakePresets.json 文件可以保存CMake参数和配置项, 不需要在命令行手动设置.

### CMakePresets.json 文件内容
```json
{
  "version": 2,
  "configurePresets": [
    {
      "name": "default",
      "generator": "Ninja",
      "binaryDir": "/tmp/build-nova-agent",
      "cacheVariables": {
        "THIRD_PARTY_INSTALL_DIR": "$env{THIRD_PARTY_INSTALL_DIR}",
        "CMAKE_MODULE_PATH": "$env{THIRD_PARTY_INSTALL_DIR}/lib/cmake",
        "CMAKE_PREFIX_PATH": "$env{THIRD_PARTY_INSTALL_DIR}",
        "CMAKE_BUILD_TYPE": "Debug",
        "SANITIZER_TYPE": "none",
        "ENABLE_IWYU": "ON"
      }
    },
    {
      "name": "release",
      "generator": "Ninja",
      "binaryDir": "/tmp/release-nova-agent",
      "cacheVariables": {
        "THIRD_PARTY_INSTALL_DIR": "$env{THIRD_PARTY_INSTALL_DIR}",
        "CMAKE_MODULE_PATH": "$env{THIRD_PARTY_INSTALL_DIR}/lib/cmake",
        "CMAKE_PREFIX_PATH": "$env{THIRD_PARTY_INSTALL_DIR}",
        "CMAKE_BUILD_TYPE": "Release",
        "SANITIZER_TYPE": "none",
        "ENABLE_IWYU": "OFF"
      }
    }
  ],
  "buildPresets": [
    {
      "name": "default",
      "configurePreset": "default"
    }
  ]
}
```

### 使用CMakePresets.json

```shell
source setup_env.sh # 设置环境变量
cmake --preset=default
```

### 使用Dockerfile部署

当我们打包好二进制后，可以使用dockerfile部署打包成为镜像，打包指令

```
 sudo docker build -f docker/deploy/Dockerfile -t test:1.01 .
```