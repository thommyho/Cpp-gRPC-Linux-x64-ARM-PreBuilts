


# googleapis/cci.20220711

---



<br>

## googleapis/cci.20220711 dependencies

* [protobuf/3.21.4](https://conan.io/center/protobuf)
* [zlib/1.2.13](https://conan.io/center/zlib)

<br>

## Using the googleapis Conan Package

<br>

Conan integrates with different build systems. You can declare which build system you want your project to use setting in the **[generators]** section of the [conanfile.txt](https://docs.conan.io/en/latest/reference/conanfile_txt.html#generators) or using the **generators** attribute in the [conanfile.py](https://docs.conan.io/en/latest/reference/conanfile/attributes.html#generators). Here, there is some basic information you can use to integrate **googleapis** in your own project. For more detailed information, please [check the Conan documentation](https://docs.conan.io/en/latest/getting_started.html).



<br>

## Using googleapis with CMake

<br>

### [Conan CMake generators](https://docs.conan.io/en/latest/reference/conanfile/tools/cmake.html)

<br>

* [CMakeDeps](https://docs.conan.io/en/latest/reference/conanfile/tools/cmake/cmakedeps.html): generates information about where the **googleapis** library and its dependencies  ( [protobuf](https://conan.io/center/protobuf),  [zlib](https://conan.io/center/zlib)) are installed together with other information like version, flags, and directory data or configuration. CMake will use this files when you invoke ``find_package()`` in your *CMakeLists.txt*.

* [CMakeToolchain](https://docs.conan.io/en/latest/reference/conanfile/tools/cmake/cmaketoolchain.html): generates a CMake toolchain file that you can later invoke with CMake in the command line using `-DCMAKE_TOOLCHAIN_FILE=conantoolchain.cmake`.

Declare these generators in your **conanfile.txt** along with your **googleapis** dependency like:

```ini
[requires]
googleapis/cci.20220711

[generators]
CMakeDeps
CMakeToolchain
```

<br>

To use **googleapis** in a simple CMake project with this structure:

```shell
.
|-- CMakeLists.txt
|-- conanfile.txt
`-- src
    `-- main..cpp
```

<br>

Your **CMakeLists.txt** could look similar to this, using the global **googleapis::googleapis** CMake's target:

```cmake
cmake_minimum_required(VERSION 3.15)
project(googleapis_project CXX)

find_package(googleapis)

add_executable(${PROJECT_NAME} src/main.cpp)

# Use the global target
target_link_libraries(${PROJECT_NAME} googleapis::googleapis)
```

<br>

To install **googleapis/cci.20220711**, its dependencies and build your project, you just have to do:

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

## Using googleapis with Visual Studio

<br>

### [Visual Studio Conan generators](https://docs.conan.io/en/latest/reference/conanfile/tools/microsoft.html)

<br>

* [MSBuildDeps](https://docs.conan.io/en/latest/reference/conanfile/tools/microsoft.html#msbuilddeps): generates the **conandeps.props** properties file with information about where the **googleapis** library and its dependencies  ( [protobuf](https://conan.io/center/protobuf),  [zlib](https://conan.io/center/zlib)) are installed together with other information like version, flags, and directory data or configuration.

* [MSBuildToolchain](https://docs.conan.io/en/latest/reference/conanfile/tools/microsoft.html#msbuildtoolchain): Generates the **conantoolchain.props** properties file with the current package configuration, settings, and options.

Declare these generators in your **conanfile.txt** along with your **googleapis** dependency like:

```ini
[requires]
googleapis/cci.20220711

[generators]
MSBuildDeps
MSBuildToolchain
```

<br>

Please, [check the Conan documentation](https://docs.conan.io/en/latest/reference/conanfile/tools/microsoft.html) for more detailed information on how to add these properties files to your Visual Studio projects.



<br>

## Using googleapis with Autotools and pkg-config

<br>

### [Autotools Conan generators](https://docs.conan.io/en/latest/reference/conanfile/tools/gnu.html)

<br>

* [AutotoolsToolchain](https://docs.conan.io/en/latest/reference/conanfile/tools/gnu/autotoolstoolchain.html): generates the **conanautotoolstoolchain.sh/bat** script translating information from the current package configuration, settings, and options setting some enviroment variables for Autotools like: ``CPPFLAGS``, ``CXXFLAGS``, ``CFLAGS`` and ``LDFLAGS``. It will also generate a ``deactivate_conanautotoolstoolchain.sh/bat`` so you can restore your environment.

* [AutotoolsDeps](https://docs.conan.io/en/latest/reference/conanfile/tools/gnu/autotoolsdeps.html): generates the **conanautotoolsdeps.sh/bat** script with information about where the **googleapis** library and its dependencies  ( [protobuf](https://conan.io/center/protobuf),  [zlib](https://conan.io/center/zlib)) are installed together with other information like version, flags, and directory data or configuration. This is done setting some enviroment variables for Autotools like: ``LIBS``, ``CPPFLAGS``,``CXXFLAGS``, ``CFLAGS`` and ``LDFLAGS``.  It will also generate a ``deactivate_conanautotoolsdeps.sh/bat`` so you can restore your environment.

Declare these generators in your **conanfile.txt** along with your **googleapis** dependency like:

```ini
[requires]
googleapis/cci.20220711

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

* [PkgConfigDeps](https://docs.conan.io/en/latest/reference/conanfile/tools/gnu/pkgconfigdeps.html): generates the **googleapis.pc** file (and the ones corresponding to **googleapis** dependencies) with information about the dependencies that can be later used by the **pkg-config** tool pkg-config to collect data about the libraries Conan installed.

<br>

You can use this generator instead of the **AutotoolsDeps** one:

```ini
[requires]
googleapis/cci.20220711

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

$ export CPPFLAGS="$CPPFLAGS $(pkg-config --cflags googleapis)"
$ export LIBS="$LIBS $(pkg-config --libs-only-l googleapis)"
$ export LDFLAGS="$LDFLAGS $(pkg-config --libs-only-L --libs-only-other googleapis)"

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

## Exposed header files for googleapis

<br>

```cpp
#include <google/container/v1beta1/cluster_service.pb.h>
#include <google/container/v1/cluster_service.pb.h>
#include <google/container/v1alpha1/cluster_service.pb.h>
#include <google/apps/script/type/addon_widget_set.pb.h>
#include <google/apps/script/type/extension_point.pb.h>
#include <google/apps/script/type/script_manifest.pb.h>
#include <google/apps/script/type/slides/slides_addon_manifest.pb.h>
#include <google/apps/script/type/calendar/calendar_addon_manifest.pb.h>
#include <google/apps/script/type/docs/docs_addon_manifest.pb.h>
#include <google/apps/script/type/drive/drive_addon_manifest.pb.h>
#include <google/apps/script/type/sheets/sheets_addon_manifest.pb.h>
#include <google/apps/script/type/gmail/gmail_addon_manifest.pb.h>
#include <google/analytics/admin/v1beta/resources.pb.h>
#include <google/analytics/admin/v1beta/analytics_admin.pb.h>
#include <google/analytics/data/v1alpha/data.pb.h>
#include <google/analytics/data/v1alpha/analytics_data_api.pb.h>
#include <google/cloud/extended_operations.pb.h>
#include <google/cloud/speech/v1/resource.pb.h>
#include <google/cloud/speech/v1/cloud_speech_adaptation.pb.h>
#include <google/cloud/speech/v1/cloud_speech.pb.h>
#include <google/cloud/commerce/consumer/procurement/v1alpha1/order.pb.h>
#include <google/cloud/commerce/consumer/procurement/v1alpha1/procurement_service.pb.h>
#include <google/cloud/notebooks/logging/v1/runtime_log.pb.h>
#include <google/cloud/notebooks/v1/instance.pb.h>
#include <google/cloud/notebooks/v1/service.pb.h>
#include <google/cloud/notebooks/v1/environment.pb.h>
#include <google/cloud/notebooks/v1/execution.pb.h>
#include <google/cloud/notebooks/v1/event.pb.h>
#include <google/cloud/notebooks/v1/instance_config.pb.h>
#include <google/cloud/notebooks/v1/managed_service.pb.h>
#include <google/cloud/notebooks/v1/runtime.pb.h>
#include <google/cloud/notebooks/v1/schedule.pb.h>
#include <google/cloud/redis/v1beta1/cloud_redis.pb.h>
#include <google/cloud/redis/v1/cloud_redis.pb.h>
#include <google/cloud/filestore/v1/cloud_filestore_service.pb.h>
#include <google/cloud/dataproc/logging/autoscaler_log.pb.h>
#include <google/cloud/dataproc/v1/autoscaling_policies.pb.h>
#include <google/cloud/dataproc/v1/operations.pb.h>
#include <google/cloud/dataproc/v1/shared.pb.h>
#include <google/cloud/dataproc/v1/jobs.pb.h>
#include <google/cloud/dataproc/v1/clusters.pb.h>
#include <google/cloud/dataproc/v1/workflow_templates.pb.h>
#include <google/cloud/dataproc/v1/batches.pb.h>
#include <google/cloud/tasks/v2/task.pb.h>
#include <google/cloud/tasks/v2/queue.pb.h>
#include <google/cloud/tasks/v2/target.pb.h>
#include <google/cloud/tasks/v2/cloudtasks.pb.h>
#include <google/cloud/stream/logging/v1/logging.pb.h>
#include <google/cloud/documentai/v1/operation_metadata.pb.h>
#include <google/cloud/documentai/v1/document_io.pb.h>
#include <google/cloud/documentai/v1/document_processor_service.pb.h>
#include <google/cloud/documentai/v1/document.pb.h>
#include <google/cloud/documentai/v1/geometry.pb.h>
#include <google/cloud/functions/v2alpha/functions.pb.h>
#include <google/cloud/functions/v1/operations.pb.h>
#include <google/cloud/functions/v1/functions.pb.h>
#include <google/cloud/functions/v2/functions.pb.h>
#include <google/cloud/functions/v2beta/functions.pb.h>
#include <google/cloud/sql/v1/cloud_sql_databases.pb.h>
#include <google/cloud/sql/v1/cloud_sql_backup_runs.pb.h>
#include <google/cloud/sql/v1/cloud_sql_ssl_certs.pb.h>
#include <google/cloud/sql/v1/cloud_sql_connect.pb.h>
#include <google/cloud/sql/v1/cloud_sql_instances.pb.h>
#include <google/cloud/sql/v1/cloud_sql_resources.pb.h>
#include <google/cloud/sql/v1/cloud_sql_operations.pb.h>
#include <google/cloud/sql/v1/cloud_sql_flags.pb.h>
#include <google/cloud/sql/v1/cloud_sql_tiers.pb.h>
#include <google/cloud/sql/v1/cloud_sql_users.pb.h>
#include <google/cloud/sql/v1/cloud_sql_instance_names.pb.h>
#include <google/cloud/sql/v1beta4/cloud_sql_connect.pb.h>
#include <google/cloud/sql/v1beta4/cloud_sql_resources.pb.h>
#include <google/cloud/sql/v1beta4/cloud_sql_tiers.pb.h>
#include <google/cloud/sql/v1beta4/cloud_sql_users.pb.h>
#include <google/cloud/sql/v1beta4/cloud_sql.pb.h>
#include <google/cloud/orgpolicy/v1/orgpolicy.pb.h>
#include <google/cloud/orgpolicy/v2/orgpolicy.pb.h>
#include <google/cloud/orgpolicy/v2/constraint.pb.h>
#include <google/cloud/policytroubleshooter/v1/checker.pb.h>
#include <google/cloud/policytroubleshooter/v1/explanations.pb.h>
#include <google/cloud/kms/v1/service.pb.h>
#include <google/cloud/kms/v1/ekm_service.pb.h>
#include <google/cloud/kms/v1/resources.pb.h>
#include <google/cloud/iap/v1/service.pb.h>
#include <google/cloud/resourcemanager/v2/folders.pb.h>
#include <google/cloud/resourcemanager/v3/tag_bindings.pb.h>
#include <google/cloud/resourcemanager/v3/organizations.pb.h>
#include <google/cloud/resourcemanager/v3/tag_keys.pb.h>
#include <google/cloud/resourcemanager/v3/projects.pb.h>
#include <google/cloud/resourcemanager/v3/folders.pb.h>
#include <google/cloud/resourcemanager/v3/tag_values.pb.h>
#include <google/cloud/security/publicca/v1beta1/service.pb.h>
#include <google/cloud/security/publicca/v1beta1/resources.pb.h>
#include <google/cloud/security/privateca/v1/service.pb.h>
#include <google/cloud/security/privateca/v1/resources.pb.h>
#include <google/cloud/talent/v4beta1/completion_service.pb.h>
#include <google/cloud/talent/v4beta1/filters.pb.h>
#include <google/cloud/talent/v4beta1/job_service.pb.h>
#include <google/cloud/talent/v4beta1/tenant_service.pb.h>
#include <google/cloud/talent/v4beta1/common.pb.h>
#include <google/cloud/talent/v4beta1/tenant.pb.h>
#include <google/cloud/talent/v4beta1/batch.pb.h>
#include <google/cloud/talent/v4beta1/job.pb.h>
#include <google/cloud/talent/v4beta1/event_service.pb.h>
#include <google/cloud/talent/v4beta1/event.pb.h>
#include <google/cloud/talent/v4beta1/histogram.pb.h>
#include <google/cloud/talent/v4beta1/company_service.pb.h>
#include <google/cloud/talent/v4beta1/company.pb.h>
#include <google/cloud/talent/v4/completion_service.pb.h>
#include <google/cloud/talent/v4/filters.pb.h>
#include <google/cloud/talent/v4/job_service.pb.h>
#include <google/cloud/talent/v4/tenant_service.pb.h>
#include <google/cloud/talent/v4/common.pb.h>
#include <google/cloud/talent/v4/tenant.pb.h>
#include <google/cloud/talent/v4/job.pb.h>
#include <google/cloud/talent/v4/event_service.pb.h>
#include <google/cloud/talent/v4/event.pb.h>
#include <google/cloud/talent/v4/histogram.pb.h>
#include <google/cloud/talent/v4/company_service.pb.h>
#include <google/cloud/talent/v4/company.pb.h>
#include <google/cloud/pubsublite/v1/cursor.pb.h>
#include <google/cloud/pubsublite/v1/common.pb.h>
#include <google/cloud/pubsublite/v1/publisher.pb.h>
#include <google/cloud/pubsublite/v1/admin.pb.h>
#include <google/cloud/pubsublite/v1/subscriber.pb.h>
#include <google/cloud/pubsublite/v1/topic_stats.pb.h>
#include <google/cloud/gsuiteaddons/logging/v1/g_suite_add_ons_log_entry.pb.h>
#include <google/cloud/gsuiteaddons/v1/gsuiteaddons.pb.h>
#include <google/cloud/essentialcontacts/v1/service.pb.h>
#include <google/cloud/essentialcontacts/v1/enums.pb.h>
#include <google/cloud/dataform/v1alpha2/dataform.pb.h>
#include <google/cloud/recaptchaenterprise/v1/recaptchaenterprise.pb.h>
#include <google/cloud/apigeeconnect/v1/tether.pb.h>
#include <google/cloud/apigeeconnect/v1/connection.pb.h>
#include <google/cloud/saasaccelerator/management/logs/v1/saas_instance_payload.pb.h>
#include <google/cloud/saasaccelerator/management/logs/v1/notification_service_payload.pb.h>
#include <google/cloud/vmmigration/v1/vmmigration.pb.h>
#include <google/cloud/resourcesettings/v1/resource_settings.pb.h>
#include <google/cloud/networkservices/v1beta1/common.pb.h>
#include <google/cloud/networkservices/v1beta1/endpoint_policy.pb.h>
#include <google/cloud/networkservices/v1beta1/network_services.pb.h>
#include <google/cloud/networkservices/v1/service_binding.pb.h>
#include <google/cloud/networkservices/v1/tcp_route.pb.h>
#include <google/cloud/networkservices/v1/common.pb.h>
#include <google/cloud/networkservices/v1/grpc_route.pb.h>
#include <google/cloud/networkservices/v1/tls_route.pb.h>
#include <google/cloud/networkservices/v1/endpoint_policy.pb.h>
#include <google/cloud/networkservices/v1/http_route.pb.h>
#include <google/cloud/networkservices/v1/network_services.pb.h>
#include <google/cloud/networkservices/v1/mesh.pb.h>
#include <google/cloud/networkservices/v1/gateway.pb.h>
#include <google/cloud/video/stitcher/v1/video_stitcher_service.pb.h>
#include <google/cloud/video/stitcher/v1/stitch_details.pb.h>
#include <google/cloud/video/stitcher/v1/sessions.pb.h>
#include <google/cloud/video/stitcher/v1/ad_tag_details.pb.h>
#include <google/cloud/video/stitcher/v1/companions.pb.h>
#include <google/cloud/video/stitcher/v1/slates.pb.h>
#include <google/cloud/video/stitcher/v1/cdn_keys.pb.h>
#include <google/cloud/video/stitcher/v1/events.pb.h>
#include <google/cloud/video/transcoder/v1/services.pb.h>
#include <google/cloud/video/transcoder/v1/resources.pb.h>
#include <google/cloud/video/livestream/logging/v1/logs.pb.h>
#include <google/cloud/video/livestream/v1/service.pb.h>
#include <google/cloud/video/livestream/v1/outputs.pb.h>
#include <google/cloud/video/livestream/v1/resources.pb.h>
#include <google/cloud/vision/v1/product_search_service.pb.h>
#include <google/cloud/vision/v1/web_detection.pb.h>
#include <google/cloud/vision/v1/image_annotator.pb.h>
#include <google/cloud/vision/v1/text_annotation.pb.h>
#include <google/cloud/vision/v1/product_search.pb.h>
#include <google/cloud/vision/v1/geometry.pb.h>
#include <google/cloud/apigeeregistry/v1/provisioning_service.pb.h>
#include <google/cloud/apigeeregistry/v1/registry_service.pb.h>
#include <google/cloud/apigeeregistry/v1/registry_models.pb.h>
#include <google/cloud/scheduler/v1/job.pb.h>
#include <google/cloud/scheduler/v1/cloudscheduler.pb.h>
#include <google/cloud/scheduler/v1/target.pb.h>
#include <google/cloud/networkmanagement/v1/trace.pb.h>
#include <google/cloud/networkmanagement/v1/connectivity_test.pb.h>
#include <google/cloud/networkmanagement/v1/reachability.pb.h>
#include <google/cloud/gkebackup/logging/v1/logged_restore.pb.h>
#include <google/cloud/gkebackup/logging/v1/logged_common.pb.h>
#include <google/cloud/gkebackup/logging/v1/logged_restore_plan.pb.h>
#include <google/cloud/gkebackup/logging/v1/logged_backup_plan.pb.h>
#include <google/cloud/gkebackup/logging/v1/logging.pb.h>
#include <google/cloud/gkebackup/logging/v1/logged_backup.pb.h>
#include <google/cloud/gkebackup/v1/restore_plan.pb.h>
#include <google/cloud/gkebackup/v1/backup.pb.h>
#include <google/cloud/gkebackup/v1/restore.pb.h>
#include <google/cloud/gkebackup/v1/volume.pb.h>
#include <google/cloud/gkebackup/v1/common.pb.h>
#include <google/cloud/gkebackup/v1/gkebackup.pb.h>
#include <google/cloud/gkebackup/v1/backup_plan.pb.h>
#include <google/cloud/common/operation_metadata.pb.h>
#include <google/cloud/audit/audit_log.pb.h>
#include <google/cloud/translate/v3/translation_service.pb.h>
#include <google/cloud/osconfig/v1beta/osconfig_common.pb.h>
#include <google/cloud/osconfig/v1beta/patch_jobs.pb.h>
#include <google/cloud/osconfig/v1beta/patch_deployments.pb.h>
#include <google/cloud/osconfig/v1beta/osconfig_service.pb.h>
#include <google/cloud/osconfig/v1beta/guest_policies.pb.h>
#include <google/cloud/osconfig/v1alpha/osconfig_common.pb.h>
#include <google/cloud/osconfig/v1alpha/instance_os_policies_compliance.pb.h>
#include <google/cloud/osconfig/v1alpha/os_policy_assignments.pb.h>
#include <google/cloud/osconfig/v1alpha/os_policy.pb.h>
#include <google/cloud/osconfig/v1alpha/osconfig_zonal_service.pb.h>
#include <google/cloud/osconfig/v1alpha/os_policy_assignment_reports.pb.h>
#include <google/cloud/osconfig/v1alpha/vulnerability.pb.h>
#include <google/cloud/osconfig/v1alpha/inventory.pb.h>
#include <google/cloud/osconfig/v1alpha/config_common.pb.h>
#include <google/cloud/osconfig/v1/osconfig_common.pb.h>
#include <google/cloud/osconfig/v1/patch_jobs.pb.h>
#include <google/cloud/osconfig/v1/patch_deployments.pb.h>
#include <google/cloud/osconfig/v1/os_policy_assignments.pb.h>
#include <google/cloud/osconfig/v1/osconfig_service.pb.h>
#include <google/cloud/osconfig/v1/os_policy.pb.h>
#include <google/cloud/osconfig/v1/osconfig_zonal_service.pb.h>
#include <google/cloud/osconfig/v1/os_policy_assignment_reports.pb.h>
#include <google/cloud/osconfig/v1/vulnerability.pb.h>
#include <google/cloud/osconfig/v1/inventory.pb.h>
#include <google/cloud/osconfig/agentendpoint/v1beta/patch_jobs.pb.h>
#include <google/cloud/osconfig/agentendpoint/v1beta/tasks.pb.h>
#include <google/cloud/osconfig/agentendpoint/v1beta/guest_policies.pb.h>
#include <google/cloud/osconfig/agentendpoint/v1beta/agentendpoint.pb.h>
#include <google/cloud/osconfig/agentendpoint/v1/patch_jobs.pb.h>
#include <google/cloud/osconfig/agentendpoint/v1/tasks.pb.h>
#include <google/cloud/osconfig/agentendpoint/v1/os_policy.pb.h>
#include <google/cloud/osconfig/agentendpoint/v1/inventory.pb.h>
#include <google/cloud/osconfig/agentendpoint/v1/agentendpoint.pb.h>
#include <google/cloud/osconfig/agentendpoint/v1/config_common.pb.h>
#include <google/cloud/baremetalsolution/v2/nfs_share.pb.h>
#include <google/cloud/baremetalsolution/v2/instance.pb.h>
#include <google/cloud/baremetalsolution/v2/volume.pb.h>
#include <google/cloud/baremetalsolution/v2/baremetalsolution.pb.h>
#include <google/cloud/baremetalsolution/v2/lun.pb.h>
#include <google/cloud/baremetalsolution/v2/network.pb.h>
#include <google/cloud/batch/v1alpha/volume.pb.h>
#include <google/cloud/batch/v1alpha/task.pb.h>
#include <google/cloud/batch/v1alpha/batch.pb.h>
#include <google/cloud/batch/v1alpha/job.pb.h>
#include <google/cloud/batch/v1/volume.pb.h>
#include <google/cloud/batch/v1/task.pb.h>
#include <google/cloud/batch/v1/batch.pb.h>
#include <google/cloud/batch/v1/job.pb.h>
#include <google/cloud/ids/v1/ids.pb.h>
#include <google/cloud/gkemulticloud/v1/azure_resources.pb.h>
#include <google/cloud/gkemulticloud/v1/azure_service.pb.h>
#include <google/cloud/gkemulticloud/v1/aws_resources.pb.h>
#include <google/cloud/gkemulticloud/v1/common_resources.pb.h>
#include <google/cloud/gkemulticloud/v1/aws_service.pb.h>
#include <google/cloud/orchestration/airflow/service/v1/operations.pb.h>
#include <google/cloud/orchestration/airflow/service/v1/image_versions.pb.h>
#include <google/cloud/orchestration/airflow/service/v1/environments.pb.h>
#include <google/cloud/clouddms/logging/v1/clouddms_platform_logs.pb.h>
#include <google/cloud/clouddms/v1/clouddms_resources.pb.h>
#include <google/cloud/clouddms/v1/clouddms.pb.h>
#include <google/cloud/location/locations.pb.h>
#include <google/cloud/deploy/v1/release_render_payload.pb.h>
#include <google/cloud/deploy/v1/rollout_notification_payload.pb.h>
#include <google/cloud/deploy/v1/release_notification_payload.pb.h>
#include <google/cloud/deploy/v1/target_notification_payload.pb.h>
#include <google/cloud/deploy/v1/log_enums.pb.h>
#include <google/cloud/deploy/v1/deliverypipeline_notification_payload.pb.h>
#include <google/cloud/deploy/v1/cloud_deploy.pb.h>
#include <google/cloud/certificatemanager/v1/certificate_manager.pb.h>
#include <google/cloud/accessapproval/v1/accessapproval.pb.h>
#include <google/cloud/aiplatform/logging/prediction.pb.h>
#include <google/cloud/aiplatform/v1/job_state.pb.h>
#include <google/cloud/aiplatform/v1/metadata_schema.pb.h>
#include <google/cloud/aiplatform/v1/hyperparameter_tuning_job.pb.h>
#include <google/cloud/aiplatform/v1/pipeline_job.pb.h>
#include <google/cloud/aiplatform/v1/job_service.pb.h>
#include <google/cloud/aiplatform/v1/index_endpoint_service.pb.h>
#include <google/cloud/aiplatform/v1/entity_type.pb.h>
#include <google/cloud/aiplatform/v1/feature_monitoring_stats.pb.h>
#include <google/cloud/aiplatform/v1/value.pb.h>
#include <google/cloud/aiplatform/v1/feature_selector.pb.h>
#include <google/cloud/aiplatform/v1/index_service.pb.h>
#include <google/cloud/aiplatform/v1/featurestore_monitoring.pb.h>
#include <google/cloud/aiplatform/v1/index.pb.h>
#include <google/cloud/aiplatform/v1/machine_resources.pb.h>
#include <google/cloud/aiplatform/v1/execution.pb.h>
#include <google/cloud/aiplatform/v1/training_pipeline.pb.h>
#include <google/cloud/aiplatform/v1/dataset.pb.h>
#include <google/cloud/aiplatform/v1/vizier_service.pb.h>
#include <google/cloud/aiplatform/v1/data_labeling_job.pb.h>
#include <google/cloud/aiplatform/v1/data_item.pb.h>
#include <google/cloud/aiplatform/v1/batch_prediction_job.pb.h>
#include <google/cloud/aiplatform/v1/artifact.pb.h>
#include <google/cloud/aiplatform/v1/endpoint.pb.h>
#include <google/cloud/aiplatform/v1/completion_stats.pb.h>
#include <google/cloud/aiplatform/v1/featurestore_service.pb.h>
#include <google/cloud/aiplatform/v1/explanation.pb.h>
#include <google/cloud/aiplatform/v1/specialist_pool.pb.h>
#include <google/cloud/aiplatform/v1/env_var.pb.h>
#include <google/cloud/aiplatform/v1/tensorboard_run.pb.h>
#include <google/cloud/aiplatform/v1/tensorboard.pb.h>
#include <google/cloud/aiplatform/v1/io.pb.h>
#include <google/cloud/aiplatform/v1/tensorboard_data.pb.h>
#include <google/cloud/aiplatform/v1/endpoint_service.pb.h>
#include <google/cloud/aiplatform/v1/dataset_service.pb.h>
#include <google/cloud/aiplatform/v1/model_service.pb.h>
#include <google/cloud/aiplatform/v1/deployed_index_ref.pb.h>
#include <google/cloud/aiplatform/v1/tensorboard_time_series.pb.h>
#include <google/cloud/aiplatform/v1/featurestore_online_service.pb.h>
#include <google/cloud/aiplatform/v1/annotation.pb.h>
#include <google/cloud/aiplatform/v1/model_evaluation_slice.pb.h>
#include <google/cloud/aiplatform/v1/model_evaluation.pb.h>
#include <google/cloud/aiplatform/v1/specialist_pool_service.pb.h>
#include <google/cloud/aiplatform/v1/featurestore.pb.h>
#include <google/cloud/aiplatform/v1/metadata_store.pb.h>
#include <google/cloud/aiplatform/v1/feature.pb.h>
#include <google/cloud/aiplatform/v1/manual_batch_tuning_parameters.pb.h>
#include <google/cloud/aiplatform/v1/pipeline_failure_policy.pb.h>
#include <google/cloud/aiplatform/v1/user_action_reference.pb.h>
#include <google/cloud/aiplatform/v1/event.pb.h>
#include <google/cloud/aiplatform/v1/unmanaged_container_model.pb.h>
#include <google/cloud/aiplatform/v1/custom_job.pb.h>
#include <google/cloud/aiplatform/v1/pipeline_state.pb.h>
#include <google/cloud/aiplatform/v1/model_deployment_monitoring_job.pb.h>
#include <google/cloud/aiplatform/v1/encryption_spec.pb.h>
#include <google/cloud/aiplatform/v1/types.pb.h>
#include <google/cloud/aiplatform/v1/index_endpoint.pb.h>
#include <google/cloud/aiplatform/v1/operation.pb.h>
#include <google/cloud/aiplatform/v1/annotation_spec.pb.h>
#include <google/cloud/aiplatform/v1/study.pb.h>
#include <google/cloud/aiplatform/v1/accelerator_type.pb.h>
#include <google/cloud/aiplatform/v1/lineage_subgraph.pb.h>
#include <google/cloud/aiplatform/v1/migration_service.pb.h>
#include <google/cloud/aiplatform/v1/tensorboard_service.pb.h>
#include <google/cloud/aiplatform/v1/tensorboard_experiment.pb.h>
#include <google/cloud/aiplatform/v1/pipeline_service.pb.h>
#include <google/cloud/aiplatform/v1/model.pb.h>
#include <google/cloud/aiplatform/v1/context.pb.h>
#include <google/cloud/aiplatform/v1/model_monitoring.pb.h>
#include <google/cloud/aiplatform/v1/explanation_metadata.pb.h>
#include <google/cloud/aiplatform/v1/migratable_resource.pb.h>
#include <google/cloud/aiplatform/v1/saved_query.pb.h>
#include <google/cloud/aiplatform/v1/metadata_service.pb.h>
#include <google/cloud/aiplatform/v1/deployed_model_ref.pb.h>
#include <google/cloud/aiplatform/v1/prediction_service.pb.h>
#include <google/cloud/aiplatform/v1/schema/predict/instance/image_segmentation.pb.h>
#include <google/cloud/aiplatform/v1/schema/predict/instance/video_classification.pb.h>
#include <google/cloud/aiplatform/v1/schema/predict/instance/text_classification.pb.h>
#include <google/cloud/aiplatform/v1/schema/predict/instance/image_classification.pb.h>
#include <google/cloud/aiplatform/v1/schema/predict/instance/video_object_tracking.pb.h>
#include <google/cloud/aiplatform/v1/schema/predict/instance/image_object_detection.pb.h>
#include <google/cloud/aiplatform/v1/schema/predict/instance/video_action_recognition.pb.h>
#include <google/cloud/aiplatform/v1/schema/predict/instance/text_extraction.pb.h>
#include <google/cloud/aiplatform/v1/schema/predict/instance/text_sentiment.pb.h>
#include <google/cloud/aiplatform/v1/schema/predict/prediction/image_segmentation.pb.h>
#include <google/cloud/aiplatform/v1/schema/predict/prediction/video_classification.pb.h>
#include <google/cloud/aiplatform/v1/schema/predict/prediction/video_object_tracking.pb.h>
#include <google/cloud/aiplatform/v1/schema/predict/prediction/image_object_detection.pb.h>
#include <google/cloud/aiplatform/v1/schema/predict/prediction/video_action_recognition.pb.h>
#include <google/cloud/aiplatform/v1/schema/predict/prediction/tabular_regression.pb.h>
#include <google/cloud/aiplatform/v1/schema/predict/prediction/classification.pb.h>
#include <google/cloud/aiplatform/v1/schema/predict/prediction/text_extraction.pb.h>
#include <google/cloud/aiplatform/v1/schema/predict/prediction/text_sentiment.pb.h>
#include <google/cloud/aiplatform/v1/schema/predict/prediction/tabular_classification.pb.h>
#include <google/cloud/aiplatform/v1/schema/predict/params/image_segmentation.pb.h>
#include <google/cloud/aiplatform/v1/schema/predict/params/video_classification.pb.h>
#include <google/cloud/aiplatform/v1/schema/predict/params/image_classification.pb.h>
#include <google/cloud/aiplatform/v1/schema/predict/params/video_object_tracking.pb.h>
#include <google/cloud/aiplatform/v1/schema/predict/params/image_object_detection.pb.h>
#include <google/cloud/aiplatform/v1/schema/predict/params/video_action_recognition.pb.h>
#include <google/cloud/aiplatform/v1/schema/trainingjob/definition/export_evaluated_data_items_config.pb.h>
#include <google/cloud/aiplatform/v1/schema/trainingjob/definition/automl_image_object_detection.pb.h>
#include <google/cloud/aiplatform/v1/schema/trainingjob/definition/automl_text_extraction.pb.h>
#include <google/cloud/aiplatform/v1/schema/trainingjob/definition/automl_video_classification.pb.h>
#include <google/cloud/aiplatform/v1/schema/trainingjob/definition/automl_video_object_tracking.pb.h>
#include <google/cloud/aiplatform/v1/schema/trainingjob/definition/automl_image_segmentation.pb.h>
#include <google/cloud/aiplatform/v1/schema/trainingjob/definition/automl_tables.pb.h>
#include <google/cloud/aiplatform/v1/schema/trainingjob/definition/automl_video_action_recognition.pb.h>
#include <google/cloud/aiplatform/v1/schema/trainingjob/definition/automl_image_classification.pb.h>
#include <google/cloud/aiplatform/v1/schema/trainingjob/definition/automl_text_sentiment.pb.h>
#include <google/cloud/aiplatform/v1/schema/trainingjob/definition/automl_text_classification.pb.h>
#include <google/cloud/datafusion/v1/datafusion.pb.h>
#include <google/cloud/managedidentities/v1beta1/managed_identities_service.pb.h>
#include <google/cloud/managedidentities/v1beta1/resource.pb.h>
#include <google/cloud/managedidentities/v1/managed_identities_service.pb.h>
#include <google/cloud/managedidentities/v1/resource.pb.h>
#include <google/cloud/metastore/v1alpha/metastore.pb.h>
#include <google/cloud/metastore/logging/v1/log_streams.pb.h>
#include <google/cloud/metastore/v1/metastore.pb.h>
#include <google/cloud/texttospeech/v1/cloud_tts.pb.h>
#include <google/cloud/workflows/type/engine_call.pb.h>
#include <google/cloud/workflows/type/executions_system.pb.h>
#include <google/cloud/workflows/v1/workflows.pb.h>
#include <google/cloud/workflows/executions/v1/executions.pb.h>
#include <google/cloud/assuredworkloads/regulatoryintercept/logging/v1/regulatory_intercept_ack_log_entry.pb.h>
#include <google/cloud/assuredworkloads/v1beta1/assuredworkloads.pb.h>
#include <google/cloud/assuredworkloads/v1/assuredworkloads.pb.h>
#include <google/cloud/gaming/v1/game_server_clusters.pb.h>
#include <google/cloud/gaming/v1/realms_service.pb.h>
#include <google/cloud/gaming/v1/game_server_configs_service.pb.h>
#include <google/cloud/gaming/v1/common.pb.h>
#include <google/cloud/gaming/v1/game_server_deployments.pb.h>
#include <google/cloud/gaming/v1/game_server_configs.pb.h>
#include <google/cloud/gaming/v1/game_server_clusters_service.pb.h>
#include <google/cloud/gaming/v1/game_server_deployments_service.pb.h>
#include <google/cloud/gaming/v1/realms.pb.h>
#include <google/cloud/domains/v1/domains.pb.h>
#include <google/cloud/tpu/v1/cloud_tpu.pb.h>
#include <google/cloud/automl/v1/text.pb.h>
#include <google/cloud/automl/v1/service.pb.h>
#include <google/cloud/automl/v1/text_segment.pb.h>
#include <google/cloud/automl/v1/operations.pb.h>
#include <google/cloud/automl/v1/data_items.pb.h>
#include <google/cloud/automl/v1/annotation_payload.pb.h>
#include <google/cloud/automl/v1/dataset.pb.h>
#include <google/cloud/automl/v1/detection.pb.h>
#include <google/cloud/automl/v1/io.pb.h>
#include <google/cloud/automl/v1/model_evaluation.pb.h>
#include <google/cloud/automl/v1/translation.pb.h>
#include <google/cloud/automl/v1/image.pb.h>
#include <google/cloud/automl/v1/annotation_spec.pb.h>
#include <google/cloud/automl/v1/classification.pb.h>
#include <google/cloud/automl/v1/text_extraction.pb.h>
#include <google/cloud/automl/v1/text_sentiment.pb.h>
#include <google/cloud/automl/v1/model.pb.h>
#include <google/cloud/automl/v1/geometry.pb.h>
#include <google/cloud/automl/v1/prediction_service.pb.h>
#include <google/cloud/websecurityscanner/v1/scan_config_error.pb.h>
#include <google/cloud/websecurityscanner/v1/finding_addon.pb.h>
#include <google/cloud/websecurityscanner/v1/crawled_url.pb.h>
#include <google/cloud/websecurityscanner/v1/scan_run_error_trace.pb.h>
#include <google/cloud/websecurityscanner/v1/scan_config.pb.h>
#include <google/cloud/websecurityscanner/v1/finding_type_stats.pb.h>
#include <google/cloud/websecurityscanner/v1/finding.pb.h>
#include <google/cloud/websecurityscanner/v1/scan_run.pb.h>
#include <google/cloud/websecurityscanner/v1/web_security_scanner.pb.h>
#include <google/cloud/websecurityscanner/v1/scan_run_warning_trace.pb.h>
#include <google/cloud/bigquery/connection/v1/connection.pb.h>
#include <google/cloud/bigquery/datatransfer/v1/transfer.pb.h>
#include <google/cloud/bigquery/datatransfer/v1/datatransfer.pb.h>
#include <google/cloud/bigquery/logging/v1/audit_data.pb.h>
#include <google/cloud/bigquery/v2/table_reference.pb.h>
#include <google/cloud/bigquery/v2/model_reference.pb.h>
#include <google/cloud/bigquery/v2/standard_sql.pb.h>
#include <google/cloud/bigquery/v2/encryption_config.pb.h>
#include <google/cloud/bigquery/v2/model.pb.h>
#include <google/cloud/bigquery/reservation/v1/reservation.pb.h>
#include <google/cloud/bigquery/dataexchange/common/common.pb.h>
#include <google/cloud/bigquery/dataexchange/v1beta1/dataexchange.pb.h>
#include <google/cloud/bigquery/storage/v1beta2/table.pb.h>
#include <google/cloud/bigquery/storage/v1beta2/arrow.pb.h>
#include <google/cloud/bigquery/storage/v1beta2/protobuf.pb.h>
#include <google/cloud/bigquery/storage/v1beta2/avro.pb.h>
#include <google/cloud/bigquery/storage/v1beta2/storage.pb.h>
#include <google/cloud/bigquery/storage/v1beta2/stream.pb.h>
#include <google/cloud/bigquery/storage/v1beta1/arrow.pb.h>
#include <google/cloud/bigquery/storage/v1beta1/table_reference.pb.h>
#include <google/cloud/bigquery/storage/v1beta1/avro.pb.h>
#include <google/cloud/bigquery/storage/v1beta1/read_options.pb.h>
#include <google/cloud/bigquery/storage/v1beta1/storage.pb.h>
#include <google/cloud/bigquery/storage/v1/table.pb.h>
#include <google/cloud/bigquery/storage/v1/arrow.pb.h>
#include <google/cloud/bigquery/storage/v1/protobuf.pb.h>
#include <google/cloud/bigquery/storage/v1/avro.pb.h>
#include <google/cloud/bigquery/storage/v1/storage.pb.h>
#include <google/cloud/bigquery/storage/v1/stream.pb.h>
#include <google/cloud/bigquery/migration/v2/migration_error_details.pb.h>
#include <google/cloud/bigquery/migration/v2/migration_metrics.pb.h>
#include <google/cloud/bigquery/migration/v2/migration_entities.pb.h>
#include <google/cloud/bigquery/migration/v2/migration_service.pb.h>
#include <google/cloud/bigquery/migration/v2/translation_config.pb.h>
#include <google/cloud/shell/v1/cloudshell.pb.h>
#include <google/cloud/networkanalyzer/logging/v1/analyzer_log.pb.h>
#include <google/cloud/securitycenter/v1/iam_binding.pb.h>
#include <google/cloud/securitycenter/v1/notification_message.pb.h>
#include <google/cloud/securitycenter/v1/access.pb.h>
#include <google/cloud/securitycenter/v1/mute_config.pb.h>
#include <google/cloud/securitycenter/v1/notification_config.pb.h>
#include <google/cloud/securitycenter/v1/securitycenter_service.pb.h>
#include <google/cloud/securitycenter/v1/contact_details.pb.h>
#include <google/cloud/securitycenter/v1/resource.pb.h>
#include <google/cloud/securitycenter/v1/indicator.pb.h>
#include <google/cloud/securitycenter/v1/file.pb.h>
#include <google/cloud/securitycenter/v1/source.pb.h>
#include <google/cloud/securitycenter/v1/finding.pb.h>
#include <google/cloud/securitycenter/v1/mitre_attack.pb.h>
#include <google/cloud/securitycenter/v1/process.pb.h>
#include <google/cloud/securitycenter/v1/organization_settings.pb.h>
#include <google/cloud/securitycenter/v1/connection.pb.h>
#include <google/cloud/securitycenter/v1/bigquery_export.pb.h>
#include <google/cloud/securitycenter/v1/compliance.pb.h>
#include <google/cloud/securitycenter/v1/vulnerability.pb.h>
#include <google/cloud/securitycenter/v1/asset.pb.h>
#include <google/cloud/securitycenter/v1/run_asset_discovery_response.pb.h>
#include <google/cloud/securitycenter/v1/external_system.pb.h>
#include <google/cloud/securitycenter/v1/security_marks.pb.h>
#include <google/cloud/securitycenter/v1/exfiltration.pb.h>
#include <google/cloud/securitycenter/v1/folder.pb.h>
#include <google/cloud/gkehub/v1alpha2/membership.pb.h>
#include <google/cloud/gkehub/v1beta1/membership.pb.h>
#include <google/cloud/gkehub/v1/service.pb.h>
#include <google/cloud/gkehub/v1/feature.pb.h>
#include <google/cloud/gkehub/v1/membership.pb.h>
#include <google/cloud/gkehub/v1/multiclusteringress/multiclusteringress.pb.h>
#include <google/cloud/gkehub/v1/configmanagement/configmanagement.pb.h>
#include <google/cloud/apigateway/v1/apigateway.pb.h>
#include <google/cloud/apigateway/v1/apigateway_service.pb.h>
#include <google/cloud/secretmanager/logging/v1/secret_event.pb.h>
#include <google/cloud/secretmanager/v1/service.pb.h>
#include <google/cloud/secretmanager/v1/resources.pb.h>
#include <google/cloud/channel/v1/service.pb.h>
#include <google/cloud/channel/v1/operations.pb.h>
#include <google/cloud/channel/v1/products.pb.h>
#include <google/cloud/channel/v1/offers.pb.h>
#include <google/cloud/channel/v1/subscriber_event.pb.h>
#include <google/cloud/channel/v1/common.pb.h>
#include <google/cloud/channel/v1/entitlements.pb.h>
#include <google/cloud/channel/v1/channel_partner_links.pb.h>
#include <google/cloud/channel/v1/customers.pb.h>
#include <google/cloud/channel/v1/repricing.pb.h>
#include <google/cloud/asset/v1/assets.pb.h>
#include <google/cloud/asset/v1/asset_service.pb.h>
#include <google/cloud/retail/v2alpha/completion_service.pb.h>
#include <google/cloud/retail/v2alpha/search_service.pb.h>
#include <google/cloud/retail/v2alpha/catalog_service.pb.h>
#include <google/cloud/retail/v2alpha/serving_config.pb.h>
#include <google/cloud/retail/v2alpha/common.pb.h>
#include <google/cloud/retail/v2alpha/serving_config_service.pb.h>
#include <google/cloud/retail/v2alpha/export_config.pb.h>
#include <google/cloud/retail/v2alpha/product_service.pb.h>
#include <google/cloud/retail/v2alpha/control_service.pb.h>
#include <google/cloud/retail/v2alpha/control.pb.h>
#include <google/cloud/retail/v2alpha/user_event_service.pb.h>
#include <google/cloud/retail/v2alpha/product.pb.h>
#include <google/cloud/retail/v2alpha/user_event.pb.h>
#include <google/cloud/retail/v2alpha/catalog.pb.h>
#include <google/cloud/retail/v2alpha/purge_config.pb.h>
#include <google/cloud/retail/v2alpha/import_config.pb.h>
#include <google/cloud/retail/v2alpha/promotion.pb.h>
#include <google/cloud/retail/v2alpha/prediction_service.pb.h>
#include <google/cloud/retail/v2/completion_service.pb.h>
#include <google/cloud/retail/v2/search_service.pb.h>
#include <google/cloud/retail/v2/catalog_service.pb.h>
#include <google/cloud/retail/v2/common.pb.h>
#include <google/cloud/retail/v2/product_service.pb.h>
#include <google/cloud/retail/v2/user_event_service.pb.h>
#include <google/cloud/retail/v2/product.pb.h>
#include <google/cloud/retail/v2/user_event.pb.h>
#include <google/cloud/retail/v2/catalog.pb.h>
#include <google/cloud/retail/v2/purge_config.pb.h>
#include <google/cloud/retail/v2/import_config.pb.h>
#include <google/cloud/retail/v2/promotion.pb.h>
#include <google/cloud/retail/v2/prediction_service.pb.h>
#include <google/cloud/retail/v2beta/completion_service.pb.h>
#include <google/cloud/retail/v2beta/search_service.pb.h>
#include <google/cloud/retail/v2beta/catalog_service.pb.h>
#include <google/cloud/retail/v2beta/serving_config.pb.h>
#include <google/cloud/retail/v2beta/common.pb.h>
#include <google/cloud/retail/v2beta/serving_config_service.pb.h>
#include <google/cloud/retail/v2beta/export_config.pb.h>
#include <google/cloud/retail/v2beta/product_service.pb.h>
#include <google/cloud/retail/v2beta/control_service.pb.h>
#include <google/cloud/retail/v2beta/control.pb.h>
#include <google/cloud/retail/v2beta/user_event_service.pb.h>
#include <google/cloud/retail/v2beta/product.pb.h>
#include <google/cloud/retail/v2beta/user_event.pb.h>
#include <google/cloud/retail/v2beta/catalog.pb.h>
#include <google/cloud/retail/v2beta/purge_config.pb.h>
#include <google/cloud/retail/v2beta/import_config.pb.h>
#include <google/cloud/retail/v2beta/promotion.pb.h>
#include <google/cloud/retail/v2beta/prediction_service.pb.h>
#include <google/cloud/run/v2/service.pb.h>
#include <google/cloud/run/v2/condition.pb.h>
#include <google/cloud/run/v2/vendor_settings.pb.h>
#include <google/cloud/run/v2/k8s.min.pb.h>
#include <google/cloud/run/v2/revision.pb.h>
#include <google/cloud/run/v2/traffic_target.pb.h>
#include <google/cloud/run/v2/revision_template.pb.h>
#include <google/cloud/videointelligence/v1/video_intelligence.pb.h>
#include <google/cloud/paymentgateway/issuerswitch/v1/common_fields.pb.h>
#include <google/cloud/paymentgateway/issuerswitch/v1/rules.pb.h>
#include <google/cloud/paymentgateway/issuerswitch/v1/transactions.pb.h>
#include <google/cloud/paymentgateway/issuerswitch/v1/resolutions.pb.h>
#include <google/cloud/gkeconnect/gateway/v1/gateway.pb.h>
#include <google/cloud/eventarc/publishing/v1/publisher.pb.h>
#include <google/cloud/eventarc/v1/channel.pb.h>
#include <google/cloud/eventarc/v1/eventarc.pb.h>
#include <google/cloud/eventarc/v1/trigger.pb.h>
#include <google/cloud/eventarc/v1/discovery.pb.h>
#include <google/cloud/eventarc/v1/channel_connection.pb.h>
#include <google/cloud/memcache/v1/cloud_memcache.pb.h>
#include <google/cloud/oslogin/common/common.pb.h>
#include <google/cloud/oslogin/v1/oslogin.pb.h>
#include <google/cloud/datacatalog/v1/gcs_fileset_spec.pb.h>
#include <google/cloud/datacatalog/v1/bigquery.pb.h>
#include <google/cloud/datacatalog/v1/datacatalog.pb.h>
#include <google/cloud/datacatalog/v1/timestamps.pb.h>
#include <google/cloud/datacatalog/v1/common.pb.h>
#include <google/cloud/datacatalog/v1/usage.pb.h>
#include <google/cloud/datacatalog/v1/dataplex_spec.pb.h>
#include <google/cloud/datacatalog/v1/schema.pb.h>
#include <google/cloud/datacatalog/v1/table_spec.pb.h>
#include <google/cloud/datacatalog/v1/policytagmanager.pb.h>
#include <google/cloud/datacatalog/v1/search.pb.h>
#include <google/cloud/datacatalog/v1/data_source.pb.h>
#include <google/cloud/datacatalog/v1/tags.pb.h>
#include <google/cloud/datacatalog/v1/policytagmanagerserialization.pb.h>
#include <google/cloud/datacatalog/v1/physical_schema.pb.h>
#include <google/cloud/datastream/v1/datastream.pb.h>
#include <google/cloud/datastream/v1/datastream_resources.pb.h>
#include <google/cloud/binaryauthorization/v1/service.pb.h>
#include <google/cloud/binaryauthorization/v1/resources.pb.h>
#include <google/cloud/vpcaccess/v1/vpc_access.pb.h>
#include <google/cloud/beyondcorp/clientgateways/v1/client_gateways_service.pb.h>
#include <google/cloud/beyondcorp/appconnections/v1/app_connections_service.pb.h>
#include <google/cloud/beyondcorp/appconnectors/v1/resource_info.pb.h>
#include <google/cloud/beyondcorp/appconnectors/v1/app_connectors_service.pb.h>
#include <google/cloud/beyondcorp/appconnectors/v1/app_connector_instance_config.pb.h>
#include <google/cloud/beyondcorp/appgateways/v1/app_gateways_service.pb.h>
#include <google/cloud/beyondcorp/clientconnectorservices/v1/client_connector_services_service.pb.h>
#include <google/cloud/webrisk/v1/webrisk.pb.h>
#include <google/cloud/optimization/v1/async_model.pb.h>
#include <google/cloud/optimization/v1/fleet_routing.pb.h>
#include <google/cloud/dialogflow/v2beta1/intent.pb.h>
#include <google/cloud/dialogflow/v2beta1/environment.pb.h>
#include <google/cloud/dialogflow/v2beta1/participant.pb.h>
#include <google/cloud/dialogflow/v2beta1/entity_type.pb.h>
#include <google/cloud/dialogflow/v2beta1/fulfillment.pb.h>
#include <google/cloud/dialogflow/v2beta1/conversation_profile.pb.h>
#include <google/cloud/dialogflow/v2beta1/gcs.pb.h>
#include <google/cloud/dialogflow/v2beta1/version.pb.h>
#include <google/cloud/dialogflow/v2beta1/human_agent_assistant_event.pb.h>
#include <google/cloud/dialogflow/v2beta1/knowledge_base.pb.h>
#include <google/cloud/dialogflow/v2beta1/conversation_event.pb.h>
#include <google/cloud/dialogflow/v2beta1/agent.pb.h>
#include <google/cloud/dialogflow/v2beta1/conversation.pb.h>
#include <google/cloud/dialogflow/v2beta1/session_entity_type.pb.h>
#include <google/cloud/dialogflow/v2beta1/session.pb.h>
#include <google/cloud/dialogflow/v2beta1/answer_record.pb.h>
#include <google/cloud/dialogflow/v2beta1/audio_config.pb.h>
#include <google/cloud/dialogflow/v2beta1/context.pb.h>
#include <google/cloud/dialogflow/v2beta1/validation_result.pb.h>
#include <google/cloud/dialogflow/v2beta1/document.pb.h>
#include <google/cloud/dialogflow/v2beta1/webhook.pb.h>
#include <google/cloud/dialogflow/v2/intent.pb.h>
#include <google/cloud/dialogflow/v2/conversation_model.pb.h>
#include <google/cloud/dialogflow/v2/environment.pb.h>
#include <google/cloud/dialogflow/v2/participant.pb.h>
#include <google/cloud/dialogflow/v2/entity_type.pb.h>
#include <google/cloud/dialogflow/v2/fulfillment.pb.h>
#include <google/cloud/dialogflow/v2/conversation_profile.pb.h>
#include <google/cloud/dialogflow/v2/gcs.pb.h>
#include <google/cloud/dialogflow/v2/version.pb.h>
#include <google/cloud/dialogflow/v2/human_agent_assistant_event.pb.h>
#include <google/cloud/dialogflow/v2/knowledge_base.pb.h>
#include <google/cloud/dialogflow/v2/conversation_event.pb.h>
#include <google/cloud/dialogflow/v2/agent.pb.h>
#include <google/cloud/dialogflow/v2/conversation.pb.h>
#include <google/cloud/dialogflow/v2/session_entity_type.pb.h>
#include <google/cloud/dialogflow/v2/session.pb.h>
#include <google/cloud/dialogflow/v2/answer_record.pb.h>
#include <google/cloud/dialogflow/v2/audio_config.pb.h>
#include <google/cloud/dialogflow/v2/conversation_dataset.pb.h>
#include <google/cloud/dialogflow/v2/context.pb.h>
#include <google/cloud/dialogflow/v2/validation_result.pb.h>
#include <google/cloud/dialogflow/v2/document.pb.h>
#include <google/cloud/dialogflow/v2/webhook.pb.h>
#include <google/cloud/dialogflow/cx/v3/validation_message.pb.h>
#include <google/cloud/dialogflow/cx/v3/transition_route_group.pb.h>
#include <google/cloud/dialogflow/cx/v3/intent.pb.h>
#include <google/cloud/dialogflow/cx/v3/test_case.pb.h>
#include <google/cloud/dialogflow/cx/v3/security_settings.pb.h>
#include <google/cloud/dialogflow/cx/v3/deployment.pb.h>
#include <google/cloud/dialogflow/cx/v3/environment.pb.h>
#include <google/cloud/dialogflow/cx/v3/entity_type.pb.h>
#include <google/cloud/dialogflow/cx/v3/fulfillment.pb.h>
#include <google/cloud/dialogflow/cx/v3/version.pb.h>
#include <google/cloud/dialogflow/cx/v3/response_message.pb.h>
#include <google/cloud/dialogflow/cx/v3/changelog.pb.h>
#include <google/cloud/dialogflow/cx/v3/agent.pb.h>
#include <google/cloud/dialogflow/cx/v3/session_entity_type.pb.h>
#include <google/cloud/dialogflow/cx/v3/session.pb.h>
#include <google/cloud/dialogflow/cx/v3/flow.pb.h>
#include <google/cloud/dialogflow/cx/v3/audio_config.pb.h>
#include <google/cloud/dialogflow/cx/v3/page.pb.h>
#include <google/cloud/dialogflow/cx/v3/advanced_settings.pb.h>
#include <google/cloud/dialogflow/cx/v3/experiment.pb.h>
#include <google/cloud/dialogflow/cx/v3/webhook.pb.h>
#include <google/cloud/dialogflow/cx/v3beta1/validation_message.pb.h>
#include <google/cloud/dialogflow/cx/v3beta1/transition_route_group.pb.h>
#include <google/cloud/dialogflow/cx/v3beta1/intent.pb.h>
#include <google/cloud/dialogflow/cx/v3beta1/test_case.pb.h>
#include <google/cloud/dialogflow/cx/v3beta1/security_settings.pb.h>
#include <google/cloud/dialogflow/cx/v3beta1/deployment.pb.h>
#include <google/cloud/dialogflow/cx/v3beta1/environment.pb.h>
#include <google/cloud/dialogflow/cx/v3beta1/entity_type.pb.h>
#include <google/cloud/dialogflow/cx/v3beta1/fulfillment.pb.h>
#include <google/cloud/dialogflow/cx/v3beta1/version.pb.h>
#include <google/cloud/dialogflow/cx/v3beta1/response_message.pb.h>
#include <google/cloud/dialogflow/cx/v3beta1/changelog.pb.h>
#include <google/cloud/dialogflow/cx/v3beta1/agent.pb.h>
#include <google/cloud/dialogflow/cx/v3beta1/session_entity_type.pb.h>
#include <google/cloud/dialogflow/cx/v3beta1/session.pb.h>
#include <google/cloud/dialogflow/cx/v3beta1/flow.pb.h>
#include <google/cloud/dialogflow/cx/v3beta1/audio_config.pb.h>
#include <google/cloud/dialogflow/cx/v3beta1/page.pb.h>
#include <google/cloud/dialogflow/cx/v3beta1/advanced_settings.pb.h>
#include <google/cloud/dialogflow/cx/v3beta1/experiment.pb.h>
#include <google/cloud/dialogflow/cx/v3beta1/webhook.pb.h>
#include <google/cloud/recommender/logging/v1/action_log.pb.h>
#include <google/cloud/recommender/v1beta1/recommender_config.pb.h>
#include <google/cloud/recommender/v1beta1/insight.pb.h>
#include <google/cloud/recommender/v1beta1/recommender_service.pb.h>
#include <google/cloud/recommender/v1beta1/recommendation.pb.h>
#include <google/cloud/recommender/v1beta1/insight_type_config.pb.h>
#include <google/cloud/recommender/v1/recommender_config.pb.h>
#include <google/cloud/recommender/v1/insight.pb.h>
#include <google/cloud/recommender/v1/recommender_service.pb.h>
#include <google/cloud/recommender/v1/recommendation.pb.h>
#include <google/cloud/recommender/v1/insight_type_config.pb.h>
#include <google/cloud/billing/v1/cloud_billing.pb.h>
#include <google/cloud/billing/v1/cloud_catalog.pb.h>
#include <google/cloud/billing/budgets/v1/budget_service.pb.h>
#include <google/cloud/billing/budgets/v1/budget_model.pb.h>
#include <google/cloud/servicedirectory/v1/service.pb.h>
#include <google/cloud/servicedirectory/v1/lookup_service.pb.h>
#include <google/cloud/servicedirectory/v1/endpoint.pb.h>
#include <google/cloud/servicedirectory/v1/namespace.pb.h>
#include <google/cloud/servicedirectory/v1/registration_service.pb.h>
#include <google/cloud/language/v1/language_service.pb.h>
#include <google/cloud/contactcenterinsights/v1/resources.pb.h>
#include <google/cloud/contactcenterinsights/v1/contact_center_insights.pb.h>
#include <google/cloud/dataplex/v1/service.pb.h>
#include <google/cloud/dataplex/v1/logs.pb.h>
#include <google/cloud/dataplex/v1/metadata.pb.h>
#include <google/cloud/dataplex/v1/resources.pb.h>
#include <google/cloud/dataplex/v1/tasks.pb.h>
#include <google/cloud/dataplex/v1/content.pb.h>
#include <google/cloud/dataplex/v1/analyze.pb.h>
#include <google/cloud/iot/v1/device_manager.pb.h>
#include <google/cloud/iot/v1/resources.pb.h>
#include <google/cloud/identitytoolkit/v2/authentication_service.pb.h>
#include <google/cloud/identitytoolkit/v2/mfa_info.pb.h>
#include <google/cloud/identitytoolkit/v2/account_management_service.pb.h>
#include <google/cloud/networkconnectivity/v1/common.pb.h>
#include <google/cloud/networkconnectivity/v1/hub.pb.h>
#include <google/devtools/build/v1/build_events.pb.h>
#include <google/devtools/build/v1/publish_build_event.pb.h>
#include <google/devtools/build/v1/build_status.pb.h>
#include <google/devtools/resultstore/v2/action.pb.h>
#include <google/devtools/resultstore/v2/file_processing_error.pb.h>
#include <google/devtools/resultstore/v2/resultstore_download.pb.h>
#include <google/devtools/resultstore/v2/configured_target.pb.h>
#include <google/devtools/resultstore/v2/common.pb.h>
#include <google/devtools/resultstore/v2/upload_metadata.pb.h>
#include <google/devtools/resultstore/v2/file_set.pb.h>
#include <google/devtools/resultstore/v2/coverage_summary.pb.h>
#include <google/devtools/resultstore/v2/configuration.pb.h>
#include <google/devtools/resultstore/v2/file.pb.h>
#include <google/devtools/resultstore/v2/resultstore_file_download.pb.h>
#include <google/devtools/resultstore/v2/coverage.pb.h>
#include <google/devtools/resultstore/v2/resultstore_upload.pb.h>
#include <google/devtools/resultstore/v2/target.pb.h>
#include <google/devtools/resultstore/v2/download_metadata.pb.h>
#include <google/devtools/resultstore/v2/test_suite.pb.h>
#include <google/devtools/resultstore/v2/invocation.pb.h>
#include <google/devtools/clouddebugger/v2/controller.pb.h>
#include <google/devtools/clouddebugger/v2/data.pb.h>
#include <google/devtools/clouddebugger/v2/debugger.pb.h>
#include <google/devtools/cloudbuild/v1/cloudbuild.pb.h>
#include <google/devtools/cloudprofiler/v2/profiler.pb.h>
#include <google/devtools/cloudtrace/v1/trace.pb.h>
#include <google/devtools/cloudtrace/v2/trace.pb.h>
#include <google/devtools/cloudtrace/v2/tracing.pb.h>
#include <google/devtools/artifactregistry/v1/service.pb.h>
#include <google/devtools/artifactregistry/v1/package.pb.h>
#include <google/devtools/artifactregistry/v1/version.pb.h>
#include <google/devtools/artifactregistry/v1/artifact.pb.h>
#include <google/devtools/artifactregistry/v1/tag.pb.h>
#include <google/devtools/artifactregistry/v1/file.pb.h>
#include <google/devtools/artifactregistry/v1/apt_artifact.pb.h>
#include <google/devtools/artifactregistry/v1/repository.pb.h>
#include <google/devtools/artifactregistry/v1/settings.pb.h>
#include <google/devtools/artifactregistry/v1/yum_artifact.pb.h>
#include <google/devtools/source/v1/source_context.pb.h>
#include <google/devtools/testing/v1/application_details.pb.h>
#include <google/devtools/testing/v1/test_environment_discovery.pb.h>
#include <google/devtools/testing/v1/test_execution.pb.h>
#include <google/devtools/containeranalysis/v1/containeranalysis.pb.h>
#include <google/example/library/v1/library.pb.h>
#include <google/streetview/publish/v1/streetview_publish.pb.h>
#include <google/streetview/publish/v1/rpcmessages.pb.h>
#include <google/streetview/publish/v1/resources.pb.h>
#include <google/privacy/dlp/v2/dlp.pb.h>
#include <google/privacy/dlp/v2/storage.pb.h>
#include <google/monitoring/dashboard/v1/xychart.pb.h>
#include <google/monitoring/dashboard/v1/text.pb.h>
#include <google/monitoring/dashboard/v1/table.pb.h>
#include <google/monitoring/dashboard/v1/service.pb.h>
#include <google/monitoring/dashboard/v1/layouts.pb.h>
#include <google/monitoring/dashboard/v1/table_display_options.pb.h>
#include <google/monitoring/dashboard/v1/common.pb.h>
#include <google/monitoring/dashboard/v1/alertchart.pb.h>
#include <google/monitoring/dashboard/v1/dashboards_service.pb.h>
#include <google/monitoring/dashboard/v1/metrics.pb.h>
#include <google/monitoring/dashboard/v1/logs_panel.pb.h>
#include <google/monitoring/dashboard/v1/dashboard_filter.pb.h>
#include <google/monitoring/dashboard/v1/collapsible_group.pb.h>
#include <google/monitoring/dashboard/v1/dashboard.pb.h>
#include <google/monitoring/dashboard/v1/widget.pb.h>
#include <google/monitoring/dashboard/v1/drilldowns.pb.h>
#include <google/monitoring/dashboard/v1/scorecard.pb.h>
#include <google/monitoring/v3/span_context.pb.h>
#include <google/monitoring/v3/alert_service.pb.h>
#include <google/monitoring/v3/uptime_service.pb.h>
#include <google/monitoring/v3/service.pb.h>
#include <google/monitoring/v3/group_service.pb.h>
#include <google/monitoring/v3/query_service.pb.h>
#include <google/monitoring/v3/notification.pb.h>
#include <google/monitoring/v3/metric.pb.h>
#include <google/monitoring/v3/dropped_labels.pb.h>
#include <google/monitoring/v3/alert.pb.h>
#include <google/monitoring/v3/uptime.pb.h>
#include <google/monitoring/v3/common.pb.h>
#include <google/monitoring/v3/notification_service.pb.h>
#include <google/monitoring/v3/metric_service.pb.h>
#include <google/monitoring/v3/service_service.pb.h>
#include <google/monitoring/v3/group.pb.h>
#include <google/monitoring/v3/mutation_record.pb.h>
#include <google/monitoring/metricsscope/v1/metrics_scope.pb.h>
#include <google/monitoring/metricsscope/v1/metrics_scopes.pb.h>
#include <google/dataflow/v1beta3/environment.pb.h>
#include <google/dataflow/v1beta3/jobs.pb.h>
#include <google/dataflow/v1beta3/snapshots.pb.h>
#include <google/dataflow/v1beta3/metrics.pb.h>
#include <google/dataflow/v1beta3/templates.pb.h>
#include <google/dataflow/v1beta3/messages.pb.h>
#include <google/dataflow/v1beta3/streaming.pb.h>
#include <google/geo/type/viewport.pb.h>
#include <google/api/field_behavior.pb.h>
#include <google/api/service.pb.h>
#include <google/api/routing.pb.h>
#include <google/api/annotations.pb.h>
#include <google/api/metric.pb.h>
#include <google/api/httpbody.pb.h>
#include <google/api/system_parameter.pb.h>
#include <google/api/consumer.pb.h>
#include <google/api/visibility.pb.h>
#include <google/api/endpoint.pb.h>
#include <google/api/distribution.pb.h>
#include <google/api/backend.pb.h>
#include <google/api/usage.pb.h>
#include <google/api/control.pb.h>
#include <google/api/source_info.pb.h>
#include <google/api/billing.pb.h>
#include <google/api/documentation.pb.h>
#include <google/api/monitored_resource.pb.h>
#include <google/api/resource.pb.h>
#include <google/api/launch_stage.pb.h>
#include <google/api/config_change.pb.h>
#include <google/api/quota.pb.h>
#include <google/api/client.pb.h>
#include <google/api/label.pb.h>
#include <google/api/context.pb.h>
#include <google/api/logging.pb.h>
#include <google/api/monitoring.pb.h>
#include <google/api/http.pb.h>
#include <google/api/auth.pb.h>
#include <google/api/log.pb.h>
#include <google/api/servicemanagement/v1/resources.pb.h>
#include <google/api/servicemanagement/v1/servicemanager.pb.h>
#include <google/api/servicecontrol/v1/service_controller.pb.h>
#include <google/api/servicecontrol/v1/check_error.pb.h>
#include <google/api/servicecontrol/v1/quota_controller.pb.h>
#include <google/api/servicecontrol/v1/distribution.pb.h>
#include <google/api/servicecontrol/v1/log_entry.pb.h>
#include <google/api/servicecontrol/v1/metric_value.pb.h>
#include <google/api/servicecontrol/v1/operation.pb.h>
#include <google/api/servicecontrol/v1/http_request.pb.h>
#include <google/api/servicecontrol/v2/service_controller.pb.h>
#include <google/api/expr/v1beta1/value.pb.h>
#include <google/api/expr/v1beta1/eval.pb.h>
#include <google/api/expr/v1beta1/decl.pb.h>
#include <google/api/expr/v1beta1/source.pb.h>
#include <google/api/expr/v1beta1/expr.pb.h>
#include <google/api/expr/conformance/v1alpha1/conformance_service.pb.h>
#include <google/api/expr/v1alpha1/value.pb.h>
#include <google/api/expr/v1alpha1/eval.pb.h>
#include <google/api/expr/v1alpha1/explain.pb.h>
#include <google/api/expr/v1alpha1/syntax.pb.h>
#include <google/api/expr/v1alpha1/checked.pb.h>
#include <google/api/serviceusage/v1/resources.pb.h>
#include <google/api/serviceusage/v1/serviceusage.pb.h>
#include <google/chromeos/uidetection/v1/ui_detection.pb.h>
#include <google/type/color.pb.h>
#include <google/type/latlng.pb.h>
#include <google/type/quaternion.pb.h>
#include <google/type/decimal.pb.h>
#include <google/type/timeofday.pb.h>
#include <google/type/phone_number.pb.h>
#include <google/type/calendar_period.pb.h>
#include <google/type/dayofweek.pb.h>
#include <google/type/date.pb.h>
#include <google/type/postal_address.pb.h>
#include <google/type/expr.pb.h>
#include <google/type/month.pb.h>
#include <google/type/fraction.pb.h>
#include <google/type/money.pb.h>
#include <google/type/datetime.pb.h>
#include <google/type/interval.pb.h>
#include <google/chat/logging/v1/chat_app_log_entry.pb.h>
#include <google/pubsub/v1/schema.pb.h>
#include <google/pubsub/v1/pubsub.pb.h>
#include <google/partner/aistreams/v1alpha1/aistreams.pb.h>
#include <google/maps/routing/v2/maneuver.pb.h>
#include <google/maps/routing/v2/speed_reading_interval.pb.h>
#include <google/maps/routing/v2/route_travel_mode.pb.h>
#include <google/maps/routing/v2/polyline.pb.h>
#include <google/maps/routing/v2/waypoint.pb.h>
#include <google/maps/routing/v2/location.pb.h>
#include <google/maps/routing/v2/fallback_info.pb.h>
#include <google/maps/routing/v2/toll_passes.pb.h>
#include <google/maps/routing/v2/routes_service.pb.h>
#include <google/maps/routing/v2/toll_info.pb.h>
#include <google/maps/routing/v2/vehicle_emission_type.pb.h>
#include <google/maps/routing/v2/units.pb.h>
#include <google/maps/routing/v2/vehicle_info.pb.h>
#include <google/maps/routing/v2/route.pb.h>
#include <google/maps/routing/v2/routing_preference.pb.h>
#include <google/maps/routing/v2/route_modifiers.pb.h>
#include <google/maps/routing/v2/navigation_instruction.pb.h>
#include <google/maps/routes/v1/compute_custom_routes_request.pb.h>
#include <google/maps/routes/v1/polyline.pb.h>
#include <google/maps/routes/v1/waypoint.pb.h>
#include <google/maps/routes/v1/fallback_info.pb.h>
#include <google/maps/routes/v1/toll_passes.pb.h>
#include <google/maps/routes/v1/compute_routes_request.pb.h>
#include <google/maps/routes/v1/route_matrix_element.pb.h>
#include <google/maps/routes/v1/vehicle_emission_type.pb.h>
#include <google/maps/routes/v1/route.pb.h>
#include <google/maps/routes/v1/compute_custom_routes_response.pb.h>
#include <google/maps/routes/v1/compute_routes_response.pb.h>
#include <google/maps/routes/v1/custom_route.pb.h>
#include <google/maps/routes/v1/compute_route_matrix_request.pb.h>
#include <google/maps/routes/v1/route_service.pb.h>
#include <google/maps/regionlookup/v1alpha/region_search_values.pb.h>
#include <google/maps/regionlookup/v1alpha/region_lookup_service.pb.h>
#include <google/maps/regionlookup/v1alpha/region_match.pb.h>
#include <google/maps/regionlookup/v1alpha/region_identifier.pb.h>
#include <google/maps/roads/v1op/roads.pb.h>
#include <google/iam/admin/v1/iam.pb.h>
#include <google/iam/admin/v1/audit_data.pb.h>
#include <google/iam/v1/iam_policy.pb.h>
#include <google/iam/v1/policy.pb.h>
#include <google/iam/v1/options.pb.h>
#include <google/iam/v1/logging/audit_data.pb.h>
#include <google/iam/v2beta/deny.pb.h>
#include <google/iam/v2beta/policy.pb.h>
#include <google/iam/credentials/v1/common.pb.h>
#include <google/iam/credentials/v1/iamcredentials.pb.h>
#include <google/networking/trafficdirector/type/traffic_director_log_entry.pb.h>
#include <google/logging/type/log_severity.pb.h>
#include <google/logging/type/http_request.pb.h>
#include <google/logging/v2/log_entry.pb.h>
#include <google/logging/v2/logging_metrics.pb.h>
#include <google/logging/v2/logging.pb.h>
#include <google/logging/v2/logging_config.pb.h>
#include <google/datastore/admin/v1/datastore_admin.pb.h>
#include <google/datastore/admin/v1/migration.pb.h>
#include <google/datastore/admin/v1/index.pb.h>
#include <google/datastore/v1/entity.pb.h>
#include <google/datastore/v1/datastore.pb.h>
#include <google/datastore/v1/query.pb.h>
#include <google/appengine/logging/v1/request_log.pb.h>
#include <google/appengine/v1/app_yaml.pb.h>
#include <google/appengine/v1/firewall.pb.h>
#include <google/appengine/v1/instance.pb.h>
#include <google/appengine/v1/service.pb.h>
#include <google/appengine/v1/certificate.pb.h>
#include <google/appengine/v1/domain_mapping.pb.h>
#include <google/appengine/v1/appengine.pb.h>
#include <google/appengine/v1/deployed_files.pb.h>
#include <google/appengine/v1/location.pb.h>
#include <google/appengine/v1/version.pb.h>
#include <google/appengine/v1/network_settings.pb.h>
#include <google/appengine/v1/audit_data.pb.h>
#include <google/appengine/v1/deploy.pb.h>
#include <google/appengine/v1/operation.pb.h>
#include <google/appengine/v1/application.pb.h>
#include <google/appengine/v1/domain.pb.h>
#include <google/appengine/legacy/audit_data.pb.h>
#include <google/actions/type/datetime_range.pb.h>
#include <google/actions/type/date_range.pb.h>
#include <google/identity/accesscontextmanager/type/device_resources.pb.h>
#include <google/identity/accesscontextmanager/v1/access_policy.pb.h>
#include <google/identity/accesscontextmanager/v1/access_context_manager.pb.h>
#include <google/identity/accesscontextmanager/v1/gcp_user_access_binding.pb.h>
#include <google/identity/accesscontextmanager/v1/access_level.pb.h>
#include <google/identity/accesscontextmanager/v1/service_perimeter.pb.h>
#include <google/bigtable/admin/v2/instance.pb.h>
#include <google/bigtable/admin/v2/table.pb.h>
#include <google/bigtable/admin/v2/bigtable_table_admin.pb.h>
#include <google/bigtable/admin/v2/common.pb.h>
#include <google/bigtable/admin/v2/bigtable_instance_admin.pb.h>
#include <google/bigtable/v2/data.pb.h>
#include <google/bigtable/v2/bigtable.pb.h>
#include <google/bigtable/v2/response_params.pb.h>
#include <google/firestore/admin/v1/index.pb.h>
#include <google/firestore/admin/v1/location.pb.h>
#include <google/firestore/admin/v1/operation.pb.h>
#include <google/firestore/admin/v1/database.pb.h>
#include <google/firestore/admin/v1/field.pb.h>
#include <google/firestore/admin/v1/firestore_admin.pb.h>
#include <google/firestore/v1/firestore.pb.h>
#include <google/firestore/v1/common.pb.h>
#include <google/firestore/v1/write.pb.h>
#include <google/firestore/v1/query.pb.h>
#include <google/firestore/v1/document.pb.h>
#include <google/firestore/bundle/bundle.pb.h>
#include <google/storage/v1/storage_resources.pb.h>
#include <google/storage/v1/storage.pb.h>
#include <google/storage/v2/storage.pb.h>
#include <google/longrunning/operations.pb.h>
#include <google/rpc/status.pb.h>
#include <google/rpc/code.pb.h>
#include <google/rpc/error_details.pb.h>
#include <google/rpc/context/attribute_context.pb.h>
#include <google/spanner/admin/instance/v1/spanner_instance_admin.pb.h>
#include <google/spanner/admin/database/v1/backup.pb.h>
#include <google/spanner/admin/database/v1/common.pb.h>
#include <google/spanner/admin/database/v1/spanner_database_admin.pb.h>
#include <google/spanner/v1/type.pb.h>
#include <google/spanner/v1/keys.pb.h>
#include <google/spanner/v1/transaction.pb.h>
#include <google/spanner/v1/commit_response.pb.h>
#include <google/spanner/v1/mutation.pb.h>
#include <google/spanner/v1/query_plan.pb.h>
#include <google/spanner/v1/result_set.pb.h>
#include <google/spanner/v1/spanner.pb.h>
#include <google/storagetransfer/v1/transfer.pb.h>
#include <google/storagetransfer/v1/transfer_types.pb.h>
#include <grafeas/v1/slsa_provenance.pb.h>
#include <grafeas/v1/intoto_statement.pb.h>
#include <grafeas/v1/provenance.pb.h>
#include <grafeas/v1/deployment.pb.h>
#include <grafeas/v1/upgrade.pb.h>
#include <grafeas/v1/attestation.pb.h>
#include <grafeas/v1/common.pb.h>
#include <grafeas/v1/package.pb.h>
#include <grafeas/v1/cvss.pb.h>
#include <grafeas/v1/grafeas.pb.h>
#include <grafeas/v1/build.pb.h>
#include <grafeas/v1/intoto_provenance.pb.h>
#include <grafeas/v1/discovery.pb.h>
#include <grafeas/v1/image.pb.h>
#include <grafeas/v1/compliance.pb.h>
#include <grafeas/v1/vulnerability.pb.h>
#include <grafeas/v1/severity.pb.h>
#include <grafeas/v1/slsa_provenance_zero_two.pb.h>
#include <grafeas/v1/dsse_attestation.pb.h>
```

<br>


---
---
Conan **1.58.0**. JFrog LTD. [https://conan.io](https://conan.io). Autogenerated 2023-02-05 20:12:53.