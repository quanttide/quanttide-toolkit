# AGENTS

## 仓库定位

quanttide-toolkit 是量潮工具库体系的元仓库，在资产轴上聚合各领域 toolkit 子模块。各 toolkit 在各自的领域轴内通常会有更新；本仓库以整理领域间关系和集中治理结构为主，不承载领域实现。因此需要经常 fetch 子模块的最新更新，使引用指针与治理视图保持时效。定位与包清单见 [README.md](README.md)，面向人的约定见 [CONTRIBUTING.md](CONTRIBUTING.md)。

## 目录结构

```text
quanttide-toolkit/
├── AGENTS.md
├── CONTRIBUTING.md
├── defaults/       # 默认工具集：tech、founder
├── domains/        # 各领域 toolkit
├── README.md
└── ROADMAP.md
```

## 工作纪律

- 领域代码的改动一律在对应的 toolkit 仓库内完成并推送，本仓库只更新引用指针；
- 更新引用前先 fetch 各子模块的最新更新；
- 提交后始终推送（always push），不把提交留在本地。

## 提交消息

遵循 Conventional Commits（`feat:` / `fix:` / `docs:` / `chore:` 等）。
