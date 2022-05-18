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
