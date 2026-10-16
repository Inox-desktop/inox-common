# inox-common

共享类型、错误处理与日志工具。属于 Inox 桌面环境的 **L1** 层。

## 状态

`v0.1.0` 已发布，并被 `inox-compositor` 通过锁定 `tag` 的 git 依赖消费。

当前提供 `logging` 模块：统一的 `tracing` 初始化入口（`RUST_LOG` 过滤，默认 `info`，不 panic），供各组件二进制复用；其余共享类型与工具随里程碑补充。

## 开发约定

- 本项目遵循根级 [AGENTS.md](https://github.com/Inox-desktop/inox/blob/main/AGENTS.md) 与仓库级 [`AGENTS.md`](./AGENTS.md)。
- **CI（GitHub Actions）是唯一的构建与测试验证途径**，不在本地进行编译验证。
- 提交信息遵循 [Conventional Commits](https://www.conventionalcommits.org/)。

## 许可证

BSD 3-Clause，见 [`LICENSE`](./LICENSE)。
