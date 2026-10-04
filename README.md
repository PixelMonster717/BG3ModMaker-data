# BG3ModMaker-data

> [!tip] 这是独立的 Obsidian Vault
> **用 Obsidian 打开本目录即可**（`.obsidian` 已配好，忽略了大目录以免拖慢索引）。
>
> **先读 `指南.md`** —— 按需求列出每个入口：要查什么、该去哪里、用哪条命令。
> 两个仓库的分工判据：**「怎么用工具」去 ModMaker；「游戏里有什么」来 data**。

**BG3 Mod 制作工具链与原版参考数据。**

## 姊妹仓库

工程按「可复用工具 / 可复用数据 / 各 Mod 产出」分三层，每层一个独立仓库：

| 仓库 | 内容 | 本地目录 |
|---|---|---|
| [BG3ModMaker](https://github.com/PixelMonster717/BG3ModMaker) | 工具与知识库（规范、脚本、模板、Vault） | `…\Documents\BG3ModMaker\` |
| **BG3ModMaker-data**（本仓库） | 工具链与原版参考数据 | `…\Documents\BG3ModMaker-data\` |
| [BG3-Mod-4RogueSet](https://github.com/PixelMonster717/BG3-Mod-4RogueSet) | 游荡者套装的产出（工程 + 文档 + 迭代记录） | `…\Documents\RogueSet\` |

> [!warning] 仓库名与本地目录名不一定相同
> 例如 RogueSet 的 GitHub 仓库名是 `BG3-Mod-4RogueSet`，本地目录是 `RogueSet`。
> 主库的脚本按**本地相对位置**引用本仓库（两者必须是同级目录），与仓库名无关。

## 为什么单独一个仓库

把「体积大但几乎不变」的内容与「体积小但每天迭代」的文档分开：

| | 主库 BG3ModMaker | 本仓库 |
|---|---|---|
| 内容 | 文档、Vault、脚本、模板 | 工具链、原版参考数据 |
| 体积 | 0.2 MB | 约 220 MB |
| 迭代频率 | 每天 | 几乎不变 |

合在一起会导致每次改一行文档都要背着 223 MB 历史，clone 与 push 都变慢。

## 内容

### `tools\` — 工具链（129 MB）

| 目录 | 用途 |
|---|---|
| `lslib-1.18.5\` | `ConverterApp.exe`（GUI）、`Tools\divine.exe`（**命令行打包器**） |
| `lslib-1.18.4\` | 旧版，回退用。产出与 1.18.5 **字节完全相同** |
| `modders-multitool\` | `bg3-modders-multitool_CHS.exe` / `_ENG.exe`：批量解包、索引、GameObject 浏览 |
| `modders-multitool-v0.10.0\` | 另一版本 |
| `data-query\` | `BaldursGate3Query-0.14.2-chenstack.exe`：按条目名查原版数据 |
| `mod-manager\` | `BG3ModManager.exe`：第三方 mod 管理器 |
| `mod-fixer\` | `Full Release Mod Fixer.pak`：旧版兼容修复 |
| `trainers\bg3-axe\` | 修改器，仅供测试 |

> [!warning] 打包必须显式指定压缩
> `divine.exe` 不加 `-c lz4` 会产出**未压缩** pak。实测同一工程：
> 默认 50318 字节 vs `-c lz4` 33222 字节。

### `reference\` — 原版参考数据（94 MB）

| 目录 | 内容 |
|---|---|
| `stats-vanilla\` | 8 个模块的 Stats 数据（167 文件 / 16593 条目 / 113184 行 data）。校验器用它做重名检测 |
| `root-templates\` | 25914 个原版 RootTemplate 导出（Gustav / GustavDev / Shared / SharedDev） |
| `sample-mods\` | 两个范例工程：`SHILI`（含 .pak，带作者手写注释）、`4Rogue`（含 .pak 与完整工程） |
| `tutorials\` | 两份第三方中文教程（`.docx` / `.pdf` / `.pak`）、**教程文本版**（含 37 张图的 Markdown）、被动技能模板 |
| `equipment-list\` | 作者整理的**原版装备数据库**（12 类约 680 条，Markdown）。分类：头冠与头盔 55 / 披风 18 / 护甲与服装 76 / 手套 77 / 靴子 39 / 盾牌 29 / 项链 62 / 戒指 66 / 近战武器 195 / 远程武器 25 / 异常状态 29 / 输出与附加伤害 54 |
| `exports\` | `UNI_HUM_ShadowBlade.lsf` / `.lsx` |

**关于 `sample-mods\`**：两个范例都带 `.pak`，可直接解包对照。
`SHILI` 的源文件里有作者手写的中文注释，本工程已对照 `stats-vanilla` 的实测数据
**逐条校正**，被更正处标了「【更正】」「【实测补充】」。
每个范例目录下有 `README.md` 说明它演示了什么、有哪些未完成处。

**关于 `equipment-list\`**：作者整理的《博德之门3装备合集》转成的 Markdown，
12 类约 680 条，含**中文装备名 / 品质 / 穿戴要求 / 效果 / 获取地点 / 获得方式**，
其中「头冠与头盔」(50/51)「披风」(16/16) 两类附有 **RootTemplate UUID**（其余待补）。
另有两张参考表：「异常状态」列出原版状态效果，
「输出与附加伤害」把效果说明与对应的 **Boost 函数写法**并列——
这是从效果反查写法最直接的一张表。索引见该目录的 `README.md`。

**关于 `tutorials\教程文本版\`**：原教程的关键内容大量存在于**图片**中，
纯文字版会丢失信息。故把 `.docx` 转成了 Markdown，**按原文顺序保留了 37 张图片**，
便于离线阅读与检索。

> [!note] 教程是第三方所写
> 写于较早版本，部分内容与当前实测不符。
> 遇到冲突以主库的 `2-工作流\Stats语法与结构.md` 与 `Stats字段字典.md` 为准。

> [!note] `stats-vanilla` 的来源与更新
> 原为 2024-11/-12 从游戏 pak 抽出，早于 Patch 8。
> **现已改用 `scripts\extract-vanilla-stats.ps1` 从当前版本 pak 重新抽取**
> （`Data\Shared.pak` 等，路径 `Public\<模块>\Stats\Generated\Data\*.txt`）。
>
> 更新方法：
> ```powershell
> powershell -File <ModMaker>\scripts\extract-vanilla-stats.ps1
> ```
> 脚本整包解包后只搬运 Stats 文件，不碰几十 GB 的贴图与模型。

## 游戏本体里的另两份数据（不在本仓库，但要知道）

| 位置 | 内容 | 与本文档的关系 |
|---|---|---|
| `<游戏>\Data\Editor\Mods\*\Stats\*.stats` | **编辑器的字段定义表**：每种类型有哪些字段、类型是什么。例如 `Weapon.stats` 定义了 Weapon 的 41 个字段 | 与 `stats-vanilla` **互补**——前者说「有哪些字段」，后者说「有哪些物品」。来自 Steam 上的官方 Toolkit Data（DLC） |
| `<游戏>\Data\*.pak` | **运行时数据**：真正的 `new entry` 物品数据 | `stats-vanilla` 就是从这些 pak 抽出来的。游戏更新后用 `extract-vanilla-stats.ps1` 重抽 |
| `<游戏>\Data\Public\Shared\GUI\Icons_Items*.lsx` | **图标定义**（7 个分片） | 做自定义图标时查 |

> [!warning] 别把 `.stats` 当成物品数据
> `Data\Editor\Mods\*\Stats\*.stats` 是 XML 格式的**字段定义**，不是运行时的
> `new entry` 语法。最初我误以为它能直接替换 `stats-vanilla`，实测后确认两者
> 性质不同：它定义「字段有哪些」，**不含具体物品**。
> 但它对查「这个类型支持哪些字段」极有价值——比从数据反推字段表可靠得多。

## 版本注意

`reference\tutorials\` 下的两份 PDF 是**第三方作者**的教程，非本工程原创。
仓库为 Private，仅供自用参考。

## 如何配合主库使用

两个仓库应为**同级目录**：

```text
D:\Administrator\Documents\
├─ BG3ModMaker\            主库
└─ BG3ModMaker-data\       本仓库
```

主库的脚本按此相对位置引用 `tools\` 与 `reference\`。
完整的恢复步骤、环境事实与踩坑速查见主库根目录的 **`恢复说明.md`**。
