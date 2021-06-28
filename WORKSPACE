workspace(name = "bazel_desugar_issue_13553")

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

## JVM External

_RULES_JVM_EXTERNAL_VERSION = "4.1"
_RULES_JVM_EXTERNAL_SHA = "f36441aa876c4f6427bfb2d1f2d723b48e9d930b62662bf723ddfb8fc80f0140"

http_archive(
    name = "rules_jvm_external",
    sha256 = _RULES_JVM_EXTERNAL_SHA,
    strip_prefix = "rules_jvm_external-{}".format(_RULES_JVM_EXTERNAL_VERSION),
    urls = [
        "https://github.com/bazelbuild/rules_jvm_external/archive/{}.zip".format(_RULES_JVM_EXTERNAL_VERSION),
    ],
)

load("@rules_jvm_external//:defs.bzl", "maven_install")

overridden_targets = {
    # Override the maven dep with the fixed target
    "org.jetbrains.kotlinx:kotlinx-coroutines-core-jvm": "@//:kotlinx_coroutines_core_jvm_fixed",
}

maven_install(
    override_targets = overridden_targets,
    artifacts = [
        "org.jetbrains.kotlinx:kotlinx-coroutines-core-jvm:jar:1.5.0",
    ],
    repositories = [
        "https://maven.google.com",
        "https://repo1.maven.org/maven2",
    ],
)

# Create a second maven repository that downloads the original kotlinx-coroutines-core-jvm
# jar. This will be used to override the root @maven target with the hacked
# version compiled against the neverlink sun dependencies.
maven_install(
    name = "kotlinx_coroutines_core_fixed",
    artifacts = ["org.jetbrains.kotlinx:kotlinx-coroutines-core-jvm:jar:1.5.0"],
    repositories = ["https://repo1.maven.org/maven2"],
)

## Android

_RULES_ANDROID_VERSION = "0.1.1"
_RULES_ANDROID_SHA = "cd06d15dd8bb59926e4d65f9003bfc20f9da4b2519985c27e190cddc8b7a7806"

http_archive(
    name = "build_bazel_rules_android",
    sha256 = _RULES_ANDROID_SHA,
    strip_prefix = "rules_android-{}".format(_RULES_ANDROID_VERSION),
    urls = [
        "https://github.com/bazelbuild/rules_android/archive/v{}.zip".format(_RULES_ANDROID_VERSION),
    ],
)

load("@build_bazel_rules_android//android:rules.bzl", "android_sdk_repository")

android_sdk_repository(
    name = "androidsdk",
    api_level = 29,
    build_tools_version = "29.0.3",
)
