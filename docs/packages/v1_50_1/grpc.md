


# grpc/1.50.1

---

## grpc/1.50.1 setup with artifactory

For Conan 1.13 and up, use the following command to activate the revision feature:

```shell
export CONAN_REVISIONS_ENABLED=1
```
For your Conan command line client to work with this Conan repository, you first need to add the repository to your client configuration using the following command:

```shell
conan remote add armv7-armv8-x86_64-linux-thommyho http://artifactory.dns.army:8081/artifactory/api/conan/armv7-armv8-x86_64-linux-thommyho
```

**No user login required: anonymous read access is always granted!**

To install the dependencies defined in your project's conanfile.txt from an Artifactory Conan repository, use the following command:

```shell
conan install . grpc/1.50.1@ -r armv7-armv8-x86_64-linux-thommyho
```

<br>

## grpc/1.50.1 dependencies

* [abseil/20220623.0](https://conan.io/center/abseil)
* [c-ares/1.18.1](https://conan.io/center/c-ares)
* [openssl/1.1.1s](https://conan.io/center/openssl)
* [re2/20220601](https://conan.io/center/re2)
* [zlib/1.2.13](https://conan.io/center/zlib)
* [protobuf/3.21.4](https://conan.io/center/protobuf)
* [googleapis/cci.20220711](https://conan.io/center/googleapis)
* [grpc-proto/cci.20220627](https://conan.io/center/grpc-proto)




<br>

## Using the grpc Conan Package

<br>

Conan integrates with different build systems. You can declare which build system you want your project to use setting in the **[generators]** section of the [conanfile.txt](https://docs.conan.io/en/latest/reference/conanfile_txt.html#generators) or using the **generators** attribute in the [conanfile.py](https://docs.conan.io/en/latest/reference/conanfile/attributes.html#generators). Here, there is some basic information you can use to integrate **grpc** in your own project. For more detailed information, please [check the Conan documentation](https://docs.conan.io/en/latest/getting_started.html).



<br>

## Using grpc with CMake

<br>

### [Conan CMake generators](https://docs.conan.io/en/latest/reference/conanfile/tools/cmake.html)

<br>

* [CMakeDeps](https://docs.conan.io/en/latest/reference/conanfile/tools/cmake/cmakedeps.html): generates information about where the **grpc** library and its dependencies  ( [abseil](https://conan.io/center/abseil),  [c-ares](https://conan.io/center/c-ares),  [openssl](https://conan.io/center/openssl),  [re2](https://conan.io/center/re2),  [zlib](https://conan.io/center/zlib),  [protobuf](https://conan.io/center/protobuf),  [googleapis](https://conan.io/center/googleapis),  [grpc-proto](https://conan.io/center/grpc-proto)) are installed together with other information like version, flags, and directory data or configuration. CMake will use this files when you invoke ``find_package()`` in your *CMakeLists.txt*.

* [CMakeToolchain](https://docs.conan.io/en/latest/reference/conanfile/tools/cmake/cmaketoolchain.html): generates a CMake toolchain file that you can later invoke with CMake in the command line using `-DCMAKE_TOOLCHAIN_FILE=conantoolchain.cmake`.

Declare these generators in your **conanfile.txt** along with your **grpc** dependency like:

```ini
[requires]
grpc/1.50.1

[generators]
CMakeDeps
CMakeToolchain
```

<br>

To use **grpc** in a simple CMake project with this structure:

```shell
.
|-- CMakeLists.txt
|-- conanfile.txt
`-- src
    `-- main..cpp
```

<br>

Your **CMakeLists.txt** could look similar to this, using the global **grpc::grpc** CMake's target:

```cmake
cmake_minimum_required(VERSION 3.15)
project(grpc_project CXX)

find_package(gRPC)

add_executable(${PROJECT_NAME} src/main.cpp)

# Use the global target
target_link_libraries(${PROJECT_NAME} grpc::grpc)
```

<br>

To install **grpc/1.50.1**, its dependencies and build your project, you just have to do:

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



As the grpc Conan package defines components, you can link only the desired parts of the library in your project. For example, linking only with the grpc **address_sorting** component, through the **gRPC::address_sorting** target.

```cmake
...
# Link just to grpc address_sorting component
target_link_libraries(${PROJECT_NAME} gRPC::address_sorting)
```

<br>

To check all the available components for **grpc** Conan package, please check the dedicated section at the end of this document.




<br>

### Declared CMake build modules

<br>

#### lib/cmake/conan_trick/grpc_cpp_plugin.cmake
  ```cmake
  if(NOT TARGET gRPC::grpc_cpp_plugin)
      if(CMAKE_CROSSCOMPILING)
          find_program(GRPC_CPP_PLUGIN_PROGRAM
              NAMES grpc_cpp_plugin
              PATHS ENV PATH
              NO_DEFAULT_PATH
          )
      else()
          find_program(GRPC_CPP_PLUGIN_PROGRAM
              NAMES grpc_cpp_plugin
              PATHS "${CMAKE_CURRENT_LIST_DIR}/../../../bin/"
              NO_DEFAULT_PATH
          )
      endif()
      # TODO: In conan v2 with CMakeToolchain, can be replaced by:
      # find_program(GRPC_CPP_PLUGIN_PROGRAM NAMES grpc_cpp_plugin))
      # # Nice enough to handle grpc not in build_requires for native build
      # if(NOT GRPC_CPP_PLUGIN_PROGRAM AND NOT CMAKE_CROSSCOMPILING)
      #     find_program(GRPC_CPP_PLUGIN_PROGRAM
      #         NAMES grpc_cpp_plugin
      #         PATHS "${CMAKE_CURRENT_LIST_DIR}/../../../bin/"
      #         NO_DEFAULT_PATH
      #     )
      # endif()

      if(GRPC_CPP_PLUGIN_PROGRAM)
          get_filename_component(GRPC_CPP_PLUGIN_PROGRAM "${GRPC_CPP_PLUGIN_PROGRAM}" ABSOLUTE)
          add_executable(gRPC::grpc_cpp_plugin IMPORTED)
          set_property(TARGET gRPC::grpc_cpp_plugin PROPERTY IMPORTED_LOCATION ${GRPC_CPP_PLUGIN_PROGRAM})
      endif()
  endif()

  ```#### lib/cmake/conan_trick/grpc_csharp_plugin.cmake
  ```cmake
  if(NOT TARGET gRPC::grpc_csharp_plugin)
      if(CMAKE_CROSSCOMPILING)
          find_program(GRPC_CSHARP_PLUGIN_PROGRAM
              NAMES grpc_csharp_plugin
              PATHS ENV PATH
              NO_DEFAULT_PATH
          )
      else()
          find_program(GRPC_CSHARP_PLUGIN_PROGRAM
              NAMES grpc_csharp_plugin
              PATHS "${CMAKE_CURRENT_LIST_DIR}/../../../bin/"
              NO_DEFAULT_PATH
          )
      endif()
      # TODO: In conan v2 with CMakeToolchain, can be replaced by:
      # find_program(GRPC_CSHARP_PLUGIN_PROGRAM NAMES grpc_csharp_plugin))
      # # Nice enough to handle grpc not in build_requires for native build
      # if(NOT GRPC_CSHARP_PLUGIN_PROGRAM AND NOT CMAKE_CROSSCOMPILING)
      #     find_program(GRPC_CSHARP_PLUGIN_PROGRAM
      #         NAMES grpc_csharp_plugin
      #         PATHS "${CMAKE_CURRENT_LIST_DIR}/../../../bin/"
      #         NO_DEFAULT_PATH
      #     )
      # endif()

      if(GRPC_CSHARP_PLUGIN_PROGRAM)
          get_filename_component(GRPC_CSHARP_PLUGIN_PROGRAM "${GRPC_CSHARP_PLUGIN_PROGRAM}" ABSOLUTE)
          add_executable(gRPC::grpc_csharp_plugin IMPORTED)
          set_property(TARGET gRPC::grpc_csharp_plugin PROPERTY IMPORTED_LOCATION ${GRPC_CSHARP_PLUGIN_PROGRAM})
      endif()
  endif()

  ```#### lib/cmake/conan_trick/grpc_node_plugin.cmake
  ```cmake
  if(NOT TARGET gRPC::grpc_node_plugin)
      if(CMAKE_CROSSCOMPILING)
          find_program(GRPC_NODE_PLUGIN_PROGRAM
              NAMES grpc_node_plugin
              PATHS ENV PATH
              NO_DEFAULT_PATH
          )
      else()
          find_program(GRPC_NODE_PLUGIN_PROGRAM
              NAMES grpc_node_plugin
              PATHS "${CMAKE_CURRENT_LIST_DIR}/../../../bin/"
              NO_DEFAULT_PATH
          )
      endif()
      # TODO: In conan v2 with CMakeToolchain, can be replaced by:
      # find_program(GRPC_NODE_PLUGIN_PROGRAM NAMES grpc_node_plugin))
      # # Nice enough to handle grpc not in build_requires for native build
      # if(NOT GRPC_NODE_PLUGIN_PROGRAM AND NOT CMAKE_CROSSCOMPILING)
      #     find_program(GRPC_NODE_PLUGIN_PROGRAM
      #         NAMES grpc_node_plugin
      #         PATHS "${CMAKE_CURRENT_LIST_DIR}/../../../bin/"
      #         NO_DEFAULT_PATH
      #     )
      # endif()

      if(GRPC_NODE_PLUGIN_PROGRAM)
          get_filename_component(GRPC_NODE_PLUGIN_PROGRAM "${GRPC_NODE_PLUGIN_PROGRAM}" ABSOLUTE)
          add_executable(gRPC::grpc_node_plugin IMPORTED)
          set_property(TARGET gRPC::grpc_node_plugin PROPERTY IMPORTED_LOCATION ${GRPC_NODE_PLUGIN_PROGRAM})
      endif()
  endif()

  ```#### lib/cmake/conan_trick/grpc_objective_c_plugin.cmake
  ```cmake
  if(NOT TARGET gRPC::grpc_objective_c_plugin)
      if(CMAKE_CROSSCOMPILING)
          find_program(GRPC_OBJECTIVE_C_PLUGIN_PROGRAM
              NAMES grpc_objective_c_plugin
              PATHS ENV PATH
              NO_DEFAULT_PATH
          )
      else()
          find_program(GRPC_OBJECTIVE_C_PLUGIN_PROGRAM
              NAMES grpc_objective_c_plugin
              PATHS "${CMAKE_CURRENT_LIST_DIR}/../../../bin/"
              NO_DEFAULT_PATH
          )
      endif()
      # TODO: In conan v2 with CMakeToolchain, can be replaced by:
      # find_program(GRPC_OBJECTIVE_C_PLUGIN_PROGRAM NAMES grpc_objective_c_plugin))
      # # Nice enough to handle grpc not in build_requires for native build
      # if(NOT GRPC_OBJECTIVE_C_PLUGIN_PROGRAM AND NOT CMAKE_CROSSCOMPILING)
      #     find_program(GRPC_OBJECTIVE_C_PLUGIN_PROGRAM
      #         NAMES grpc_objective_c_plugin
      #         PATHS "${CMAKE_CURRENT_LIST_DIR}/../../../bin/"
      #         NO_DEFAULT_PATH
      #     )
      # endif()

      if(GRPC_OBJECTIVE_C_PLUGIN_PROGRAM)
          get_filename_component(GRPC_OBJECTIVE_C_PLUGIN_PROGRAM "${GRPC_OBJECTIVE_C_PLUGIN_PROGRAM}" ABSOLUTE)
          add_executable(gRPC::grpc_objective_c_plugin IMPORTED)
          set_property(TARGET gRPC::grpc_objective_c_plugin PROPERTY IMPORTED_LOCATION ${GRPC_OBJECTIVE_C_PLUGIN_PROGRAM})
      endif()
  endif()

  ```#### lib/cmake/conan_trick/grpc_php_plugin.cmake
  ```cmake
  if(NOT TARGET gRPC::grpc_php_plugin)
      if(CMAKE_CROSSCOMPILING)
          find_program(GRPC_PHP_PLUGIN_PROGRAM
              NAMES grpc_php_plugin
              PATHS ENV PATH
              NO_DEFAULT_PATH
          )
      else()
          find_program(GRPC_PHP_PLUGIN_PROGRAM
              NAMES grpc_php_plugin
              PATHS "${CMAKE_CURRENT_LIST_DIR}/../../../bin/"
              NO_DEFAULT_PATH
          )
      endif()
      # TODO: In conan v2 with CMakeToolchain, can be replaced by:
      # find_program(GRPC_PHP_PLUGIN_PROGRAM NAMES grpc_php_plugin))
      # # Nice enough to handle grpc not in build_requires for native build
      # if(NOT GRPC_PHP_PLUGIN_PROGRAM AND NOT CMAKE_CROSSCOMPILING)
      #     find_program(GRPC_PHP_PLUGIN_PROGRAM
      #         NAMES grpc_php_plugin
      #         PATHS "${CMAKE_CURRENT_LIST_DIR}/../../../bin/"
      #         NO_DEFAULT_PATH
      #     )
      # endif()

      if(GRPC_PHP_PLUGIN_PROGRAM)
          get_filename_component(GRPC_PHP_PLUGIN_PROGRAM "${GRPC_PHP_PLUGIN_PROGRAM}" ABSOLUTE)
          add_executable(gRPC::grpc_php_plugin IMPORTED)
          set_property(TARGET gRPC::grpc_php_plugin PROPERTY IMPORTED_LOCATION ${GRPC_PHP_PLUGIN_PROGRAM})
      endif()
  endif()

  ```#### lib/cmake/conan_trick/grpc_python_plugin.cmake
  ```cmake
  if(NOT TARGET gRPC::grpc_python_plugin)
      if(CMAKE_CROSSCOMPILING)
          find_program(GRPC_PYTHON_PLUGIN_PROGRAM
              NAMES grpc_python_plugin
              PATHS ENV PATH
              NO_DEFAULT_PATH
          )
      else()
          find_program(GRPC_PYTHON_PLUGIN_PROGRAM
              NAMES grpc_python_plugin
              PATHS "${CMAKE_CURRENT_LIST_DIR}/../../../bin/"
              NO_DEFAULT_PATH
          )
      endif()
      # TODO: In conan v2 with CMakeToolchain, can be replaced by:
      # find_program(GRPC_PYTHON_PLUGIN_PROGRAM NAMES grpc_python_plugin))
      # # Nice enough to handle grpc not in build_requires for native build
      # if(NOT GRPC_PYTHON_PLUGIN_PROGRAM AND NOT CMAKE_CROSSCOMPILING)
      #     find_program(GRPC_PYTHON_PLUGIN_PROGRAM
      #         NAMES grpc_python_plugin
      #         PATHS "${CMAKE_CURRENT_LIST_DIR}/../../../bin/"
      #         NO_DEFAULT_PATH
      #     )
      # endif()

      if(GRPC_PYTHON_PLUGIN_PROGRAM)
          get_filename_component(GRPC_PYTHON_PLUGIN_PROGRAM "${GRPC_PYTHON_PLUGIN_PROGRAM}" ABSOLUTE)
          add_executable(gRPC::grpc_python_plugin IMPORTED)
          set_property(TARGET gRPC::grpc_python_plugin PROPERTY IMPORTED_LOCATION ${GRPC_PYTHON_PLUGIN_PROGRAM})
      endif()
  endif()

  ```#### lib/cmake/conan_trick/grpc_ruby_plugin.cmake
  ```cmake
  if(NOT TARGET gRPC::grpc_ruby_plugin)
      if(CMAKE_CROSSCOMPILING)
          find_program(GRPC_RUBY_PLUGIN_PROGRAM
              NAMES grpc_ruby_plugin
              PATHS ENV PATH
              NO_DEFAULT_PATH
          )
      else()
          find_program(GRPC_RUBY_PLUGIN_PROGRAM
              NAMES grpc_ruby_plugin
              PATHS "${CMAKE_CURRENT_LIST_DIR}/../../../bin/"
              NO_DEFAULT_PATH
          )
      endif()
      # TODO: In conan v2 with CMakeToolchain, can be replaced by:
      # find_program(GRPC_RUBY_PLUGIN_PROGRAM NAMES grpc_ruby_plugin))
      # # Nice enough to handle grpc not in build_requires for native build
      # if(NOT GRPC_RUBY_PLUGIN_PROGRAM AND NOT CMAKE_CROSSCOMPILING)
      #     find_program(GRPC_RUBY_PLUGIN_PROGRAM
      #         NAMES grpc_ruby_plugin
      #         PATHS "${CMAKE_CURRENT_LIST_DIR}/../../../bin/"
      #         NO_DEFAULT_PATH
      #     )
      # endif()

      if(GRPC_RUBY_PLUGIN_PROGRAM)
          get_filename_component(GRPC_RUBY_PLUGIN_PROGRAM "${GRPC_RUBY_PLUGIN_PROGRAM}" ABSOLUTE)
          add_executable(gRPC::grpc_ruby_plugin IMPORTED)
          set_property(TARGET gRPC::grpc_ruby_plugin PROPERTY IMPORTED_LOCATION ${GRPC_RUBY_PLUGIN_PROGRAM})
      endif()
  endif()

  ```



<br>

## Using grpc with Visual Studio

<br>

### [Visual Studio Conan generators](https://docs.conan.io/en/latest/reference/conanfile/tools/microsoft.html)

<br>

* [MSBuildDeps](https://docs.conan.io/en/latest/reference/conanfile/tools/microsoft.html#msbuilddeps): generates the **conandeps.props** properties file with information about where the **grpc** library and its dependencies  ( [abseil](https://conan.io/center/abseil),  [c-ares](https://conan.io/center/c-ares),  [openssl](https://conan.io/center/openssl),  [re2](https://conan.io/center/re2),  [zlib](https://conan.io/center/zlib),  [protobuf](https://conan.io/center/protobuf),  [googleapis](https://conan.io/center/googleapis),  [grpc-proto](https://conan.io/center/grpc-proto)) are installed together with other information like version, flags, and directory data or configuration.

* [MSBuildToolchain](https://docs.conan.io/en/latest/reference/conanfile/tools/microsoft.html#msbuildtoolchain): Generates the **conantoolchain.props** properties file with the current package configuration, settings, and options.

Declare these generators in your **conanfile.txt** along with your **grpc** dependency like:

```ini
[requires]
grpc/1.50.1

[generators]
MSBuildDeps
MSBuildToolchain
```

<br>

Please, [check the Conan documentation](https://docs.conan.io/en/latest/reference/conanfile/tools/microsoft.html) for more detailed information on how to add these properties files to your Visual Studio projects.



<br>

## Using grpc with Autotools and pkg-config

<br>

### [Autotools Conan generators](https://docs.conan.io/en/latest/reference/conanfile/tools/gnu.html)

<br>

* [AutotoolsToolchain](https://docs.conan.io/en/latest/reference/conanfile/tools/gnu/autotoolstoolchain.html): generates the **conanautotoolstoolchain.sh/bat** script translating information from the current package configuration, settings, and options setting some enviroment variables for Autotools like: ``CPPFLAGS``, ``CXXFLAGS``, ``CFLAGS`` and ``LDFLAGS``. It will also generate a ``deactivate_conanautotoolstoolchain.sh/bat`` so you can restore your environment.

* [AutotoolsDeps](https://docs.conan.io/en/latest/reference/conanfile/tools/gnu/autotoolsdeps.html): generates the **conanautotoolsdeps.sh/bat** script with information about where the **grpc** library and its dependencies  ( [abseil](https://conan.io/center/abseil),  [c-ares](https://conan.io/center/c-ares),  [openssl](https://conan.io/center/openssl),  [re2](https://conan.io/center/re2),  [zlib](https://conan.io/center/zlib),  [protobuf](https://conan.io/center/protobuf),  [googleapis](https://conan.io/center/googleapis),  [grpc-proto](https://conan.io/center/grpc-proto)) are installed together with other information like version, flags, and directory data or configuration. This is done setting some enviroment variables for Autotools like: ``LIBS``, ``CPPFLAGS``,``CXXFLAGS``, ``CFLAGS`` and ``LDFLAGS``.  It will also generate a ``deactivate_conanautotoolsdeps.sh/bat`` so you can restore your environment.

Declare these generators in your **conanfile.txt** along with your **grpc** dependency like:

```ini
[requires]
grpc/1.50.1

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

* [PkgConfigDeps](https://docs.conan.io/en/latest/reference/conanfile/tools/gnu/pkgconfigdeps.html): generates the **grpc.pc** file (and the ones corresponding to **grpc** dependencies) with information about the dependencies that can be later used by the **pkg-config** tool pkg-config to collect data about the libraries Conan installed.

<br>

You can use this generator instead of the **AutotoolsDeps** one:

```ini
[requires]
grpc/1.50.1

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

$ export CPPFLAGS="$CPPFLAGS $(pkg-config --cflags grpc)"
$ export LIBS="$LIBS $(pkg-config --libs-only-l grpc)"
$ export LDFLAGS="$LDFLAGS $(pkg-config --libs-only-L --libs-only-other grpc)"

$ ./configure
$ make

# restore the environment after the build is completed
$ source deactivate_conanautotoolstoolchain.sh
```



<br>

As the grpc Conan package defines components you can use them to link only that desired part of the library in your project.  To check all the available components for **grpc** Conan package, and the corresponding *.pc* files names, please check the dedicated section at the end of this document.


<br>

## Other build systems

<br>

Please, [check the Conan documentation](https://docs.conan.io/en/latest/reference/conanfile/tools.html) for other integrations besides the ones listed in this document.





<br>

## Declared components for grpc

<br>

These are all the declared components for the **grpc** Conan package:
* Component **address_sorting**:
  * CMake target name: ``gRPC::address_sorting``
  * pkg-config *.pc* file: **address_sorting.pc**
  * Links to libraries: **address_sorting**
  * Systems libs: **m**, **pthread**
* Component **gpr**:
  * CMake target name: ``gRPC::gpr``
  * pkg-config *.pc* file: **gpr.pc**
  * Requires other components: **upb**, **abseil::absl_base**, **abseil::absl_memory**, **abseil::absl_status**, **abseil::absl_str_format**, **abseil::absl_strings**, **abseil::absl_synchronization**, **abseil::absl_time**, **abseil::absl_optional**
  * Links to libraries: **gpr**
  * Systems libs: **m**, **pthread**
* Component **_grpc**:
  * CMake target name: ``gRPC::grpc``
  * pkg-config *.pc* file: **grpc.pc**
  * Requires other components: **address_sorting**, **gpr**, **upb**, **abseil::absl_bind_front**, **abseil::absl_flat_hash_map**, **abseil::absl_inlined_vector**, **abseil::absl_statusor**, **abseil::absl_random_random**, **c-ares::cares**, **openssl::crypto**, **openssl::ssl**, **re2::re2**, **zlib::zlib**
  * Links to libraries: **grpc**
  * Systems libs: **m**, **pthread**
* Component **grpc++**:
  * CMake target name: ``gRPC::grpc++``
  * pkg-config *.pc* file: **grpc++.pc**
  * Requires other components: **_grpc**, **protobuf::libprotobuf**
  * Links to libraries: **grpc++**
  * Systems libs: **m**, **pthread**
* Component **grpc++_alts**:
  * CMake target name: ``gRPC::grpc++_alts``
  * pkg-config *.pc* file: **grpc++_alts.pc**
  * Requires other components: **grpc++**, **protobuf::libprotobuf**
  * Links to libraries: **grpc++_alts**
  * Systems libs: **m**, **pthread**
* Component **grpc++_error_details**:
  * CMake target name: ``gRPC::grpc++_error_details``
  * pkg-config *.pc* file: **grpc++_error_details.pc**
  * Requires other components: **grpc++**, **protobuf::libprotobuf**
  * Links to libraries: **grpc++_error_details**
  * Systems libs: **m**, **pthread**
* Component **upb**:
  * CMake target name: ``gRPC::upb``
  * pkg-config *.pc* file: **upb.pc**
  * Links to libraries: **upb**
  * Systems libs: **m**, **pthread**
* Component **grpc_plugin_support**:
  * CMake target name: ``gRPC::grpc_plugin_support``
  * pkg-config *.pc* file: **grpc_plugin_support.pc**
  * Requires other components: **protobuf::libprotoc**, **protobuf::libprotobuf**
  * Links to libraries: **grpc_plugin_support**
  * Systems libs: **m**, **pthread**
* Component **grpc_unsecure**:
  * CMake target name: ``gRPC::grpc_unsecure``
  * pkg-config *.pc* file: **grpc_unsecure.pc**
  * Requires other components: **address_sorting**, **gpr**, **upb**, **abseil::absl_flat_hash_map**, **abseil::absl_inlined_vector**, **abseil::absl_statusor**, **c-ares::cares**, **re2::re2**, **zlib::zlib**, **abseil::absl_random_random**
  * Links to libraries: **grpc_unsecure**
  * Systems libs: **m**, **pthread**
* Component **grpc++_unsecure**:
  * CMake target name: ``gRPC::grpc++_unsecure``
  * pkg-config *.pc* file: **grpc++_unsecure.pc**
  * Requires other components: **grpc_unsecure**, **protobuf::libprotobuf**
  * Links to libraries: **grpc++_unsecure**
  * Systems libs: **m**, **pthread**
* Component **grpc++_reflection**:
  * CMake target name: ``gRPC::grpc++_reflection``
  * pkg-config *.pc* file: **grpc++_reflection.pc**
  * Requires other components: **grpc++**, **protobuf::libprotobuf**, **grpc-proto::grpc-proto**, **googleapis::googleapis**
  * Links to libraries: **grpc++_reflection**
  * Systems libs: **m**, **pthread**
* Component **grpcpp_channelz**:
  * CMake target name: ``gRPC::grpcpp_channelz``
  * pkg-config *.pc* file: **grpcpp_channelz.pc**
  * Requires other components: **grpc++**, **protobuf::libprotobuf**, **grpc-proto::grpc-proto**, **googleapis::googleapis**
  * Links to libraries: **grpcpp_channelz**
  * Systems libs: **m**, **pthread**
* Component **grpc_execs**:
  * CMake target name: ``grpc::grpc_execs``
  * pkg-config *.pc* file: **grpc-grpc_execs.pc**


<br>

## Exposed header files for grpc

<br>

```cpp
#include <grpc/slice.h>
#include <grpc/byte_buffer_reader.h>
#include <grpc/grpc.h>
#include <grpc/load_reporting.h>
#include <grpc/grpc_security.h>
#include <grpc/grpc_security_constants.h>
#include <grpc/compression.h>
#include <grpc/fork.h>
#include <grpc/byte_buffer.h>
#include <grpc/census.h>
#include <grpc/status.h>
#include <grpc/slice_buffer.h>
#include <grpc/grpc_posix.h>
#include <grpc/support/atm_windows.h>
#include <grpc/support/sync_posix.h>
#include <grpc/support/string_util.h>
#include <grpc/support/log.h>
#include <grpc/support/sync_abseil.h>
#include <grpc/support/cpu.h>
#include <grpc/support/log_windows.h>
#include <grpc/support/time.h>
#include <grpc/support/port_platform.h>
#include <grpc/support/atm.h>
#include <grpc/support/sync.h>
#include <grpc/support/thd_id.h>
#include <grpc/support/atm_gcc_sync.h>
#include <grpc/support/sync_windows.h>
#include <grpc/support/workaround_list.h>
#include <grpc/support/sync_generic.h>
#include <grpc/support/atm_gcc_atomic.h>
#include <grpc/support/sync_custom.h>
#include <grpc/support/alloc.h>
#include <grpc/impl/codegen/atm_windows.h>
#include <grpc/impl/codegen/slice.h>
#include <grpc/impl/codegen/sync_posix.h>
#include <grpc/impl/codegen/log.h>
#include <grpc/impl/codegen/sync_abseil.h>
#include <grpc/impl/codegen/gpr_slice.h>
#include <grpc/impl/codegen/port_platform.h>
#include <grpc/impl/codegen/atm.h>
#include <grpc/impl/codegen/byte_buffer_reader.h>
#include <grpc/impl/codegen/sync.h>
#include <grpc/impl/codegen/atm_gcc_sync.h>
#include <grpc/impl/codegen/sync_windows.h>
#include <grpc/impl/codegen/sync_generic.h>
#include <grpc/impl/codegen/connectivity_state.h>
#include <grpc/impl/codegen/fork.h>
#include <grpc/impl/codegen/grpc_types.h>
#include <grpc/impl/codegen/atm_gcc_atomic.h>
#include <grpc/impl/codegen/sync_custom.h>
#include <grpc/impl/codegen/byte_buffer.h>
#include <grpc/impl/codegen/compression_types.h>
#include <grpc/impl/codegen/gpr_types.h>
#include <grpc/impl/codegen/status.h>
#include <grpc/impl/codegen/propagation_bits.h>
#include <grpc/event_engine/slice.h>
#include <grpc/event_engine/endpoint_config.h>
#include <grpc/event_engine/event_engine.h>
#include <grpc/event_engine/port.h>
#include <grpc/event_engine/memory_request.h>
#include <grpc/event_engine/memory_allocator.h>
#include <grpc/event_engine/slice_buffer.h>
#include <grpc/event_engine/internal/memory_allocator_impl.h>
#include <grpc++/grpc++.h>
#include <grpc++/create_channel.h>
#include <grpc++/resource_quota.h>
#include <grpc++/create_channel_posix.h>
#include <grpc++/alarm.h>
#include <grpc++/channel.h>
#include <grpc++/client_context.h>
#include <grpc++/health_check_service_interface.h>
#include <grpc++/server_context.h>
#include <grpc++/completion_queue.h>
#include <grpc++/server_builder.h>
#include <grpc++/server.h>
#include <grpc++/server_posix.h>
#include <grpc++/security/credentials.h>
#include <grpc++/security/auth_metadata_processor.h>
#include <grpc++/security/server_credentials.h>
#include <grpc++/security/auth_context.h>
#include <grpc++/support/async_unary_call.h>
#include <grpc++/support/slice.h>
#include <grpc++/support/config.h>
#include <grpc++/support/status_code_enum.h>
#include <grpc++/support/channel_arguments.h>
#include <grpc++/support/time.h>
#include <grpc++/support/stub_options.h>
#include <grpc++/support/async_stream.h>
#include <grpc++/support/string_ref.h>
#include <grpc++/support/sync_stream.h>
#include <grpc++/support/byte_buffer.h>
#include <grpc++/support/error_details.h>
#include <grpc++/support/status.h>
#include <grpc++/generic/async_generic_service.h>
#include <grpc++/generic/generic_stub.h>
#include <grpc++/ext/proto_server_reflection_plugin.h>
#include <grpc++/ext/health_check_service_server_builder_option.h>
#include <grpc++/impl/server_builder_option.h>
#include <grpc++/impl/server_builder_plugin.h>
#include <grpc++/impl/call.h>
#include <grpc++/impl/server_initializer.h>
#include <grpc++/impl/channel_argument_option.h>
#include <grpc++/impl/service_type.h>
#include <grpc++/impl/method_handler_impl.h>
#include <grpc++/impl/rpc_method.h>
#include <grpc++/impl/grpc_library.h>
#include <grpc++/impl/serialization_traits.h>
#include <grpc++/impl/rpc_service_method.h>
#include <grpc++/impl/client_unary_call.h>
#include <grpc++/impl/codegen/async_unary_call.h>
#include <grpc++/impl/codegen/slice.h>
#include <grpc++/impl/codegen/config.h>
#include <grpc++/impl/codegen/status_code_enum.h>
#include <grpc++/impl/codegen/core_codegen_interface.h>
#include <grpc++/impl/codegen/completion_queue_tag.h>
#include <grpc++/impl/codegen/time.h>
#include <grpc++/impl/codegen/proto_utils.h>
#include <grpc++/impl/codegen/call.h>
#include <grpc++/impl/codegen/core_codegen.h>
#include <grpc++/impl/codegen/metadata_map.h>
#include <grpc++/impl/codegen/config_protobuf.h>
#include <grpc++/impl/codegen/client_context.h>
#include <grpc++/impl/codegen/channel_interface.h>
#include <grpc++/impl/codegen/stub_options.h>
#include <grpc++/impl/codegen/call_hook.h>
#include <grpc++/impl/codegen/service_type.h>
#include <grpc++/impl/codegen/server_interface.h>
#include <grpc++/impl/codegen/method_handler_impl.h>
#include <grpc++/impl/codegen/rpc_method.h>
#include <grpc++/impl/codegen/async_stream.h>
#include <grpc++/impl/codegen/create_auth_context.h>
#include <grpc++/impl/codegen/server_context.h>
#include <grpc++/impl/codegen/string_ref.h>
#include <grpc++/impl/codegen/sync_stream.h>
#include <grpc++/impl/codegen/byte_buffer.h>
#include <grpc++/impl/codegen/grpc_library.h>
#include <grpc++/impl/codegen/serialization_traits.h>
#include <grpc++/impl/codegen/completion_queue.h>
#include <grpc++/impl/codegen/status.h>
#include <grpc++/impl/codegen/rpc_service_method.h>
#include <grpc++/impl/codegen/client_unary_call.h>
#include <grpc++/impl/codegen/security/auth_context.h>
#include <grpcpp/xds_server_builder.h>
#include <grpcpp/create_channel.h>
#include <grpcpp/resource_quota.h>
#include <grpcpp/grpcpp.h>
#include <grpcpp/create_channel_posix.h>
#include <grpcpp/alarm.h>
#include <grpcpp/channel.h>
#include <grpcpp/client_context.h>
#include <grpcpp/health_check_service_interface.h>
#include <grpcpp/create_channel_binder.h>
#include <grpcpp/server_context.h>
#include <grpcpp/completion_queue.h>
#include <grpcpp/server_builder.h>
#include <grpcpp/server.h>
#include <grpcpp/server_posix.h>
#include <grpcpp/security/credentials.h>
#include <grpcpp/security/tls_certificate_verifier.h>
#include <grpcpp/security/tls_credentials_options.h>
#include <grpcpp/security/auth_metadata_processor.h>
#include <grpcpp/security/server_credentials.h>
#include <grpcpp/security/binder_security_policy.h>
#include <grpcpp/security/tls_certificate_provider.h>
#include <grpcpp/security/binder_credentials.h>
#include <grpcpp/security/auth_context.h>
#include <grpcpp/security/authorization_policy_provider.h>
#include <grpcpp/security/alts_util.h>
#include <grpcpp/security/alts_context.h>
#include <grpcpp/support/async_unary_call.h>
#include <grpcpp/support/slice.h>
#include <grpcpp/support/config.h>
#include <grpcpp/support/message_allocator.h>
#include <grpcpp/support/validate_service_config.h>
#include <grpcpp/support/client_interceptor.h>
#include <grpcpp/support/server_interceptor.h>
#include <grpcpp/support/status_code_enum.h>
#include <grpcpp/support/channel_arguments.h>
#include <grpcpp/support/time.h>
#include <grpcpp/support/proto_buffer_reader.h>
#include <grpcpp/support/proto_buffer_writer.h>
#include <grpcpp/support/stub_options.h>
#include <grpcpp/support/interceptor.h>
#include <grpcpp/support/async_stream.h>
#include <grpcpp/support/string_ref.h>
#include <grpcpp/support/sync_stream.h>
#include <grpcpp/support/byte_buffer.h>
#include <grpcpp/support/client_callback.h>
#include <grpcpp/support/error_details.h>
#include <grpcpp/support/status.h>
#include <grpcpp/support/server_callback.h>
#include <grpcpp/support/method_handler.h>
#include <grpcpp/generic/async_generic_service.h>
#include <grpcpp/generic/generic_stub.h>
#include <grpcpp/ext/proto_server_reflection_plugin.h>
#include <grpcpp/ext/channelz_service_plugin.h>
#include <grpcpp/ext/call_metric_recorder.h>
#include <grpcpp/ext/health_check_service_server_builder_option.h>
#include <grpcpp/impl/call_op_set_interface.h>
#include <grpcpp/impl/server_builder_option.h>
#include <grpcpp/impl/server_builder_plugin.h>
#include <grpcpp/impl/call.h>
#include <grpcpp/impl/server_initializer.h>
#include <grpcpp/impl/channel_argument_option.h>
#include <grpcpp/impl/call_hook.h>
#include <grpcpp/impl/service_type.h>
#include <grpcpp/impl/method_handler_impl.h>
#include <grpcpp/impl/rpc_method.h>
#include <grpcpp/impl/grpc_library.h>
#include <grpcpp/impl/serialization_traits.h>
#include <grpcpp/impl/rpc_service_method.h>
#include <grpcpp/impl/client_unary_call.h>
#include <grpcpp/impl/codegen/async_unary_call.h>
#include <grpcpp/impl/codegen/server_callback_handlers.h>
#include <grpcpp/impl/codegen/slice.h>
#include <grpcpp/impl/codegen/call_op_set.h>
#include <grpcpp/impl/codegen/call_op_set_interface.h>
#include <grpcpp/impl/codegen/config.h>
#include <grpcpp/impl/codegen/async_generic_service.h>
#include <grpcpp/impl/codegen/message_allocator.h>
#include <grpcpp/impl/codegen/delegating_channel.h>
#include <grpcpp/impl/codegen/client_interceptor.h>
#include <grpcpp/impl/codegen/server_interceptor.h>
#include <grpcpp/impl/codegen/status_code_enum.h>
#include <grpcpp/impl/codegen/core_codegen_interface.h>
#include <grpcpp/impl/codegen/completion_queue_tag.h>
#include <grpcpp/impl/codegen/time.h>
#include <grpcpp/impl/codegen/sync.h>
#include <grpcpp/impl/codegen/proto_utils.h>
#include <grpcpp/impl/codegen/call.h>
#include <grpcpp/impl/codegen/intercepted_channel.h>
#include <grpcpp/impl/codegen/core_codegen.h>
#include <grpcpp/impl/codegen/metadata_map.h>
#include <grpcpp/impl/codegen/config_protobuf.h>
#include <grpcpp/impl/codegen/client_context.h>
#include <grpcpp/impl/codegen/proto_buffer_reader.h>
#include <grpcpp/impl/codegen/proto_buffer_writer.h>
#include <grpcpp/impl/codegen/channel_interface.h>
#include <grpcpp/impl/codegen/stub_options.h>
#include <grpcpp/impl/codegen/call_hook.h>
#include <grpcpp/impl/codegen/service_type.h>
#include <grpcpp/impl/codegen/server_interface.h>
#include <grpcpp/impl/codegen/method_handler_impl.h>
#include <grpcpp/impl/codegen/interceptor.h>
#include <grpcpp/impl/codegen/rpc_method.h>
#include <grpcpp/impl/codegen/async_stream.h>
#include <grpcpp/impl/codegen/create_auth_context.h>
#include <grpcpp/impl/codegen/server_context.h>
#include <grpcpp/impl/codegen/string_ref.h>
#include <grpcpp/impl/codegen/sync_stream.h>
#include <grpcpp/impl/codegen/byte_buffer.h>
#include <grpcpp/impl/codegen/grpc_library.h>
#include <grpcpp/impl/codegen/interceptor_common.h>
#include <grpcpp/impl/codegen/client_callback.h>
#include <grpcpp/impl/codegen/serialization_traits.h>
#include <grpcpp/impl/codegen/completion_queue.h>
#include <grpcpp/impl/codegen/status.h>
#include <grpcpp/impl/codegen/callback_common.h>
#include <grpcpp/impl/codegen/rpc_service_method.h>
#include <grpcpp/impl/codegen/server_callback.h>
#include <grpcpp/impl/codegen/client_unary_call.h>
#include <grpcpp/impl/codegen/method_handler.h>
#include <grpcpp/impl/codegen/security/auth_context.h>
```

<br>


---
---
Conan **1.58.0**. JFrog LTD. [https://conan.io](https://conan.io). Autogenerated 2023-02-05 17:31:47.
