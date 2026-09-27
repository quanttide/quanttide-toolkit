# quanttide-toolkit 贡献指南

quanttide-toolkit 是量潮工具库体系的元仓库，聚合各领域 toolkit 子模块。仓库定位、架构思想与包清单见 [README.md](README.md)，演进路线见 [ROADMAP.md](ROADMAP.md)，面向智能体的约定见 [AGENTS.md](AGENTS.md)。

## 资产轴与领域轴

各 toolkit 在各自的领域轴内独立演进，更新频繁；本仓库处在资产轴，职责是整理领域间关系、维护集中治理结构，不承载任何领域的实现。因此本仓库的日常动作以同步为主，需要经常 fetch 各子模块的最新更新，使引用指针与治理视图保持时效。

> 领域代码的改动一律在对应的 toolkit 仓库内完成并推送，本仓库只更新引用指针。

## 日常同步

1. 拉取各子模块最新提交：`git submodule update --init --recursive --remote`。
2. 检视本次更新涉及的领域间关系变化，必要时同步修订 `README.md` 与 `ROADMAP.md`。
3. 在本仓库提交引用更新。

若只想刷新本地引用、暂不改动检出，可先执行 `git submodule foreach --recursive 'git fetch --prune origin'`，再按需处理。同步前建议丢弃子模块内的本地改动，避免把未推送的领域改动混入引用更新。

## 提交规范

遵循 Conventional Commits（`feat:` / `fix:` / `docs:` / `chore:` 等）；破坏性变更标 `!` 并在正文说明迁移方式。
