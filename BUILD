load("@build_bazel_rules_android//android:rules.bzl", "android_binary")

android_binary(
    name = "bazel_desugar_issue_13553",
    custom_package = "cm.ben.android.bazel.desugar.example",
    manifest = "AndroidManifest.xml",
    deps = [
        "@maven//:org_jetbrains_kotlinx_kotlinx_coroutines_core_jvm",
    ],
)
