workspace(name = "bazel_and_package_managers")

load(
    "@bazel_tools//tools/build_defs/repo:http.bzl",
    "http_archive"
)

http_archive(
    name = "rules_haskell",
    strip_prefix = "rules_haskell-6a2c09fa4da023ff890749125590fe752a1ba2c4",
    urls = ["https://github.com/tweag/rules_haskell/archive/6a2c09fa4da023ff890749125590fe752a1ba2c4.tar.gz"],
    sha256 = "a3d588ca64163d59a2330554e9c8704ab6e07bab861957595e8c26c02a6c2a29",
)

load(
    "@rules_haskell//haskell:repositories.bzl",
    "rules_haskell_dependencies",
    "rules_haskell_toolchains",
)

rules_haskell_dependencies()
rules_haskell_toolchains()

http_archive(
    name = "zlib",
    build_file_content = """
cc_library(
    name = "zlib",
    srcs = [":z"],
    hdrs = glob(["*.h"]),
    visibility = ["//visibility:public"],
)
cc_library(name = "z", srcs = glob(["*.c"]), hdrs = glob(["*.h"]))
""",
    sha256 = "c3e5e9fdd5004dcb542feda5ee4f0ff0744628baf8ed2dd5d66f8ca1197cb1a1",
    strip_prefix = "zlib-1.2.11",
    urls = ["http://zlib.net/zlib-1.2.11.tar.gz"],
)

load(
    "@rules_haskell//haskell:cabal.bzl",
    "stack_snapshot",
)

stack_snapshot(
    name = "stackage",
    packages = [
        "aeson",
        "base",
        "directory",
        "filepath",
        "hspec",
        "hspec-discover",
        "http-client",
        "http-types",
        "servant",
        "servant-client",
        "servant-server",
        "transformers",
        "wai",
        "warp",
    ],
    extra_deps = {
        "zlib": ["@zlib"],
    },
    snapshot = "lts-13.8",
)

http_archive(
    name = "hspec-discover",
    strip_prefix = "hspec-discover-2.6.1",
    urls = [
        "http://hackage.haskell.org/package/hspec-discover-2.6.1/hspec-discover-2.6.1.tar.gz",
    ],
    sha256 = "9d569a9587d2034272d287442855490a06266192eba1da871cae7d971b922fa1",
    build_file_content = """
load(
    "@rules_haskell//haskell:cabal.bzl",
    "haskell_cabal_binary",
)
haskell_cabal_binary(
    name = "hspec-discover",
    srcs = glob(["**"]),
    deps = [
        "@stackage//:base",
        "@stackage//:directory",
        "@stackage//:filepath",
        "@stackage//:hspec-discover",
    ],
    visibility = ["//visibility:public"],
)
""",
)
