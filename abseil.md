


# abseil/20220623.0

---



<br>

## Using the abseil Conan Package

<br>

Conan integrates with different build systems. You can declare which build system you want your project to use setting in the **[generators]** section of the [conanfile.txt](https://docs.conan.io/en/latest/reference/conanfile_txt.html#generators) or using the **generators** attribute in the [conanfile.py](https://docs.conan.io/en/latest/reference/conanfile/attributes.html#generators). Here, there is some basic information you can use to integrate **abseil** in your own project. For more detailed information, please [check the Conan documentation](https://docs.conan.io/en/latest/getting_started.html).



<br>

## Using abseil with CMake

<br>

### [Conan CMake generators](https://docs.conan.io/en/latest/reference/conanfile/tools/cmake.html)

<br>

* [CMakeDeps](https://docs.conan.io/en/latest/reference/conanfile/tools/cmake/cmakedeps.html): generates information about where the **abseil** library and its dependencies  are installed together with other information like version, flags, and directory data or configuration. CMake will use this files when you invoke ``find_package()`` in your *CMakeLists.txt*.

* [CMakeToolchain](https://docs.conan.io/en/latest/reference/conanfile/tools/cmake/cmaketoolchain.html): generates a CMake toolchain file that you can later invoke with CMake in the command line using `-DCMAKE_TOOLCHAIN_FILE=conantoolchain.cmake`.

Declare these generators in your **conanfile.txt** along with your **abseil** dependency like:

```ini
[requires]
abseil/20220623.0

[generators]
CMakeDeps
CMakeToolchain
```

<br>

To use **abseil** in a simple CMake project with this structure:

```shell
.
|-- CMakeLists.txt
|-- conanfile.txt
`-- src
    `-- main..cpp
```

<br>

Your **CMakeLists.txt** could look similar to this, using the global **abseil::abseil** CMake's target:

```cmake
cmake_minimum_required(VERSION 3.15)
project(abseil_project CXX)

find_package(absl)

add_executable(${PROJECT_NAME} src/main.cpp)

# Use the global target
target_link_libraries(${PROJECT_NAME} abseil::abseil)
```

<br>

To install **abseil/20220623.0**, its dependencies and build your project, you just have to do:

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



As the abseil Conan package defines components, you can link only the desired parts of the library in your project. For example, linking only with the abseil **absl_atomic_hook** component, through the **absl::atomic_hook** target.

```cmake
...
# Link just to abseil absl_atomic_hook component
target_link_libraries(${PROJECT_NAME} absl::atomic_hook)
```

<br>

To check all the available components for **abseil** Conan package, please check the dedicated section at the end of this document.




<br>

### Declared CMake build modules

<br>

#### lib/cmake/conan_trick/cxx_std.cmake
  ```cmake
  target_compile_features(absl::atomic_hook INTERFACE cxx_std_11)
  target_compile_features(absl::errno_saver INTERFACE cxx_std_11)
  target_compile_features(absl::log_severity INTERFACE cxx_std_11)
  target_compile_features(absl::raw_logging_internal INTERFACE cxx_std_11)
  target_compile_features(absl::spinlock_wait INTERFACE cxx_std_11)
  target_compile_features(absl::config INTERFACE cxx_std_11)
  target_compile_features(absl::dynamic_annotations INTERFACE cxx_std_11)
  target_compile_features(absl::core_headers INTERFACE cxx_std_11)
  target_compile_features(absl::malloc_internal INTERFACE cxx_std_11)
  target_compile_features(absl::base_internal INTERFACE cxx_std_11)
  target_compile_features(absl::base INTERFACE cxx_std_11)
  target_compile_features(absl::throw_delegate INTERFACE cxx_std_11)
  target_compile_features(absl::pretty_function INTERFACE cxx_std_11)
  target_compile_features(absl::endian INTERFACE cxx_std_11)
  target_compile_features(absl::scoped_set_env INTERFACE cxx_std_11)
  target_compile_features(absl::strerror INTERFACE cxx_std_11)
  target_compile_features(absl::fast_type_id INTERFACE cxx_std_11)
  target_compile_features(absl::prefetch INTERFACE cxx_std_11)
  target_compile_features(absl::algorithm INTERFACE cxx_std_11)
  target_compile_features(absl::algorithm_container INTERFACE cxx_std_11)
  target_compile_features(absl::cleanup_internal INTERFACE cxx_std_11)
  target_compile_features(absl::cleanup INTERFACE cxx_std_11)
  target_compile_features(absl::btree INTERFACE cxx_std_11)
  target_compile_features(absl::compressed_tuple INTERFACE cxx_std_11)
  target_compile_features(absl::fixed_array INTERFACE cxx_std_11)
  target_compile_features(absl::inlined_vector_internal INTERFACE cxx_std_11)
  target_compile_features(absl::inlined_vector INTERFACE cxx_std_11)
  target_compile_features(absl::counting_allocator INTERFACE cxx_std_11)
  target_compile_features(absl::flat_hash_map INTERFACE cxx_std_11)
  target_compile_features(absl::flat_hash_set INTERFACE cxx_std_11)
  target_compile_features(absl::node_hash_map INTERFACE cxx_std_11)
  target_compile_features(absl::node_hash_set INTERFACE cxx_std_11)
  target_compile_features(absl::container_memory INTERFACE cxx_std_11)
  target_compile_features(absl::hash_function_defaults INTERFACE cxx_std_11)
  target_compile_features(absl::hash_policy_traits INTERFACE cxx_std_11)
  target_compile_features(absl::hashtablez_sampler INTERFACE cxx_std_11)
  target_compile_features(absl::hashtable_debug INTERFACE cxx_std_11)
  target_compile_features(absl::hashtable_debug_hooks INTERFACE cxx_std_11)
  target_compile_features(absl::node_slot_policy INTERFACE cxx_std_11)
  target_compile_features(absl::raw_hash_map INTERFACE cxx_std_11)
  target_compile_features(absl::container_common INTERFACE cxx_std_11)
  target_compile_features(absl::raw_hash_set INTERFACE cxx_std_11)
  target_compile_features(absl::layout INTERFACE cxx_std_11)
  target_compile_features(absl::stacktrace INTERFACE cxx_std_11)
  target_compile_features(absl::symbolize INTERFACE cxx_std_11)
  target_compile_features(absl::examine_stack INTERFACE cxx_std_11)
  target_compile_features(absl::failure_signal_handler INTERFACE cxx_std_11)
  target_compile_features(absl::debugging_internal INTERFACE cxx_std_11)
  target_compile_features(absl::demangle_internal INTERFACE cxx_std_11)
  target_compile_features(absl::leak_check INTERFACE cxx_std_11)
  target_compile_features(absl::debugging INTERFACE cxx_std_11)
  target_compile_features(absl::flags_path_util INTERFACE cxx_std_11)
  target_compile_features(absl::flags_program_name INTERFACE cxx_std_11)
  target_compile_features(absl::flags_config INTERFACE cxx_std_11)
  target_compile_features(absl::flags_marshalling INTERFACE cxx_std_11)
  target_compile_features(absl::flags_commandlineflag_internal INTERFACE cxx_std_11)
  target_compile_features(absl::flags_commandlineflag INTERFACE cxx_std_11)
  target_compile_features(absl::flags_private_handle_accessor INTERFACE cxx_std_11)
  target_compile_features(absl::flags_reflection INTERFACE cxx_std_11)
  target_compile_features(absl::flags_internal INTERFACE cxx_std_11)
  target_compile_features(absl::flags INTERFACE cxx_std_11)
  target_compile_features(absl::flags_usage_internal INTERFACE cxx_std_11)
  target_compile_features(absl::flags_usage INTERFACE cxx_std_11)
  target_compile_features(absl::flags_parse INTERFACE cxx_std_11)
  target_compile_features(absl::any_invocable INTERFACE cxx_std_11)
  target_compile_features(absl::bind_front INTERFACE cxx_std_11)
  target_compile_features(absl::function_ref INTERFACE cxx_std_11)
  target_compile_features(absl::hash INTERFACE cxx_std_11)
  target_compile_features(absl::city INTERFACE cxx_std_11)
  target_compile_features(absl::low_level_hash INTERFACE cxx_std_11)
  target_compile_features(absl::memory INTERFACE cxx_std_11)
  target_compile_features(absl::type_traits INTERFACE cxx_std_11)
  target_compile_features(absl::meta INTERFACE cxx_std_11)
  target_compile_features(absl::bits INTERFACE cxx_std_11)
  target_compile_features(absl::int128 INTERFACE cxx_std_11)
  target_compile_features(absl::numeric INTERFACE cxx_std_11)
  target_compile_features(absl::numeric_representation INTERFACE cxx_std_11)
  target_compile_features(absl::sample_recorder INTERFACE cxx_std_11)
  target_compile_features(absl::exponential_biased INTERFACE cxx_std_11)
  target_compile_features(absl::periodic_sampler INTERFACE cxx_std_11)
  target_compile_features(absl::random_random INTERFACE cxx_std_11)
  target_compile_features(absl::random_bit_gen_ref INTERFACE cxx_std_11)
  target_compile_features(absl::random_internal_mock_helpers INTERFACE cxx_std_11)
  target_compile_features(absl::random_distributions INTERFACE cxx_std_11)
  target_compile_features(absl::random_seed_gen_exception INTERFACE cxx_std_11)
  target_compile_features(absl::random_seed_sequences INTERFACE cxx_std_11)
  target_compile_features(absl::random_internal_traits INTERFACE cxx_std_11)
  target_compile_features(absl::random_internal_distribution_caller INTERFACE cxx_std_11)
  target_compile_features(absl::random_internal_fast_uniform_bits INTERFACE cxx_std_11)
  target_compile_features(absl::random_internal_seed_material INTERFACE cxx_std_11)
  target_compile_features(absl::random_internal_pool_urbg INTERFACE cxx_std_11)
  target_compile_features(absl::random_internal_salted_seed_seq INTERFACE cxx_std_11)
  target_compile_features(absl::random_internal_iostream_state_saver INTERFACE cxx_std_11)
  target_compile_features(absl::random_internal_generate_real INTERFACE cxx_std_11)
  target_compile_features(absl::random_internal_wide_multiply INTERFACE cxx_std_11)
  target_compile_features(absl::random_internal_fastmath INTERFACE cxx_std_11)
  target_compile_features(absl::random_internal_nonsecure_base INTERFACE cxx_std_11)
  target_compile_features(absl::random_internal_pcg_engine INTERFACE cxx_std_11)
  target_compile_features(absl::random_internal_randen_engine INTERFACE cxx_std_11)
  target_compile_features(absl::random_internal_platform INTERFACE cxx_std_11)
  target_compile_features(absl::random_internal_randen INTERFACE cxx_std_11)
  target_compile_features(absl::random_internal_randen_slow INTERFACE cxx_std_11)
  target_compile_features(absl::random_internal_randen_hwaes INTERFACE cxx_std_11)
  target_compile_features(absl::random_internal_randen_hwaes_impl INTERFACE cxx_std_11)
  target_compile_features(absl::random_internal_distribution_test_util INTERFACE cxx_std_11)
  target_compile_features(absl::random_internal_uniform_helper INTERFACE cxx_std_11)
  target_compile_features(absl::status INTERFACE cxx_std_11)
  target_compile_features(absl::statusor INTERFACE cxx_std_11)
  target_compile_features(absl::strings INTERFACE cxx_std_11)
  target_compile_features(absl::strings_internal INTERFACE cxx_std_11)
  target_compile_features(absl::str_format INTERFACE cxx_std_11)
  target_compile_features(absl::str_format_internal INTERFACE cxx_std_11)
  target_compile_features(absl::cord_internal INTERFACE cxx_std_11)
  target_compile_features(absl::cordz_update_tracker INTERFACE cxx_std_11)
  target_compile_features(absl::cordz_functions INTERFACE cxx_std_11)
  target_compile_features(absl::cordz_statistics INTERFACE cxx_std_11)
  target_compile_features(absl::cordz_handle INTERFACE cxx_std_11)
  target_compile_features(absl::cordz_info INTERFACE cxx_std_11)
  target_compile_features(absl::cordz_sample_token INTERFACE cxx_std_11)
  target_compile_features(absl::cordz_update_scope INTERFACE cxx_std_11)
  target_compile_features(absl::cord INTERFACE cxx_std_11)
  target_compile_features(absl::graphcycles_internal INTERFACE cxx_std_11)
  target_compile_features(absl::kernel_timeout_internal INTERFACE cxx_std_11)
  target_compile_features(absl::synchronization INTERFACE cxx_std_11)
  target_compile_features(absl::time INTERFACE cxx_std_11)
  target_compile_features(absl::civil_time INTERFACE cxx_std_11)
  target_compile_features(absl::time_zone INTERFACE cxx_std_11)
  target_compile_features(absl::any INTERFACE cxx_std_11)
  target_compile_features(absl::bad_any_cast INTERFACE cxx_std_11)
  target_compile_features(absl::bad_any_cast_impl INTERFACE cxx_std_11)
  target_compile_features(absl::span INTERFACE cxx_std_11)
  target_compile_features(absl::optional INTERFACE cxx_std_11)
  target_compile_features(absl::bad_optional_access INTERFACE cxx_std_11)
  target_compile_features(absl::bad_variant_access INTERFACE cxx_std_11)
  target_compile_features(absl::variant INTERFACE cxx_std_11)
  target_compile_features(absl::compare INTERFACE cxx_std_11)
  target_compile_features(absl::utility INTERFACE cxx_std_11)

  ```



<br>

## Using abseil with Visual Studio

<br>

### [Visual Studio Conan generators](https://docs.conan.io/en/latest/reference/conanfile/tools/microsoft.html)

<br>

* [MSBuildDeps](https://docs.conan.io/en/latest/reference/conanfile/tools/microsoft.html#msbuilddeps): generates the **conandeps.props** properties file with information about where the **abseil** library and its dependencies  are installed together with other information like version, flags, and directory data or configuration.

* [MSBuildToolchain](https://docs.conan.io/en/latest/reference/conanfile/tools/microsoft.html#msbuildtoolchain): Generates the **conantoolchain.props** properties file with the current package configuration, settings, and options.

Declare these generators in your **conanfile.txt** along with your **abseil** dependency like:

```ini
[requires]
abseil/20220623.0

[generators]
MSBuildDeps
MSBuildToolchain
```

<br>

Please, [check the Conan documentation](https://docs.conan.io/en/latest/reference/conanfile/tools/microsoft.html) for more detailed information on how to add these properties files to your Visual Studio projects.



<br>

## Using abseil with Autotools and pkg-config

<br>

### [Autotools Conan generators](https://docs.conan.io/en/latest/reference/conanfile/tools/gnu.html)

<br>

* [AutotoolsToolchain](https://docs.conan.io/en/latest/reference/conanfile/tools/gnu/autotoolstoolchain.html): generates the **conanautotoolstoolchain.sh/bat** script translating information from the current package configuration, settings, and options setting some enviroment variables for Autotools like: ``CPPFLAGS``, ``CXXFLAGS``, ``CFLAGS`` and ``LDFLAGS``. It will also generate a ``deactivate_conanautotoolstoolchain.sh/bat`` so you can restore your environment.

* [AutotoolsDeps](https://docs.conan.io/en/latest/reference/conanfile/tools/gnu/autotoolsdeps.html): generates the **conanautotoolsdeps.sh/bat** script with information about where the **abseil** library and its dependencies  are installed together with other information like version, flags, and directory data or configuration. This is done setting some enviroment variables for Autotools like: ``LIBS``, ``CPPFLAGS``,``CXXFLAGS``, ``CFLAGS`` and ``LDFLAGS``.  It will also generate a ``deactivate_conanautotoolsdeps.sh/bat`` so you can restore your environment.

Declare these generators in your **conanfile.txt** along with your **abseil** dependency like:

```ini
[requires]
abseil/20220623.0

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

* [PkgConfigDeps](https://docs.conan.io/en/latest/reference/conanfile/tools/gnu/pkgconfigdeps.html): generates the **abseil.pc** file (and the ones corresponding to **abseil** dependencies) with information about the dependencies that can be later used by the **pkg-config** tool pkg-config to collect data about the libraries Conan installed.

<br>

You can use this generator instead of the **AutotoolsDeps** one:

```ini
[requires]
abseil/20220623.0

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

$ export CPPFLAGS="$CPPFLAGS $(pkg-config --cflags abseil)"
$ export LIBS="$LIBS $(pkg-config --libs-only-l abseil)"
$ export LDFLAGS="$LDFLAGS $(pkg-config --libs-only-L --libs-only-other abseil)"

$ ./configure
$ make

# restore the environment after the build is completed
$ source deactivate_conanautotoolstoolchain.sh
```



<br>

As the abseil Conan package defines components you can use them to link only that desired part of the library in your project.  To check all the available components for **abseil** Conan package, and the corresponding *.pc* files names, please check the dedicated section at the end of this document.


<br>

## Other build systems

<br>

Please, [check the Conan documentation](https://docs.conan.io/en/latest/reference/conanfile/tools.html) for other integrations besides the ones listed in this document.





<br>

## Declared components for abseil

<br>

These are all the declared components for the **abseil** Conan package:
* Component **absl_atomic_hook**:
  * CMake target name: ``absl::atomic_hook``
  * pkg-config *.pc* file: **absl_atomic_hook.pc**
  * Requires other components: **absl_config**, **absl_core_headers**
* Component **absl_errno_saver**:
  * CMake target name: ``absl::errno_saver``
  * pkg-config *.pc* file: **absl_errno_saver.pc**
  * Requires other components: **absl_config**
* Component **absl_log_severity**:
  * CMake target name: ``absl::log_severity``
  * pkg-config *.pc* file: **absl_log_severity.pc**
  * Requires other components: **absl_core_headers**
  * Links to libraries: **absl_log_severity**
* Component **absl_raw_logging_internal**:
  * CMake target name: ``absl::raw_logging_internal``
  * pkg-config *.pc* file: **absl_raw_logging_internal.pc**
  * Requires other components: **absl_atomic_hook**, **absl_config**, **absl_core_headers**, **absl_errno_saver**, **absl_log_severity**
  * Links to libraries: **absl_raw_logging_internal**
* Component **absl_spinlock_wait**:
  * CMake target name: ``absl::spinlock_wait``
  * pkg-config *.pc* file: **absl_spinlock_wait.pc**
  * Requires other components: **absl_base_internal**, **absl_core_headers**, **absl_errno_saver**
  * Links to libraries: **absl_spinlock_wait**
* Component **absl_config**:
  * CMake target name: ``absl::config``
  * pkg-config *.pc* file: **absl_config.pc**
* Component **absl_dynamic_annotations**:
  * CMake target name: ``absl::dynamic_annotations``
  * pkg-config *.pc* file: **absl_dynamic_annotations.pc**
  * Requires other components: **absl_config**
* Component **absl_core_headers**:
  * CMake target name: ``absl::core_headers``
  * pkg-config *.pc* file: **absl_core_headers.pc**
  * Requires other components: **absl_config**
* Component **absl_malloc_internal**:
  * CMake target name: ``absl::malloc_internal``
  * pkg-config *.pc* file: **absl_malloc_internal.pc**
  * Requires other components: **absl_base**, **absl_base_internal**, **absl_config**, **absl_core_headers**, **absl_dynamic_annotations**, **absl_raw_logging_internal**
  * Links to libraries: **absl_malloc_internal**
  * Systems libs: **pthread**
* Component **absl_base_internal**:
  * CMake target name: ``absl::base_internal``
  * pkg-config *.pc* file: **absl_base_internal.pc**
  * Requires other components: **absl_config**, **absl_type_traits**
* Component **absl_base**:
  * CMake target name: ``absl::base``
  * pkg-config *.pc* file: **absl_base.pc**
  * Requires other components: **absl_atomic_hook**, **absl_base_internal**, **absl_config**, **absl_core_headers**, **absl_dynamic_annotations**, **absl_log_severity**, **absl_raw_logging_internal**, **absl_spinlock_wait**, **absl_type_traits**
  * Links to libraries: **absl_base**
  * Systems libs: **pthread**, **rt**
* Component **absl_throw_delegate**:
  * CMake target name: ``absl::throw_delegate``
  * pkg-config *.pc* file: **absl_throw_delegate.pc**
  * Requires other components: **absl_config**, **absl_raw_logging_internal**
  * Links to libraries: **absl_throw_delegate**
* Component **absl_pretty_function**:
  * CMake target name: ``absl::pretty_function``
  * pkg-config *.pc* file: **absl_pretty_function.pc**
* Component **absl_endian**:
  * CMake target name: ``absl::endian``
  * pkg-config *.pc* file: **absl_endian.pc**
  * Requires other components: **absl_base**, **absl_config**, **absl_core_headers**
* Component **absl_scoped_set_env**:
  * CMake target name: ``absl::scoped_set_env``
  * pkg-config *.pc* file: **absl_scoped_set_env.pc**
  * Requires other components: **absl_config**, **absl_raw_logging_internal**
  * Links to libraries: **absl_scoped_set_env**
* Component **absl_strerror**:
  * CMake target name: ``absl::strerror``
  * pkg-config *.pc* file: **absl_strerror.pc**
  * Requires other components: **absl_config**, **absl_core_headers**, **absl_errno_saver**
  * Links to libraries: **absl_strerror**
* Component **absl_fast_type_id**:
  * CMake target name: ``absl::fast_type_id``
  * pkg-config *.pc* file: **absl_fast_type_id.pc**
  * Requires other components: **absl_config**
* Component **absl_prefetch**:
  * CMake target name: ``absl::prefetch``
  * pkg-config *.pc* file: **absl_prefetch.pc**
  * Requires other components: **absl_config**
* Component **absl_algorithm**:
  * CMake target name: ``absl::algorithm``
  * pkg-config *.pc* file: **absl_algorithm.pc**
  * Requires other components: **absl_config**
* Component **absl_algorithm_container**:
  * CMake target name: ``absl::algorithm_container``
  * pkg-config *.pc* file: **absl_algorithm_container.pc**
  * Requires other components: **absl_algorithm**, **absl_core_headers**, **absl_meta**
* Component **absl_cleanup_internal**:
  * CMake target name: ``absl::cleanup_internal``
  * pkg-config *.pc* file: **absl_cleanup_internal.pc**
  * Requires other components: **absl_base_internal**, **absl_core_headers**, **absl_utility**
* Component **absl_cleanup**:
  * CMake target name: ``absl::cleanup``
  * pkg-config *.pc* file: **absl_cleanup.pc**
  * Requires other components: **absl_cleanup_internal**, **absl_config**, **absl_core_headers**
* Component **absl_btree**:
  * CMake target name: ``absl::btree``
  * pkg-config *.pc* file: **absl_btree.pc**
  * Requires other components: **absl_container_common**, **absl_compare**, **absl_compressed_tuple**, **absl_container_memory**, **absl_cord**, **absl_core_headers**, **absl_layout**, **absl_memory**, **absl_raw_logging_internal**, **absl_strings**, **absl_throw_delegate**, **absl_type_traits**, **absl_utility**
* Component **absl_compressed_tuple**:
  * CMake target name: ``absl::compressed_tuple``
  * pkg-config *.pc* file: **absl_compressed_tuple.pc**
  * Requires other components: **absl_utility**
* Component **absl_fixed_array**:
  * CMake target name: ``absl::fixed_array``
  * pkg-config *.pc* file: **absl_fixed_array.pc**
  * Requires other components: **absl_compressed_tuple**, **absl_algorithm**, **absl_config**, **absl_core_headers**, **absl_dynamic_annotations**, **absl_throw_delegate**, **absl_memory**
* Component **absl_inlined_vector_internal**:
  * CMake target name: ``absl::inlined_vector_internal``
  * pkg-config *.pc* file: **absl_inlined_vector_internal.pc**
  * Requires other components: **absl_compressed_tuple**, **absl_core_headers**, **absl_memory**, **absl_span**, **absl_type_traits**
* Component **absl_inlined_vector**:
  * CMake target name: ``absl::inlined_vector``
  * pkg-config *.pc* file: **absl_inlined_vector.pc**
  * Requires other components: **absl_algorithm**, **absl_core_headers**, **absl_inlined_vector_internal**, **absl_throw_delegate**, **absl_memory**
* Component **absl_counting_allocator**:
  * CMake target name: ``absl::counting_allocator``
  * pkg-config *.pc* file: **absl_counting_allocator.pc**
  * Requires other components: **absl_config**
* Component **absl_flat_hash_map**:
  * CMake target name: ``absl::flat_hash_map``
  * pkg-config *.pc* file: **absl_flat_hash_map.pc**
  * Requires other components: **absl_container_memory**, **absl_core_headers**, **absl_hash_function_defaults**, **absl_raw_hash_map**, **absl_algorithm_container**, **absl_memory**
* Component **absl_flat_hash_set**:
  * CMake target name: ``absl::flat_hash_set``
  * pkg-config *.pc* file: **absl_flat_hash_set.pc**
  * Requires other components: **absl_container_memory**, **absl_hash_function_defaults**, **absl_raw_hash_set**, **absl_algorithm_container**, **absl_core_headers**, **absl_memory**
* Component **absl_node_hash_map**:
  * CMake target name: ``absl::node_hash_map``
  * pkg-config *.pc* file: **absl_node_hash_map.pc**
  * Requires other components: **absl_container_memory**, **absl_core_headers**, **absl_hash_function_defaults**, **absl_node_slot_policy**, **absl_raw_hash_map**, **absl_algorithm_container**, **absl_memory**
* Component **absl_node_hash_set**:
  * CMake target name: ``absl::node_hash_set``
  * pkg-config *.pc* file: **absl_node_hash_set.pc**
  * Requires other components: **absl_core_headers**, **absl_hash_function_defaults**, **absl_node_slot_policy**, **absl_raw_hash_set**, **absl_algorithm_container**, **absl_memory**
* Component **absl_container_memory**:
  * CMake target name: ``absl::container_memory``
  * pkg-config *.pc* file: **absl_container_memory.pc**
  * Requires other components: **absl_config**, **absl_memory**, **absl_type_traits**, **absl_utility**
* Component **absl_hash_function_defaults**:
  * CMake target name: ``absl::hash_function_defaults``
  * pkg-config *.pc* file: **absl_hash_function_defaults.pc**
  * Requires other components: **absl_config**, **absl_cord**, **absl_hash**, **absl_strings**
* Component **absl_hash_policy_traits**:
  * CMake target name: ``absl::hash_policy_traits``
  * pkg-config *.pc* file: **absl_hash_policy_traits.pc**
  * Requires other components: **absl_meta**
* Component **absl_hashtablez_sampler**:
  * CMake target name: ``absl::hashtablez_sampler``
  * pkg-config *.pc* file: **absl_hashtablez_sampler.pc**
  * Requires other components: **absl_base**, **absl_config**, **absl_exponential_biased**, **absl_sample_recorder**, **absl_synchronization**
  * Links to libraries: **absl_hashtablez_sampler**
* Component **absl_hashtable_debug**:
  * CMake target name: ``absl::hashtable_debug``
  * pkg-config *.pc* file: **absl_hashtable_debug.pc**
  * Requires other components: **absl_hashtable_debug_hooks**
* Component **absl_hashtable_debug_hooks**:
  * CMake target name: ``absl::hashtable_debug_hooks``
  * pkg-config *.pc* file: **absl_hashtable_debug_hooks.pc**
  * Requires other components: **absl_config**
* Component **absl_node_slot_policy**:
  * CMake target name: ``absl::node_slot_policy``
  * pkg-config *.pc* file: **absl_node_slot_policy.pc**
  * Requires other components: **absl_config**
* Component **absl_raw_hash_map**:
  * CMake target name: ``absl::raw_hash_map``
  * pkg-config *.pc* file: **absl_raw_hash_map.pc**
  * Requires other components: **absl_container_memory**, **absl_raw_hash_set**, **absl_throw_delegate**
* Component **absl_container_common**:
  * CMake target name: ``absl::container_common``
  * pkg-config *.pc* file: **absl_container_common.pc**
  * Requires other components: **absl_type_traits**
* Component **absl_raw_hash_set**:
  * CMake target name: ``absl::raw_hash_set``
  * pkg-config *.pc* file: **absl_raw_hash_set.pc**
  * Requires other components: **absl_bits**, **absl_compressed_tuple**, **absl_config**, **absl_container_common**, **absl_container_memory**, **absl_core_headers**, **absl_endian**, **absl_hash_policy_traits**, **absl_hashtable_debug_hooks**, **absl_memory**, **absl_meta**, **absl_optional**, **absl_prefetch**, **absl_utility**, **absl_hashtablez_sampler**
  * Links to libraries: **absl_raw_hash_set**
* Component **absl_layout**:
  * CMake target name: ``absl::layout``
  * pkg-config *.pc* file: **absl_layout.pc**
  * Requires other components: **absl_config**, **absl_core_headers**, **absl_meta**, **absl_strings**, **absl_span**, **absl_utility**
* Component **absl_stacktrace**:
  * CMake target name: ``absl::stacktrace``
  * pkg-config *.pc* file: **absl_stacktrace.pc**
  * Requires other components: **absl_debugging_internal**, **absl_config**, **absl_core_headers**
  * Links to libraries: **absl_stacktrace**
* Component **absl_symbolize**:
  * CMake target name: ``absl::symbolize``
  * pkg-config *.pc* file: **absl_symbolize.pc**
  * Requires other components: **absl_debugging_internal**, **absl_demangle_internal**, **absl_base**, **absl_config**, **absl_core_headers**, **absl_dynamic_annotations**, **absl_malloc_internal**, **absl_raw_logging_internal**, **absl_strings**
  * Links to libraries: **absl_symbolize**
* Component **absl_examine_stack**:
  * CMake target name: ``absl::examine_stack``
  * pkg-config *.pc* file: **absl_examine_stack.pc**
  * Requires other components: **absl_stacktrace**, **absl_symbolize**, **absl_config**, **absl_core_headers**, **absl_raw_logging_internal**
  * Links to libraries: **absl_examine_stack**
* Component **absl_failure_signal_handler**:
  * CMake target name: ``absl::failure_signal_handler``
  * pkg-config *.pc* file: **absl_failure_signal_handler.pc**
  * Requires other components: **absl_examine_stack**, **absl_stacktrace**, **absl_base**, **absl_config**, **absl_core_headers**, **absl_raw_logging_internal**
  * Links to libraries: **absl_failure_signal_handler**
* Component **absl_debugging_internal**:
  * CMake target name: ``absl::debugging_internal``
  * pkg-config *.pc* file: **absl_debugging_internal.pc**
  * Requires other components: **absl_core_headers**, **absl_config**, **absl_dynamic_annotations**, **absl_errno_saver**, **absl_raw_logging_internal**
  * Links to libraries: **absl_debugging_internal**
* Component **absl_demangle_internal**:
  * CMake target name: ``absl::demangle_internal``
  * pkg-config *.pc* file: **absl_demangle_internal.pc**
  * Requires other components: **absl_base**, **absl_core_headers**
  * Links to libraries: **absl_demangle_internal**
* Component **absl_leak_check**:
  * CMake target name: ``absl::leak_check``
  * pkg-config *.pc* file: **absl_leak_check.pc**
  * Requires other components: **absl_config**, **absl_core_headers**
  * Links to libraries: **absl_leak_check**
* Component **absl_debugging**:
  * CMake target name: ``absl::debugging``
  * pkg-config *.pc* file: **absl_debugging.pc**
  * Requires other components: **absl_stacktrace**, **absl_leak_check**
* Component **absl_flags_path_util**:
  * CMake target name: ``absl::flags_path_util``
  * pkg-config *.pc* file: **absl_flags_path_util.pc**
  * Requires other components: **absl_config**, **absl_strings**
* Component **absl_flags_program_name**:
  * CMake target name: ``absl::flags_program_name``
  * pkg-config *.pc* file: **absl_flags_program_name.pc**
  * Requires other components: **absl_config**, **absl_core_headers**, **absl_flags_path_util**, **absl_strings**, **absl_synchronization**
  * Links to libraries: **absl_flags_program_name**
* Component **absl_flags_config**:
  * CMake target name: ``absl::flags_config``
  * pkg-config *.pc* file: **absl_flags_config.pc**
  * Requires other components: **absl_config**, **absl_flags_path_util**, **absl_flags_program_name**, **absl_core_headers**, **absl_strings**, **absl_synchronization**
  * Links to libraries: **absl_flags_config**
* Component **absl_flags_marshalling**:
  * CMake target name: ``absl::flags_marshalling``
  * pkg-config *.pc* file: **absl_flags_marshalling.pc**
  * Requires other components: **absl_config**, **absl_core_headers**, **absl_log_severity**, **absl_optional**, **absl_strings**, **absl_str_format**
  * Links to libraries: **absl_flags_marshalling**
* Component **absl_flags_commandlineflag_internal**:
  * CMake target name: ``absl::flags_commandlineflag_internal``
  * pkg-config *.pc* file: **absl_flags_commandlineflag_internal.pc**
  * Requires other components: **absl_config**, **absl_dynamic_annotations**, **absl_fast_type_id**
  * Links to libraries: **absl_flags_commandlineflag_internal**
* Component **absl_flags_commandlineflag**:
  * CMake target name: ``absl::flags_commandlineflag``
  * pkg-config *.pc* file: **absl_flags_commandlineflag.pc**
  * Requires other components: **absl_config**, **absl_fast_type_id**, **absl_flags_commandlineflag_internal**, **absl_optional**, **absl_strings**
  * Links to libraries: **absl_flags_commandlineflag**
* Component **absl_flags_private_handle_accessor**:
  * CMake target name: ``absl::flags_private_handle_accessor``
  * pkg-config *.pc* file: **absl_flags_private_handle_accessor.pc**
  * Requires other components: **absl_config**, **absl_flags_commandlineflag**, **absl_flags_commandlineflag_internal**, **absl_strings**
  * Links to libraries: **absl_flags_private_handle_accessor**
* Component **absl_flags_reflection**:
  * CMake target name: ``absl::flags_reflection``
  * pkg-config *.pc* file: **absl_flags_reflection.pc**
  * Requires other components: **absl_config**, **absl_flags_commandlineflag**, **absl_flags_private_handle_accessor**, **absl_flags_config**, **absl_strings**, **absl_synchronization**, **absl_flat_hash_map**
  * Links to libraries: **absl_flags_reflection**
* Component **absl_flags_internal**:
  * CMake target name: ``absl::flags_internal``
  * pkg-config *.pc* file: **absl_flags_internal.pc**
  * Requires other components: **absl_base**, **absl_config**, **absl_flags_commandlineflag**, **absl_flags_commandlineflag_internal**, **absl_flags_config**, **absl_flags_marshalling**, **absl_synchronization**, **absl_meta**, **absl_utility**
  * Links to libraries: **absl_flags_internal**
* Component **absl_flags**:
  * CMake target name: ``absl::flags``
  * pkg-config *.pc* file: **absl_flags.pc**
  * Requires other components: **absl_config**, **absl_flags_commandlineflag**, **absl_flags_config**, **absl_flags_internal**, **absl_flags_reflection**, **absl_base**, **absl_core_headers**, **absl_strings**
  * Links to libraries: **absl_flags**
* Component **absl_flags_usage_internal**:
  * CMake target name: ``absl::flags_usage_internal``
  * pkg-config *.pc* file: **absl_flags_usage_internal.pc**
  * Requires other components: **absl_config**, **absl_flags_config**, **absl_flags**, **absl_flags_commandlineflag**, **absl_flags_internal**, **absl_flags_path_util**, **absl_flags_private_handle_accessor**, **absl_flags_program_name**, **absl_flags_reflection**, **absl_flat_hash_map**, **absl_strings**, **absl_synchronization**
  * Links to libraries: **absl_flags_usage_internal**
* Component **absl_flags_usage**:
  * CMake target name: ``absl::flags_usage``
  * pkg-config *.pc* file: **absl_flags_usage.pc**
  * Requires other components: **absl_config**, **absl_core_headers**, **absl_flags_usage_internal**, **absl_strings**, **absl_synchronization**
  * Links to libraries: **absl_flags_usage**
* Component **absl_flags_parse**:
  * CMake target name: ``absl::flags_parse``
  * pkg-config *.pc* file: **absl_flags_parse.pc**
  * Requires other components: **absl_config**, **absl_core_headers**, **absl_flags_config**, **absl_flags**, **absl_flags_commandlineflag**, **absl_flags_commandlineflag_internal**, **absl_flags_internal**, **absl_flags_private_handle_accessor**, **absl_flags_program_name**, **absl_flags_reflection**, **absl_flags_usage**, **absl_strings**, **absl_synchronization**
  * Links to libraries: **absl_flags_parse**
* Component **absl_any_invocable**:
  * CMake target name: ``absl::any_invocable``
  * pkg-config *.pc* file: **absl_any_invocable.pc**
  * Requires other components: **absl_base_internal**, **absl_config**, **absl_core_headers**, **absl_type_traits**, **absl_utility**
* Component **absl_bind_front**:
  * CMake target name: ``absl::bind_front``
  * pkg-config *.pc* file: **absl_bind_front.pc**
  * Requires other components: **absl_base_internal**, **absl_compressed_tuple**
* Component **absl_function_ref**:
  * CMake target name: ``absl::function_ref``
  * pkg-config *.pc* file: **absl_function_ref.pc**
  * Requires other components: **absl_base_internal**, **absl_core_headers**, **absl_meta**
* Component **absl_hash**:
  * CMake target name: ``absl::hash``
  * pkg-config *.pc* file: **absl_hash.pc**
  * Requires other components: **absl_city**, **absl_config**, **absl_core_headers**, **absl_endian**, **absl_fixed_array**, **absl_function_ref**, **absl_meta**, **absl_int128**, **absl_strings**, **absl_optional**, **absl_variant**, **absl_utility**, **absl_low_level_hash**
  * Links to libraries: **absl_hash**
* Component **absl_city**:
  * CMake target name: ``absl::city``
  * pkg-config *.pc* file: **absl_city.pc**
  * Requires other components: **absl_config**, **absl_core_headers**, **absl_endian**
  * Links to libraries: **absl_city**
* Component **absl_low_level_hash**:
  * CMake target name: ``absl::low_level_hash``
  * pkg-config *.pc* file: **absl_low_level_hash.pc**
  * Requires other components: **absl_bits**, **absl_config**, **absl_endian**, **absl_int128**
  * Links to libraries: **absl_low_level_hash**
* Component **absl_memory**:
  * CMake target name: ``absl::memory``
  * pkg-config *.pc* file: **absl_memory.pc**
  * Requires other components: **absl_core_headers**, **absl_meta**
* Component **absl_type_traits**:
  * CMake target name: ``absl::type_traits``
  * pkg-config *.pc* file: **absl_type_traits.pc**
  * Requires other components: **absl_config**
* Component **absl_meta**:
  * CMake target name: ``absl::meta``
  * pkg-config *.pc* file: **absl_meta.pc**
  * Requires other components: **absl_type_traits**
* Component **absl_bits**:
  * CMake target name: ``absl::bits``
  * pkg-config *.pc* file: **absl_bits.pc**
  * Requires other components: **absl_core_headers**
* Component **absl_int128**:
  * CMake target name: ``absl::int128``
  * pkg-config *.pc* file: **absl_int128.pc**
  * Requires other components: **absl_config**, **absl_core_headers**, **absl_bits**
  * Links to libraries: **absl_int128**
* Component **absl_numeric**:
  * CMake target name: ``absl::numeric``
  * pkg-config *.pc* file: **absl_numeric.pc**
  * Requires other components: **absl_int128**
* Component **absl_numeric_representation**:
  * CMake target name: ``absl::numeric_representation``
  * pkg-config *.pc* file: **absl_numeric_representation.pc**
  * Requires other components: **absl_config**
* Component **absl_sample_recorder**:
  * CMake target name: ``absl::sample_recorder``
  * pkg-config *.pc* file: **absl_sample_recorder.pc**
  * Requires other components: **absl_base**, **absl_synchronization**
* Component **absl_exponential_biased**:
  * CMake target name: ``absl::exponential_biased``
  * pkg-config *.pc* file: **absl_exponential_biased.pc**
  * Requires other components: **absl_config**, **absl_core_headers**
  * Links to libraries: **absl_exponential_biased**
* Component **absl_periodic_sampler**:
  * CMake target name: ``absl::periodic_sampler``
  * pkg-config *.pc* file: **absl_periodic_sampler.pc**
  * Requires other components: **absl_core_headers**, **absl_exponential_biased**
  * Links to libraries: **absl_periodic_sampler**
* Component **absl_random_random**:
  * CMake target name: ``absl::random_random``
  * pkg-config *.pc* file: **absl_random_random.pc**
  * Requires other components: **absl_random_distributions**, **absl_random_internal_nonsecure_base**, **absl_random_internal_pcg_engine**, **absl_random_internal_pool_urbg**, **absl_random_internal_randen_engine**, **absl_random_seed_sequences**
* Component **absl_random_bit_gen_ref**:
  * CMake target name: ``absl::random_bit_gen_ref``
  * pkg-config *.pc* file: **absl_random_bit_gen_ref.pc**
  * Requires other components: **absl_core_headers**, **absl_random_internal_distribution_caller**, **absl_random_internal_fast_uniform_bits**, **absl_type_traits**
* Component **absl_random_internal_mock_helpers**:
  * CMake target name: ``absl::random_internal_mock_helpers``
  * pkg-config *.pc* file: **absl_random_internal_mock_helpers.pc**
  * Requires other components: **absl_fast_type_id**, **absl_optional**
* Component **absl_random_distributions**:
  * CMake target name: ``absl::random_distributions``
  * pkg-config *.pc* file: **absl_random_distributions.pc**
  * Requires other components: **absl_base_internal**, **absl_config**, **absl_core_headers**, **absl_random_internal_generate_real**, **absl_random_internal_distribution_caller**, **absl_random_internal_fast_uniform_bits**, **absl_random_internal_fastmath**, **absl_random_internal_iostream_state_saver**, **absl_random_internal_traits**, **absl_random_internal_uniform_helper**, **absl_random_internal_wide_multiply**, **absl_strings**, **absl_type_traits**
  * Links to libraries: **absl_random_distributions**
* Component **absl_random_seed_gen_exception**:
  * CMake target name: ``absl::random_seed_gen_exception``
  * pkg-config *.pc* file: **absl_random_seed_gen_exception.pc**
  * Requires other components: **absl_config**
  * Links to libraries: **absl_random_seed_gen_exception**
* Component **absl_random_seed_sequences**:
  * CMake target name: ``absl::random_seed_sequences``
  * pkg-config *.pc* file: **absl_random_seed_sequences.pc**
  * Requires other components: **absl_config**, **absl_inlined_vector**, **absl_random_internal_pool_urbg**, **absl_random_internal_salted_seed_seq**, **absl_random_internal_seed_material**, **absl_random_seed_gen_exception**, **absl_span**
  * Links to libraries: **absl_random_seed_sequences**
* Component **absl_random_internal_traits**:
  * CMake target name: ``absl::random_internal_traits``
  * pkg-config *.pc* file: **absl_random_internal_traits.pc**
  * Requires other components: **absl_config**
* Component **absl_random_internal_distribution_caller**:
  * CMake target name: ``absl::random_internal_distribution_caller``
  * pkg-config *.pc* file: **absl_random_internal_distribution_caller.pc**
  * Requires other components: **absl_config**, **absl_utility**, **absl_fast_type_id**
* Component **absl_random_internal_fast_uniform_bits**:
  * CMake target name: ``absl::random_internal_fast_uniform_bits``
  * pkg-config *.pc* file: **absl_random_internal_fast_uniform_bits.pc**
  * Requires other components: **absl_config**
* Component **absl_random_internal_seed_material**:
  * CMake target name: ``absl::random_internal_seed_material``
  * pkg-config *.pc* file: **absl_random_internal_seed_material.pc**
  * Requires other components: **absl_core_headers**, **absl_optional**, **absl_random_internal_fast_uniform_bits**, **absl_raw_logging_internal**, **absl_span**, **absl_strings**
  * Links to libraries: **absl_random_internal_seed_material**
* Component **absl_random_internal_pool_urbg**:
  * CMake target name: ``absl::random_internal_pool_urbg``
  * pkg-config *.pc* file: **absl_random_internal_pool_urbg.pc**
  * Requires other components: **absl_base**, **absl_config**, **absl_core_headers**, **absl_endian**, **absl_random_internal_randen**, **absl_random_internal_seed_material**, **absl_random_internal_traits**, **absl_random_seed_gen_exception**, **absl_raw_logging_internal**, **absl_span**
  * Links to libraries: **absl_random_internal_pool_urbg**
* Component **absl_random_internal_salted_seed_seq**:
  * CMake target name: ``absl::random_internal_salted_seed_seq``
  * pkg-config *.pc* file: **absl_random_internal_salted_seed_seq.pc**
  * Requires other components: **absl_inlined_vector**, **absl_optional**, **absl_span**, **absl_random_internal_seed_material**, **absl_type_traits**
* Component **absl_random_internal_iostream_state_saver**:
  * CMake target name: ``absl::random_internal_iostream_state_saver``
  * pkg-config *.pc* file: **absl_random_internal_iostream_state_saver.pc**
  * Requires other components: **absl_int128**, **absl_type_traits**
* Component **absl_random_internal_generate_real**:
  * CMake target name: ``absl::random_internal_generate_real``
  * pkg-config *.pc* file: **absl_random_internal_generate_real.pc**
  * Requires other components: **absl_bits**, **absl_random_internal_fastmath**, **absl_random_internal_traits**, **absl_type_traits**
* Component **absl_random_internal_wide_multiply**:
  * CMake target name: ``absl::random_internal_wide_multiply``
  * pkg-config *.pc* file: **absl_random_internal_wide_multiply.pc**
  * Requires other components: **absl_bits**, **absl_config**, **absl_int128**
* Component **absl_random_internal_fastmath**:
  * CMake target name: ``absl::random_internal_fastmath``
  * pkg-config *.pc* file: **absl_random_internal_fastmath.pc**
  * Requires other components: **absl_bits**
* Component **absl_random_internal_nonsecure_base**:
  * CMake target name: ``absl::random_internal_nonsecure_base``
  * pkg-config *.pc* file: **absl_random_internal_nonsecure_base.pc**
  * Requires other components: **absl_core_headers**, **absl_inlined_vector**, **absl_random_internal_pool_urbg**, **absl_random_internal_salted_seed_seq**, **absl_random_internal_seed_material**, **absl_span**, **absl_type_traits**
* Component **absl_random_internal_pcg_engine**:
  * CMake target name: ``absl::random_internal_pcg_engine``
  * pkg-config *.pc* file: **absl_random_internal_pcg_engine.pc**
  * Requires other components: **absl_config**, **absl_int128**, **absl_random_internal_fastmath**, **absl_random_internal_iostream_state_saver**, **absl_type_traits**
* Component **absl_random_internal_randen_engine**:
  * CMake target name: ``absl::random_internal_randen_engine``
  * pkg-config *.pc* file: **absl_random_internal_randen_engine.pc**
  * Requires other components: **absl_endian**, **absl_random_internal_iostream_state_saver**, **absl_random_internal_randen**, **absl_raw_logging_internal**, **absl_type_traits**
* Component **absl_random_internal_platform**:
  * CMake target name: ``absl::random_internal_platform``
  * pkg-config *.pc* file: **absl_random_internal_platform.pc**
  * Requires other components: **absl_config**
  * Links to libraries: **absl_random_internal_platform**
* Component **absl_random_internal_randen**:
  * CMake target name: ``absl::random_internal_randen``
  * pkg-config *.pc* file: **absl_random_internal_randen.pc**
  * Requires other components: **absl_random_internal_platform**, **absl_random_internal_randen_hwaes**, **absl_random_internal_randen_slow**
  * Links to libraries: **absl_random_internal_randen**
* Component **absl_random_internal_randen_slow**:
  * CMake target name: ``absl::random_internal_randen_slow``
  * pkg-config *.pc* file: **absl_random_internal_randen_slow.pc**
  * Requires other components: **absl_random_internal_platform**, **absl_config**
  * Links to libraries: **absl_random_internal_randen_slow**
* Component **absl_random_internal_randen_hwaes**:
  * CMake target name: ``absl::random_internal_randen_hwaes``
  * pkg-config *.pc* file: **absl_random_internal_randen_hwaes.pc**
  * Requires other components: **absl_random_internal_platform**, **absl_random_internal_randen_hwaes_impl**, **absl_config**
  * Links to libraries: **absl_random_internal_randen_hwaes**
* Component **absl_random_internal_randen_hwaes_impl**:
  * CMake target name: ``absl::random_internal_randen_hwaes_impl``
  * pkg-config *.pc* file: **absl_random_internal_randen_hwaes_impl.pc**
  * Requires other components: **absl_random_internal_platform**, **absl_config**
  * Links to libraries: **absl_random_internal_randen_hwaes_impl**
* Component **absl_random_internal_distribution_test_util**:
  * CMake target name: ``absl::random_internal_distribution_test_util``
  * pkg-config *.pc* file: **absl_random_internal_distribution_test_util.pc**
  * Requires other components: **absl_config**, **absl_core_headers**, **absl_raw_logging_internal**, **absl_strings**, **absl_str_format**, **absl_span**
  * Links to libraries: **absl_random_internal_distribution_test_util**
* Component **absl_random_internal_uniform_helper**:
  * CMake target name: ``absl::random_internal_uniform_helper``
  * pkg-config *.pc* file: **absl_random_internal_uniform_helper.pc**
  * Requires other components: **absl_config**, **absl_random_internal_traits**, **absl_type_traits**
* Component **absl_status**:
  * CMake target name: ``absl::status``
  * pkg-config *.pc* file: **absl_status.pc**
  * Requires other components: **absl_atomic_hook**, **absl_config**, **absl_cord**, **absl_core_headers**, **absl_function_ref**, **absl_inlined_vector**, **absl_optional**, **absl_raw_logging_internal**, **absl_stacktrace**, **absl_str_format**, **absl_strerror**, **absl_strings**, **absl_symbolize**
  * Links to libraries: **absl_status**
* Component **absl_statusor**:
  * CMake target name: ``absl::statusor``
  * pkg-config *.pc* file: **absl_statusor.pc**
  * Requires other components: **absl_base**, **absl_status**, **absl_core_headers**, **absl_raw_logging_internal**, **absl_type_traits**, **absl_strings**, **absl_utility**, **absl_variant**
  * Links to libraries: **absl_statusor**
* Component **absl_strings**:
  * CMake target name: ``absl::strings``
  * pkg-config *.pc* file: **absl_strings.pc**
  * Requires other components: **absl_strings_internal**, **absl_base**, **absl_bits**, **absl_config**, **absl_core_headers**, **absl_endian**, **absl_int128**, **absl_memory**, **absl_raw_logging_internal**, **absl_throw_delegate**, **absl_type_traits**
  * Links to libraries: **absl_strings**
  * Systems libs: **m**
* Component **absl_strings_internal**:
  * CMake target name: ``absl::strings_internal``
  * pkg-config *.pc* file: **absl_strings_internal.pc**
  * Requires other components: **absl_config**, **absl_core_headers**, **absl_endian**, **absl_raw_logging_internal**, **absl_type_traits**
  * Links to libraries: **absl_strings_internal**
* Component **absl_str_format**:
  * CMake target name: ``absl::str_format``
  * pkg-config *.pc* file: **absl_str_format.pc**
  * Requires other components: **absl_str_format_internal**
* Component **absl_str_format_internal**:
  * CMake target name: ``absl::str_format_internal``
  * pkg-config *.pc* file: **absl_str_format_internal.pc**
  * Requires other components: **absl_bits**, **absl_strings**, **absl_config**, **absl_core_headers**, **absl_numeric_representation**, **absl_type_traits**, **absl_utility**, **absl_int128**, **absl_span**
  * Links to libraries: **absl_str_format_internal**
* Component **absl_cord_internal**:
  * CMake target name: ``absl::cord_internal``
  * pkg-config *.pc* file: **absl_cord_internal.pc**
  * Requires other components: **absl_base_internal**, **absl_compressed_tuple**, **absl_config**, **absl_core_headers**, **absl_endian**, **absl_inlined_vector**, **absl_layout**, **absl_raw_logging_internal**, **absl_strings**, **absl_throw_delegate**, **absl_type_traits**
  * Links to libraries: **absl_cord_internal**
* Component **absl_cordz_update_tracker**:
  * CMake target name: ``absl::cordz_update_tracker``
  * pkg-config *.pc* file: **absl_cordz_update_tracker.pc**
  * Requires other components: **absl_config**
* Component **absl_cordz_functions**:
  * CMake target name: ``absl::cordz_functions``
  * pkg-config *.pc* file: **absl_cordz_functions.pc**
  * Requires other components: **absl_config**, **absl_core_headers**, **absl_exponential_biased**, **absl_raw_logging_internal**
  * Links to libraries: **absl_cordz_functions**
* Component **absl_cordz_statistics**:
  * CMake target name: ``absl::cordz_statistics``
  * pkg-config *.pc* file: **absl_cordz_statistics.pc**
  * Requires other components: **absl_config**, **absl_core_headers**, **absl_cordz_update_tracker**, **absl_synchronization**
* Component **absl_cordz_handle**:
  * CMake target name: ``absl::cordz_handle``
  * pkg-config *.pc* file: **absl_cordz_handle.pc**
  * Requires other components: **absl_base**, **absl_config**, **absl_raw_logging_internal**, **absl_synchronization**
  * Links to libraries: **absl_cordz_handle**
* Component **absl_cordz_info**:
  * CMake target name: ``absl::cordz_info``
  * pkg-config *.pc* file: **absl_cordz_info.pc**
  * Requires other components: **absl_base**, **absl_config**, **absl_cord_internal**, **absl_cordz_functions**, **absl_cordz_handle**, **absl_cordz_statistics**, **absl_cordz_update_tracker**, **absl_core_headers**, **absl_inlined_vector**, **absl_span**, **absl_raw_logging_internal**, **absl_stacktrace**, **absl_synchronization**
  * Links to libraries: **absl_cordz_info**
* Component **absl_cordz_sample_token**:
  * CMake target name: ``absl::cordz_sample_token``
  * pkg-config *.pc* file: **absl_cordz_sample_token.pc**
  * Requires other components: **absl_config**, **absl_cordz_handle**, **absl_cordz_info**
  * Links to libraries: **absl_cordz_sample_token**
* Component **absl_cordz_update_scope**:
  * CMake target name: ``absl::cordz_update_scope``
  * pkg-config *.pc* file: **absl_cordz_update_scope.pc**
  * Requires other components: **absl_config**, **absl_cord_internal**, **absl_cordz_info**, **absl_cordz_update_tracker**, **absl_core_headers**
* Component **absl_cord**:
  * CMake target name: ``absl::cord``
  * pkg-config *.pc* file: **absl_cord.pc**
  * Requires other components: **absl_base**, **absl_config**, **absl_cord_internal**, **absl_cordz_functions**, **absl_cordz_info**, **absl_cordz_update_scope**, **absl_cordz_update_tracker**, **absl_core_headers**, **absl_endian**, **absl_fixed_array**, **absl_function_ref**, **absl_inlined_vector**, **absl_optional**, **absl_raw_logging_internal**, **absl_span**, **absl_strings**, **absl_type_traits**
  * Links to libraries: **absl_cord**
* Component **absl_graphcycles_internal**:
  * CMake target name: ``absl::graphcycles_internal``
  * pkg-config *.pc* file: **absl_graphcycles_internal.pc**
  * Requires other components: **absl_base**, **absl_base_internal**, **absl_config**, **absl_core_headers**, **absl_malloc_internal**, **absl_raw_logging_internal**
  * Links to libraries: **absl_graphcycles_internal**
* Component **absl_kernel_timeout_internal**:
  * CMake target name: ``absl::kernel_timeout_internal``
  * pkg-config *.pc* file: **absl_kernel_timeout_internal.pc**
  * Requires other components: **absl_core_headers**, **absl_raw_logging_internal**, **absl_time**
* Component **absl_synchronization**:
  * CMake target name: ``absl::synchronization``
  * pkg-config *.pc* file: **absl_synchronization.pc**
  * Requires other components: **absl_graphcycles_internal**, **absl_kernel_timeout_internal**, **absl_atomic_hook**, **absl_base**, **absl_base_internal**, **absl_config**, **absl_core_headers**, **absl_dynamic_annotations**, **absl_malloc_internal**, **absl_raw_logging_internal**, **absl_stacktrace**, **absl_symbolize**, **absl_time**
  * Links to libraries: **absl_synchronization**
  * Systems libs: **pthread**
* Component **absl_time**:
  * CMake target name: ``absl::time``
  * pkg-config *.pc* file: **absl_time.pc**
  * Requires other components: **absl_base**, **absl_civil_time**, **absl_core_headers**, **absl_int128**, **absl_raw_logging_internal**, **absl_strings**, **absl_time_zone**
  * Links to libraries: **absl_time**
* Component **absl_civil_time**:
  * CMake target name: ``absl::civil_time``
  * pkg-config *.pc* file: **absl_civil_time.pc**
  * Links to libraries: **absl_civil_time**
* Component **absl_time_zone**:
  * CMake target name: ``absl::time_zone``
  * pkg-config *.pc* file: **absl_time_zone.pc**
  * Links to libraries: **absl_time_zone**
* Component **absl_any**:
  * CMake target name: ``absl::any``
  * pkg-config *.pc* file: **absl_any.pc**
  * Requires other components: **absl_bad_any_cast**, **absl_config**, **absl_core_headers**, **absl_fast_type_id**, **absl_type_traits**, **absl_utility**
* Component **absl_bad_any_cast**:
  * CMake target name: ``absl::bad_any_cast``
  * pkg-config *.pc* file: **absl_bad_any_cast.pc**
  * Requires other components: **absl_bad_any_cast_impl**, **absl_config**
* Component **absl_bad_any_cast_impl**:
  * CMake target name: ``absl::bad_any_cast_impl``
  * pkg-config *.pc* file: **absl_bad_any_cast_impl.pc**
  * Requires other components: **absl_config**, **absl_raw_logging_internal**
  * Links to libraries: **absl_bad_any_cast_impl**
* Component **absl_span**:
  * CMake target name: ``absl::span``
  * pkg-config *.pc* file: **absl_span.pc**
  * Requires other components: **absl_algorithm**, **absl_core_headers**, **absl_throw_delegate**, **absl_type_traits**
* Component **absl_optional**:
  * CMake target name: ``absl::optional``
  * pkg-config *.pc* file: **absl_optional.pc**
  * Requires other components: **absl_bad_optional_access**, **absl_base_internal**, **absl_config**, **absl_core_headers**, **absl_memory**, **absl_type_traits**, **absl_utility**
* Component **absl_bad_optional_access**:
  * CMake target name: ``absl::bad_optional_access``
  * pkg-config *.pc* file: **absl_bad_optional_access.pc**
  * Requires other components: **absl_config**, **absl_raw_logging_internal**
  * Links to libraries: **absl_bad_optional_access**
* Component **absl_bad_variant_access**:
  * CMake target name: ``absl::bad_variant_access``
  * pkg-config *.pc* file: **absl_bad_variant_access.pc**
  * Requires other components: **absl_config**, **absl_raw_logging_internal**
  * Links to libraries: **absl_bad_variant_access**
* Component **absl_variant**:
  * CMake target name: ``absl::variant``
  * pkg-config *.pc* file: **absl_variant.pc**
  * Requires other components: **absl_bad_variant_access**, **absl_base_internal**, **absl_config**, **absl_core_headers**, **absl_type_traits**, **absl_utility**
* Component **absl_compare**:
  * CMake target name: ``absl::compare``
  * pkg-config *.pc* file: **absl_compare.pc**
  * Requires other components: **absl_core_headers**, **absl_type_traits**
* Component **absl_utility**:
  * CMake target name: ``absl::utility``
  * pkg-config *.pc* file: **absl_utility.pc**
  * Requires other components: **absl_base_internal**, **absl_config**, **absl_type_traits**


<br>

## Exposed header files for abseil

<br>

```cpp
#include <absl/cleanup/cleanup.h>
#include <absl/cleanup/internal/cleanup.h>
#include <absl/base/call_once.h>
#include <absl/base/config.h>
#include <absl/base/macros.h>
#include <absl/base/const_init.h>
#include <absl/base/port.h>
#include <absl/base/options.h>
#include <absl/base/optimization.h>
#include <absl/base/dynamic_annotations.h>
#include <absl/base/log_severity.h>
#include <absl/base/casts.h>
#include <absl/base/thread_annotations.h>
#include <absl/base/policy_checks.h>
#include <absl/base/attributes.h>
#include <absl/base/internal/spinlock_linux.inc>
#include <absl/base/internal/spinlock_akaros.inc>
#include <absl/base/internal/sysinfo.h>
#include <absl/base/internal/scoped_set_env.h>
#include <absl/base/internal/unscaledcycleclock.h>
#include <absl/base/internal/errno_saver.h>
#include <absl/base/internal/hide_ptr.h>
#include <absl/base/internal/strerror.h>
#include <absl/base/internal/pretty_function.h>
#include <absl/base/internal/identity.h>
#include <absl/base/internal/tsan_mutex_interface.h>
#include <absl/base/internal/endian.h>
#include <absl/base/internal/cycleclock.h>
#include <absl/base/internal/spinlock_win32.inc>
#include <absl/base/internal/fast_type_id.h>
#include <absl/base/internal/direct_mmap.h>
#include <absl/base/internal/prefetch.h>
#include <absl/base/internal/spinlock_posix.inc>
#include <absl/base/internal/raw_logging.h>
#include <absl/base/internal/atomic_hook.h>
#include <absl/base/internal/exception_safety_testing.h>
#include <absl/base/internal/per_thread_tls.h>
#include <absl/base/internal/spinlock_wait.h>
#include <absl/base/internal/atomic_hook_test_helper.h>
#include <absl/base/internal/low_level_scheduling.h>
#include <absl/base/internal/exception_testing.h>
#include <absl/base/internal/invoke.h>
#include <absl/base/internal/spinlock.h>
#include <absl/base/internal/dynamic_annotations.h>
#include <absl/base/internal/low_level_alloc.h>
#include <absl/base/internal/inline_variable_testing.h>
#include <absl/base/internal/thread_annotations.h>
#include <absl/base/internal/thread_identity.h>
#include <absl/base/internal/throw_delegate.h>
#include <absl/base/internal/scheduling_mode.h>
#include <absl/base/internal/unaligned_access.h>
#include <absl/base/internal/inline_variable.h>
#include <absl/container/flat_hash_map.h>
#include <absl/container/inlined_vector.h>
#include <absl/container/btree_map.h>
#include <absl/container/flat_hash_set.h>
#include <absl/container/btree_set.h>
#include <absl/container/node_hash_set.h>
#include <absl/container/fixed_array.h>
#include <absl/container/btree_test.h>
#include <absl/container/node_hash_map.h>
#include <absl/container/internal/container_memory.h>
#include <absl/container/internal/inlined_vector.h>
#include <absl/container/internal/hash_generator_testing.h>
#include <absl/container/internal/btree.h>
#include <absl/container/internal/unordered_map_lookup_test.h>
#include <absl/container/internal/hashtable_debug.h>
#include <absl/container/internal/unordered_set_constructor_test.h>
#include <absl/container/internal/tracked.h>
#include <absl/container/internal/unordered_set_modifiers_test.h>
#include <absl/container/internal/compressed_tuple.h>
#include <absl/container/internal/hash_function_defaults.h>
#include <absl/container/internal/hash_policy_testing.h>
#include <absl/container/internal/common.h>
#include <absl/container/internal/unordered_set_lookup_test.h>
#include <absl/container/internal/test_instance_tracker.h>
#include <absl/container/internal/raw_hash_set.h>
#include <absl/container/internal/hashtablez_sampler.h>
#include <absl/container/internal/hash_policy_traits.h>
#include <absl/container/internal/unordered_map_members_test.h>
#include <absl/container/internal/unordered_map_constructor_test.h>
#include <absl/container/internal/unordered_map_modifiers_test.h>
#include <absl/container/internal/layout.h>
#include <absl/container/internal/counting_allocator.h>
#include <absl/container/internal/hashtable_debug_hooks.h>
#include <absl/container/internal/raw_hash_map.h>
#include <absl/container/internal/btree_container.h>
#include <absl/container/internal/unordered_set_members_test.h>
#include <absl/container/internal/node_slot_policy.h>
#include <absl/strings/substitute.h>
#include <absl/strings/escaping.h>
#include <absl/strings/str_cat.h>
#include <absl/strings/str_join.h>
#include <absl/strings/str_format.h>
#include <absl/strings/numbers.h>
#include <absl/strings/cord.h>
#include <absl/strings/cord_test_helpers.h>
#include <absl/strings/str_split.h>
#include <absl/strings/string_view.h>
#include <absl/strings/ascii.h>
#include <absl/strings/cordz_test_helpers.h>
#include <absl/strings/str_replace.h>
#include <absl/strings/cord_analysis.h>
#include <absl/strings/match.h>
#include <absl/strings/charconv.h>
#include <absl/strings/strip.h>
#include <absl/strings/cord_buffer.h>
#include <absl/strings/internal/escaping.h>
#include <absl/strings/internal/cord_rep_crc.h>
#include <absl/strings/internal/pow10_helper.h>
#include <absl/strings/internal/cordz_update_scope.h>
#include <absl/strings/internal/cord_rep_btree.h>
#include <absl/strings/internal/numbers_test_common.h>
#include <absl/strings/internal/memutil.h>
#include <absl/strings/internal/cord_rep_ring_reader.h>
#include <absl/strings/internal/cord_internal.h>
#include <absl/strings/internal/cord_rep_flat.h>
#include <absl/strings/internal/cordz_handle.h>
#include <absl/strings/internal/cord_rep_consume.h>
#include <absl/strings/internal/resize_uninitialized.h>
#include <absl/strings/internal/cordz_update_tracker.h>
#include <absl/strings/internal/char_map.h>
#include <absl/strings/internal/cord_data_edge.h>
#include <absl/strings/internal/charconv_parse.h>
#include <absl/strings/internal/cord_rep_btree_reader.h>
#include <absl/strings/internal/ostringstream.h>
#include <absl/strings/internal/str_split_internal.h>
#include <absl/strings/internal/cord_rep_test_util.h>
#include <absl/strings/internal/str_join_internal.h>
#include <absl/strings/internal/cordz_functions.h>
#include <absl/strings/internal/cordz_sample_token.h>
#include <absl/strings/internal/charconv_bigint.h>
#include <absl/strings/internal/escaping_test_common.h>
#include <absl/strings/internal/string_constant.h>
#include <absl/strings/internal/cordz_statistics.h>
#include <absl/strings/internal/cordz_info.h>
#include <absl/strings/internal/cord_rep_ring.h>
#include <absl/strings/internal/utf8.h>
#include <absl/strings/internal/stl_type_traits.h>
#include <absl/strings/internal/cord_rep_btree_navigator.h>
#include <absl/strings/internal/str_format/arg.h>
#include <absl/strings/internal/str_format/extension.h>
#include <absl/strings/internal/str_format/checker.h>
#include <absl/strings/internal/str_format/output.h>
#include <absl/strings/internal/str_format/bind.h>
#include <absl/strings/internal/str_format/parser.h>
#include <absl/strings/internal/str_format/float_conversion.h>
#include <absl/flags/config.h>
#include <absl/flags/flag.h>
#include <absl/flags/declare.h>
#include <absl/flags/parse.h>
#include <absl/flags/usage_config.h>
#include <absl/flags/usage.h>
#include <absl/flags/commandlineflag.h>
#include <absl/flags/reflection.h>
#include <absl/flags/marshalling.h>
#include <absl/flags/internal/sequence_lock.h>
#include <absl/flags/internal/flag.h>
#include <absl/flags/internal/program_name.h>
#include <absl/flags/internal/private_handle_accessor.h>
#include <absl/flags/internal/parse.h>
#include <absl/flags/internal/usage.h>
#include <absl/flags/internal/commandlineflag.h>
#include <absl/flags/internal/registry.h>
#include <absl/flags/internal/flag_msvc.inc>
#include <absl/flags/internal/path_util.h>
#include <absl/debugging/stacktrace.h>
#include <absl/debugging/symbolize.h>
#include <absl/debugging/leak_check.h>
#include <absl/debugging/failure_signal_handler.h>
#include <absl/debugging/symbolize_win32.inc>
#include <absl/debugging/symbolize_emscripten.inc>
#include <absl/debugging/symbolize_darwin.inc>
#include <absl/debugging/symbolize_elf.inc>
#include <absl/debugging/symbolize_unimplemented.inc>
#include <absl/debugging/internal/stacktrace_powerpc-inl.inc>
#include <absl/debugging/internal/symbolize.h>
#include <absl/debugging/internal/address_is_readable.h>
#include <absl/debugging/internal/stacktrace_x86-inl.inc>
#include <absl/debugging/internal/vdso_support.h>
#include <absl/debugging/internal/stacktrace_win32-inl.inc>
#include <absl/debugging/internal/stack_consumption.h>
#include <absl/debugging/internal/stacktrace_riscv-inl.inc>
#include <absl/debugging/internal/examine_stack.h>
#include <absl/debugging/internal/stacktrace_aarch64-inl.inc>
#include <absl/debugging/internal/stacktrace_config.h>
#include <absl/debugging/internal/demangle.h>
#include <absl/debugging/internal/elf_mem_image.h>
#include <absl/debugging/internal/stacktrace_emscripten-inl.inc>
#include <absl/debugging/internal/stacktrace_arm-inl.inc>
#include <absl/debugging/internal/stacktrace_unimplemented-inl.inc>
#include <absl/debugging/internal/stacktrace_generic-inl.inc>
#include <absl/time/civil_time.h>
#include <absl/time/time.h>
#include <absl/time/clock.h>
#include <absl/time/internal/get_current_time_chrono.inc>
#include <absl/time/internal/get_current_time_posix.inc>
#include <absl/time/internal/test_util.h>
#include <absl/time/internal/zoneinfo.inc>
#include <absl/time/internal/cctz/src/time_zone_if.h>
#include <absl/time/internal/cctz/src/time_zone_info.h>
#include <absl/time/internal/cctz/src/time_zone_impl.h>
#include <absl/time/internal/cctz/src/time_zone_fixed.h>
#include <absl/time/internal/cctz/src/time_zone_libc.h>
#include <absl/time/internal/cctz/src/tzfile.h>
#include <absl/time/internal/cctz/src/time_zone_posix.h>
#include <absl/time/internal/cctz/include/cctz/civil_time.h>
#include <absl/time/internal/cctz/include/cctz/zone_info_source.h>
#include <absl/time/internal/cctz/include/cctz/civil_time_detail.h>
#include <absl/time/internal/cctz/include/cctz/time_zone.h>
#include <absl/meta/type_traits.h>
#include <absl/functional/any_invocable.h>
#include <absl/functional/function_ref.h>
#include <absl/functional/bind_front.h>
#include <absl/functional/internal/front_binder.h>
#include <absl/functional/internal/any_invocable.h>
#include <absl/functional/internal/function_ref.h>
#include <absl/status/status_payload_printer.h>
#include <absl/status/statusor.h>
#include <absl/status/status.h>
#include <absl/status/internal/statusor_internal.h>
#include <absl/status/internal/status_internal.h>
#include <absl/random/bit_gen_ref.h>
#include <absl/random/exponential_distribution.h>
#include <absl/random/distributions.h>
#include <absl/random/bernoulli_distribution.h>
#include <absl/random/log_uniform_int_distribution.h>
#include <absl/random/random.h>
#include <absl/random/gaussian_distribution.h>
#include <absl/random/seed_gen_exception.h>
#include <absl/random/beta_distribution.h>
#include <absl/random/poisson_distribution.h>
#include <absl/random/zipf_distribution.h>
#include <absl/random/uniform_int_distribution.h>
#include <absl/random/mocking_bit_gen.h>
#include <absl/random/seed_sequences.h>
#include <absl/random/uniform_real_distribution.h>
#include <absl/random/discrete_distribution.h>
#include <absl/random/mock_distributions.h>
#include <absl/random/internal/fastmath.h>
#include <absl/random/internal/fast_uniform_bits.h>
#include <absl/random/internal/salted_seed_seq.h>
#include <absl/random/internal/chi_square.h>
#include <absl/random/internal/randen_traits.h>
#include <absl/random/internal/pool_urbg.h>
#include <absl/random/internal/distribution_caller.h>
#include <absl/random/internal/mock_helpers.h>
#include <absl/random/internal/traits.h>
#include <absl/random/internal/seed_material.h>
#include <absl/random/internal/uniform_helper.h>
#include <absl/random/internal/sequence_urbg.h>
#include <absl/random/internal/generate_real.h>
#include <absl/random/internal/nonsecure_base.h>
#include <absl/random/internal/platform.h>
#include <absl/random/internal/pcg_engine.h>
#include <absl/random/internal/mock_overload_set.h>
#include <absl/random/internal/explicit_seed_seq.h>
#include <absl/random/internal/iostream_state_saver.h>
#include <absl/random/internal/randen_hwaes.h>
#include <absl/random/internal/wide_multiply.h>
#include <absl/random/internal/randen_detect.h>
#include <absl/random/internal/randen_slow.h>
#include <absl/random/internal/randen_engine.h>
#include <absl/random/internal/randen.h>
#include <absl/random/internal/distribution_test_util.h>
#include <absl/random/internal/nanobenchmark.h>
#include <absl/types/variant.h>
#include <absl/types/bad_variant_access.h>
#include <absl/types/bad_optional_access.h>
#include <absl/types/span.h>
#include <absl/types/bad_any_cast.h>
#include <absl/types/optional.h>
#include <absl/types/compare.h>
#include <absl/types/any.h>
#include <absl/types/internal/variant.h>
#include <absl/types/internal/conformance_archetype.h>
#include <absl/types/internal/parentheses.h>
#include <absl/types/internal/conformance_testing_helpers.h>
#include <absl/types/internal/conformance_aliases.h>
#include <absl/types/internal/span.h>
#include <absl/types/internal/transform_args.h>
#include <absl/types/internal/optional.h>
#include <absl/types/internal/conformance_testing.h>
#include <absl/types/internal/conformance_profile.h>
#include <absl/synchronization/blocking_counter.h>
#include <absl/synchronization/mutex.h>
#include <absl/synchronization/barrier.h>
#include <absl/synchronization/notification.h>
#include <absl/synchronization/internal/graphcycles.h>
#include <absl/synchronization/internal/futex.h>
#include <absl/synchronization/internal/waiter.h>
#include <absl/synchronization/internal/create_thread_identity.h>
#include <absl/synchronization/internal/kernel_timeout.h>
#include <absl/synchronization/internal/per_thread_sem.h>
#include <absl/synchronization/internal/thread_pool.h>
#include <absl/utility/utility.h>
#include <absl/memory/memory.h>
#include <absl/numeric/int128_have_intrinsic.inc>
#include <absl/numeric/bits.h>
#include <absl/numeric/int128_no_intrinsic.inc>
#include <absl/numeric/int128.h>
#include <absl/numeric/internal/representation.h>
#include <absl/numeric/internal/bits.h>
#include <absl/profiling/internal/periodic_sampler.h>
#include <absl/profiling/internal/exponential_biased.h>
#include <absl/profiling/internal/sample_recorder.h>
#include <absl/algorithm/algorithm.h>
#include <absl/algorithm/container.h>
#include <absl/hash/hash.h>
#include <absl/hash/hash_testing.h>
#include <absl/hash/internal/hash.h>
#include <absl/hash/internal/low_level_hash.h>
#include <absl/hash/internal/city.h>
#include <absl/hash/internal/spy_hash_state.h>
```

<br>


---
---
Conan **1.58.0**. JFrog LTD. [https://conan.io](https://conan.io). Autogenerated 2023-02-05 20:14:38.