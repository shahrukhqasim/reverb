workspace(name = "reverb")

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

http_archive(
    name = "rules_cc",
    urls = ["https://github.com/bazelbuild/rules_cc/releases/download/0.0.13/rules_cc-0.0.13.tar.gz"],
    sha256 = "d9bdd3ec66b6871456ec9c965809f43a0901e692d754885e89293807762d3d80",
    strip_prefix = "rules_cc-0.0.13",
)

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")
http_archive(
    name = "rules_java",
    urls = [
        "https://github.com/bazelbuild/rules_java/releases/download/8.6.2/rules_java-8.6.2.tar.gz",
    ],
    sha256 = "a64ab04616e76a448c2c2d8165d836f0d2fb0906200d0b7c7376f46dd62e59cc",
)

load("@rules_java//java:rules_java_deps.bzl", "rules_java_dependencies")
rules_java_dependencies()

load("@rules_java//java:repositories.bzl", "rules_java_toolchains")
rules_java_toolchains()

# To change to a version of protoc compatible with tensorflow:
#  1. Convert the required header version to a version string, e.g.:
#     3011004 => "3.11.4"
#  2. Calculate the sha256 of the binary:
#     PROTOC_VERSION="3.11.4"
#     curl -L "https://github.com/protocolbuffers/protobuf/releases/download/v${PROTOC_VERSION}/protoc-${PROTOC_VERSION}-linux-x86_64.zip" | sha256sum
#  3. Update the two variables below.
#
PROTOC_VERSION = "21.0"
PROTOC_SHA256 = "a2a92003da7b8c0c08aab530a3c1967d377c2777723482adb9d2eb38c87a9d5f"

load(
    "//reverb/cc/platform/default:repo.bzl",
    "absl_deps",
    "cc_tf_configure",
    "github_apple_deps",
    "github_grpc_deps",
    "googletest_deps",
    "protoc_deps",
    "python_deps",
)

googletest_deps()

absl_deps()

# Note that the Python dependencies are not tracked by bazel here, but
# in setup.py.

github_apple_deps()

## Begin GRPC related deps
github_grpc_deps()

load("@com_github_grpc_grpc//bazel:grpc_deps.bzl", "grpc_deps")

grpc_deps()

load("@com_github_grpc_grpc//bazel:grpc_extra_deps.bzl", "grpc_extra_deps")

grpc_extra_deps()


load("@upb//bazel:workspace_deps.bzl", "upb_deps")

upb_deps()

load(
    "@build_bazel_rules_apple//apple:repositories.bzl",
    "apple_rules_dependencies",
)

apple_rules_dependencies()

load(
    "@build_bazel_apple_support//lib:repositories.bzl",
    "apple_support_dependencies",
)

apple_support_dependencies()
## End GRPC related deps


cc_tf_configure()

python_deps()

protoc_deps(version = PROTOC_VERSION, sha256 = PROTOC_SHA256)
