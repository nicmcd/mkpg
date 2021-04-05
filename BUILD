package(licenses = ["notice"])

exports_files([
    "LICENSE",
    "NOTICE",
])

cc_binary(
    name = "mkpg_stencil",
    srcs = ["src/mkpg_stencil.cc"],
    copts = ["-UNDEBUG"],
    deps = [
        "@libprim//:prim",
        "@com_google_paragraph//paragraph/graph",
        "@tclap//:tclap",
    ],
    visibility = ["//visibility:public"],
)

cc_binary(
    name = "mkss_stencil",
    srcs = ["src/mkss_stencil.cc"],
    copts = ["-UNDEBUG"],
    deps = [
        "@libprim//:prim",
        "@tclap//:tclap",
    ],
    visibility = ["//visibility:public"],
)

genrule(
    name = "lint",
    srcs = glob([
        "src/**/*.cc",
        "src/**/*.h",
        "src/**/*.tcc",
    ]),
    outs = ["linted"],
    cmd = """
    python $(location @cpplint//:cpplint) \
      --root=$$(pwd) \
      --headers=h,tcc \
      --extensions=cc,h,tcc \
      --quiet $(SRCS) > $@
    echo // $$(date) > $@
    """,
    tools = [
        "@cpplint",
    ],
    visibility = ["//visibility:public"],
)

genrule(
    name = "format_check",
    srcs = glob([
        "src/**/*.cc",
        "src/**/*.h",
        "src/**/*.tcc",
    ]),
    outs = ["format_checked"],
    cmd = """
    cp $(location @clang_format//file) .clang-format
    clang-format --style=file --dry-run --Werror $(SRCS)
    echo // $$(date) > $@
    """,
    tools = [
        "@clang_format//file",
    ],
    visibility = ["//visibility:public"],
)
