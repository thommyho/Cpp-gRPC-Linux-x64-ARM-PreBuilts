


# re2/20220601

---



<br>

## Using the re2 Conan Package

<br>

Conan integrates with different build systems. You can declare which build system you want your project to use setting in the **[generators]** section of the [conanfile.txt](https://docs.conan.io/en/latest/reference/conanfile_txt.html#generators) or using the **generators** attribute in the [conanfile.py](https://docs.conan.io/en/latest/reference/conanfile/attributes.html#generators). Here, there is some basic information you can use to integrate **re2** in your own project. For more detailed information, please [check the Conan documentation](https://docs.conan.io/en/latest/getting_started.html).



<br>

## Using re2 with CMake

<br>

### [Conan CMake generators](https://docs.conan.io/en/latest/reference/conanfile/tools/cmake.html)

<br>

* [CMakeDeps](https://docs.conan.io/en/latest/reference/conanfile/tools/cmake/cmakedeps.html): generates information about where the **re2** library and its dependencies  are installed together with other information like version, flags, and directory data or configuration. CMake will use this files when you invoke ``find_package()`` in your *CMakeLists.txt*.

* [CMakeToolchain](https://docs.conan.io/en/latest/reference/conanfile/tools/cmake/cmaketoolchain.html): generates a CMake toolchain file that you can later invoke with CMake in the command line using `-DCMAKE_TOOLCHAIN_FILE=conantoolchain.cmake`.

Declare these generators in your **conanfile.txt** along with your **re2** dependency like:

```ini
[requires]
re2/20220601

[generators]
CMakeDeps
CMakeToolchain
```

<br>

To use **re2** in a simple CMake project with this structure:

```shell
.
|-- CMakeLists.txt
|-- conanfile.txt
`-- src
    `-- main..cpp
```

<br>

Your **CMakeLists.txt** could look similar to this, using the global **re2::re2** CMake's target:

```cmake
cmake_minimum_required(VERSION 3.15)
project(re2_project CXX)

find_package(re2)

add_executable(${PROJECT_NAME} src/main.cpp)

# Use the global target
target_link_libraries(${PROJECT_NAME} re2::re2)
```

<br>

To install **re2/20220601**, its dependencies and build your project, you just have to do:

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

## Using re2 with Visual Studio

<br>

### [Visual Studio Conan generators](https://docs.conan.io/en/latest/reference/conanfile/tools/microsoft.html)

<br>

* [MSBuildDeps](https://docs.conan.io/en/latest/reference/conanfile/tools/microsoft.html#msbuilddeps): generates the **conandeps.props** properties file with information about where the **re2** library and its dependencies  are installed together with other information like version, flags, and directory data or configuration.

* [MSBuildToolchain](https://docs.conan.io/en/latest/reference/conanfile/tools/microsoft.html#msbuildtoolchain): Generates the **conantoolchain.props** properties file with the current package configuration, settings, and options.

Declare these generators in your **conanfile.txt** along with your **re2** dependency like:

```ini
[requires]
re2/20220601

[generators]
MSBuildDeps
MSBuildToolchain
```

<br>

Please, [check the Conan documentation](https://docs.conan.io/en/latest/reference/conanfile/tools/microsoft.html) for more detailed information on how to add these properties files to your Visual Studio projects.



<br>

## Using re2 with Autotools and pkg-config

<br>

### [Autotools Conan generators](https://docs.conan.io/en/latest/reference/conanfile/tools/gnu.html)

<br>

* [AutotoolsToolchain](https://docs.conan.io/en/latest/reference/conanfile/tools/gnu/autotoolstoolchain.html): generates the **conanautotoolstoolchain.sh/bat** script translating information from the current package configuration, settings, and options setting some enviroment variables for Autotools like: ``CPPFLAGS``, ``CXXFLAGS``, ``CFLAGS`` and ``LDFLAGS``. It will also generate a ``deactivate_conanautotoolstoolchain.sh/bat`` so you can restore your environment.

* [AutotoolsDeps](https://docs.conan.io/en/latest/reference/conanfile/tools/gnu/autotoolsdeps.html): generates the **conanautotoolsdeps.sh/bat** script with information about where the **re2** library and its dependencies  are installed together with other information like version, flags, and directory data or configuration. This is done setting some enviroment variables for Autotools like: ``LIBS``, ``CPPFLAGS``,``CXXFLAGS``, ``CFLAGS`` and ``LDFLAGS``.  It will also generate a ``deactivate_conanautotoolsdeps.sh/bat`` so you can restore your environment.

Declare these generators in your **conanfile.txt** along with your **re2** dependency like:

```ini
[requires]
re2/20220601

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

* [PkgConfigDeps](https://docs.conan.io/en/latest/reference/conanfile/tools/gnu/pkgconfigdeps.html): generates the **re2.pc** file (and the ones corresponding to **re2** dependencies) with information about the dependencies that can be later used by the **pkg-config** tool pkg-config to collect data about the libraries Conan installed.

<br>

You can use this generator instead of the **AutotoolsDeps** one:

```ini
[requires]
re2/20220601

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

$ export CPPFLAGS="$CPPFLAGS $(pkg-config --cflags re2)"
$ export LIBS="$LIBS $(pkg-config --libs-only-l re2)"
$ export LDFLAGS="$LDFLAGS $(pkg-config --libs-only-L --libs-only-other re2)"

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

## Exposed header files for re2

<br>

```cpp
#include <re2/filtered_re2.h>
#include <re2/set.h>
#include <re2/stringpiece.h>
#include <re2/re2.h>
```

<br>


---
---
Conan **1.58.0**. JFrog LTD. [https://conan.io](https://conan.io). Autogenerated 2023-02-05 17:37:10.