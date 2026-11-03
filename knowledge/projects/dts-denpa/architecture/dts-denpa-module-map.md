# dts-denpa 模块地图（电波版）

- Scope: `dts-denpa`
- Topic: `architecture`
- Last updated: `2026-11-03 00:26:10 UTC+8`

## Summary

电波版（dts-denpa）是模块化组织的 PHP 游戏仓库（分支 `Unstable`，当前版本 v2.4.8）。结构核心为 `include/modules/`（base 基础玩法 / extra 扩展内容 / core 系统），模块启停由 `gamedata/modules.list.php` 控制；卡片系统数据集中在 `include/modules/extra/card/`。与常磐版（phpdts）同世界观但实现独立，跨版知识必须分版记录。

## Details

### 版本与发布
- 分支 `Unstable`；版本号在 `include/modules/core/sys/config/version.config.php`（v2.4.8）。
- 发布历史文本：`templates/default/updatelist_2024.htm`、`updatelist_2025.htm`。

### 基础模块（base）
- NPC：`include/modules/base/npc/`、`include/modules/base/addnpc/`
- 道具：`include/modules/base/itemmain/`、`include/modules/base/itemmix/`
- 开场/结局故事板：`include/modules/base/opening/`、`include/modules/base/ending/`

### 扩展模块（extra）
- 卡片：`include/modules/extra/card/cardbase/config/card.config.php`（卡面文本/效果登记）、`include/modules/extra/card/skills/`
- 社团/成就：`include/modules/extra/club/skills/`、`include/modules/extra/achievement/skills/`
- 活动/副本：`include/modules/extra/activities/`、`include/modules/extra/instance/`（如 `instance10_rogue`、`instance12_dream`）
- 属性扩展：`include/modules/extra/attr/`（如 `ex_armor_crack`）

### 索引与房间
- 技能 ID 索引：`include/modules/skill_table.readme.txt`（技能 ID → 名称）
- 房间管理：`include/roommng/`；模块清单：`gamedata/modules.list.php`

## Constraints and Caveats

- 卡片/技能/NPC 机制一律以配置文件实际挂载为准，不按名称猜机制。
- 与常磐版（phpdts）同世界观不同实现：机制、卡池、术语分版记录，不把电波独有内容反推到常磐。
- 本仓库只读参考；改动由开发机完成。

## References

### Related Knowledge

None.

### Supporting Worklogs

- [dts-denpa 首批知识文档创建](../../../../worklogs/members/hermes/projects/dts-denpa/logs/20261103-002610.md)

### Repositories

| URL | Ref | Commit | Immutable |
| --- | --- | --- | --- |
| https://github.com/winddramon/dts.git | `Unstable` | `ba8f607a57d5352327113f41b32676d16fe7c3ba` | `no` |
