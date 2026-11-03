# DTS Team Knowledge Repository（DTS 团队知识仓库）

《常磐大逃杀》(DTS) 团队的协作知识仓库：worklog（谁实际改了什么）+ 可复用知识（怎么改、为什么）。基于 [Da'at](https://github.com/purerosefallen/da-at) 框架（MIT），按 DTS 需要改造：双语内容、pull 触发式日志、表设定安全边界。

## 为什么存在

多人多 agent 协作（Nemo / NazoBlaster / 开发机 LLM / Hermes），改动只以 commit 形式落盘，缺少"实际落地了什么"的团队可见日志。本仓库按项目记录 phpdts（常磐版）、dts-denpa（电波版）、amarillonmc.github.io（设定站）的实际改动与可复用知识。

## Repository Structure

- `worklogs/` — 按成员/项目/时间戳记录的实际改动日志
- `knowledge/` — 沉淀后的可复用知识（架构 / 流程 / 运维 / 排障 / 决策 + 小工具）
- `AGENTS.md` — 本仓库的 agent 工作流与契约
- `UPDATE_KNOWLEDGE.md` — 知识创建、组织、更新的唯一规则
- `ref-repo.sh` — 外部仓库浅层参考 checkout 工具
- `_example/` — 模板目录，不代表真实数据

## 语言与安全

- 文件名英文（lowercase kebab-case），文档内容中英双语皆可。
- **表设定安全铁则**：本仓库可能公开，内容只写到玩家可见层面；里设定细节留在 Nemo 的私有知识仓库与 V4BB，禁止入此库。

## Getting Started

写一条 worklog 或创建知识的完整规则见 `AGENTS.md` 与 `UPDATE_KNOWLEDGE.md`。参考 checkout：

```shell
./ref-repo.sh <repo-url> <ref>
```

## 上游

框架基于 [Da'at](https://github.com/purerosefallen/da-at)，MIT License。框架部分版权归上游，本仓库 DTS 内容归团队所有。
