# 量潮工具集（quanttide-toolkit）

量潮工具库体系的**元仓库**——聚合语言无关的 toolkit 包，分置于 `domains/` 与 `defaults/` 两个目录。各 toolkit 是独立仓库（Git 子模块），独立演进，本仓库只追踪引用。

## 架构思想

2026-08-09 重构确立。核心思想是**去中心化**——不设所有库强制依赖的基础库（BASE/CORE），消除单点依赖。传统 BASE 的问题在于：

- 单点故障：BASE 一旦变更，全系统大面积变更。
- 兼容性灾难：BASE 变动对上层造成不可逆影响。
- 难以拆除：BASE/CORE 拆不掉，也改不动。

量潮的解法是用 META 元领域取代 BASE。

### META 元领域

`quanttide-meta-toolkit` 是对各个模块的总结和再次抽象——识别跨模块的共同模式（元模式），归纳为独立领域的标准字段/模型。它与 BASE 的本质区别：

| **对比项** | **BASE/CORE** | **META** |
|:--|:--|:--|
| 依赖关系 | 所有库强制依赖 | 可选、模块化依赖 |
| 变更影响 | 全局灾难 | 局部，可独立迭代 |
| 可拆除性 | 拆不掉 | 不好用可拆 |
| 定位 | 强制基础 | 归纳总结 |

它承担三类核心功能：

- 领域增加：新领域出现时，沉淀共同模式。
- 一致性治理：领域间出现混乱时，统一概念及其关系，二次抽象。
- 通用特性：与各库排列组合，向上层提供通用能力。

META 最重要的价值是独立快速迭代——元规范（统一概念、关系、抽象）不需要等待其他库，可以更快地独立更新。

### INDEX 入口库

`quanttide-index-toolkit` 继承 base 历史并推翻重写，是人和 AI 查找所有库的统一入口。它以 `quanttide` 名义发布（v0.2.0 起），`quanttide-*` 作为可选插件；不提供实际功能，可随时拆除，不构成单点。

整体的查找与依赖路径：

```text
用户 / AI
    ↓ 查找
quanttide-index-toolkit（入口）
    ↓ 发现
quanttide-toolkit（元仓库：领域 toolkit 列表）
    ↓ 依赖（可选）
quanttide-meta-toolkit（元领域：标准字段/模型）
```

## 包清单

| **层** | **库** | **定位** |
|:--|:--|:--|
| 入口层 | [`quanttide-index-toolkit`](domains/quanttide-index-toolkit) | 统一入口——人和 AI 从这里找到所有库 |
| 元领域层 | [`quanttide-meta-toolkit`](domains/quanttide-meta-toolkit) | 归纳特征——标准字段/模型（Summarize 模式） |
| 应用层 | [`quanttide-tech-toolkit`](defaults/quanttide-tech-toolkit) | 跨业务、跨领域流程整合 |
| 领域层 | [`quanttide-agent-toolkit`](domains/quanttide-agent-toolkit) | 智能体工程 |
| 领域层 | [`quanttide-audit-toolkit`](domains/quanttide-audit-toolkit) | 审计领域数据模型 |
| 领域层 | [`quanttide-connect-toolkit`](domains/quanttide-connect-toolkit) | 沟通工程 |
| 领域层 | [`quanttide-course-toolkit`](domains/quanttide-course-toolkit) | 课程研发 |
| 领域层 | [`quanttide-data-toolkit`](domains/quanttide-data-toolkit) | 数据工程 |
| 领域层 | [`quanttide-devops-toolkit`](domains/quanttide-devops-toolkit) | DevOps |
| 领域层 | [`quanttide-docs-toolkit`](domains/quanttide-docs-toolkit) | 文档工程 |
| 领域层 | [`quanttide-founder-toolkit`](defaults/quanttide-founder-toolkit) | 创始人工具箱 |
| 领域层 | [`quanttide-knowl-toolkit`](domains/quanttide-knowl-toolkit) | 知识工程 |
| 领域层 | [`quanttide-media-toolkit`](domains/quanttide-media-toolkit) | 媒体（Flutter） |
| 领域层 | [`quanttide-product-toolkit`](domains/quanttide-product-toolkit) | 产品（Flutter） |
| 领域层 | [`quanttide-project-toolkit`](domains/quanttide-project-toolkit) | 项目管理 |

预留：`quanttide-feishu-toolkit`（基础设施层，统一底层依赖），见 [ROADMAP.md](ROADMAP.md)。

## 目录结构

```text
quanttide-toolkit/
├── AGENTS.md                # 智能体约定
├── CONTRIBUTING.md          # 贡献指南
├── defaults/                # 子模块：tech、founder（见上表）
├── domains/                 # 子模块：各领域 toolkit（见上表）
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

子模块是独立仓库，改动请在各 toolkit 仓库内提交推送，本仓库只更新引用；日常同步与提交约定见 [CONTRIBUTING.md](CONTRIBUTING.md)，智能体约定见 [AGENTS.md](AGENTS.md)。

## 许可证

本项目采用 [MIT](LICENSE) 许可证。
