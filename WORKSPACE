workspace(name = 'ren')

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

### NODEJS, dep management 
http_archive(
    name = "build_bazel_rules_nodejs",
    sha256 = "c077680a307eb88f3e62b0b662c2e9c6315319385bc8c637a861ffdbed8ca247",
    urls = ["https://github.com/bazelbuild/rules_nodejs/releases/download/5.1.0/rules_nodejs-5.1.0.tar.gz"],
)
 
load("@build_bazel_rules_nodejs//:repositories.bzl", "build_bazel_rules_nodejs_dependencies")

build_bazel_rules_nodejs_dependencies()
 
# Setup the NodeJS toolchain
load("@build_bazel_rules_nodejs//:index.bzl", "node_repositories", "yarn_install")

node_repositories(
    node_version = "17.5.0",
    yarn_version = "3.1.1"
)

# Setup Bazel managed npm dependencies with the `yarn_install` rule.
yarn_install(
    name = "npm",
    package_json = "//:package.json",
    yarn_lock = "//:yarn.lock",
)

#############

### SHARED
# flatbuffers
new_local_repository(
    name = "flatbuffers",
    path = "third_party/flatbuffers",
    build_file = "third_party/flatbuffers/BUILD.bazel"
)

# gRPC (C++/Python)
http_archive(
    name = "gRPC",
    sha256 = "1",
    urls = ["https://github.com/grpc/grpc/archive/refs/tags/v1.44.0.tar.gz"],
)

### RUST
# Rust rules
http_archive(
    name = "rules_rust",
    sha256 = "531bdd470728b61ce41cf7604dc4f9a115983e455d46ac1d0c1632f613ab9fc3",
    strip_prefix = "rules_rust-d8238877c0e552639d3e057aadd6bfcf37592408",
    urls = [
        # `main` branch as of 2021-08-23
        # "https://github.com/bazelbuild/rules_rust/archive/d8238877c0e552639d3e057aadd6bfcf37592408.tar.gz",
        "https://github.com/bazelbuild/rules_rust/archive/refs/tags/0.0.7.tar.gz",
    ],
)

load("@rules_rust//rust:repositories.bzl", "rust_repositories")

rust_repositories(version = "1.59.0", edition="2021")

### C++
# glog
http_archive(
    name = "glog",
    sha256 = "21bc744fb7f2fa701ee8db339ded7dce4f975d0d55837a97be7d46e8382dea5a",
    strip_prefix = "glog-0.5.0",
    urls = ["https://github.com/google/glog/archive/refs/tags/v0.5.0.zip"],
)

# gflags (glog dependency)
http_archive(
    name = "com_github_gflags_gflags",
    sha256 = "34af2f15cf7367513b352bdcd2493ab14ce43692d2dcd9dfc499492966c64dcf",
    strip_prefix = "gflags-2.2.2",
    urls = ["https://github.com/gflags/gflags/archive/v2.2.2.tar.gz"],
)

