---
title: 装备参考索引
type: reference
kind: equipment-list
status: active
version: "v1.0"
tags:
  - bg3
  - 装备参考
created: 2026-10-04
updated: 2026-10-04
---

# 装备参考 · 索引

> [!info] 这是什么
> 作者整理的《博德之门3装备合集》，按部位分类的**原版装备数据库**。
> 共 **12 类、约 700 条**。
>
> **用途**：做装备 mod 时找同类参考——
> 想知道某效果怎么实现、某品质的数值区间、某部位有哪些原版装备，都可以从这里入手。
> 找到目标后，用 `query-stats.cmd entry <条目名>` 拿它的完整 Stats 定义照抄。

## 分类

### 装备部位

| 分类 | 条数 | 文件 | RootTemplate UUID |
|---|---|---|---|
| 头部装备 | 55 | [[reference/equipment-list/头冠与头盔\|头冠与头盔]] | 已填 50/51 |
| 身体装备 | 76 | [[reference/equipment-list/护甲与中装\|护甲与中装]] | 未收录 |
| 身体装备 | 18 | [[reference/equipment-list/服装\|服装]] | 已填 16/16 |
| 手部装备 | 77 | [[reference/equipment-list/手套\|手套]] | 未收录 |
| 脚部装备 | 39 | [[reference/equipment-list/靴子\|靴子]] | 未收录 |
| 背部装备 | 62 | [[reference/equipment-list/披风\|披风]] | 未收录 |

### 饰品

| 分类 | 条数 | 文件 | RootTemplate UUID |
|---|---|---|---|
| 饰品 | 66 | [[reference/equipment-list/戒指\|戒指]] | 未收录 |
| 饰品 | 29 | [[reference/equipment-list/项链\|项链]] | 未收录 |

### 武器

| 分类 | 条数 | 文件 | RootTemplate UUID |
|---|---|---|---|
| 武器 | 195 | [[reference/equipment-list/近战武器\|近战武器]] | 未收录 |
| 武器 | 25 | [[reference/equipment-list/远程武器\|远程武器]] | 未收录 |

### 参考

| 分类 | 条数 | 文件 |
|---|---|---|
| 状态说明 | 29 | [[reference/equipment-list/异常状态\|异常状态]] |
| Boost 写法 | 55 | [[reference/equipment-list/输出与附加伤害\|输出与附加伤害]] |

> [!note] 两个参考表说明了什么
> - **异常状态**：原版状态效果的名称与效果描述
> - **输出与附加伤害**：把「效果说明」与对应的 **Boost 函数写法** 并列，
>   例如「雇佣兵资源 → `ActionResource(BonusActionPoint,1,0)`」。
>   这是**从效果反查 Boost 写法**最直接的一张表。

## RootTemplate UUID 的覆盖情况

**只有「头冠与头盔」与「服装」两张表收录了 UUID**，其余表需要另外查。

三种查法（优先级从高到低）：

```powershell
# 1. 已知原版条目名时，直接查它的完整定义
.\query-stats.cmd entry ARM_TalismanOfJergal

# 2. 只记得中文名时，先在装备参考里找到它，再查条目名
#    （本目录各表都带"名称"列）

# 3. 需要某部位的所有原始物品模板时
.\query-stats.cmd field RootTemplate
```

> [!tip] RootTemplate 必须指向真实存在的模板
> 编造的 UUID 会让物品**创建不出来**（表现为「给了也拿不到」）。
> 详见 ModMaker 的 `2-工作流\ScriptExtender实战配方.md` 与 `Stats语法与结构.md`。

## 数据来源与维护

- 原始文件：作者的 `博德之门3装备合集.xlsx`
- 本目录由脚本从 xlsx 转换而来，**表格内容原样保留**
- 缺失的 RootTemplate UUID 待作者补充后用同一脚本重转

> [!note] 为什么不把 xlsx 放进仓库
> Markdown 便于 Obsidian 检索、diff 与 wikilink；
> xlsx 是二进制，改动无法逐行比对。需要编辑时改 xlsx 后重转即可。

## 相关

- [[2-工作流/Stats字段字典|Stats 字段字典]]
- [[2-工作流/Stats语法与结构|Stats 语法与结构]]
- [[2-工作流/ScriptExtender实战配方|Script Extender 实战配方]]
