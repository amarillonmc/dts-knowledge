# HANDOFF 规格工作流

- Scope: `phpdts`
- Topic: `workflows`
- Last updated: `2026-11-03 00:26:08 UTC+8`

## Summary

设计阶段不动源码；设计侧只写「位置+改法」规格文档，交由开发机 LLM 实装；实装成功后废弃对应 HANDOFF 文件。评审稿不是实装状态；读代码现状前先 pull。

## Details

### 流程
1. 设计阶段只产出规格，写入 `doc/design/`（例：`zhenjiejin_jiaotou_spec.md`），内容为「在哪里改 / 改什么 / 怎么改」。
2. HANDOFF 文件**不进入 phpdts 仓库**，由 Nemo 手动经 RDP 交付开发机 LLM 实装。
3. 实装成功后废弃删除对应 HANDOFF 文件。
4. 玩法/逻辑/数据格式改动在 `doc/YYYYMMDD-HHMMSS-<描述>.txt` 留简短记录（中文为主）：改了什么、为什么、如何验证、已知限制。

### 设计铁律（团队约定）
- 玩家与 NPC 同 Player 对象（type=0）：新机制做双档设计（NPC 全功率 / 玩家档缩范围加成本）。
- 多人任务/公共事件：NPC 全局单实例（不按玩家数复刷）；全局资源（如天气）不得被任务滥用。
- 任务解法 build-agnostic：不强制特定武器系/熟练度。
- 复用旧机制前先查 `doc/etc/` 封存史；修过但从未实测的机制只走个人特判，不碰全局开关。
- 涉及实现现状的核对：先 `git pull`（当前分支 `nouveau`）再读代码——设计规格与实装可能已分叉。

## Constraints and Caveats

- 设计侧只写规格，不改源码；改代码的始终是开发机 LLM。
- 「设计已定但实现冲突」的点只在修订注记里标「待 XX 拍」，不替玩法负责人拍板。

## References

### Related Knowledge

- [phpdts 代码地图与配置体系](../architecture/phpdts-codebase-map.md)

### Supporting Worklogs

- [phpdts 首批知识文档创建](../../../../worklogs/members/hermes/projects/phpdts/logs/20261103-002608.md)

### Repositories

| URL | Ref | Commit | Immutable |
| --- | --- | --- | --- |
| https://github.com/amarillonmc/phpdts.git | `nouveau` | `3cc1559265590aecd10c9e4b0ce863edc774185a` | `no` |
