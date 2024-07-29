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
