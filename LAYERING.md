# 量潮工具库领域分层模型

> 2026-08-09 重构确立。核心思想：**去中心化**——消除单点基础库。

## 一、分层模型

| 层 | 库 | 角色 | 可否拆除 |
|----|----|------|---------|
| 用户界面层 | `quanttide-index-toolkit` | 统一入口——人和 AI 从这里找到所有库 | 可拆（不提供实际功能） |
| 应用层 | `quanttide-tech-toolkit`（预留） | 跨业务、跨领域流程整合 | — |
| 元领域层 | `quanttide-meta-toolkit` | 归纳特征——标准字段/模型（Summarize 模式） | 可拆（不好用就拆） |
| 领域层 | 各领域 toolkit（挂载于 quanttide-toolkit 元仓库） | 业务领域工具 | — |
| 基础设施层 | `quanttide-feishu-toolkit` 等 | 统一底层依赖 | — |

## 二、核心思想：为什么没有 BASE 库

传统工程体系有一个所有库强制依赖的基础库（BASE/CORE）。问题：

- **单点故障**：BASE 一旦变更，全系统大面积变更
- **兼容性灾难**：BASE 变动对上层造成不可逆影响
- **难以拆除**：BASE/CORE 拆不掉的，改不动

量潮的解法：**META 元领域**取代 BASE。

## 三、META 元领域（quanttide-meta-toolkit）

### 3.1 定义

META 是对各个模块的**总结和再次抽象**——识别出跨模块的共同模式（元模式），归纳为独立领域。

### 3.2 与 BASE 的本质区别

| | BASE/CORE | META（Summarize） |
|--|-----------|-------------------|
| 依赖关系 | 所有库强制依赖 | 可选、模块化依赖 |
| 变更影响 | 全局灾难 | 局部，可独立迭代 |
| 可拆除性 | 拆不掉 | 不好用可拆 |
| 定位 | 强制基础 | 归纳总结 |

### 3.3 核心功能

1. **领域增加**：新领域出现时，沉淀共同模式
2. **一致性治理**：领域间出现混乱时，统一概念、统一概念之间的关系、二次抽象
3. **通用特性**：与各库排列组合，向上层提供通用能力

### 3.4 独立迭代

META 最重要的价值：**可以独立快速迭代**——元规范（统一概念、关系、抽象）不需要等待其他库，以更快模式更新。

## 四、INDEX 入口库（quanttide-index-toolkit）

- 继承 base 历史，**推翻重写**
- 提供入口：人和 AI 从一个库找到所有可用库
- 以 `quanttide` 名义发布（v0.2.0 起），quanttide-* 作为可选插件
- 不提供实际功能 → 可拆除 → 不构成单点

## 五、关系图

```
用户 / AI
    ↓ 查找
quanttide-index-toolkit（入口）
    ↓ 发现
quanttide-toolkit（元仓库：领域 toolkit 列表）
    ↓ 依赖（可选）
quanttide-meta-toolkit（元领域：标准字段/模型）
```

## 六、演进记录

- 2026-08-09：quanttide-base-toolkit 拆解。storage/fields → meta-toolkit（元领域）；base 历史 → index-toolkit（入口库，推翻重写）；quanttide-toolkit 成为元仓库（挂载 10 个领域 toolkit）。
