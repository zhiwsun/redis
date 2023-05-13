# Continuous Learning :: redis #


## 一、编译和构建 ##

1. 代码分支 [redis/redis - tag:7.0.11](https://github.com/redis/redis/tree/7.0.11)

2. `Redis` 采用 `Makefile` 系统构建，在通过 `clangd` 进行项目代码分析时须要额外指定编译指令文件 `compile_comands.json` 。
可以通过 `bear` 工具由 `Makefile` 生成 `compile_commands.json` 文件（文件中包含编译相关的绝对路径信息等，须要针对性自动生成，不可托管）。另外，我的 VSCODE 中配置 `clangd` 的提示文件部署于 `${projectRoot}/build/` 。

    > 参考： https://clangd.llvm.org/installation
    > 
    > eg: `bear -- make`

3. 在配合 VSCODE 阅读代码时，会发现 `clangd` 工具会提示出 `drv_unknown_arguments` 异常，原因是在于按照模板的 `Makefile` 生成的 `compile_commands.json` 指令中包含了很多冗余无用的编译参数，`clang` 会把冗余无用的参数直接当异常抛出，所以需要在生成编译指令的过程中过滤掉冗余无用的参数。具体的解法是：在 `Makefile` 对应的 `.make-settings` 文件中指定编译 `FLAG` ，增加 `-Qunused-arguments` 。

    > 参考：https://stackoverflow.com/questions/60227510/clang-tidy-report-error-unknown-argument-when-contain-other-compiler-options
    >
    > eg: `STD=-pedantic -DREDIS_STATIC= -Wno-c11-extensions -std=c11 -Qunused-argument`


## 二、项目架构 ##
