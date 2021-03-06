# Copyright 2020 Google LLC
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#      http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

if(APPLE AND NOT ANDROID)
  set(settings_apple_SRCS
      src/common/settings_ios.mm)
else()
  set(settings_apple_SRCS)
endif()

set(common_SRCS
    src/common/cleanup.h
    src/common/collection_reference.cc
    src/common/compiler_info.cc
    src/common/compiler_info.h
    src/common/document_change.cc
    src/common/document_reference.cc
    src/common/document_snapshot.cc
    src/common/exception_common.cc
    src/common/exception_common.h
    src/common/field_path.cc
    src/common/field_value.cc
    src/common/firestore.cc
    src/common/futures.cc
    src/common/futures.h
    src/common/listener_registration.cc
    src/common/macros.h
    src/common/main_for_testing_build.cc
    src/common/query.cc
    src/common/query_snapshot.cc
    src/common/set_options.cc
    src/common/settings.cc
    src/common/snapshot_metadata.cc
    src/common/to_string.cc
    src/common/to_string.h
    src/common/type_mapping.h
    src/common/transaction.cc
    src/common/util.cc
    src/common/util.h
    src/common/write_batch.cc
    ${settings_apple_SRCS})

# Define the resource build needed for Android
firebase_cpp_gradle(":firestore:firestore_resources:generateDexJarRelease"
    "${CMAKE_CURRENT_LIST_DIR}/firestore_resources/build/dexed.jar")
binary_to_array("firestore_resources"
    "${CMAKE_CURRENT_LIST_DIR}/firestore_resources/build/dexed.jar"
    "firebase_firestore"
    "${FIREBASE_GEN_FILE_DIR}/firestore")

set(android_SRCS
    ${firestore_resources_source}
    src/android/blob_android.cc
    src/android/blob_android.h
    src/android/collection_reference_android.cc
    src/android/collection_reference_android.h
    src/android/direction_android.cc
    src/android/direction_android.h
    src/android/document_change_android.cc
    src/android/document_change_android.h
    src/android/document_change_type_android.cc
    src/android/document_change_type_android.h
    src/android/document_reference_android.cc
    src/android/document_reference_android.h
    src/android/document_snapshot_android.cc
    src/android/document_snapshot_android.h
    src/android/event_listener_android.cc
    src/android/event_listener_android.h
    src/android/exception_android.cc
    src/android/exception_android.h
    src/android/field_path_android.cc
    src/android/field_path_android.h
    src/android/field_path_portable.cc
    src/android/field_path_portable.h
    src/android/field_value_android.cc
    src/android/field_value_android.h
    src/android/firestore_android.cc
    src/android/firestore_android.h
    src/android/firestore_exceptions_android.h
    src/android/geo_point_android.cc
    src/android/geo_point_android.h
    src/android/geo_point_portable.cc
    src/android/lambda_event_listener.h
    src/android/lambda_transaction_function.h
    src/android/listener_registration_android.cc
    src/android/listener_registration_android.h
    src/android/metadata_changes_android.cc
    src/android/metadata_changes_android.h
    src/android/promise_android.h
    src/android/promise_factory_android.h
    src/android/query_android.cc
    src/android/query_android.h
    src/android/query_snapshot_android.cc
    src/android/query_snapshot_android.h
    src/android/server_timestamp_behavior_android.cc
    src/android/server_timestamp_behavior_android.h
    src/android/set_options_android.cc
    src/android/set_options_android.h
    src/android/settings_android.cc
    src/android/settings_android.h
    src/android/snapshot_metadata_android.cc
    src/android/snapshot_metadata_android.h
    src/android/source_android.cc
    src/android/source_android.h
    src/android/timestamp_android.cc
    src/android/timestamp_android.h
    src/android/timestamp_portable.cc
    src/android/transaction_android.cc
    src/android/transaction_android.h
    src/android/util_android.cc
    src/android/util_android.h
    src/android/wrapper.cc
    src/android/wrapper.h
    src/android/write_batch_android.cc
    src/android/write_batch_android.h
    src/jni/array.h
    src/jni/array_list.cc
    src/jni/array_list.h
    src/jni/boolean.cc
    src/jni/boolean.h
    src/jni/call_traits.h
    src/jni/class.cc
    src/jni/class.h
    src/jni/collection.cc
    src/jni/collection.h
    src/jni/declaration.h
    src/jni/double.cc
    src/jni/double.h
    src/jni/env.cc
    src/jni/env.h
    src/jni/hash_map.cc
    src/jni/hash_map.h
    src/jni/integer.cc
    src/jni/integer.h
    src/jni/iterator.cc
    src/jni/iterator.h
    src/jni/jni.cc
    src/jni/jni.h
    src/jni/jni_fwd.h
    src/jni/list.cc
    src/jni/list.h
    src/jni/loader.cc
    src/jni/loader.h
    src/jni/long.cc
    src/jni/long.h
    src/jni/map.cc
    src/jni/map.h
    src/jni/object.cc
    src/jni/object.h
    src/jni/ownership.h
    src/jni/set.h
    src/jni/string.cc
    src/jni/string.h
    src/jni/task.cc
    src/jni/task.h
    src/jni/throwable.cc
    src/jni/throwable.h
    src/jni/traits.h)

# Sources that apply to all non-Android platforms.
set(main_SRCS
    src/ios/collection_reference_ios.cc
    src/ios/collection_reference_ios.h
    src/ios/converter_ios.h
    src/ios/document_change_ios.cc
    src/ios/document_change_ios.h
    src/ios/document_reference_ios.cc
    src/ios/document_reference_ios.h
    src/ios/document_snapshot_ios.cc
    src/ios/document_snapshot_ios.h
    src/ios/field_value_ios.cc
    src/ios/field_value_ios.h
    src/ios/firestore_ios.cc
    src/ios/firestore_ios.h
    src/ios/hard_assert_ios.cc
    src/ios/hard_assert_ios.h
    src/ios/listener_ios.h
    src/ios/listener_registration_ios.cc
    src/ios/listener_registration_ios.h
    src/ios/promise_factory_ios.h
    src/ios/promise_ios.h
    src/ios/query_ios.cc
    src/ios/query_ios.h
    src/ios/query_snapshot_ios.cc
    src/ios/query_snapshot_ios.h
    src/ios/set_options_ios.h
    src/ios/source_ios.h
    src/ios/transaction_ios.cc
    src/ios/transaction_ios.h
    src/ios/user_data_converter_ios.cc
    src/ios/user_data_converter_ios.h
    src/ios/util_ios.h
    src/ios/write_batch_ios.cc
    src/ios/write_batch_ios.h)

# CredentialsProvider has no implementatation on Android and distinct
# implementations for iOS and desktop platforms. On iOS, the implementation of
# the interface actually comes from the FirebaseFirestore CocoaPod, so there's
# no implementation listed here.
set(credentials_provider_desktop_SRCS
    src/ios/create_credentials_provider.h
    src/ios/create_credentials_provider_desktop.cc
    src/ios/credentials_provider_desktop.cc
    src/ios/credentials_provider_desktop.h)

set(credentials_provider_ios_SRCS
    src/ios/create_credentials_provider.h
    src/ios/create_credentials_provider_ios.mm)

# FirebaseMetadataProvider has no implementation on Android and distinct
# implementations for iOS and desktop platforms. On iOS, the implementation of
# the interface actually comes from the FirebaseFirestore CocoaPod, so there's
# no implementation listed here.
set(firebase_metadata_provider_desktop_SRCS
    src/ios/create_firebase_metadata_provider.h
    src/ios/create_firebase_metadata_provider_desktop.cc
    src/ios/firebase_metadata_provider_desktop.cc
    src/ios/firebase_metadata_provider_desktop.h)

set(firebase_metadata_provider_ios_SRCS
    src/ios/create_firebase_metadata_provider.h
    src/ios/create_firebase_metadata_provider_apple.mm)

set(wrapper_assertions_SRCS
    src/common/wrapper_assertions.cc
    src/common/wrapper_assertions.h)

set(ios_only_SRCS
    src/ios/create_firebase_metadata_provider_apple.mm)

set(desktop_only_SRCS
    src/ios/create_firebase_metadata_provider_desktop.cc
    src/ios/firebase_metadata_provider_desktop.cc)

if(ANDROID)
  set(firestore_platform_SRCS "${android_SRCS}")

elseif(IOS)
  set(firestore_platform_SRCS
      "${main_SRCS}"
      "${credentials_provider_ios_SRCS}"
      "${firebase_metadata_provider_ios_SRCS}")

else()
  set(firestore_platform_SRCS
      "${main_SRCS}"
      "${credentials_provider_desktop_SRCS}"
      "${firebase_metadata_provider_desktop_SRCS}")
endif()

add_library(firebase_firestore STATIC
    ${common_SRCS}
    ${firestore_platform_SRCS})

set_property(TARGET firebase_firestore PROPERTY FOLDER "Firebase Cpp")

# Set up the dependency on Firebase App.
target_link_libraries(firebase_firestore
  PUBLIC
    firebase_app
    firebase_auth
)

if(FIRESTORE_USE_EXTERNAL_CMAKE_BUILD)
  target_link_libraries(firebase_firestore
    PRIVATE
      firestore_core
      absl_variant
  )
endif()

# Public C++ headers all refer to each other relative to the src/include
# directory, while private headers are relative to the entire C++ SDK
# directory.
target_include_directories(firebase_firestore
  PUBLIC
    ${CMAKE_CURRENT_LIST_DIR}/src/include
  PRIVATE
    ${FIREBASE_CPP_SDK_ROOT_DIR}
)

# Additional public headers come from the Firestore core
if(IOS)
  target_include_directories(firebase_firestore
    PUBLIC
      # The Firestore core on iOS comes via the FirebaseFirestore CocoaPod, and
      # public headers should come from there.
      ${FIREBASE_POD_DIR}/Pods/FirebaseFirestore/Firestore/core/include
    PRIVATE
      # Additionally, the core C++ API is not declared publicly within the
      # FirebaseFirestore pod, so depend on headers available in the source
      # distribution.
      ${FIREBASE_POD_DIR}/Pods/FirebaseFirestore
  )

else()
  # Desktop and Android get their public headers from the CMake build in
  # firebase-ios-sdk.
  target_include_directories(firebase_firestore
    PUBLIC
      ${FIRESTORE_SOURCE_DIR}/Firestore/core/include
    PRIVATE
      ${FIRESTORE_SOURCE_DIR}
  )
endif()

set(FIREBASE_FIRESTORE_CPP_DEFINES -DINTERNAL_EXPERIMENTAL=1)

if (WIN32 AND NOT ANDROID AND NOT IOS)
  # On Windows, gRPC gives a compiler error in firebase_metadata_provider_desktop.cc
  # unless _WIN32_WINNT is defined to this value (0x0600, Windows Vista).
  set(FIREBASE_FIRESTORE_CPP_DEFINES ${FIREBASE_FIRESTORE_CPP_DEFINES} -D_WIN32_WINNT=0x0600)
endif()

target_compile_definitions(firebase_firestore
  PRIVATE
    ${FIREBASE_FIRESTORE_CPP_DEFINES}
)

if(ANDROID)
  firebase_cpp_proguard_file(firestore)

elseif(IOS)
  # Enable Automatic Reference Counting (ARC) and Bitcode.
  target_compile_options(firebase_firestore
                         PUBLIC "-fobjc-arc" "-fembed-bitcode")
  target_link_libraries(firebase_firestore
                        PUBLIC "-fembed-bitcode")

  setup_pod_headers(
    firebase_firestore
    INCLUDE_PRIVATE_HEADERS
    POD_NAMES
      FirebaseCore
      FirebaseFirestore
      abseil
      nanopb
      gRPC-C++
      gRPC-Core
  )

  if (FIREBASE_XCODE_TARGET_FORMAT STREQUAL "frameworks")
    set_target_properties(firebase_firestore PROPERTIES
      FRAMEWORK TRUE
    )
  endif()
endif()

cpp_pack_library(firebase_firestore "")
cpp_pack_public_headers()
