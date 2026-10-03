# BG3ModMaker-data

**BG3 Mod 制作工具链与原版参考数据。** 这是主库 [BG3](https://github.com/PixelMonster717/BG3)
的配套数据仓库。

## 为什么单独一个仓库

把「体积大但几乎不变」的内容与「体积小但每天迭代」的文档分开：

| | 主库 BG3 | 本仓库 |
|---|---|---|
| 内容 | 文档、Vault、脚本、模板 | 工具链、原版参考数据 |
| 体积 | 0.18 MB | 223 MB |
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
| `stats-vanilla\` | 5 个模块的 Stats 数据（119 文件 / 9.5 MB）。校验器用它做重名检测，索引 15387 条 |
| `root-templates\` | 25914 个原版 RootTemplate 导出（Gustav / GustavDev / Shared / SharedDev） |
| `sample-mods\` | `SHILI`（含 .pak）、`4Rouger` 两个范例工程 |
| `tutorials\` | 两份中文教程 PDF、被动技能模板 |
| `exports\` | `UNI_HUM_ShadowBlade.lsf` / `.lsx` |

> [!warning] `stats-vanilla` 可能已过时
> 时间戳为 2024-11/-12，早于当前 Patch 8 + HotFix 10。
> 查「条目是否存在」可靠，查具体数值需留意。详见主库「原版数据参考」。

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
