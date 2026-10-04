---
title: bg3-schema 索引
type: reference
kind: schema
status: active
version: "v1.0"
tags:
  - bg3
  - 参考
  - schema
created: 2026-10-04
updated: 2026-10-04
---

# bg3-schema（第三方数据架构参考）

> [!info] 这是什么
> [NellsRelo/bg3-schema](https://github.com/NellsRelo/bg3-schema) —— BG3 的
> **Stats 与 LSX Region 架构定义**。作者扫描解包的游戏文件，整理出每种数据类型的
> **完整字段列表、取值、默认值与交叉引用**。
>
> 归档于 `reference\bg3-schema\`，326 个文件 / 约 1.3 MB。

> [!warning] 作者自己的免责声明（转述）
> README 里明确写着：本资料是**用 AI 扫描解包文件**整理而成，
> 「大部分信息经过核对，也采取了措施降低臆造风险，但**不要盲信这份 schema**——
> 可能有错，**最权威的来源始终是解包后的游戏文件本身**。」
>
> **本工程的用法**：把它当**索引与线索**，不当结论。
> 任何要写进代码的字段，都用 `query-stats.cmd` 回原版数据核对一遍
> （原版 `stats-vanilla\` 才是实测来源）。

## 与现有资料的分工

| 资料 | 性质 | 该怎么用 |
|---|---|---|
| `stats-vanilla\` | **实测数据**：原版全部条目原文 | 查"有没有人这么写"、抄写法 → **权威** |
| **`bg3-schema\`** | **结构说明**：字段含义、取值、交叉引用 | 查"这个字段是干什么的" → **索引** |
| `root-templates\` | 原版模板文件 | 复用/复制模板 |
| `equipment-list\` | 装备清单（中文名、效果、获取） | 找同类装备参考 |
| `larian-docs\` | 官方模组文档 | 流程与编辑器操作 |

**典型配合方式**：

```
① 在 bg3-schema 里查到「PassiveData 有 Boosts 字段，取值是 functor 表达式」
② 在 functor-boosts.md 里查到 Ability 的正确写法
③ 用 query-stats.cmd 回原版核对：这个写法真的有人用吗、用了几次
④ 照抄写法
```

## 目录结构

### `stats\` —— 最有价值的部分

| 路径 | 内容 |
|---|---|
| `stats\types\*.md` | **9 种数据类型的完整字段表**：`Armor` / `Weapon` / `Object` / `PassiveData` / `SpellData` / `StatusData` / `Character` / `InterruptData` / `CriticalHitTypeData` |
| `stats\reference\functors-boosts.md` | **Boost / Functor 函数大全**（30 KB）——写效果时查这个 |
| `stats\reference\functor-contexts.md` | `StatsFunctorContext` 的实体映射 |
| `stats\reference\inheritance.md` | `using` 继承、合并、加载顺序 |
| `stats\reference\per-type-form-reference.md` | 各类型的字段速查（43 KB） |
| `stats\formats\*.md` | 非类型化格式：`TreasureTable` / `Equipment` / `SpellSet` / `Modifiers` / `ValueLists` / `ItemCombos` / `SpecialDataFiles` |

### `regions\` —— LSX 区域定义

118 个区域，每个含 `_REGION.md`（索引）+ 各节点类型说明。
用于编辑 `.lsx`（RootTemplate 等）时查「这个字段什么意思、能填什么」。

### `content-banks\` —— 资源库定义

61 个资源库类型（动画、材质、视觉、特效等）。做**自定义外观**时用。

## 与本工程实测结论的对照提示

有几处本工程已实测、值得注意的地方：

| 主题 | 本工程实测 | 说明 |
|---|---|---|
| `BoostContext` / `BoostConditions` | **只在 `PassiveData` 上**（Armor/Weapon 上 0 例） | 若 schema 把这些字段列在 Armor 上，以实测为准 |
| `HasStatus` 必须带 `context.Source` | 原版 14 处用例的规律 | 这是最容易静默失效的一条 |
| `ValueUUID` 非必需 | 装备类 3133 条中 75.9% 没有它 | 但本工程约定统一写上 |

## 更新方式

上游更新时，重新下载并覆盖：

```powershell
$dl = "$env:USERPROFILE\Downloads\bg3-schema-main.zip"
Invoke-WebRequest -Uri 'https://codeload.github.com/NellsRelo/bg3-schema/zip/refs/heads/main' -OutFile $dl
Expand-Archive -LiteralPath $dl -DestinationPath "$env:TEMP\schema" -Force
# 再把 stats\ / regions\ / content-banks\ 覆盖到本目录
```

## 相关

- `reference\larian-docs\README.md`（本库）
- ModMaker 仓库的 `2-工作流\Stats字段字典.md`（本工程对原版数据的实测统计）
- ModMaker 仓库的 `2-工作流\Stats语法与结构.md`
