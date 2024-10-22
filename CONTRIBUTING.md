# 提交备忘

提交备忘是在本项目中进行 Commit 提交的注意事项备忘文件。

**目录：**

- [提交备忘](#提交备忘)
  - [仓库结构](#仓库结构)
  - [翻译用语共识](#翻译用语共识)
  - [翻译贡献方针](#翻译贡献方针)
    - [翻译审查](#翻译审查)
    - [搁置规则](#搁置规则)
    - [公示规则](#公示规则)
    - [提示](#提示)
  - [代码贡献指南](#代码贡献指南)
  - [配置更改指南](#配置更改指南)
    - [Packer](#packer)
  - [联系我们](#联系我们)

## 仓库结构

```text
Minecraft-Mod-Language-Package
  ├─.github --------------- // GitHub 相关配置文件
  ├─config ---------------- // 配置文件
  │ └─packer -------------- // 打包器配置文件
  ├─projects -------------- // 翻译文件
  │ └─(Minecraft 版本) ---- // 不带 fabric 字样的是用于 Forge 和 NeoForge 模组的
  │   └─assets
  │     ├─(CurseForge 项目名称) ---- // 见下
  │     │ └─(命名空间) ------------- // 见下
  │     │   └─lang ----------------- // 语言文件文件夹
  │     │     ├─en_us.json --------- // English (United States) 语言文件
  │     │     └─zh_cn.json --------- // 中文 (简体) 语言文件
  │     ├─(Modrinth 项目名称)------- // 见下
  │     │ └─(命名空间) ------------- // 见下
  │     │   └─lang ----------------- // 语言文件文件夹
  │     │     ├─en_us.json --------- // English (United States) 语言文件
  │     │     └─zh_cn.json --------- // 中文 (简体) 语言文件
  │     ├─minecraft
  │     │ └─minecraft -------------- // Minecraft 原版使用的命名空间
  │     │   ├─font
  │     │   │ └─glyph_sizes.bin ---- // 全角标点修复文件
  │     │   └─textures
  │     │     └─font --------------- // 全角标点修复文件
  │     └─1UNKNOWN ----------------- // 存放不在 CurseForge 和 Modrinth 上发布的模组
  │         └─(命名空间)
  │           └─lang
  └─src --------------- // 各种自动化工具的源码
    ├─Formatter ------- // 格式化工具，曾用于统一翻译文件格式
    ├─Language.Core 
    ├─Packer ---------- // 打包器，用于自动生成资源包文件并发布 Release
    ├─Spider ---------- // 爬虫，曾用于爬取热门模组的语言文件供翻译
    └─Uploader -------- // 上传器，用于将资源包文件上传到文件分发服务器
```

**CurseForge 项目名称**：以匠魂为例，它的 CurseForge 页面地址是 `https://www.curseforge.com/minecraft/mc-mods/tinkers-construct`，则 `CurseForge 项目名称` 为 `tinkers-construct`。因为它是唯一的，被用来追溯模组来源。

**命名空间（Namespace）**：以匠魂为例，用压缩软件打开模组文件（JAR 格式），它的 en_us.json 的路径为 `assets/tconstruct/lang/en_us.json`，则 `{命名空间}` 为 `assets/` 和 `/lang` 之间的内容，即 `tconstruct`。一个模组可能有多个命名空间。命名空间介绍见 [Minecraft Wiki](https://zh.minecraft.wiki/w/%E5%91%BD%E5%90%8D%E7%A9%BA%E9%97%B4ID?variant=zh-cn#%E5%91%BD%E5%90%8D%E7%A9%BA%E9%97%B4)。

**Modrinth 项目名称**：以 Modrinth 独占模组 Clean F3 为例，它的 Modrinth 页面地址是 `https://modrinth.com/mod/clean-f3`，则在 `mod/` 后的内容 `clean-f3` 为 `{Modrinth 项目名称}` 的**主体**部分，而为了与 Curseforge 上发布的模组作以区分，所有仅在 Modrinth 上发布的模组，在其之前需要添加 `modrinth-` 作为区分。综上，它的 `{Modrinth 项目名称}` 为 `modrinth-clean-f3`。

仓库中“命名空间”文件夹下的目录结构与[资源包](https://zh.minecraft.wiki/w/%E8%B5%84%E6%BA%90%E5%8C%85)的相应结构相同，其他可用资源包加载的本地化文件亦可接收。

projects 文件夹下只标出模组所属的大版本号，其中的模组翻译文件应满足以下优先级：

1. 模组活跃更新的 Minecraft 版本优先。
2. 若所有小版本都活跃更新，则 Minecraft 版本高者优先。


* 例：Minecraft 版本 1.19.2 与 1.19.4 均属同一大版本号 1.19 下的子版本。  
若某一模组在两个版本上的开发均活跃，由于 1.19.4 的版本号更高，因此优先考虑该模组在 1.19.4 下的译名标准化情况与适配情况。  
这一优先级不会影响到模组在其他大版本下（如 1.18、1.12 等）的分支。

## 翻译用语共识

不适用

## 翻译贡献方针

不适用

### 翻译审查

不适用

### 搁置规则

不适用

### 公示规则

不适用

### 提示

- 如果文件路径不包含语言标记 `zh_cn`，一般需要**修改全局或局域的 Packer 配置**，否则它们会被打包器排除，不会进入用户使用的资源包。具体操作参见[文档](Packer-Doc.md#添加无语言标识的文件)。
  - 如果这些文件放置在 `font` 或 `textures` 中，无需修改配置；默认已经对这两处进行了特殊处理。
- 不同版本的同一模组可通过[自定义文件检索策略](./Packer-Doc.md#检索策略)同步翻译。

## 代码贡献指南

不适用

## 配置更改指南

以下内容只针对对 [config](./config) 文件夹下的贡献。这里里只列出了部分修改可能较大的文件。

<!--### config/spider/config.json

> Spider目前暂时停用，以下事项仅作参考。

- `"version"`：游戏版本，**请勿修改**
- `"spider_conf"`：爬虫相关设置
- `"base_mod_count"`：默认爬取模组的数量
- `"black_list"`：模组黑名单，元素为 `String` 类型，内容为 CurseForge 的 Project ID
- `"white_list"`：同上，为模组白名单

注意事项：

- 请不要随意删除黑名单模组，这些模组在这里是有原因的。
- 请不要在**未经同意**的情况下修改默认爬取数量。
-->

### Packer

路径：`./config/packer/[version].json`（如 1.12 的文件在 [1.12.2.json](./config/packer/1.12.2.json)）

该文件内放置了**所有**正在维护的版本的打包配置。
不要随意*删去*内容，除非你知道它为什么弃用。
加入内容相对而言宽松一些，但最好还是说明理由。

*下面没有提到的一般都不适合改动；如果需要，最好说明理由。*

主要的更改场景：

- 增加新翻译版本
  - 需要将所有项填写一遍，同时需要更新 `.github/workflows/packer.yml`、`.github/workflows/pr-packer.yml`、`.github\boring-cyborg.yml`，以及 [CFPABot](https://github.com/Cyl18/CFPABot) 等相关服务。没有规划最好不要乱动。
- 更改字符替换表
  - 修改`characterReplacement`，格式与已有文本一致。对于**基础多语种平面（BMP）**以外的字符，最好用 **UTF-16 代理对**书写。
  - 同时可能需要修改字体文件。
- 处理非文本文件
  - 参考 [Packer-Doc](Packer-Doc.md) 对其的描述。
- 停止对某模组的支持
  - 把该模组的 `CurseForge 项目名称`或`命名空间`中的加入相应的 `exclusionMods` 或 `exclusionDomains`（二者取其一）。

## 联系我们

不适用
