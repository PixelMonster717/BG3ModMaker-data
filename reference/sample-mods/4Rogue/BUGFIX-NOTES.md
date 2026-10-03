# 4Rogue 旧代码：流血重复触发的根因存档

> 状态：**已归档，不再维护**。作者将重新设计，本目录仅作为案例参考保留。
> `src\` 里的括号笔误已修复，但**产物从未部署进游戏**，也未经过实测验证。

---

## 症状

作者描述："某个流血 debuff 会重复判断多次" —— 定义为只触发 1 次的 DOT 却触发多次。

## 根因

`src\Public\4Rogue\Stats\Generated\Data\Passive.txt` 第 33 行，
条目 `4Rogue_AssassinArt2_Passive` 的 `Conditions` 字段末尾多了一个右括号：

```
data "Conditions" "not WearingArmor(context.Source) and not HasShieldEquipped(context.Source) and IsWeaponAttack() and HasAdvantage() and not HasDisadvantage())"
                                                                                                                                                      ↑ 多这一个
```

对照同文件第 24 行 `4Rogue_AssassinArt1_Passive`，条件串**逐字相同但括号配平** —— 证明这是单点笔误，
不是设计意图。

## 因果链

1. 条件串括号不配平，BG3 解析**不报错**，而是**静默丢弃整个条件串**；
2. 条件一丢，默认按"成立"处理，于是
   `StatsFunctors "IF(not SavingThrow(Ability.Constitution, ManeuverSaveDC())):ApplyStatus(BLEEDING, 100, 2)"`
   变成**每次 OnDamage 事件都执行**，不再受 `IsWeaponAttack()` / `HasAdvantage()` / 无甲无盾的约束；
3. 该被动挂在装备上：`Armor.txt` 的 `4Rogue_AssassinArts_Hat` →
   `PassivesOnEquip "4Rogue_AssassinArt0_Passive;4Rogue_AssassinArt1_Passive;4Rogue_AssassinArt2_Passive;4Rogue_AssassinArt3_Passive"`；
4. 流血自身的跳伤**也是伤害事件**，会再次进入 OnDamage 判定 → 施加新流血 → 再跳 → 再判定，形成自我强化循环。

## 排除项（都已核实，不是原因）

| 怀疑对象 | 核实结果 |
|---|---|
| 原版 `BLEEDING` 状态本身 | **健康**。`StackId` / `TickType "StartTurn"` / `TickFunctors` 齐全，是标准的每回合跳一次 |
| `Properties "OncePerAttack"` 写法违法 | **合法**。原版有 33 条 passive 使用该属性 |
| 引用了不存在的原版条目 | **不存在此问题**。所有引用的母版/状态/法术全部存在 |
| 全工程还有其他括号错误 | **只有这 1 处**。数据行 100% 覆盖扫描 |
| `GAPING_WOUND` / `GapingWound_Passive` | 原版 `GapingWound_Passive` 是 `OnDamaged`（受伤时）触发，语义与本人的 `OnDamage` 不同，但未参与本 bug |

## 教训（写新版本时用得上）

1. **条件串一旦解析失败，失败方向是"条件全部成立"，不是"全部不成立"。** 所以笔误的后果是效果变强、触发变多，
   而不是静默失效。这让 bug 表现得像"设计值太高"，很难往语法错误上想。
2. **括号配平是纯文本层面唯一能提前发现这类错误的手段。** `BG3ModMaker\scripts\validate.ps1`
   现在会在打包前检查 16 个表达式字段的括号配平，覆盖全部条目。
3. **写 `Conditions` 时逐字复制一个已知正确的同类条目再改**，比手敲整个表达式安全。
4. DOT 的三要素（`StackId` / `TickType` / `TickFunctors`）缺一都会多重触发，但**本案例不是这个原因** ——
   施加流血的被动语法错误，与原版状态定义无关。排查时要区分"施加方"和"状态本身"。

## 其他已发现但未处理的问题

- **6 件护甲共用 `ValueUUID` `240eb257-ef20-4877-89bd-6956b4b7c41a`**，2 把手弩共用
  `d24c441f-7ebe-4229-8522-cf34c257ff20`。该值本应每件物品唯一。
- `4Rogue_PhaseMissile1_HandCrossbow_Combo` 是 `InterruptData`，却定义在 `Spell.txt` 第 68 行。
  游戏按 `Interrupt.txt` 读取 interrupt 条目。

## 产物说明

`dist\4Rogue.pak` 是**已修复打包、但未部署**的产物，33222 字节，
与作者原始 pak 字节数一致（原始 pak 用 LZ4 压缩；`divine.exe` 需显式加 `-c lz4`，否则产出未压缩 pak）。

作者原始 pak 保留在 `D:\Administrator\下载\4Rogue.pak`，未做任何改动。
