load("@rules_python//python:pip.bzl", "compile_pip_requirements")
load("@rules_python//python:defs.bzl", "py_library")
load("@my_deps//:requirements.bzl", "requirement")

compile_pip_requirements(
    name = "requirements",
)

py_library(
    name = "containers_utils",
    srcs = glob(["*.py"]),
    deps = [requirement("testcontainers")],    
)
