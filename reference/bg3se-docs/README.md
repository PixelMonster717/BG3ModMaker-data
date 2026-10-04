---
title: Script Extender 官方文档
type: reference
kind: official-docs
status: active
version: "v1.0"
tags:
  - bg3
  - 参考
  - 官方文档
  - script-extender
created: 2026-10-04
updated: 2026-10-04
---

# Script Extender 官方文档

> [!info] 这是什么
> [Norbyte/bg3se](https://github.com/Norbyte/bg3se) —— **BG3 Script Extender 的官方文档**。
> SE 是本工程最依赖的外部组件（职业判定、套装联动、跨系统逻辑都靠它），
> 但先前一直没有它的权威 API 参考，导致大量时间花在**猜 API 名字**上。
>
> 归档于 `reference\bg3se-docs\`，6 个文件。

## 文件清单

| 文件 | 大小 | 内容 |
|---|---|---|
| **`API.md`** | **81 KB / 1937 行** | **Lua API v30 完整参考**。最重要的一份 |
| `ReleaseNotes.md` | 14.6 KB | 各版本变更 |
| `VirtualTextures.md` | 6.0 KB | 虚拟纹理 |
| `Debugger.md` | 4.9 KB | 调试器用法 |
| `TROUBLESHOOTING.md` | 3.2 KB | 疑难排查 |
| `README-上游.md` | 2.3 KB | 项目说明与安装（上游原文） |

## API.md 的章节

| 章节 | 用途 |
|---|---|
| Getting Started / Bootstrap Scripts | 入口脚本怎么写（`BootstrapServer.lua` / `BootstrapClient.lua`） |
| Client / Server States | **服务端与客户端是两个独立的 Lua 状态，不能互访全局变量** |
| General SE Lua Rules | 对象作用域、参数传递、枚举、位域 |
| Calling Osiris from Lua | **从 Lua 调 Osiris**（`Osi.xxx`） |
| Calling Lua from Osiris | 反向调用 |
| Persistence | 变量持久化 |
| ECS | 实体-组件系统概念 |
| **Entity class - `Ext.Entity`** | **读组件、订阅事件**（本工程最常用） |
| Networking | 服务端/客户端通信 |
| Stats - `Ext.Stats` | 运行时读写 Stats |
| Timers / Events / Utils / Loca / Template / … | 各类工具 |

## 本工程踩过的坑，文档里其实都有

> [!warning] 六轮探针的教训
> 套装联动判定卡了很久，根因是**一直在猜 API 名字**。
> 事后翻 API.md，关键信息都在文档里。

### 1 · `Osi` 表的键无法用于探测存在性

> 原文：「*getting any key from the `Osi` table returns an object, even if no function
> with that name exists. Therefore, `Osi.Something ~= nil` cannot be used to determine
> whether a given Osiris symbol exists.*」

所以 `Osi.HasStatus` **取得到、调用时才报错**，不能用 `~= nil` 判断存在性。
**本工程实测：`Osi.HasStatus` 在 SE v32 上不存在**（`attempt to call a nil value`）。

### 2 · `GetComponent` 要用原生组件名

```lua
-- 拿到实体上全部组件的原生名（不用猜）
local names = entity:GetAllComponentNames()

-- 用原生名取组件
local comp = entity:GetComponent("eoc::status::ContainerComponent")
```

**简名（如 `"DisplayName"`）虽然不报错，但返回的组件不可枚举、读不出字段。**
本工程实测：`e:GetComponent("DisplayName")` 返回 `true`，但 `type=userdata`、0 个可读键。
而 `e.DisplayName`（`__index` 简写）能正常取到。

> [!tip] `__index` 是 `GetComponent` 的简写
> 原文：「*The `__index` metamethod of the Entity object is a shorthand for `GetComponent`*」
> → `entity.PassiveContainer` 等价于 `entity:GetComponent("PassiveContainer")`

### 3 · 状态与被动容器的真实组件名（实测）

```
eoc::status::ContainerComponent       状态容器
eoc::PassiveContainerComponent        被动容器
eoc::BoostsContainerComponent         加成容器
eoc::BackgroundPassivesComponent
eoc::OriginPassivesComponent
esv::passive::BaseComponent
esv::boost::BaseComponent
```

（该实体共 212 个组件，以上是与状态 / 被动 / 加成相关的全部。）

### 4 · 官方辅助函数（仅供开发期使用）

| 函数 | 用途 |
|---|---|
| `_D(x)` | 等价 `Ext.Dump()`，**层级打印表与 userdata** —— 写探针就该用它 |
| `_P(x)` | 等价 `Ext.Utils.Print()` |
| `_C()` | 等价 `Ext.Entity.Get(Osi.GetHostCharacter())` |

原文注明这些是「designed for developer use only」，mod 代码里不建议用，
但**调试时非常有用**——尤其 `_D()`，能直接看清 userdata 的层级结构。

## 更新方式

```powershell
$base = 'https://raw.githubusercontent.com/Norbyte/bg3se/main'
foreach ($f in @('Docs/API.md','Docs/Debugger.md','Docs/ReleaseNotes.md',
                 'Docs/VirtualTextures.md','README.md','TROUBLESHOOTING.md')) {
    $name = Split-Path $f -Leaf
    Invoke-WebRequest -Uri "$base/$f" -OutFile "<本目录>\$name"
}
```

用 PowerShell 的 `Invoke-WebRequest`（Python 的 urllib 因证书验证会失败）。

## 相关

- `reference\larian-docs\README.md` —— Larian 官方编辑器文档。
  注意它讲的是 **Osiris / Anubis，不含 SE**（SE 是第三方项目）。
- ModMaker 仓库的 `2-工作流\ScriptExtender实战配方.md` —— 本工程实测的用法与坑。
