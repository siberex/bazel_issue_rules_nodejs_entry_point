# Bazel workspace created by @bazel/create 0.31.1

# Declares that this directory is the root of a Bazel workspace.
# See https://docs.bazel.build/versions/master/build-ref.html#workspace
workspace(
    # How this workspace would be referenced with absolute labels from another workspace
    name = "entry_point_label",
    # Map the @npm bazel workspace to the node_modules directory.
    # This lets Bazel use the same node_modules as other local tooling.
    managed_directories = {"@npm": ["node_modules"]},
)

# Install the nodejs "bootstrap" package
# This provides the basic tools for running and packaging nodejs programs in Bazel
load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")
RULES_NODEJS_VERSION = "0.31.1"
RULES_NODEJS_SHA256 = "e04a82a72146bfbca2d0575947daa60fda1878c8d3a3afe868a8ec39a6b968bb"
http_archive(
    name = "build_bazel_rules_nodejs",
    sha256 = RULES_NODEJS_SHA256,
    url = "https://github.com/bazelbuild/rules_nodejs/releases/download/%s/rules_nodejs-%s.tar.gz" % (RULES_NODEJS_VERSION, RULES_NODEJS_VERSION),
)

# The yarn_install rule runs yarn anytime the package.json or yarn.lock file changes.
# It also extracts and installs any Bazel rules distributed in an npm package.
load("@build_bazel_rules_nodejs//:defs.bzl", "yarn_install")
yarn_install(
    # Name this npm so that Bazel Label references look like @npm//package
    name = "npm",
    package_json = "//:package.json",
    yarn_lock = "//:yarn.lock",
)

# Install any Bazel rules which were extracted earlier by the yarn_install rule.
load("@npm//:install_bazel_dependencies.bzl", "install_bazel_dependencies")
install_bazel_dependencies()
