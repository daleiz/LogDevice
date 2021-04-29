# Build without Submodules

## Motivation

logdevice 的主要的外部依赖是 fbthrift 等 fb 全家桶，
每次重新构建都需要先编译这些 submodules，
导致速度非常慢。

这里我们使用 vcpkg 来预先安装 fbthrift 和 rocksdb 等外部依赖，
这样重新 build 的时候就只需要构建 logdevice 本身的代码了。

## Build

### install system packages with apt 

test with `ubuntu 18.04` and `ubuntu 20.04`

```bash

sudo apt-get install -y $(cat LogDevice/logdevice/build_tools/ubuntu.deps)

```
### install vcpkg

当前使用的 vcpkg 的 version 是 `2021-01-13-unknownhash`

## use vcpkg install fbthrift

安装的 fbthrift 的版本是 `2020.10.19.00`

安装 fbthrift 的同时会自动安装上 folly, fizz, wangle 等 fb 全家桶

注意，这里 vcpkg 安装的 fbthrift 的 FBThriftConfig.cmake 文件有点问题，
需要进行以下修改：

```cmake

set_and_check(FBTHRIFT_CMAKE_DIR "${PACKAGE_PREFIX_DIR}/share/fbthrift")
set_and_check(FBTHRIFT_INCLUDE_DIR "${PACKAGE_PREFIX_DIR}/include")
if (WIN32)
  set_and_check(FBTHRIFT_COMPILER "${PACKAGE_PREFIX_DIR}/tools/fbthrift/thrift1.exe")
else()
  set_and_check(FBTHRIFT_COMPILER "${PACKAGE_PREFIX_DIR}/tools/fbthrift/thrift1")
endif()

```

主要是 `FBTHRIFT_INCLUDE_DIR`, `FBTHRIFT_INCLUDE_DIR`, `FBTHRIFT_COMPILER` 这些变量要进行调整

## use vcpkg install rocksdb 

当前使用的版本是 `6.14.6`

### build with cmake

`gcc 9+` or `clang 9+`


```bash

mkdir _build

cd _build

cmake -DCMAKE_TOOLCHAIN_FILE=/path/to/vcpkg/scripts/buildsystems/vcpkg.cmake ../logdevice

make -j$(nproc)

```
