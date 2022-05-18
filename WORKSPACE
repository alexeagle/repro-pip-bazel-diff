load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")
http_archive(
    name = "rules_python",
    sha256 = "cdf6b84084aad8f10bf20b46b77cb48d83c319ebe6458a18e9d2cebf57807cdd",
    strip_prefix = "rules_python-0.8.1",
    url = "https://github.com/bazelbuild/rules_python/archive/refs/tags/0.8.1.tar.gz",
)

load("@rules_python//python:repositories.bzl", "python_register_toolchains")

python_register_toolchains(
    name = "python3_9",
    # Available versions are listed in @rules_python//python:versions.bzl.
    # We recommend using the same version your team is already standardized on.
    python_version = "3.9",
)

load("@python3_9//:defs.bzl", "interpreter")

load("@rules_python//python:pip.bzl", "pip_parse")

pip_parse(
    name = "my_deps",
    requirements_lock = "//:requirements.txt",
    python_interpreter_target = interpreter,
)

# Load the starlark macro which will define your dependencies.
load("@my_deps//:requirements.bzl", "install_deps")
# Call it to define repos for your requirements.
install_deps()

_BAZEL_DIFF_VERSION = "3.4.2"
http_archive(
    name = "bazel_diff",
    urls = [
        "https://github.com/Tinder/bazel-diff/archive/refs/tags/%s.tar.gz" % _BAZEL_DIFF_VERSION,
    ],
    sha256 = "5fa8f207ae5e7e1fb151cb56c68d82d407d4b0e57c460758a8635985d50eba6b",
    strip_prefix = "bazel-diff-%s" % _BAZEL_DIFF_VERSION,
)

http_archive(
    name = "rules_proto",
    sha256 = "66bfdf8782796239d3875d37e7de19b1d94301e8972b3cbd2446b332429b4df1",
    strip_prefix = "rules_proto-4.0.0",
    urls = [
        "https://github.com/bazelbuild/rules_proto/archive/refs/tags/4.0.0.tar.gz",
    ],
)

http_archive(
    name = "com_google_protobuf",
    sha256 = "3bd7828aa5af4b13b99c191e8b1e884ebfa9ad371b0ce264605d347f135d2568",
    strip_prefix = "protobuf-3.19.4",
    urls = ["https://github.com/protocolbuffers/protobuf/archive/v3.19.4.tar.gz"],
)

load("@rules_proto//proto:repositories.bzl", "rules_proto_dependencies", "rules_proto_toolchains")

rules_proto_dependencies()

rules_proto_toolchains()

# Using HEAD from 2021-08-09 to get fix for error messaging reported in
# https://github.com/bazelbuild/rules_jvm_external/issues/541
RULES_JVM_EXTERNAL_TAG = "d610f38add575692ae711a905822d65e126d96ae"
RULES_JVM_EXTERNAL_SHA = "570d0b22982dffcf3878286d293e734b0d8da8525ee716af9d85622dc667e762"
http_archive(
    name = "rules_jvm_external",
    strip_prefix = "rules_jvm_external-%s" % RULES_JVM_EXTERNAL_TAG,
    sha256 = RULES_JVM_EXTERNAL_SHA,
    urls = [
        "https://github.com/bazelbuild/rules_jvm_external/archive/%s.zip" % RULES_JVM_EXTERNAL_TAG,
    ],
)

load("@bazel_diff//:repositories.bzl", "bazel_diff_dependencies")
load("@bazel_diff//:artifacts.bzl", "BAZEL_DIFF_MAVEN_ARTIFACTS")
bazel_diff_dependencies(RULES_JVM_EXTERNAL_TAG, RULES_JVM_EXTERNAL_SHA)

load("@rules_jvm_external//:defs.bzl", "maven_install")
maven_install(
    name = "bazel_diff_maven",
    artifacts = BAZEL_DIFF_MAVEN_ARTIFACTS,
    repositories = [
        "https://jcenter.bintray.com/",
    ],
)
