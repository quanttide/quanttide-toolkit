# quanttide-toolkit ROADMAP

## 预留项（2026-08-10 标注，暂不开发）

| # | 项 | 层 | 说明 |
|---|----|----|------|
| 1 | `quanttide-tech-toolkit` | 应用层 | 跨业务、跨领域流程整合（预留） |
| 2 | `quanttide-feishu-toolkit` | 基础设施层 | 统一底层依赖（预留） |
| 3 | 各领域库 base 依赖清理 | 领域层 | 后续遇到 base 残留逐渐拆解处理 |

## 演进记录

- 2026-08-09：quanttide-base-toolkit 拆解完成。storage/fields → meta-toolkit（元领域）；base 历史 → index-toolkit（入口库）；本仓库成为元仓库（挂载 10 个领域 toolkit）。分层模型见 docs/dev-guide/layering.md。
