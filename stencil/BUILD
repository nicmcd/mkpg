package(licenses = ["notice"])

cc_binary(
    name = "mkpg_stencil",
    srcs = ["mkpg_stencil.cc"],
    copts = ["-UNDEBUG"],
    deps = [
        "@libprim//:prim",
        "@com_google_paragraph//paragraph/graph",
        "@tclap//:tclap",
    ],
    visibility = ["//visibility:public"],
)

genrule(
    name = "lint",
    srcs = glob([
        "*.cc",
        "*.h",
        "*.tcc",
    ]),
    outs = ["linted"],
    cmd = """
    python $(location @cpplint//:cpplint) \
      --root=$$(pwd)/src \
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
        "*.cc",
        "*.h",
        "*.tcc",
    ]),
    outs = ["format_checked"],
    cmd = """
    cp $(location @clang_format//file) .clang-format
    clang-format --style=file --dry-run --Werror src/main.cc
    echo // $$(date) > $@
    """,
    tools = [
        "@clang_format//file",
    ],
    visibility = ["//visibility:public"],
)
