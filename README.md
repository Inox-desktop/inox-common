# inox-common

共享类型、错误处理与日志工具。属于 Inox 桌面环境的 **L1** 层。

## 状态

- `v0.1.0` 已发布，并被 `inox-compositor` 通过锁定 `tag` 的 git 依赖消费。
- `v0.1.1` 新增 `paths` 模块（按 [ADR 0010](https://github.com/Inox-desktop/inox/blob/main/docs/adr/0010-versioning-and-release-policy.md) 的 0.x 语义，兼容的新增走 patch）：按 XDG Base Directory Specification 解析 `$XDG_CONFIG_HOME` / `$XDG_DATA_HOME` / `$XDG_STATE_HOME` / `$XDG_CACHE_HOME` / `$XDG_RUNTIME_DIR`，并给出 Inox 的 `<base>/inox` 目录，供 `inox-config` 等上层组件复用（PRD §9.1）。

当前模块：

| 模块 | 作用 |
|------|------|
| `logging` | 统一的 `tracing` 初始化入口（`RUST_LOG` 过滤，默认 `info`，不 panic），供各组件二进制复用 |
| `paths` | XDG 基础目录解析（含 Inox 子目录）：不读全局状态，环境以 `XdgEnv` 快照注入，因此可完整单测 |

其余共享类型与工具函数在其**首个真实消费者出现时**再引入：本 crate 刻意不提前声明无人使用的抽象（依赖排期原则见元仓库 ADR 0004）。

## 开发约定

- 本项目遵循根级 [AGENTS.md](https://github.com/Inox-desktop/inox/blob/main/AGENTS.md) 与仓库级 [`AGENTS.md`](./AGENTS.md)。
- **CI（GitHub Actions）是唯一的构建与测试验证途径**，不在本地进行编译验证。
- 提交信息遵循 [Conventional Commits](https://www.conventionalcommits.org/)。

## 许可证

BSD 3-Clause，见 [`LICENSE`](./LICENSE)。
