# 量潮工具集（quanttide-toolkit）

量潮工具库体系的**元仓库**——聚合语言无关的 toolkit 包（`packages/`）。各 toolkit 是独立仓库（Git 子模块），独立演进，本仓库只追踪引用。

## 架构思想

量潮工具库没有传统意义上的 BASE/CORE 基础库。核心思想是**去中心化**——消除单点基础库：

- **无 BASE**：传统 BASE 一旦变更，全系统大面积变更，且拆不掉。量潮用 META 元领域取代 BASE。
- **META 元领域**（`quanttide-meta-toolkit`）：对各模块的总结和再次抽象——识别跨模块的共同模式，归纳为标准字段/模型。可选依赖，不好用可拆。
- **INDEX 入口库**（`quanttide-index-toolkit`）：统一入口——人和 AI 从这里找到所有库。不提供实际功能，可随时拆掉。

```
用户 / AI
    ↓ 查找
quanttide-index-toolkit（入口）
    ↓ 发现
quanttide-toolkit（元仓库：领域 toolkit 列表）
    ↓ 依赖（可选）
quanttide-meta-toolkit（元领域：标准字段/模型）
```

完整分层模型见 [docs/dev-guide/layering.md](docs/dev-guide/layering.md)。

## 包清单

| 层 | 库 | 定位 |
|----|----|------|
| 入口层 | [`quanttide-index-toolkit`](packages/quanttide-index-toolkit) | 统一入口——人和 AI 从这里找到所有库 |
| 元领域层 | [`quanttide-meta-toolkit`](packages/quanttide-meta-toolkit) | 归纳特征——标准字段/模型（Summarize 模式） |
| 领域层 | [`quanttide-agent-toolkit`](packages/quanttide-agent-toolkit) | 智能体工程 |
| 领域层 | [`quanttide-audit-toolkit`](packages/quanttide-audit-toolkit) | 审计领域数据模型 |
| 领域层 | [`quanttide-connect-toolkit`](packages/quanttide-connect-toolkit) | 沟通工程 |
| 领域层 | [`quanttide-course-toolkit`](packages/quanttide-course-toolkit) | 课程研发 |
| 领域层 | [`quanttide-data-toolkit`](packages/quanttide-data-toolkit) | 数据工程 |
| 领域层 | [`quanttide-devops-toolkit`](packages/quanttide-devops-toolkit) | DevOps |
| 领域层 | [`quanttide-docs-toolkit`](packages/quanttide-docs-toolkit) | 文档工程 |
| 领域层 | [`quanttide-knowl-toolkit`](packages/quanttide-knowl-toolkit) | 知识工程 |
| 领域层 | [`quanttide-project-toolkit`](packages/quanttide-project-toolkit) | 项目管理 |

预留：`quanttide-tech-toolkit`（应用层）、`quanttide-feishu-toolkit`（基础设施层），见 [ROADMAP.md](ROADMAP.md)。

## 目录结构

```
quanttide-toolkit/
├── docs/dev-guide/          # 开发者指南
│   └── layering.md          # 领域分层模型
├── packages/                # 子模块：各领域 toolkit（见上表）
├── LICENSE                  # MIT 许可证
├── README.md                # 本文件
└── ROADMAP.md               # 路线图
```

## 快速开始

```bash
# 克隆（含子模块）
git clone --recurse-submodules git@github.com:quanttide/quanttide-toolkit.git

# 已有克隆时初始化/更新子模块
git submodule update --init --recursive
```

子模块是独立仓库，改动请在各 toolkit 仓库内提交推送，本仓库只更新引用。

## 许可证

本项目采用 [MIT](LICENSE) 许可证。
