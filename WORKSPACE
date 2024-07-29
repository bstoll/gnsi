workspace(name = "com_github_openconfig_gnsi")

load("deps.bzl", "gnsi_deps")

gnsi_deps()

load("@com_google_googleapis//:repository_rules.bzl", "switched_rules_by_language")

switched_rules_by_language(
    name = "com_google_googleapis_imports",
    cc = True,
    go = True,
    grpc = True,
)

load("@bazel_features//:deps.bzl", "bazel_features_deps")

bazel_features_deps()

load("@bazel_gazelle//:deps.bzl", "gazelle_dependencies", "go_repository")
load("@io_bazel_rules_go//go:deps.bzl", "go_register_toolchains", "go_rules_dependencies")

# Required go_repository rules for protobuf code generation - see bazel/tools.go
# and go.mod
go_repository(
    name = "org_golang_google_protobuf",
    build_directives = [
        "gazelle:proto disable",  # https://github.com/bazelbuild/rules_go/issues/3906
    ],
    importpath = "google.golang.org/protobuf",
    sum = "h1:6xV6lTsCfpGD21XK49h7MhtcApnLqkfYgPcdHftf6hg=",
    version = "v1.34.2",
)

go_repository(
    name = "org_golang_google_grpc",
    importpath = "google.golang.org/grpc",
    sum = "h1:bs/cUb4lp1G5iImFFd3u5ixQzweKizoZJAwBNLR42lc=",
    version = "v1.65.0",
)

go_repository(
    name = "org_golang_google_grpc_cmd_protoc_gen_go_grpc",
    importpath = "google.golang.org/grpc/cmd/protoc-gen-go-grpc",
    sum = "h1:9SxA29VM43MF5Z9dQu694wmY5t8E/Gxr7s+RSxiIDmc=",
    version = "v1.4.0",
)

go_repository(
    name = "org_golang_google_genproto_googleapis_rpc",
    importpath = "google.golang.org/genproto/googleapis/rpc",
    sum = "h1:oCRSWfwGXQsqlVdErcyTt4A93Y8fo0/9D4b1gnI++qo=",
    version = "v0.0.0-20240722135656-d784300faade",
)

go_rules_dependencies()

go_register_toolchains(version = "1.22.5")

gazelle_dependencies()

load("@rules_proto_grpc_cpp//:repositories.bzl", "rules_proto_grpc_repos", "rules_proto_grpc_toolchains")

rules_proto_grpc_toolchains()

rules_proto_grpc_repos()

load("@com_github_grpc_grpc//bazel:grpc_deps.bzl", "grpc_deps")

grpc_deps()

load("@rules_proto//proto:repositories.bzl", "rules_proto_dependencies")

rules_proto_dependencies()

load("@rules_proto//proto:toolchains.bzl", "rules_proto_toolchains")

rules_proto_toolchains()
#load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")
#
#### Bazel rules for many languages to compile PROTO into gRPC libraries
## Note: any version of this which is less than 4.3.0 requires bazel version 5.4.0 (set in .bazelversion file)
#http_archive(
#    name = "rules_proto_grpc",
#    sha256 = "c0d718f4d892c524025504e67a5bfe83360b3a982e654bc71fed7514eb8ac8ad",
#    strip_prefix = "rules_proto_grpc-4.6.0",
#    urls = ["https://github.com/rules-proto-grpc/rules_proto_grpc/archive/4.6.0.tar.gz"],
#)
#
## googleapis has not had a release since 2016 - take the master version as of 4-jan-23
#http_archive(
#    name = "com_google_googleapis",
#    sha256 = "9fc03150d86501d7da35eefa989d5553bdd77a95cfe4373cdafe8eee92f6bfb1",
#    strip_prefix = "googleapis-870a5ed7e141b4faf70e2a0858854e9b5bb18612",
#    urls = ["https://github.com/googleapis/googleapis/archive/870a5ed7e141b4faf70e2a0858854e9b5bb18612.tar.gz"],
#)
#
#load("@com_google_googleapis//:repository_rules.bzl", "switched_rules_by_language")
#switched_rules_by_language(
#    name = "com_google_googleapis_imports",
#    cc = True,
#    go = True,
#)
#
#load(
#    "@rules_proto_grpc//:repositories.bzl",
#    "bazel_gazelle",
#    "io_bazel_rules_go",
#    "rules_proto_grpc_repos",
#    "rules_proto_grpc_toolchains",
#)
#
#rules_proto_grpc_toolchains()
#
#rules_proto_grpc_repos()
#
#load("@rules_proto//proto:repositories.bzl", "rules_proto_dependencies", "rules_proto_toolchains")
#
#rules_proto_dependencies()
#
#rules_proto_toolchains()
#
#### Golang
#io_bazel_rules_go()
#
#load("@io_bazel_rules_go//go:deps.bzl", "go_register_toolchains", "go_rules_dependencies")
#
#go_rules_dependencies()
#
#go_register_toolchains(go_version = "1.20")
#
## gazelle:repo bazel_gazelle
#bazel_gazelle()
#
#load("@bazel_gazelle//:deps.bzl", "gazelle_dependencies")
#
#load("//:deps.bzl", "gnsi_deps")
#
#gnsi_deps()
#
#load("@rules_proto_grpc//go:repositories.bzl", rules_proto_grpc_go_repos = "go_repos")
#
#rules_proto_grpc_go_repos()
#
## Load gazelle_dependencies last, so that the newer version of org_golang_google_grpc is used.
## see https://github.com/rules-proto-grpc/rules_proto_grpc/issues/160
#gazelle_dependencies()
#
#### C++
#load("@rules_proto_grpc//cpp:repositories.bzl", rules_proto_grpc_cpp_repos = "cpp_repos")
#
#rules_proto_grpc_cpp_repos()
#
#load("@com_github_grpc_grpc//bazel:grpc_deps.bzl", "grpc_deps")
#
#grpc_deps()
#
## open-config YANG files
#http_archive(
#    name = "github_openconfig_yang",
#    build_file_content = """exports_files(glob(["release/models/**/*.yang"]), visibility = ["//visibility:public"])""",
#    sha256 = "f6b2b6c0ffe0b66881287bcd43241a57583f353cc5cc41cba973601c32232f45",
#    strip_prefix = "public-bf737a5567ec248456cb528efcd63cab15e8fc69",
#    urls = [
#        "https://github.com/openconfig/public/archive/bf737a5567ec248456cb528efcd63cab15e8fc69.zip",
#    ],
#)
#
## YANG files from other standard bodies.
#http_archive(
#    name = "github_yang",
#    build_file_content = """exports_files(glob(["standard/**/*.yang"]), visibility = ["//visibility:public"])""",
#    sha256 = "55913058f64a1ec7fe9e6e70d7128f08e66b20c859803b1fb02dbaf7eef2c64d",
#    strip_prefix = "yang-2fa291d6bdb4b281d4e1b3dfa3254ffa7257d800",
#    urls = [
#        "https://github.com/YangModels/yang/archive/2fa291d6bdb4b281d4e1b3dfa3254ffa7257d800.zip",
#    ],
#)
#
