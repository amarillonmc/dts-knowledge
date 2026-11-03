# Team Repository Instructions（DTS 团队知识仓库）

《常磐大逃杀》(DTS) 团队的协作知识仓库，基于 [Da'at 框架](https://github.com/purerosefallen/da-at)（MIT）改造。本文件是所有协作 agent（Hermes、开发机 LLM 等）在本仓库内必须遵守的规则。

## Repository Language（双语规则）

- 文件名、目录名、时间戳文件名：英文、lowercase kebab-case（git 安全）。
- 文档内容、标题、索引条目、worklog 正文：中文、英文或双语皆可。
- Member 与 Project 名按下方命名规则。
- **内容安全边界（铁则）**：本仓库存放于 GitHub，可能公开。全部内容必须**表设定安全**——只写玩家可见层面的事实（表设定 = GitHub + bbs + phpdts 玩家可见内容）。**严禁**写入里设定（V4BB 层设定、种火语、时空帧体系、最高机密等）的名词、解释与因果。涉及里设定的改动只以中性技术层面记录（改了哪些文件、规格名、游戏内表现），细节归 Nemo 的私有知识仓库（skill knowledge/）或 V4BB。
  - 一句话自检：**玩家看到这条日志/知识也不会损失任何东西**——不通过就改写或删掉。

## Required Task Workflow（pull 触发式）

本仓库的主要写入时机 = **拉取游戏仓库并确认实际改动**。触发条件：

- Nemo 让我 pull phpdts（或 dts-denpa / amarillonmc.github.io）；或
- 我自己按工作规则 pull 上述仓库（如「凡涉及实现现状的核对先 git pull」）；或
- Nemo 明确要求写一条 worklog。

流程：

1. pull 对应游戏仓库，记录 pull 前/后的 commit 范围（无新 commit = no-change，不写日志）。
2. 用 `git log <old>..<new>` / `git diff --stat` 确认**实际落地了什么**（不写推测、不写未发生的计划）。
3. 读本仓库相关 worklog 与 knowledge。
4. 每个受影响项目写一条 worklog，更新所有受影响 INDEX。
5. commit。remote 未配置时只 commit 不 push（Nemo 手动同步，或由他配置 remote 后再 push）。

## Fixed File Contracts

仓库根目录固定文件：

- `README.md`：仓库标题、用途、内容地图与两份规则文件的链接。
- `AGENTS.md`：任务工作流、worklog 契约、知识读取工作流、参考仓库用法与交付检查。
- `UPDATE_KNOWLEDGE.md`：创建、组织、更新知识的唯一规则。
- `LICENSE`：Da'at 框架的 MIT 协议；README 说明其范围与下游内容归属。
- `.gitignore`：排除完整的 `/ref-repos/` 缓存。
- `ref-repo.sh`：物化浅层参考 checkout 并输出其绝对路径。
- `_example/`：动态根目录下的保留模板目录名。绝不把 `_example` 用作真实成员/项目名，绝不视其内容为运营记录。

当上述文件之一能承载某条规则时，不新增根级流程文档。

## Member and Project Names

Member 名取自 `git config user.name`，trim 空白、`/` 替换为 `-`，保持单一路径段。为空则先配置身份再写 worklog。

本仓库预注册的 DTS 规范项目名（优先于 origin 推导）：

- `phpdts` — 常磐版游戏源码（当前分支 `nouveau`）
- `dts-denpa` — 电波版（当前分支 `Unstable`）
- `amarillonmc-github-io` — 设定站
- `dts-knowledge` — 本仓库自身

其它仓库按上游规则推导：`<namespace>_<repository>`（去 `.git`、嵌套 namespace 以 `-` 连接、路径不安全字符替换为 `-`）；仓库外目录 = `nongit-<directory-name>`；无法判定 = `misc`。

## Creating Worklog Directories

绝不手工拼装 member / project 目录树。

- `worklogs/members/<member>/` 不存在时，复制 `worklogs/members/_example/`。将复制出的 member `INDEX.md` 中的 `_example` 替换为真实成员名，保留复制出的 `projects/_example/` 模板，并把成员加入 `worklogs/INDEX.md`。
- `worklogs/members/<member>/projects/<project>/` 不存在时，复制该成员的 `projects/_example/`。替换 `_example` 值，把示例日志重命名为本次任务时间戳，替换全部示例日志内容，并把项目加入成员索引。

实例化时不得改动源 `_example` 树，不得把 `_example` 列入真实成员/项目表。

## Worklog Tree and File Contracts

Worklog 树：

```text
worklogs/
  INDEX.md
  members/
    <member>/
      INDEX.md
      projects/
        _example/
          INDEX.md
          logs/
            20000101-000000.md
        <project>/
          INDEX.md
          logs/
            <timestamp>.md
```

`<timestamp>` 以 UTC+8 生成：

```sh
TZ=Asia/Shanghai date '+%Y%m%d-%H%M%S'
```

目标文件名已存在则等下一秒，绝不覆盖日志。

### Root Worklog Index

`worklogs/INDEX.md` 必须恰含一个标题与成员表：

```markdown
# Worklog Members

## Template

- [Example structure](members/_example/INDEX.md)

## Members

| Member | Index |
| --- | --- |
| `<member>` | [Open](members/<member>/INDEX.md) |
```

真实成员按目录名字典序排列，`_example` 不入成员表。

### Member Index

`worklogs/members/<member>/INDEX.md`：

```markdown
# <member> Projects

## Template

- [Example project structure](projects/_example/INDEX.md)

## Projects

| Project | Index |
| --- | --- |
| `<project>` | [Open](projects/<project>/INDEX.md) |
```

真实项目按目录名字典序排列，`_example` 不入项目表。

### Project Index

`worklogs/members/<member>/projects/<project>/INDEX.md`：

```markdown
# <project> Worklogs

| Timestamp | Status | Summary | Log |
| --- | --- | --- | --- |
| `YYYYMMDD-HHmmss` | `<status>` | <one-line summary> | [Open](logs/<timestamp>.md) |
```

按时间倒序排列。Status 为 `completed`、`partial`、`blocked`、`failed`、`no-change` 之一。

### Worklog Document

每条 `logs/<timestamp>.md` 必须包含以下全部标题（无条目写 `None`）：

```markdown
# <Task title>

- Timestamp: `YYYY-MM-DD HH:mm:ss UTC+8`
- Member: `<member>`
- Project: `<project>`
- Status: `<status>`

## Objective

<Goal and requested scope.>

## Work Performed

<Actions, investigations, and changes.>

## Results

<Outcome and material decisions.>

## Validation

| Command or Check | Result |
| --- | --- |
| `<command or check>` | <observed result> |

## Limitations and Follow-up

<Remaining limitations or follow-up work, or `None`.>

## References

### Repositories

- `<repository URL>` at `<full commit hash>`

### Documents

- [<document title>](<relative path>)

### Related Worklogs

- [<project and timestamp>](<relative path>)
```

每个受影响项目一条日志；跨项目任务的所有日志须在 `Related Worklogs` 互链。仓库内文档用相对 Markdown 链接。保留历史日志，仅可修正不准确内容或坏链。

## Reading Knowledge

知识分两个 scope：`knowledge/common/`（跨项目通用）与 `knowledge/projects/<project>/`（项目专属）。

阅读顺序：

1. 打开 `knowledge/INDEX.md` 定位 scope。
2. 打开 scope 的 `INDEX.md` 选择主题。
3. 打开主题的 `INDEX.md` 定位文档。
4. 阅读所选文档，跟随其关联知识与支撑 worklog 链接。
5. 需要仓库源码时，用 `ref-repo.sh` 物化并记录 URL、ref、resolved commit 与不可变状态。

不得凭旧的可变分支引用推断当前行为；依赖前先用 `ref-repo.sh` 刷新。

### Reuse-Driven Engineering Migration

仅当当前任务引用了某知识文档、该知识无对应 tool 项目、且其逻辑有可复用价值时，按 [Reuse-driven migration](UPDATE_KNOWLEDGE.md#reuse-driven-migration) 迁移。这是对该有界知识更新及其必需 worklog 的常设授权；明确限定只读的任务优先。

对应 tool 项目已存在时，不得静默迁移或重写其知识——此类知识迁移需 Nemo 明确要求。按现状使用既有工程化项目，不得仅为改进工程性或对齐新模板而重设计/重打包/移动/重构。不得在迁移过程中扩大授权操作。无关 tool 或空的 `tools/` 目录不触发此限制。

## Reference Repositories

```sh
./ref-repo.sh [--immutable] <repo-url> <ref>
```

- tag 用 `--immutable`；完整 commit hash 自动视为不可变；分支等可变 ref 省略该参数。
- 返回的 checkout 视为一次性只读参考材料；绝不把 `ref-repos/` 下内容提交入库。
- 引用时注明原始 URL 与 resolved commit，不引用缓存路径。

## Delivery Checks

提交前核对：

- 新文件名英文 kebab-case；内容可中文（双语合规）；
- **表设定安全自检通过**（里设定零泄漏）；
- 所有新文件符合本文或 `UPDATE_KNOWLEDGE.md` 的契约；
- 受影响 INDEX 的相对链接有效；
- 跨项目日志互相链接；
- 无 `ref-repos/` 内容被跟踪；
- 每条 worklog 记录了实际执行的验证。

只提交本次仓库管理相关的改动，不混入无关的项目改动。
