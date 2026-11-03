# phpdts 常见坑与验证

- Scope: `phpdts`
- Topic: `troubleshooting`
- Last updated: `2026-11-03 00:26:08 UTC+8`

## Summary

本机环境只做语法检查与规格设计；`php -l` 通过 ≠ 玩法验证。高频坑：模板编译缓存、`gamedata/cache` 误当生成目录、`config()` 被 RuleSet 覆盖、`global`/引用传递、`$now` 时差、`gstrfilter()` 输入安全、回归脚本不替代联调。

## Details

### 本机 lint
```sh
php -d short_open_tag=1 -l include/game/item.main.php
```
- 本机 PHP 7.4.32（绝对路径调用）；仓库保留部分短标签，lint/运行需 `short_open_tag=1`。

### 模板不生效
- 检查实际模板选择、`$tplrefresh` 与编译缓存（`gamedata/templates/`）；清理走已有入口，勿删正式资源目录。

### 配置与缓存
- `gamedata/cache/` 是受版本控制的正式配置；部分 `.php` 实为带访问保护头的逗号分隔资源，按原列顺序与格式编辑。
- `config($file, $cfg)` 优先返回当前 RuleSet 的同名 cache 配置；修改前确认实际加载哪份，勿批量同步所有副本。

### 状态与引用
- `include` 继承调用处变量作用域；`global`、引用参数、`extract($data, EXTR_REFS)`、动态物品槽（itm0 待拾取 / itm1–itm6 背包）常见。
- 改状态前确认操作对象与保存时机：玩家经 `player_save()`，房间经 `save_gameinfo()`；勿让旧数组覆盖刚写入的结果。
- `clbpara`、物品 `para` 有 JSON 与数组两种形态，沿用 `get_clbpara()` / `get_itmpara()`。
- 时间基准沿用调用链的 `$now`（含部署时差），勿与 `time()` 混用。

### 输入与安全
- `gstrfilter()` 是旧输入过滤，不保证 SQL/HTML 上下文安全；SQL 按实际驱动处理、输出按上下文转义。

### 验证口径
- 功能改动至少检查直接相关的正常操作与失败分支；涉及奖励/进度/共享状态时检查重复提交与重载。
- 回归脚本（`gamedata/tests/`、各 RuleSet `tests/`）不能替代真实站点联调；不能连库/开站时如实说明未验证部分。
- 提交前 `git diff --check` 与完整 diff；勿提交运行数据、缓存或无关变动。

## Constraints and Caveats

- `config.inc.php.sample` 的旧 `mysql` 驱动配置不能直接用于 PHP 7.4/8。
- `doc/etc/debug_archive/` 是历史调试资料，不是可批量执行的测试套件。

## References

### Related Knowledge

- [phpdts 代码地图与配置体系](../architecture/phpdts-codebase-map.md)

### Supporting Worklogs

- [phpdts 首批知识文档创建](../../../../worklogs/members/hermes/projects/phpdts/logs/20261103-002608.md)

### Repositories

| URL | Ref | Commit | Immutable |
| --- | --- | --- | --- |
| https://github.com/amarillonmc/phpdts.git | `nouveau` | `3cc1559265590aecd10c9e4b0ce863edc774185a` | `no` |
