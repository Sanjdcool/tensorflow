# Description:
#    Libraries for helping construct LLVM IR for XLA backends.

load("//tensorflow:tensorflow.bzl", "filegroup")
load("//tensorflow/core/platform:rules_cc.bzl", "cc_library")
load(
    "//tensorflow:tensorflow.bzl",
    "tf_cc_test",
)

package(
    default_visibility = [":friends"],
    licenses = ["notice"],
)

package_group(
    name = "friends",
    includes = [
        "//tensorflow/compiler/xla:friends",
    ],
)

# Filegroup used to collect source files for dependency checking.
filegroup(
    name = "c_srcs",
    data = glob([
        "**/*.cc",
        "**/*.h",
    ]),
)

cc_library(
    name = "alias_analysis",
    srcs = ["alias_analysis.cc"],
    hdrs = ["alias_analysis.h"],
    deps = [
        ":ir_array",
        ":llvm_type_conversion_util",
        "//tensorflow/compiler/xla:types",
        "//tensorflow/compiler/xla/service:buffer_assignment",
        "//tensorflow/compiler/xla/service:hlo",
        "//tensorflow/compiler/xla/service:logical_buffer",
        "//tensorflow/core:lib",
        "//tensorflow/tsl/platform:logging",
        "@com_google_absl//absl/container:flat_hash_map",
        "@com_google_absl//absl/container:flat_hash_set",
        "@com_google_absl//absl/strings",
        "@llvm-project//llvm:Core",
    ],
)

tf_cc_test(
    name = "alias_analysis_test",
    srcs = ["alias_analysis_test.cc"],
    deps = [
        ":alias_analysis",
        "//tensorflow/compiler/xla/service:custom_call_status_public_headers",
        "//tensorflow/compiler/xla/service:custom_call_target_registry",
        "//tensorflow/compiler/xla/service:hlo_parser",
        "//tensorflow/compiler/xla/service/cpu/tests:cpu_codegen_test",
        "//tensorflow/compiler/xla/tests:filecheck",
        "//tensorflow/core:test",
    ],
)

cc_library(
    name = "llvm_util",
    srcs = ["llvm_util.cc"],
    hdrs = ["llvm_util.h"],
    deps = [
        ":llvm_type_conversion_util",
        "//tensorflow/compiler/xla:debug_options_flags",
        "//tensorflow/compiler/xla:literal",
        "//tensorflow/compiler/xla:shape_util",
        "//tensorflow/compiler/xla:types",
        "//tensorflow/compiler/xla:util",
        "//tensorflow/compiler/xla:xla_data_proto_cc",
        "//tensorflow/compiler/xla/service:dump",
        "//tensorflow/compiler/xla/service:hlo",
        "//tensorflow/compiler/xla/service:hlo_module_config",
        "//tensorflow/compiler/xla/service:name_uniquer",
        "//tensorflow/compiler/xla/service/cpu:cpu_options",
        "//tensorflow/core:lib",
        "//tensorflow/tsl/platform:logging",
        "@com_google_absl//absl/base",
        "@com_google_absl//absl/strings",
        "@com_google_absl//absl/types:span",
        "@llvm-project//llvm:Core",
        "@llvm-project//llvm:Support",
        "@llvm-project//llvm:Target",
        "@llvm-project//llvm:TransformUtils",
        "@llvm-project//mlir:IR",
    ],
)

cc_library(
    name = "llvm_type_conversion_util",
    hdrs = ["llvm_type_conversion_util.h"],
    deps = [
        "@com_google_absl//absl/strings",
        "@com_google_absl//absl/types:span",
        "@llvm-project//llvm:Support",
    ],
)

cc_library(
    name = "llvm_command_line_options",
    hdrs = ["llvm_command_line_options.h"],
    deps = [
        "//tensorflow/tsl/platform:logging",
        "@com_google_absl//absl/strings",
        "@llvm-project//llvm:Support",
    ],
)

cc_library(
    name = "ir_array",
    srcs = ["ir_array.cc"],
    hdrs = ["ir_array.h"],
    deps = [
        ":llvm_type_conversion_util",
        ":llvm_util",
        "//tensorflow/compiler/xla:permutation_util",
        "//tensorflow/compiler/xla:shape_util",
        "//tensorflow/compiler/xla:statusor",
        "//tensorflow/compiler/xla:types",
        "//tensorflow/compiler/xla:util",
        "//tensorflow/compiler/xla:xla_data_proto_cc",
        "//tensorflow/core:lib",
        "//tensorflow/tsl/platform:logging",
        "@com_google_absl//absl/algorithm:container",
        "@com_google_absl//absl/strings",
        "@com_google_absl//absl/types:span",
        "@llvm-project//llvm:Core",
    ],
)

cc_library(
    name = "llvm_loop",
    srcs = ["llvm_loop.cc"],
    hdrs = ["llvm_loop.h"],
    deps = [
        ":ir_array",
        ":llvm_util",
        "//tensorflow/compiler/xla:shape_util",
        "//tensorflow/compiler/xla:types",
        "//tensorflow/compiler/xla:xla_data_proto_cc",
        "//tensorflow/core:lib",
        "//tensorflow/tsl/platform:logging",
        "@com_google_absl//absl/algorithm:container",
        "@com_google_absl//absl/strings",
        "@com_google_absl//absl/types:span",
        "@llvm-project//llvm:Core",
    ],
)

cc_library(
    name = "loop_emitter",
    srcs = ["loop_emitter.cc"],
    hdrs = ["loop_emitter.h"],
    deps = [
        ":ir_array",
        ":llvm_loop",
        "//tensorflow/compiler/xla:shape_util",
        "//tensorflow/compiler/xla:status_macros",
        "//tensorflow/compiler/xla:statusor",
        "//tensorflow/compiler/xla:types",
        "//tensorflow/compiler/xla:xla_data_proto_cc",
        "//tensorflow/core:lib",
        "//tensorflow/tsl/platform:logging",
        "@com_google_absl//absl/strings:str_format",
        "@llvm-project//llvm:Core",
    ],
)

cc_library(
    name = "fused_ir_emitter",
    srcs = ["fused_ir_emitter.cc"],
    hdrs = ["fused_ir_emitter.h"],
    deps = [
        ":ir_array",
        ":llvm_util",
        ":tuple_ops",
        "//tensorflow/compiler/xla:shape_util",
        "//tensorflow/compiler/xla:status_macros",
        "//tensorflow/compiler/xla:statusor",
        "//tensorflow/compiler/xla:util",
        "//tensorflow/compiler/xla/service:elemental_ir_emitter",
        "//tensorflow/compiler/xla/service:fusion_node_indexing_evaluation",
        "//tensorflow/compiler/xla/service:hlo",
        "//tensorflow/core:lib",
        "//tensorflow/tsl/platform:logging",
        "@com_google_absl//absl/container:flat_hash_map",
        "@llvm-project//llvm:Core",
    ],
)

cc_library(
    name = "dynamic_update_slice_util",
    srcs = ["dynamic_update_slice_util.cc"],
    hdrs = ["dynamic_update_slice_util.h"],
    deps = [
        ":fused_ir_emitter",
        ":ir_array",
        ":llvm_util",
        ":loop_emitter",
        "//tensorflow/compiler/xla/service:buffer_assignment",
        "//tensorflow/compiler/xla/service:elemental_ir_emitter",
        "//tensorflow/compiler/xla/service:hlo",
        "//tensorflow/compiler/xla/service/cpu:backend_config_proto_cc",
        "//tensorflow/compiler/xla/service/gpu:launch_dimensions",
        "//tensorflow/compiler/xla/service/gpu:parallel_loop_emitter",
    ],
)

cc_library(
    name = "sort_util",
    srcs = ["sort_util.cc"],
    hdrs = ["sort_util.h"],
    deps = [
        ":ir_array",
        ":kernel_support_library",
        ":llvm_loop",
        ":llvm_util",
        ":loop_emitter",
        "//tensorflow/compiler/xla:shape_util",
        "//tensorflow/compiler/xla:util",
        "//tensorflow/compiler/xla/service/gpu:launch_dimensions",
        "//tensorflow/compiler/xla/service/gpu:parallel_loop_emitter",
        "//tensorflow/compiler/xla/service/gpu:target_util",
        "//tensorflow/tsl/platform:status",
        "@com_google_absl//absl/strings",
        "@com_google_absl//absl/types:span",
        "@llvm-project//llvm:Core",
        "@llvm-project//llvm:Support",
    ],
)

cc_library(
    name = "tuple_ops",
    srcs = ["tuple_ops.cc"],
    hdrs = ["tuple_ops.h"],
    deps = [
        ":ir_array",
        ":llvm_type_conversion_util",
        ":llvm_util",
        "//tensorflow/compiler/xla:shape_util",
        "//tensorflow/compiler/xla:types",
        "//tensorflow/compiler/xla:xla_data_proto_cc",
        "//tensorflow/core:lib",
        "//tensorflow/tsl/platform:logging",
        "@com_google_absl//absl/types:span",
        "@llvm-project//llvm:Core",
    ],
)

cc_library(
    name = "kernel_support_library",
    srcs = ["kernel_support_library.cc"],
    hdrs = ["kernel_support_library.h"],
    deps = [
        ":llvm_loop",
        ":llvm_type_conversion_util",
        ":llvm_util",
        "@com_google_absl//absl/strings",
        "@llvm-project//llvm:Core",
    ],
)

cc_library(
    name = "buffer_assignment_util",
    srcs = ["buffer_assignment_util.cc"],
    hdrs = ["buffer_assignment_util.h"],
    deps = [
        "//tensorflow/compiler/xla/service:buffer_assignment",
        "@com_google_absl//absl/strings",
    ],
)

cc_library(
    name = "math_ops",
    srcs = ["math_ops.cc"],
    hdrs = ["math_ops.h"],
    deps = [
        ":llvm_util",
        "@llvm-project//llvm:Core",
    ],
)

cc_library(
    name = "ir_builder_mixin",
    srcs = [],
    hdrs = ["ir_builder_mixin.h"],
    deps = [
        "@llvm-project//llvm:Core",
    ],
)

tf_cc_test(
    name = "ir_array_test",
    srcs = ["ir_array_test.cc"],
    deps = [
        ":ir_array",
        "//tensorflow/compiler/xla:test",
        "//tensorflow/compiler/xla/tests:xla_internal_test_main",
    ],
)
