java_library(
    name = "testutil",
    srcs = glob(["com/google/devtools/build/lib/testutil/*.java"]),
    visibility = ["//visibility:public"],
    deps = [
        "//src/main/java:actions",
        "//src/main/java:analysis-exec-rules-skyframe",
        "//src/main/java:bazel-core",
        "//src/main/java:collect",
        "//src/main/java:events",
        "//src/main/java:packages",
        "//src/main/java:vfs",
        "//third_party:guava",
        "//third_party:guava-testlib",
        "//third_party:junit4",
        "//third_party:truth",
    ],
)

java_test(
    name = "skyframe_test",
    srcs = glob([
        "com/google/devtools/build/skyframe/*.java",
    ]),
    args = ["com.google.devtools.build.skyframe.AllTests"],
    tags = ["skyframe"],
    deps = [
        ":testutil",
        "//src/main/java:bazel-core",
        "//src/main/java:collect",
        "//src/main/java:concurrent",
        "//src/main/java:events",
        "//src/main/java:skyframe-base",
        "//src/main/java:vfs",
        "//third_party:guava",
        "//third_party:guava-testlib",
        "//third_party:jsr305",
        "//third_party:junit4",
        "//third_party:truth",
    ],
)

java_test(
    name = "options_test",
    srcs = glob(["com/google/devtools/common/options/*.java"]),
    args = ["com.google.devtools.common.options.AllTests"],
    deps = [
        "//src/main/java:options",
        "//src/test/java:testutil",
        "//third_party:guava",
        "//third_party:jsr305",
        "//third_party:junit4",
        "//third_party:truth",
    ],
)

test_prefix = "com/google/devtools/build/lib"

java_library(
    name = "foundations_testutil",
    srcs = glob([
        "com/google/devtools/build/lib/vfs/util/*.java",
        "com/google/devtools/build/lib/events/util/*.java",
    ]),
    data = [
        "//src/main/native:libunix.dylib",
        "//src/main/native:libunix.so",
    ],
    deps = [
        ":testutil",
        "//src/main/java:bazel-core",
        "//src/main/java:concurrent",
        "//src/main/java:events",
        "//src/main/java:packages",
        "//src/main/java:shell",
        "//src/main/java:vfs",
        "//third_party:guava",
        "//third_party:guava-testlib",
        "//third_party:junit4",
        "//third_party:truth",
    ],
)

java_library(
    name = "test_runner",
    srcs = [test_prefix + "/AllTests.java"],
    deps = [
        ":testutil",
        "//third_party:junit4",
    ],
)

java_test(
    name = "foundations_test",
    srcs = glob(
        ["%s/%s" % (test_prefix, p) for p in [
            "concurrent/*.java",
            "collect/*.java",
            "collect/nestedset/*.java",
            "events/*.java",
            "testutiltests/*.java",
            "unix/*.java",
            "util/*.java",
            "util/io/*.java",
            "vfs/*.java",
            "vfs/inmemoryfs/*.java",
        ]],
        # java_rules_skylark doesn't support resource loading with
        # qualified paths.
        exclude = [
            test_prefix + f
            for f in [
                "/util/DependencySetWindowsTest.java",
                "/util/ResourceFileLoaderTest.java",
                "/vfs/PathFragmentWindowsTest.java",
                "/vfs/PathWindowsTest.java",
            ]
        ],
    ),
    args = ["com.google.devtools.build.lib.AllTests"],
    data = glob([test_prefix + "/vfs/*.zip"]),
    tags = ["foundations"],
    deps = [
        ":foundations_testutil",
        ":test_runner",
        ":testutil",
        "//src/main/java:bazel-core",
        "//src/main/java:collect",
        "//src/main/java:concurrent",
        "//src/main/java:events",
        "//src/main/java:options",
        "//src/main/java:packages",
        "//src/main/java:shell",
        "//src/main/java:unix",
        "//src/main/java:vfs",
        "//third_party:guava",
        "//third_party:guava-testlib",
        "//third_party:junit4",
        "//third_party:truth",
    ],
)

java_test(
    name = "windows_test",
    srcs = glob(["%s/%s" % (test_prefix, p) for p in [
        "util/DependencySetWindowsTest.java",
        "vfs/PathFragmentWindowsTest.java",
        "vfs/PathWindowsTest.java",
    ]]),
    args = [
        "com.google.devtools.build.lib.AllTests",
    ],
    jvm_flags = ["-Dblaze.os=Windows"],
    deps = [
        ":foundations_testutil",
        ":test_runner",
        ":testutil",
        "//src/main/java:bazel-core",
        "//src/main/java:options",
        "//src/main/java:vfs",
        "//third_party:guava",
        "//third_party:guava-testlib",
        "//third_party:junit4",
        "//third_party:truth",
    ],
)

java_library(
    name = "actions_testutil",
    srcs = glob([
        "com/google/devtools/build/lib/actions/util/*.java",
    ]),
    deps = [
        ":foundations_testutil",
        ":test_runner",
        ":testutil",
        "//src/main/java:actions",
        "//src/main/java:analysis-exec-rules-skyframe",
        "//src/main/java:bazel-core",
        "//src/main/java:concurrent",
        "//src/main/java:events",
        "//src/main/java:options",
        "//src/main/java:packages",
        "//src/main/java:skyframe-base",
        "//src/main/java:vfs",
        "//third_party:guava",
        "//third_party:guava-testlib",
        "//third_party:jsr305",
        "//third_party:junit4",
        "//third_party:mockito",
        "//third_party:truth",
    ],
)

java_test(
    name = "actions_test",
    srcs = glob([
        "com/google/devtools/build/lib/actions/*.java",
    ]),
    args = ["com.google.devtools.build.lib.AllTests"],
    deps = [
        ":actions_testutil",
        ":foundations_testutil",
        ":test_runner",
        ":testutil",
        "//src/main/java:actions",
        "//src/main/java:analysis-exec-rules-skyframe",
        "//src/main/java:bazel-core",
        "//src/main/java:collect",
        "//src/main/java:concurrent",
        "//src/main/java:events",
        "//src/main/java:options",
        "//src/main/java:packages",
        "//src/main/java:vfs",
        "//third_party:guava",
        "//third_party:guava-testlib",
        "//third_party:jsr305",
        "//third_party:junit4",
        "//third_party:mockito",
        "//third_party:truth",
    ],
)

java_library(
    name = "analysis_testutil",
    srcs = glob([
        "com/google/devtools/build/lib/analysis/mock/BazelAnalysisMock.java",
        "com/google/devtools/build/lib/analysis/util/*.java",
        "com/google/devtools/build/lib/exec/util/*.java",
        "com/google/devtools/build/lib/skyframe/util/*.java",
    ]),
    resources = [
        "MOCK_CROSSTOOL",
    ],
    tags = ["analysis"],
    deps = [
        ":actions_testutil",
        ":foundations_testutil",
        ":packages_testutil",
        ":testutil",
        "//src/main/java:actions",
        "//src/main/java:analysis-exec-rules-skyframe",
        "//src/main/java:bazel-core",
        "//src/main/java:collect",
        "//src/main/java:concurrent",
        "//src/main/java:events",
        "//src/main/java:options",
        "//src/main/java:packages",
        "//src/main/java:skyframe-base",
        "//src/main/java:vfs",
        "//src/main/protobuf:proto_extra_actions_base",
        "//third_party:guava",
        "//third_party:guava-testlib",
        "//third_party:jsr305",
        "//third_party:junit4",
        "//third_party:mockito",
        "//third_party:truth",
    ],
)

java_test(
    name = "analysis_actions_test",
    srcs = glob([
        "com/google/devtools/build/lib/analysis/actions/*.java",
    ]),
    args = ["com.google.devtools.build.lib.AllTests"],
    tags = ["analysis"],
    deps = [
        ":actions_testutil",
        ":analysis_testutil",
        ":foundations_testutil",
        ":test_runner",
        ":testutil",
        "//src/main/java:actions",
        "//src/main/java:analysis-exec-rules-skyframe",
        "//src/main/java:bazel-core",
        "//src/main/java:vfs",
        "//src/main/protobuf:proto_extra_actions_base",
        "//third_party:guava",
        "//third_party:guava-testlib",
        "//third_party:jsr305",
        "//third_party:junit4",
        "//third_party:mockito",
        "//third_party:truth",
    ],
)

java_test(
    name = "analysis_config_test",
    srcs = glob([
        "com/google/devtools/build/lib/analysis/config/*.java",
    ]),
    args = ["com.google.devtools.build.lib.AllTests"],
    tags = ["analysis"],
    deps = [
        ":actions_testutil",
        ":analysis_testutil",
        ":foundations_testutil",
        ":test_runner",
        ":testutil",
        "//src/main/java:analysis-exec-rules-skyframe",
        "//src/main/java:bazel-core",
        "//src/main/java:options",
        "//src/main/java:packages",
        "//src/main/java:vfs",
        "//src/main/protobuf:proto_extra_actions_base",
        "//third_party:guava",
        "//third_party:guava-testlib",
        "//third_party:jsr305",
        "//third_party:junit4",
        "//third_party:mockito",
        "//third_party:truth",
    ],
)

java_test(
    name = "analysis_constraints_test",
    srcs = glob([
        "com/google/devtools/build/lib/analysis/constraints/*.java",
    ]),
    args = ["com.google.devtools.build.lib.AllTests"],
    tags = ["analysis"],
    deps = [
        ":actions_testutil",
        ":analysis_testutil",
        ":foundations_testutil",
        ":test_runner",
        ":testutil",
        "//src/main/java:analysis-exec-rules-skyframe",
        "//src/main/java:bazel-core",
        "//src/main/java:packages",
        "//src/main/java:vfs",
        "//third_party:guava",
        "//third_party:junit4",
        "//third_party:truth",
    ],
)

java_test(
    name = "analysis_select_test",
    srcs = glob([
        "com/google/devtools/build/lib/analysis/select/*.java",
    ]),
    args = ["com.google.devtools.build.lib.AllTests"],
    tags = ["analysis"],
    deps = [
        ":actions_testutil",
        ":analysis_testutil",
        ":foundations_testutil",
        ":packages_testutil",
        ":test_runner",
        ":testutil",
        "//src/main/java:analysis-exec-rules-skyframe",
        "//src/main/java:bazel-core",
        "//src/main/java:packages",
        "//src/main/java:vfs",
        "//third_party:guava",
        "//third_party:junit4",
        "//third_party:truth",
    ],
)

java_test(
    name = "analysis_test",
    srcs = glob([
        "com/google/devtools/build/lib/analysis/*.java",
    ]),
    args = ["com.google.devtools.build.lib.AllTests"],
    tags = ["analysis"],
    deps = [
        ":actions_testutil",
        ":analysis_testutil",
        ":foundations_testutil",
        ":test_runner",
        ":testutil",
        "//src/main/java:actions",
        "//src/main/java:analysis-exec-rules-skyframe",
        "//src/main/java:bazel-core",
        "//src/main/java:collect",
        "//src/main/java:events",
        "//src/main/java:packages",
        "//src/main/java:vfs",
        "//third_party:guava",
        "//third_party:guava-testlib",
        "//third_party:jsr305",
        "//third_party:junit4",
        "//third_party:mockito",
        "//third_party:truth",
    ],
)

java_library(
    name = "packages_testutil",
    srcs = glob([
        "com/google/devtools/build/lib/packages/util/*.java",
    ]),
    deps = [
        ":foundations_testutil",
        ":testutil",
        "//src/main/java:analysis-exec-rules-skyframe",
        "//src/main/java:bazel-core",
        "//src/main/java:events",
        "//src/main/java:options",
        "//src/main/java:packages",
        "//src/main/java:skyframe-base",
        "//src/main/java:vfs",
        "//src/main/protobuf:proto_extra_actions_base",
        "//third_party:guava",
        "//third_party:guava-testlib",
        "//third_party:jsr305",
        "//third_party:junit4",
        "//third_party:mockito",
        "//third_party:truth",
    ],
)

java_test(
    name = "packages_test",
    srcs = glob([
        "com/google/devtools/build/lib/packages/*.java",
    ]),
    args = ["com.google.devtools.build.lib.AllTests"],
    deps = [
        ":actions_testutil",
        ":foundations_testutil",
        ":packages_testutil",
        ":test_runner",
        ":testutil",
        "//src/main/java:analysis-exec-rules-skyframe",
        "//src/main/java:bazel-core",
        "//src/main/java:events",
        "//src/main/java:packages",
        "//src/main/java:vfs",
        "//third_party:guava",
        "//third_party:guava-testlib",
        "//third_party:jsr305",
        "//third_party:junit4",
        "//third_party:truth",
    ],
)

cc_binary(
    name = "com/google/devtools/build/lib/shell/killmyself",
    srcs = ["com/google/devtools/build/lib/shell/killmyself.cc"],
)

java_test(
    name = "shell_test",
    srcs = glob([
        "com/google/devtools/build/lib/shell/*.java",
    ]),
    args = ["com.google.devtools.build.lib.AllTests"],
    data = [
        ":com/google/devtools/build/lib/shell/killmyself",
    ],
    tags = ["shell"],
    deps = [
        ":foundations_testutil",
        ":test_runner",
        ":testutil",
        "//src/main/java:bazel-core",
        "//src/main/java:collect",
        "//src/main/java:shell",
        "//third_party:guava",
        "//third_party:guava-testlib",
        "//third_party:jsr305",
        "//third_party:junit4",
        "//third_party:mockito",
        "//third_party:truth",
    ],
)

java_binary(
    name = "skylarkshell",
    srcs = ["com/google/devtools/build/lib/syntax/SkylarkShell.java"],
    main_class = "com.google.devtools.build.lib.syntax.SkylarkShell",
    deps = [
        "//src/main/java:bazel-core",
        "//src/main/java:events",
    ],
)

java_test(
    name = "syntax_test",
    srcs = glob([
        "com/google/devtools/build/lib/syntax/*.java",
    ]),
    args = ["com.google.devtools.build.lib.AllTests"],
    deps = [
        ":foundations_testutil",
        ":test_runner",
        ":testutil",
        "//src/main/java:actions",
        "//src/main/java:analysis-exec-rules-skyframe",
        "//src/main/java:bazel-core",
        "//src/main/java:collect",
        "//src/main/java:concurrent",
        "//src/main/java:events",
        "//src/main/java:packages",
        "//src/main/java:vfs",
        "//third_party:guava",
        "//third_party:guava-testlib",
        "//third_party:jsr305",
        "//third_party:junit4",
        "//third_party:truth",
    ],
)

java_test(
    name = "common-rules-tests",
    srcs = glob(["com/google/devtools/build/lib/rules/filegroup/*.java"]),
    args = ["com.google.devtools.build.lib.AllTests"],
    tags = ["rules"],
    deps = [
        ":actions_testutil",
        ":analysis_testutil",
        ":testutil",
        "//src/main/java:analysis-exec-rules-skyframe",
        "//src/main/java:bazel-core",
        "//src/main/java:vfs",
        "//third_party:guava",
        "//third_party:guava-testlib",
        "//third_party:jsr305",
        "//third_party:junit4",
        "//third_party:truth",
    ],
)

TEST_SUITES = [
    "rules",
    "analysis",
    "foundations",
    "shell",
    "skyframe",
]

[
    test_suite(
        name = n,
        tags = [n],
    )
    for n in TEST_SUITES
]

test_suite(
    name = "others",
    tags = ["-" + n for n in TEST_SUITES],
)
