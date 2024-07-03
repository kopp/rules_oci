# Declare the local Bazel workspace.
# This is *not* included in the published distribution.
workspace(name = "rules_oci")

# Fetch deps needed only locally for development
load(":internal_deps.bzl", "rules_oci_internal_deps")

rules_oci_internal_deps()

## Stardoc
load("@io_bazel_stardoc//:setup.bzl", "stardoc_repositories")

stardoc_repositories()

## Setup rules_oci
load("//oci:dependencies.bzl", "rules_oci_dependencies")

rules_oci_dependencies()

load("//oci:repositories.bzl", "oci_register_toolchains")

oci_register_toolchains(name = "oci")

## Setup bazel-lib
load("@aspect_bazel_lib//lib:repositories.bzl", "aspect_bazel_lib_dependencies", "aspect_bazel_lib_register_toolchains")

aspect_bazel_lib_dependencies()

aspect_bazel_lib_register_toolchains()

## Setup cosign
load("//cosign:repositories.bzl", "cosign_register_toolchains")

cosign_register_toolchains(name = "oci_cosign")

## Setup skylib unittest
load("@bazel_skylib//lib:unittest.bzl", "register_unittest_toolchains")

register_unittest_toolchains()

## Setup rules_go
load("@io_bazel_rules_go//go:deps.bzl", "go_register_toolchains", "go_rules_dependencies")

go_rules_dependencies()

go_register_toolchains(version = "1.20.5")

## Setup gazelle
load("@bazel_gazelle//:deps.bzl", "gazelle_dependencies")

gazelle_dependencies()

## Setup test repositories
load(":fetch.bzl", "fetch_images", "fetch_test_repos")

fetch_images()

fetch_test_repos()

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

http_archive(
    name = "io_buildbuddy_buildbuddy_toolchain",
    sha256 = "a3492ce5357425eedd4ba0af0571f6b7e70d9c343319fe49f98ef24291e62649",
    strip_prefix = "buildbuddy-toolchain-5b47b1252d6bff48d1087c3ebebc798247ea2635",
    urls = ["https://github.com/buildbuddy-io/buildbuddy-toolchain/archive/5b47b1252d6bff48d1087c3ebebc798247ea2635.tar.gz"],
)

load("@io_buildbuddy_buildbuddy_toolchain//:deps.bzl", "buildbuddy_deps")

buildbuddy_deps()

load("@io_buildbuddy_buildbuddy_toolchain//:rules.bzl", "UBUNTU20_04_IMAGE", "buildbuddy")

buildbuddy(
    name = "buildbuddy_toolchain",
    container_image = UBUNTU20_04_IMAGE,
)
