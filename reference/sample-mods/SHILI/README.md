---
title: SHILI 范例 Mod
type: reference
kind: sample-mod
status: active
version: "v1.0"
tags:
  - bg3
  - 范例
  - sample-mod
created: 2026-10-03
updated: 2026-10-03
---

# SHILI 范例 Mod

> [!info] 这是什么
> 第三方教程自带的一个可运行范例 mod，演示了
> **新建武器 / 护甲 / 法术 / 被动、自定义外观、自定义汉化、放进宝箱** 的完整做法。
>
> 目录里的 `.txt` / `.lsx` 文件**带有作者手写的中文注释**，是本工程最有价值的参考资料之一。
> 本工程已对照 `stats-vanilla\` 的实测数据**逐条校正过这些注释**，
> 被更正的地方在注释里标了「【更正】」「【实测补充】」。

## 目录结构

```
SHILI\
├─ Localization\Chinese\       汉化（.xml 是编辑源，.loca 是游戏实际读的）
├─ Mods\SHILI\meta.lsx         mod 身份定义
└─ Public\SHILI\
    ├─ RootTemplates\merged.lsf 物品模板（RootTemplate UUID 指向它的 MapKey）
    └─ Stats\Generated\
        ├─ Data\               武器 / 护甲 / 被动 / 法术
        └─ TreasureTable.txt   宝箱掉落
```

## 本范例演示了什么

| 文件 | 演示内容 |
|---|---|
| `Data\Weapon.txt` | 新建武器、RootTemplate 与 ValueUUID 的作用、`using` 继承、汉化 handle |
| `Data\Armor.txt` | 新建护甲、三级 `using` 继承链（`ARM_Plate_Body` → `_2` → `MAG_Infernal_Plate_Armor`） |
| `Data\Passive.txt` | 被动写法：`StatsFunctorContext` + `Conditions` + `StatsFunctors` |
| `Data\Spell.txt` | 新建法术、修改 `UseCosts` 让它不消耗法术位 |
| `RootTemplates\merged.lsx` | 物品模板的字段含义（MapKey / Name / Stats / DisplayName 四处必须闭环） |
| `TreasureTable.txt` | 把物品放进教学宝箱 `TUT_Chest_Potions` |
| `Localization\Chinese\` | 汉化链路：`.xml` 的 `contentuid` ↔ RootTemplate 的 `DisplayName` handle |

## 已知未完成处（不是可直接运行的完整 mod）

- `Weapon.txt` 里 `PassivesOnEquip` 指向的 `MAG_WYRM_Commander_Longsword_Passive` **没有定义**
- `Passive.txt` 里 `ApplyStatus(SELF, MAG_BONUS_ACTION, ...)` 用到的 `MAG_BONUS_ACTION` 状态**没有定义**
- `.loca` 与 `.lsf` 是二进制，需要分别由 `.xml` / `.lsx` 转成

> 所以它是**写法示范**，不是拿来直接装就能跑通的 mod。

## 相关

- ModMaker 仓库的 `2-工作流\Stats语法与结构.md`
- ModMaker 仓库的 `2-工作流\Stats字段字典.md`
- ModMaker 仓库的 `2-工作流\ScriptExtender实战配方.md`