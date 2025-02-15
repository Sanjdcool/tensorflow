load("//tensorflow:tensorflow.bzl", "tf_cc_test")

# Snappy targets.

load(
    "//tensorflow/core/platform:rules_cc.bzl",
    "cc_library",
)

package(
    default_visibility = [
        "//tensorflow/core/lib/io:__pkg__",
        "//tensorflow/tsl/lib/io:__pkg__",
    ],
    licenses = ["notice"],
)

exports_files([
    "snappy_compression_options.h",
    "snappy_inputbuffer.h",
    "snappy_inputstream.h",
    "snappy_outputbuffer.h",
    "snappy_inputstream.cc",
    "snappy_test.cc",
])

cc_library(
    name = "snappy_inputbuffer",
    srcs = ["snappy_inputbuffer.cc"],
    hdrs = ["snappy_inputbuffer.h"],
    deps = [
        "//tensorflow/tsl/lib/io:inputstream_interface",
        "//tensorflow/tsl/platform:env",
        "//tensorflow/tsl/platform:macros",
        "//tensorflow/tsl/platform:platform_port",
        "//tensorflow/tsl/platform:status",
        "//tensorflow/tsl/platform:types",
    ],
    alwayslink = True,
)

cc_library(
    name = "snappy_outputbuffer",
    srcs = ["snappy_outputbuffer.cc"],
    hdrs = ["snappy_outputbuffer.h"],
    deps = [
        "//tensorflow/tsl/platform",
        "//tensorflow/tsl/platform:env",
        "//tensorflow/tsl/platform:macros",
        "//tensorflow/tsl/platform:platform_port",
        "//tensorflow/tsl/platform:status",
        "//tensorflow/tsl/platform:types",
    ],
    alwayslink = True,
)

cc_library(
    name = "snappy_inputstream",
    srcs = ["snappy_inputstream.cc"],
    hdrs = ["snappy_inputstream.h"],
    deps = [
        "//tensorflow/tsl/lib/io:inputstream_interface",
        "//tensorflow/tsl/platform:errors",
        "//tensorflow/tsl/platform:platform_port",
        "@com_google_absl//absl/memory",
    ],
    alwayslink = True,
)

cc_library(
    name = "snappy_compression_options",
    hdrs = ["snappy_compression_options.h"],
    deps = [
        "//tensorflow/tsl/platform:types",
    ],
    alwayslink = True,
)

tf_cc_test(
    name = "snappy_test",
    size = "small",
    srcs = ["snappy_test.cc"],
    deps = [
        ":snappy_inputbuffer",
        ":snappy_inputstream",
        ":snappy_outputbuffer",
        "//tensorflow/tsl/lib/core:status_test_util",
        "//tensorflow/tsl/lib/io:inputbuffer",
        "//tensorflow/tsl/lib/io:random_inputstream",
        "//tensorflow/tsl/platform:env",
        "//tensorflow/tsl/platform:env_impl",
        "//tensorflow/tsl/platform:test",
        "//tensorflow/tsl/platform:test_main",
    ],
)
