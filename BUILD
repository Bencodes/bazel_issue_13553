load("@build_bazel_rules_android//android:rules.bzl", "android_binary")

android_binary(
    name = "bazel_desugar_issue_13553",
    custom_package = "cm.ben.android.bazel.desugar.example",
    manifest = "AndroidManifest.xml",
    deps = [
        "@maven//:org_jetbrains_kotlinx_kotlinx_coroutines_core_jvm",
    ],
)

java_import(
    name = "kotlinx_coroutines_core_jvm_fixed",
    jars = ["@kotlinx_coroutines_core_fixed//:v1/https/repo1.maven.org/maven2/org/jetbrains/kotlinx/kotlinx-coroutines-core-jvm/1.5.0/kotlinx-coroutines-core-jvm-1.5.0.jar"],
    deps = [
        ":sun_dependencies_neverlink",
		"@maven//:org_jetbrains_kotlin_kotlin_stdlib_common",
		"@maven//:org_jetbrains_kotlin_kotlin_stdlib_jdk8",
    ],
    visibility = ["//visibility:public"],
)

java_library(
    name = "sun_dependencies_neverlink",
    srcs = ["SignalHandler.java", "Signal.java"],
    neverlink = True,
)