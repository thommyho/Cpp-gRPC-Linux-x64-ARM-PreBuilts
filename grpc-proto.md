


# grpc-proto/cci.20220627

---



<br>

## grpc-proto/cci.20220627 dependencies

* [protobuf/3.21.4](https://conan.io/center/protobuf)
* [googleapis/cci.20220711](https://conan.io/center/googleapis)
* [zlib/1.2.13](https://conan.io/center/zlib)

<br>

## Using the grpc-proto Conan Package

<br>

Conan integrates with different build systems. You can declare which build system you want your project to use setting in the **[generators]** section of the [conanfile.txt](https://docs.conan.io/en/latest/reference/conanfile_txt.html#generators) or using the **generators** attribute in the [conanfile.py](https://docs.conan.io/en/latest/reference/conanfile/attributes.html#generators). Here, there is some basic information you can use to integrate **grpc-proto** in your own project. For more detailed information, please [check the Conan documentation](https://docs.conan.io/en/latest/getting_started.html).



<br>

## Using grpc-proto with CMake

<br>

### [Conan CMake generators](https://docs.conan.io/en/latest/reference/conanfile/tools/cmake.html)

<br>

* [CMakeDeps](https://docs.conan.io/en/latest/reference/conanfile/tools/cmake/cmakedeps.html): generates information about where the **grpc-proto** library and its dependencies  ( [protobuf](https://conan.io/center/protobuf),  [googleapis](https://conan.io/center/googleapis),  [zlib](https://conan.io/center/zlib)) are installed together with other information like version, flags, and directory data or configuration. CMake will use this files when you invoke ``find_package()`` in your *CMakeLists.txt*.

* [CMakeToolchain](https://docs.conan.io/en/latest/reference/conanfile/tools/cmake/cmaketoolchain.html): generates a CMake toolchain file that you can later invoke with CMake in the command line using `-DCMAKE_TOOLCHAIN_FILE=conantoolchain.cmake`.

Declare these generators in your **conanfile.txt** along with your **grpc-proto** dependency like:

```ini
[requires]
grpc-proto/cci.20220627

[generators]
CMakeDeps
CMakeToolchain
```

<br>

To use **grpc-proto** in a simple CMake project with this structure:

```shell
.
|-- CMakeLists.txt
|-- conanfile.txt
`-- src
    `-- main..cpp
```

<br>

Your **CMakeLists.txt** could look similar to this, using the global **grpc-proto::grpc-proto** CMake's target:

```cmake
cmake_minimum_required(VERSION 3.15)
project(grpc-proto_project CXX)

find_package(grpc-proto)

add_executable(${PROJECT_NAME} src/main.cpp)

# Use the global target
target_link_libraries(${PROJECT_NAME} grpc-proto::grpc-proto)
```

<br>

To install **grpc-proto/cci.20220627**, its dependencies and build your project, you just have to do:

```shell
# for Linux/macOS
$ conan install . --install-folder cmake-build-release --build=missing
$ cmake . -DCMAKE_TOOLCHAIN_FILE=cmake-build-release/conan_toolchain.cmake -DCMAKE_BUILD_TYPE=Release
$ cmake --build .

# for Windows and Visual Studio 2017
$ conan install . --output-folder cmake-build --build=missing
$ cmake . -G "Visual Studio 15 2017" -DCMAKE_TOOLCHAIN_FILE=cmake-build/conan_toolchain.cmake
$ cmake --build . --config Release
```








<br>

## Using grpc-proto with Visual Studio

<br>

### [Visual Studio Conan generators](https://docs.conan.io/en/latest/reference/conanfile/tools/microsoft.html)

<br>

* [MSBuildDeps](https://docs.conan.io/en/latest/reference/conanfile/tools/microsoft.html#msbuilddeps): generates the **conandeps.props** properties file with information about where the **grpc-proto** library and its dependencies  ( [protobuf](https://conan.io/center/protobuf),  [googleapis](https://conan.io/center/googleapis),  [zlib](https://conan.io/center/zlib)) are installed together with other information like version, flags, and directory data or configuration.

* [MSBuildToolchain](https://docs.conan.io/en/latest/reference/conanfile/tools/microsoft.html#msbuildtoolchain): Generates the **conantoolchain.props** properties file with the current package configuration, settings, and options.

Declare these generators in your **conanfile.txt** along with your **grpc-proto** dependency like:

```ini
[requires]
grpc-proto/cci.20220627

[generators]
MSBuildDeps
MSBuildToolchain
```

<br>

Please, [check the Conan documentation](https://docs.conan.io/en/latest/reference/conanfile/tools/microsoft.html) for more detailed information on how to add these properties files to your Visual Studio projects.



<br>

## Using grpc-proto with Autotools and pkg-config

<br>

### [Autotools Conan generators](https://docs.conan.io/en/latest/reference/conanfile/tools/gnu.html)

<br>

* [AutotoolsToolchain](https://docs.conan.io/en/latest/reference/conanfile/tools/gnu/autotoolstoolchain.html): generates the **conanautotoolstoolchain.sh/bat** script translating information from the current package configuration, settings, and options setting some enviroment variables for Autotools like: ``CPPFLAGS``, ``CXXFLAGS``, ``CFLAGS`` and ``LDFLAGS``. It will also generate a ``deactivate_conanautotoolstoolchain.sh/bat`` so you can restore your environment.

* [AutotoolsDeps](https://docs.conan.io/en/latest/reference/conanfile/tools/gnu/autotoolsdeps.html): generates the **conanautotoolsdeps.sh/bat** script with information about where the **grpc-proto** library and its dependencies  ( [protobuf](https://conan.io/center/protobuf),  [googleapis](https://conan.io/center/googleapis),  [zlib](https://conan.io/center/zlib)) are installed together with other information like version, flags, and directory data or configuration. This is done setting some enviroment variables for Autotools like: ``LIBS``, ``CPPFLAGS``,``CXXFLAGS``, ``CFLAGS`` and ``LDFLAGS``.  It will also generate a ``deactivate_conanautotoolsdeps.sh/bat`` so you can restore your environment.

Declare these generators in your **conanfile.txt** along with your **grpc-proto** dependency like:

```ini
[requires]
grpc-proto/cci.20220627

[generators]
AutotoolsToolchain
AutotoolsDeps
```

<br>

Then, building your project is as easy as:

```shell
$ conan install .
# set the environment variables for Autotools
$ source conanautotoolstoolchain.sh
$ source conanautotoolsdeps.sh
$ ./configure
$ make

# restore the environment after the build is completed
$ source deactivate_conanautotoolstoolchain.sh
$ source deactivate_conanautotoolsdeps.sh
```

<br>

### [pkg-config Conan generator](https://docs.conan.io/en/latest/reference/conanfile/tools/gnu/pkgconfigdeps.html)

<br>

* [PkgConfigDeps](https://docs.conan.io/en/latest/reference/conanfile/tools/gnu/pkgconfigdeps.html): generates the **grpc-proto.pc** file (and the ones corresponding to **grpc-proto** dependencies) with information about the dependencies that can be later used by the **pkg-config** tool pkg-config to collect data about the libraries Conan installed.

<br>

You can use this generator instead of the **AutotoolsDeps** one:

```ini
[requires]
grpc-proto/cci.20220627

[generators]
AutotoolsToolchain
PkgConfigDeps
```

<br>

And then using **pkg-config** to set the environment variables you want, like:

```shell
$ conan install .
# set the environment variables for Autotools
$ source conanautotoolstoolchain.sh

$ export CPPFLAGS="$CPPFLAGS $(pkg-config --cflags grpc-proto)"
$ export LIBS="$LIBS $(pkg-config --libs-only-l grpc-proto)"
$ export LDFLAGS="$LDFLAGS $(pkg-config --libs-only-L --libs-only-other grpc-proto)"

$ ./configure
$ make

# restore the environment after the build is completed
$ source deactivate_conanautotoolstoolchain.sh
```




<br>

## Other build systems

<br>

Please, [check the Conan documentation](https://docs.conan.io/en/latest/reference/conanfile/tools.html) for other integrations besides the ones listed in this document.






<br>

## Exposed header files for grpc-proto

<br>

```cpp
#include <grpc/channelz/v1/channelz.pb.h>
#include <grpc/gcp/handshaker.pb.h>
#include <grpc/gcp/transport_security_common.pb.h>
#include <grpc/gcp/altscontext.pb.h>
#include <grpc/core/stats.pb.h>
#include <grpc/health/v1/health.pb.h>
#include <grpc/reflection/v1alpha/reflection.pb.h>
#include <grpc/reflection/v1/reflection.pb.h>
#include <grpc/service_config/service_config.pb.h>
#include <grpc/testing/stats.pb.h>
#include <grpc/testing/benchmark_service.pb.h>
#include <grpc/testing/control.pb.h>
#include <grpc/testing/worker_service.pb.h>
#include <grpc/testing/payloads.pb.h>
#include <grpc/testing/messages.pb.h>
#include <grpc/testing/report_qps_scenario_service.pb.h>
#include <grpc/lookup/v1/rls_config.pb.h>
#include <grpc/lookup/v1/rls.pb.h>
#include <grpc/binlog/v1/binarylog.pb.h>
#include <grpc/lb/v1/load_balancer.pb.h>
#include <grpc/lb/v1/load_reporter.pb.h>
```

<br>


---
---
Conan **1.58.0**. JFrog LTD. [https://conan.io](https://conan.io). Autogenerated 2023-02-05 20:12:53.