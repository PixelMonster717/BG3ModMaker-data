---
title: Larian 官方模组文档
type: reference
kind: official-docs
status: active
version: "v1.0"
tags:
  - bg3
  - 参考
  - 官方文档
created: 2026-10-04
updated: 2026-10-04
---

# Larian 官方模组文档（抓取存档）

> [!info] 这是什么
> [docs.baldursgate3.game](https://docs.baldursgate3.game/) —— **Larian 官方的 BG3 模组文档**，
> 随官方 Modding Toolkit 一同发布。共抓取 **12 页**存档于此，便于离线查阅与检索。
>
> 完整站点可访问，需要其他页面时告诉我页面名即可抓取。

## 已归档页面

### 入门

| 页面 | 大小 | 内容 |
|---|---|---|
| `reference\larian-docs\入门-最佳实践.md` | 3.4 KB | Best Practices |
| `reference\larian-docs\入门-新建mod.md` | 4.8 KB | 用 Toolkit 新建 mod 的流程 |
| `reference\larian-docs\入门-发布mod.md` | 8.5 KB | 发布到 mod.io 的流程 |

### 编辑器

| 页面 | 大小 | 内容 |
|---|---|---|
| `reference\larian-docs\编辑器-覆盖资源.md` | 6.0 KB | **覆盖原版资源**的做法（与 Stats 覆盖式加载同理） |

### 制作物品

| 页面 | 大小 | 内容 |
|---|---|---|
| `reference\larian-docs\创建武器.md` | 4.6 KB | |
| `reference\larian-docs\创建护甲.md` | 8.6 KB | |
| `reference\larian-docs\添加护甲.md` | 14.8 KB | |
| `reference\larian-docs\制作基础法术.md` | 19.2 KB | 篇幅最大，含完整法术流程 |
| `reference\larian-docs\添加技能与物品图标.md` | 7.9 KB | **图标**相关——本工程一直缺外观资源知识 |

### 脚本

| 页面 | 大小 | 内容 |
|---|---|---|
| `reference\larian-docs\脚本-总览.md` | 0.8 KB | |
| `reference\larian-docs\脚本-Osiris入门.md` | 7.2 KB | **Osiris** —— 游戏内事件系统 |
| `reference\larian-docs\脚本-Anubis入门.md` | 1.1 KB | **Anubis** —— Osiris 的新版替代 |

> [!warning] 官方文档讲的是 Osiris/Anubis，不是 Script Extender
> Script Extender 是**第三方**项目，官方文档不含它。
> 两者的关系：
>
> | | 官方 | 本工程 |
> |---|---|---|
> | 脚本系统 | Osiris / Anubis（游戏内置） | [Script Extender](https://github.com/Norbyte/bg3se)（第三方 DLL） |
> | 能力 | 事件钩子、DB 查询 | 完整的实体/组件访问、Lua |
>
> 本工程用 SE，因为需要**读组件**（如判断装备了哪几件），
> 而 Osiris 做不到。但官方文档对理解**游戏的数据组织方式**仍有价值。

## 与现有资料的分工

| 资料 | 性质 | 该怎么用 |
|---|---|---|
| **`larian-docs\`** | **官方流程与编辑器操作** | 做新东西前先看有没有官方讲法 |
| `bg3-schema\` | 数据架构定义（字段/取值） | 查字段含义 |
| `stats-vanilla\` | 原版数据原文 | 查"有没有人这么写" → **最权威** |
| ModMaker `2-工作流\` | 本工程实测结论 | 踩过的坑与验证过的写法 |

## 未归档但值得抓的页面

站点上还有这些页面，需要时告我：
`Adding_Classes_and_Subclasses`、`Making_a_Projectile_Spell`、`Projectiles`、
`UI:_Setting_Up`、`UI:_Extending_UI`、`Journal`、`Adding_Dice`、
`VFX`（4 篇）、`Animation:_Creating_Shortnames`、`Hair_and_Beards`（4 篇）、
`Generating_Icons_for_Character_Creation`

## 抓取方式（供复现）

站点可直接访问。**用 PowerShell 的 `Invoke-WebRequest`**，
不要用 Python 的 `urllib`（后者因证书验证失败）。

提取正文的关键点：

1. 正文在 `mw-parser-output` 那个 div 里，但 class 可能是
   `class="mw-content-ltr mw-parser-output"`，**不能按 `class="mw-parser-output"` 字面匹配**
2. 目录框 `<div id="toc">` 要剔除，且**必须按 div 配平计数**——
   用非贪婪正则会停在第一个 `</div>`，把正文一起吃掉

## 相关

- `reference\bg3-schema\README.md`（本库）
- ModMaker 仓库的 `2-工作流\环境与工具链.md`
