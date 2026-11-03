# phpdts 代码地图与配置体系

- Scope: `phpdts`
- Topic: `architecture`
- Last updated: `2026-11-03 00:26:08 UTC+8`

## Summary

phpdts（常磐大逃杀）是过程式 PHP 网页游戏：PHP 7.4 兼容语法、MySQL 兼容数据库、自定义模板引擎、浏览器 JavaScript。新 `rev*` 模块与同名旧模块并存，不能仅凭文件名认定入口。`gamedata/cache/` 是受版本控制的正式配置（部分为带访问保护头的逗号分隔资源），不是可清空的生成目录。本仓库 `AGENTS.md` 是权威开发指引。

## Details

### 入口与请求
- 请求初始化/房间/配置：`include/common.inc.php`、`include/global.func.php`、`include/roommng.func.php`
- 玩家页面/指令/保存：`game.php`、`command.php`、`include/game.func.php`
- 移动/搜索/遭遇：`include/game/search.func.php`、`include/game/revbattle.func.php`

### 战斗与属性
- `include/game/revcombat*.php`、`include/game/revattr*.php`、`include/game/revclubskills*.php`；核心能力逻辑在 `revattr_extra.func.php`。

### 道具与任务
- 道具：`include/game/item.main.php` + `item.*.php` + `itemmain.func.php` + `itemmix.func.php`（`item.func.php` 主要是兼容入口）
- 任务/事件/死亡/结局：`quest.func.php`、`event.func.php`、`revevent.func.php`、`item.ending.php`；另有 `state.func.php`、`system.func.php`、`end.php`。

### 资源与规则集
- `gamedata/cache/`、`gamedata/`、`gamedata/ruleset/`；`include/resources.func.php`、`include/ruleset_override.func.php`
- `config($file, $cfg)` 查找顺序：当前 RuleSet 的 `cache/{$file}_{$cfg}.php` → 该 RuleSet 版本 1 → 公共 `gamedata/cache/`。没有 RuleSet 间自动继承。
- RuleSet 注册在 `gamedata/ruleset/ruleset_config.php`；模式逻辑优先 `include/ruleset.func.php`，兼容旧 `include/ruleset_functions.php`。

### 模板
- 源文件 `templates/*/*.htm`，语法 `{$name}` / `<!--{if ...}-->` / `<!--{loop ...}-->` / `{template ...}`；由 `template()` + `include/template.func.php` 编译到 `gamedata/templates/`。
- `nouveau` 缺失的模板回退 `default`；只改源模板，不手改编译产物。

### 数据库
- `include/db_*.class.php`，实际驱动由部署配置选择；`$tablepre` 是房间前缀、`$gtablepre` 是公共前缀。

### 测试
- 无统一测试框架；独立回归脚本（运行需先 `define('IN_GAME', true)`）：`gamedata/tests/quest_q6_test.php`、`gamedata/tests/fcg_test.php` 等，及各 RuleSet 的 `tests/`（LAIKAADVENT / RAIDCAGEDBIRD / FLASH）。

## Constraints and Caveats

- 普通改动保持 PHP 7.4 可用语法；Dockerfile 的 PHP 8.1 只是部署方案之一。
- 没有 composer/yii 工程；README 中的 composer 流程是历史说明。
- 部分 `gamedata/cache/*.php` 是带访问保护头的逗号分隔资源，按原列顺序与格式编辑。
- `doc/20260915-*.md` 评审稿中的建议不是已实装能力。
- 本机无 MySQL：只做 lint 与规格设计，不做站点联调（见 troubleshooting 文档）。

## References

### Related Knowledge

- [HANDOFF 规格工作流](../workflows/handoff-spec-workflow.md)
- [phpdts 常见坑与验证](../troubleshooting/phpdts-pitfalls.md)

### Supporting Worklogs

- [phpdts 首批知识文档创建](../../../../worklogs/members/hermes/projects/phpdts/logs/20261103-002608.md)

### Repositories

| URL | Ref | Commit | Immutable |
| --- | --- | --- | --- |
| https://github.com/amarillonmc/phpdts.git | `nouveau` | `3cc1559265590aecd10c9e4b0ce863edc774185a` | `no` |
