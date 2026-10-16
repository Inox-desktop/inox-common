# AGENTS.md — inox-common

本仓库遵循根级 [AGENTS.md](https://github.com/Inox-desktop/inox/blob/main/AGENTS.md) 的**全部硬性规则**，本文件只补充仓库特有内容，不放宽任何根级约束。

## 职责

共享类型、错误处理与日志工具。所属层级：**L1**。

## 仓库特有约束

- 默认禁止 `unsafe`：`Cargo.toml` 中 `[lints.rust] unsafe_code = "forbid"`。
- 非测试路径禁止 `unwrap()` / `expect()` / `panic!()` / `todo!()` / `unimplemented!()`。
- 日志统一使用 `tracing`，禁止 `println!` / `eprintln!`。
- 本 crate **已被跨仓库消费**（M1）：`inox-compositor` 通过根级 §8 的锁定 git `tag` 依赖 `inox-common v0.1.0`。任何破坏性变更须发布新 `tag`，下游再按根级 §8 锁定升级；不要在已发布的 `tag` 上重写历史。

## 主要依赖

`tracing`, `tracing-subscriber`（`env-filter`）, `thiserror`

## 命令

> 仅作参考，不作为本地验收依据；真正判定在 CI。

| 目的 | 命令 |
|------|------|
| 格式化 | `cargo fmt --all` |
| 格式检查 | `cargo fmt --all -- --check` |
| 静态检查 | `cargo clippy --all-targets --all-features -- -D warnings` |
| 测试 | `cargo test --all-features` |
| 构建 | `cargo build --release --all-features` |
| 文档 | `cargo doc --no-deps --all-features` |
| 依赖检查 | `cargo deny check` |

## 测试要求

- 纯逻辑必须有单元测试（`#[cfg(test)]`）。
- 测试代码不受“禁止 unwrap/expect/panic”约束。
- `logging` 模块已具备单元测试（显式指令优先、缺失/空白回退默认、首尾空白 trim、非法指令报错并携带原指令）；`cargo test --all-features` 必须保持全绿。

## 目录结构

```
src/            源码（lib.rs 库入口 / main.rs 可执行入口）
tests/          集成测试（按需创建）
.github/        CI 工作流
deny.toml       cargo-deny 依赖与许可证策略
```

## 提交信息格式

Conventional Commits，scope 使用 `common`。
