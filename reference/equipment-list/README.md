---
title: 装备参考索引
type: reference
kind: equipment-list
status: active
version: "v2.0"
tags:
  - bg3
  - 装备参考
created: 2026-10-04
updated: 2026-10-04
---

# 装备参考 · 索引

> [!info] 这是什么
> 作者整理的《博德之门3装备合集》，按部位分类的**原版装备数据库**。
> 共 **12 类、约 680 条**。
>
> **用途**：做装备 mod 时找同类参考——
> 想知道某效果怎么实现、某品质的数值区间、某部位有哪些原版装备，都可以从这里入手。
> 找到目标后，用 `query-stats.cmd entry <条目名>` 拿它的完整 Stats 定义照抄。

## 分类

### 装备部位

| 分类 | 条数 | 文件 | RootTemplate UUID |
|---|---|---|---|
| 头部装备 | 55 | [[reference/equipment-list/头冠与头盔\|头冠与头盔]] | **已填 50/51** |
| 背部装备 | 18 | [[reference/equipment-list/披风\|披风]] | **已填 16/16** |
| 身体装备 | 76 | [[reference/equipment-list/护甲与服装\|护甲与服装]] | 未收录 |
| 手部装备 | 77 | [[reference/equipment-list/手套\|手套]] | 未收录 |
| 脚部装备 | 39 | [[reference/equipment-list/靴子\|靴子]] | 未收录 |
| 副手装备 | 29 | [[reference/equipment-list/盾牌\|盾牌]] | 未收录 |

> [!note] 关于「护甲与服装」
> 这一类里同时包含**护甲**和**不提供 AC 的服装/法袍**（如水木法袍、投毒者长袍）。
> 区分方式：看「护甲AC」列是否有值。

### 饰品

| 分类 | 条数 | 文件 |
|---|---|---|
| 饰品 | 62 | [[reference/equipment-list/项链\|项链]] |
| 饰品 | 66 | [[reference/equipment-list/戒指\|戒指]] |

### 武器

| 分类 | 条数 | 文件 |
|---|---|---|
| 武器 | 195 | [[reference/equipment-list/近战武器\|近战武器]] |
| 武器 | 25 | [[reference/equipment-list/远程武器\|远程武器]] |

### 参考

| 分类 | 条数 | 文件 |
|---|---|---|
| 状态说明 | 29 | [[reference/equipment-list/异常状态\|异常状态]] |
| Boost 写法 | 54 | [[reference/equipment-list/输出与附加伤害\|输出与附加伤害]] |

> [!tip] 「输出与附加伤害」是最实用的一张
> 它把**效果说明**与对应的 **Boost 函数写法**并列，例如：
>
> | 名称 | 写法 |
> |---|---|
> | 添加反应资源 | `ActionResource(ReactionActionPoint,1,0)` |
> | 添加附赠动作资源 | `ActionResource(BonusActionPoint,1,0)` |
> | 添加法术位（一环） | `ActionResource(SpellSlot,1,1)` |
>
> **从「想做什么效果」反查到「该写什么函数」**，这一张表最直接。
> 动手写 Stats 前先在这里找一遍，能省掉大量试错。

## RootTemplate UUID 的覆盖情况

**只有「头冠与头盔」与「披风」两张表收录了 UUID**，其余表需要另外查。

```powershell
# 已知原版条目名时，直接查完整定义（含 RootTemplate）
.\query-stats.cmd entry ARM_TalismanOfJergal
```

> [!warning] RootTemplate 必须指向真实存在的模板
> 编造的 UUID 会让物品**创建不出来**（表现为「给了也拿不到」）。
> `check-mod.ps1` 的检查 1 会验证这一点。

## 数据来源与维护

- 原始文件：作者的 `博德之门3装备合集.xlsx`（12 个工作表）
- 本目录由脚本从 xlsx 转换而来，**表格内容原样保留**
- 缺失的 RootTemplate UUID 待作者补充后用同一脚本重转

> [!note] 为什么不把 xlsx 放进仓库
> Markdown 便于 Obsidian 检索、diff 与 wikilink；
> xlsx 是二进制，改动无法逐行比对。需要编辑时改 xlsx 后重转即可。

> [!warning] 转换时的一个坑（记录备查）
> xlsx 里的**工作表名与实际内容不一致**，例如名为「服装」的表装的是披风、
> 名为「项链」的表装的是盾牌。转换脚本因此**按工作表索引映射显示名**，
> 不依赖 sheet 名。修改 xlsx 时若**调整了工作表顺序或增删工作表**，
> 需要同步修改转换脚本的索引映射。

## 相关

- [[2-工作流/Stats字段字典|Stats 字段字典]]
- [[2-工作流/Stats语法与结构|Stats 语法与结构]]
- [[2-工作流/ScriptExtender实战配方|Script Extender 实战配方]]