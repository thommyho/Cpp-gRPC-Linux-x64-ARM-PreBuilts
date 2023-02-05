


# openssl/1.1.1s

---



<br>

## Using the openssl Conan Package

<br>

Conan integrates with different build systems. You can declare which build system you want your project to use setting in the **[generators]** section of the [conanfile.txt](https://docs.conan.io/en/latest/reference/conanfile_txt.html#generators) or using the **generators** attribute in the [conanfile.py](https://docs.conan.io/en/latest/reference/conanfile/attributes.html#generators). Here, there is some basic information you can use to integrate **openssl** in your own project. For more detailed information, please [check the Conan documentation](https://docs.conan.io/en/latest/getting_started.html).



<br>

## Using openssl with CMake

<br>

### [Conan CMake generators](https://docs.conan.io/en/latest/reference/conanfile/tools/cmake.html)

<br>

* [CMakeDeps](https://docs.conan.io/en/latest/reference/conanfile/tools/cmake/cmakedeps.html): generates information about where the **openssl** library and its dependencies  are installed together with other information like version, flags, and directory data or configuration. CMake will use this files when you invoke ``find_package()`` in your *CMakeLists.txt*.

* [CMakeToolchain](https://docs.conan.io/en/latest/reference/conanfile/tools/cmake/cmaketoolchain.html): generates a CMake toolchain file that you can later invoke with CMake in the command line using `-DCMAKE_TOOLCHAIN_FILE=conantoolchain.cmake`.

Declare these generators in your **conanfile.txt** along with your **openssl** dependency like:

```ini
[requires]
openssl/1.1.1s

[generators]
CMakeDeps
CMakeToolchain
```

<br>

To use **openssl** in a simple CMake project with this structure:

```shell
.
|-- CMakeLists.txt
|-- conanfile.txt
`-- src
    `-- main..c
```

<br>

Your **CMakeLists.txt** could look similar to this, using the global **openssl::openssl** CMake's target:

```cmake
cmake_minimum_required(VERSION 3.15)
project(openssl_project C)

find_package(OpenSSL)

add_executable(${PROJECT_NAME} src/main.c)

# Use the global target
target_link_libraries(${PROJECT_NAME} openssl::openssl)
```

<br>

To install **openssl/1.1.1s**, its dependencies and build your project, you just have to do:

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



As the openssl Conan package defines components, you can link only the desired parts of the library in your project. For example, linking only with the openssl **crypto** component, through the **OpenSSL::Crypto** target.

```cmake
...
# Link just to openssl crypto component
target_link_libraries(${PROJECT_NAME} OpenSSL::Crypto)
```

<br>

To check all the available components for **openssl** Conan package, please check the dedicated section at the end of this document.




<br>

### Declared CMake build modules

<br>

#### lib/cmake/conan-official-openssl-variables.cmake
  ```cmake
  set(OPENSSL_FOUND TRUE)
  if(DEFINED OpenSSL_INCLUDE_DIR)
      set(OPENSSL_INCLUDE_DIR ${OpenSSL_INCLUDE_DIR})
  endif()
  if(DEFINED OpenSSL_Crypto_LIBS)
      set(OPENSSL_CRYPTO_LIBRARY ${OpenSSL_Crypto_LIBS})
      set(OPENSSL_CRYPTO_LIBRARIES ${OpenSSL_Crypto_LIBS}
                                   ${OpenSSL_Crypto_DEPENDENCIES}
                                   ${OpenSSL_Crypto_FRAMEWORKS}
                                   ${OpenSSL_Crypto_SYSTEM_LIBS})
  elseif(DEFINED openssl_OpenSSL_Crypto_LIBS_RELEASE)
      set(OPENSSL_CRYPTO_LIBRARY ${openssl_OpenSSL_Crypto_LIBS_RELEASE})
      set(OPENSSL_CRYPTO_LIBRARIES ${openssl_OpenSSL_Crypto_LIBS_RELEASE}
                                   ${openssl_OpenSSL_Crypto_DEPENDENCIES_RELEASE}
                                   ${openssl_OpenSSL_Crypto_FRAMEWORKS_RELEASE}
                                   ${openssl_OpenSSL_Crypto_SYSTEM_LIBS_RELEASE})
  endif()
  if(DEFINED OpenSSL_SSL_LIBS)
      set(OPENSSL_SSL_LIBRARY ${OpenSSL_SSL_LIBS})
      set(OPENSSL_SSL_LIBRARIES ${OpenSSL_SSL_LIBS}
                                ${OpenSSL_SSL_DEPENDENCIES}
                                ${OpenSSL_SSL_FRAMEWORKS}
                                ${OpenSSL_SSL_SYSTEM_LIBS})
  elseif(DEFINED openssl_OpenSSL_SSL_LIBS_RELEASE)
      set(OPENSSL_SSL_LIBRARY ${openssl_OpenSSL_SSL_LIBS_RELEASE})
      set(OPENSSL_SSL_LIBRARIES ${openssl_OpenSSL_SSL_LIBS_RELEASE}
                                ${openssl_OpenSSL_SSL_DEPENDENCIES_RELEASE}
                                ${openssl_OpenSSL_SSL_FRAMEWORKS_RELEASE}
                                ${openssl_OpenSSL_SSL_SYSTEM_LIBS_RELEASE})
  endif()
  if(DEFINED OpenSSL_LIBRARIES)
      set(OPENSSL_LIBRARIES ${OpenSSL_LIBRARIES})
  endif()
  if(DEFINED OpenSSL_VERSION)
      set(OPENSSL_VERSION ${OpenSSL_VERSION})
  endif()

  ```



<br>

## Using openssl with Visual Studio

<br>

### [Visual Studio Conan generators](https://docs.conan.io/en/latest/reference/conanfile/tools/microsoft.html)

<br>

* [MSBuildDeps](https://docs.conan.io/en/latest/reference/conanfile/tools/microsoft.html#msbuilddeps): generates the **conandeps.props** properties file with information about where the **openssl** library and its dependencies  are installed together with other information like version, flags, and directory data or configuration.

* [MSBuildToolchain](https://docs.conan.io/en/latest/reference/conanfile/tools/microsoft.html#msbuildtoolchain): Generates the **conantoolchain.props** properties file with the current package configuration, settings, and options.

Declare these generators in your **conanfile.txt** along with your **openssl** dependency like:

```ini
[requires]
openssl/1.1.1s

[generators]
MSBuildDeps
MSBuildToolchain
```

<br>

Please, [check the Conan documentation](https://docs.conan.io/en/latest/reference/conanfile/tools/microsoft.html) for more detailed information on how to add these properties files to your Visual Studio projects.



<br>

## Using openssl with Autotools and pkg-config

<br>

### [Autotools Conan generators](https://docs.conan.io/en/latest/reference/conanfile/tools/gnu.html)

<br>

* [AutotoolsToolchain](https://docs.conan.io/en/latest/reference/conanfile/tools/gnu/autotoolstoolchain.html): generates the **conanautotoolstoolchain.sh/bat** script translating information from the current package configuration, settings, and options setting some enviroment variables for Autotools like: ``CPPFLAGS``, ``CXXFLAGS``, ``CFLAGS`` and ``LDFLAGS``. It will also generate a ``deactivate_conanautotoolstoolchain.sh/bat`` so you can restore your environment.

* [AutotoolsDeps](https://docs.conan.io/en/latest/reference/conanfile/tools/gnu/autotoolsdeps.html): generates the **conanautotoolsdeps.sh/bat** script with information about where the **openssl** library and its dependencies  are installed together with other information like version, flags, and directory data or configuration. This is done setting some enviroment variables for Autotools like: ``LIBS``, ``CPPFLAGS``,``CXXFLAGS``, ``CFLAGS`` and ``LDFLAGS``.  It will also generate a ``deactivate_conanautotoolsdeps.sh/bat`` so you can restore your environment.

Declare these generators in your **conanfile.txt** along with your **openssl** dependency like:

```ini
[requires]
openssl/1.1.1s

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

* [PkgConfigDeps](https://docs.conan.io/en/latest/reference/conanfile/tools/gnu/pkgconfigdeps.html): generates the **openssl.pc** file (and the ones corresponding to **openssl** dependencies) with information about the dependencies that can be later used by the **pkg-config** tool pkg-config to collect data about the libraries Conan installed.

<br>

You can use this generator instead of the **AutotoolsDeps** one:

```ini
[requires]
openssl/1.1.1s

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

$ export CPPFLAGS="$CPPFLAGS $(pkg-config --cflags openssl)"
$ export LIBS="$LIBS $(pkg-config --libs-only-l openssl)"
$ export LDFLAGS="$LDFLAGS $(pkg-config --libs-only-L --libs-only-other openssl)"

$ ./configure
$ make

# restore the environment after the build is completed
$ source deactivate_conanautotoolstoolchain.sh
```



<br>

As the openssl Conan package defines components you can use them to link only that desired part of the library in your project.  To check all the available components for **openssl** Conan package, and the corresponding *.pc* files names, please check the dedicated section at the end of this document.


<br>

## Other build systems

<br>

Please, [check the Conan documentation](https://docs.conan.io/en/latest/reference/conanfile/tools.html) for other integrations besides the ones listed in this document.





<br>

## Declared components for openssl

<br>

These are all the declared components for the **openssl** Conan package:
* Component **crypto**:
  * CMake target name: ``OpenSSL::Crypto``
  * pkg-config *.pc* file: **libcrypto.pc**
  * Links to libraries: **crypto**
  * Systems libs: **dl**, **rt**, **pthread**
* Component **ssl**:
  * CMake target name: ``OpenSSL::SSL``
  * pkg-config *.pc* file: **libssl.pc**
  * Requires other components: **crypto**
  * Links to libraries: **ssl**
  * Systems libs: **dl**, **pthread**


<br>

## Exposed header files for openssl

<br>

```cpp
#include <openssl/e_os2.h>
#include <openssl/dsaerr.h>
#include <openssl/opensslconf.h>
#include <openssl/conf.h>
#include <openssl/crypto.h>
#include <openssl/x509err.h>
#include <openssl/asn1.h>
#include <openssl/lhash.h>
#include <openssl/des.h>
#include <openssl/ocsperr.h>
#include <openssl/rand_drbg.h>
#include <openssl/randerr.h>
#include <openssl/cmserr.h>
#include <openssl/rc4.h>
#include <openssl/idea.h>
#include <openssl/pem.h>
#include <openssl/conf_api.h>
#include <openssl/err.h>
#include <openssl/pkcs12err.h>
#include <openssl/pemerr.h>
#include <openssl/buffer.h>
#include <openssl/obj_mac.h>
#include <openssl/x509_vfy.h>
#include <openssl/rc5.h>
#include <openssl/md5.h>
#include <openssl/stack.h>
#include <openssl/ssl3.h>
#include <openssl/bio.h>
#include <openssl/ossl_typ.h>
#include <openssl/aes.h>
#include <openssl/modes.h>
#include <openssl/dh.h>
#include <openssl/rsa.h>
#include <openssl/comp.h>
#include <openssl/asn1_mac.h>
#include <openssl/cast.h>
#include <openssl/ssl2.h>
#include <openssl/sslerr.h>
#include <openssl/safestack.h>
#include <openssl/hmac.h>
#include <openssl/symhacks.h>
#include <openssl/ssl.h>
#include <openssl/kdferr.h>
#include <openssl/bn.h>
#include <openssl/srp.h>
#include <openssl/buffererr.h>
#include <openssl/dsa.h>
#include <openssl/ecerr.h>
#include <openssl/ui.h>
#include <openssl/comperr.h>
#include <openssl/engineerr.h>
#include <openssl/store.h>
#include <openssl/rand.h>
#include <openssl/pkcs12.h>
#include <openssl/ocsp.h>
#include <openssl/pem2.h>
#include <openssl/pkcs7.h>
#include <openssl/async.h>
#include <openssl/cterr.h>
#include <openssl/asyncerr.h>
#include <openssl/bnerr.h>
#include <openssl/objects.h>
#include <openssl/cryptoerr.h>
#include <openssl/opensslv.h>
#include <openssl/x509v3.h>
#include <openssl/tls1.h>
#include <openssl/asn1err.h>
#include <openssl/dtls1.h>
#include <openssl/pkcs7err.h>
#include <openssl/rc2.h>
#include <openssl/md4.h>
#include <openssl/ts.h>
#include <openssl/kdf.h>
#include <openssl/txt_db.h>
#include <openssl/ebcdic.h>
#include <openssl/evp.h>
#include <openssl/md2.h>
#include <openssl/ec.h>
#include <openssl/ecdh.h>
#include <openssl/objectserr.h>
#include <openssl/uierr.h>
#include <openssl/dherr.h>
#include <openssl/bioerr.h>
#include <openssl/evperr.h>
#include <openssl/x509.h>
#include <openssl/camellia.h>
#include <openssl/rsaerr.h>
#include <openssl/mdc2.h>
#include <openssl/cmac.h>
#include <openssl/seed.h>
#include <openssl/tserr.h>
#include <openssl/engine.h>
#include <openssl/blowfish.h>
#include <openssl/conferr.h>
#include <openssl/storeerr.h>
#include <openssl/cms.h>
#include <openssl/asn1t.h>
#include <openssl/sha.h>
#include <openssl/whrlpool.h>
#include <openssl/srtp.h>
#include <openssl/ecdsa.h>
#include <openssl/ct.h>
#include <openssl/x509v3err.h>
#include <openssl/ripemd.h>
```

<br>


---
---
Conan **1.58.0**. JFrog LTD. [https://conan.io](https://conan.io). Autogenerated 2023-02-05 17:37:10.