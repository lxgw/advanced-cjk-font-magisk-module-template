> [!CAUTION]
> **⚠️ 重要警告**
> - 刷机、刷入 Magisk 模块可能导致系统无法正常启动，请在操作前审慎考虑，并务必备份重要数据。因操作不当导致的任何系统故障（包括卡开机动画、功能异常等）与模块模板作者无关。
> - 本模板内容及相关文档**已过时**，本人已无力继续适配和维护，因此本模板可能存在[**兼容性问题**](https://github.com/lxgw/advanced-cjk-font-magisk-module-template/issues)。
>
> **📜 免责声明**
> - 本模块按「原样」（AS-IS）提供，作者不对因使用、修改或分发本模块所导致的任何直接或间接损失承担责任。
> - 用户须自行确保所使用的字体文件拥有合法的使用和分发授权，因字体版权引发的一切纠纷由用户自行承担。
> - 使用本模块即表示您已阅读并同意以上条款。
>
> **💡 建议**
> - 如果您在使用过程中遇到问题，可参考下方 **「兼容性调整」** 章节（部分信息可能已过时，仅供参考），或改用**其他仍在维护的字体模块模板**，亦可直接使用他人的**可用成品字体模块**并替换其中的字体文件（替换前需确认目标模块的字体配置文件中所引用的文件名及扩展名，将自己的字体文件重命名为与之完全一致即可）。
> - 欢迎 Fork 本仓库进行二次开发。

# CJK Font Magisk Module Template <sup>ADVANCED</sup> </br> CJK 字体 Magisk 模块模板 <sup>高级版</sup>

本项目为 **Magisk 字体模块模板**的 GitHub 发行项目。该模板用于制作 Magisk 字体模块，支持 9 个字重，可对西文、中文、日语、韩语字体进行任意搭配。在安装 Magisk 的手机上，使用该模板制作字体模块并刷入，更换字体或许会更简便。

有关套用模板的介绍和原理，请看：[为 Android 换上任意喜欢的字体，你可以试试这个 Magisk 模块（少数派）](https://sspai.com/post/58049)

[简易版](https://github.com/lxgw/simple-cjk-font-magisk-module-template)

## 使用方法

1. 在 [Release](https://github.com/lxgw/advanced-cjk-font-magisk-module-template/releases/latest) 界面下载最新版本的模块模板压缩包（`FontTemplate-Magisk204.zip`，基于 Magisk 20.4 模板，更高版本 Magisk 通常也兼容）。**注意：不要直接点击 "Download Zip" 下载整个仓库，请从 Release 附件中下载。**

2. 利用压缩软件（电脑上如 7-Zip，手机上如 MT 管理器）打开模块模板包，进入其中的 `/system/fonts` 文件夹，向里面添加 `.ttf` 或 `.otf` 格式的字体文件。字体文件的命名按照第 3 步的指示。

3. 要使加入的字体能够正常显示，**字体文件须遵循以下命名规则**：
   - 将喜爱的字体文件按字重（粗细）及语言（或优先级）依次重命名为 `fontxxwy.ttf` 或 `fontxxwy.otf`，复制到模块的 `/system/fonts` 目录下，刷入后重启即可。**重命名方式如下：**

     - `xx` 表示字体的语言代号。本模块模板支持斜体西文。

       | xx 代号 | 语言 | 调用条件 |
       | ------- | ---- | -------- |
       | en      | 西文（常规） | 所有非斜体西文场景 |
       | ei      | 西文（斜体） | 西文斜体场景 |
       | ch      | 中文 | 系统语言为简体/繁体中文时 |
       | kr      | 韩文 | 系统语言为韩语时 |
       | jp      | 日文 | 系统语言为日语时 |

     - `wy` 表示字体的字重等级，从 1 至 9 由细到粗。**系统正文调用的基准字重（即 Regular 字重）**，`y` 数值为 4；**系统标题文本、加粗文本调用的粗字重（即 Bold 字重）**，`y` 数值为 7；Light、Medium 字重 `y` 分别为 3 和 5，`y` 越小则字重越细，越大则字重越粗。

       | y 值 | 字重（Font-Weight） | 中文名称 |
       | ---- | ------------------- | -------- |
       | 1    | Thin (100)          | 极细     |
       | 2    | UltraLight (200)    | 纤细     |
       | 3    | Light (300)         | 细体     |
       | 4    | Regular (400)       | 常规     |
       | 5    | Medium (500)        | 中等     |
       | 6    | SemiBold (600)      | 次粗     |
       | 7    | Bold (700)          | 粗体     |
       | 8    | ExtraBold (800)     | 特粗     |
       | 9    | Heavy/Black (900)   | 超粗     |

     **例如：** `fontchw4.ttf` 表示中文部分的正文字重，`fonteiw7.otf` 表示西文部分的粗斜体。

   - **关于 `.ttf` 与 `.otf` 格式：**
     - 如果使用 `.ttf` 格式字体，直接按规则重命名即可（扩展名保持 `.ttf`）。
     - 如果使用 `.otf` 格式字体，**建议保持扩展名为 `.otf`**，同时需要修改模块内 `system/etc/fonts.xml` 文件中对应的文件名，将 `.ttf` 改为 `.otf`。
     - **不推荐** 强行将 `.otf` 重命名为 `.ttf`，可能在某些系统上导致字体加载失败。

4. 模块根目录的 `module.prop` 用于存放模块信息，如模块的名称、版本号、作者等。
   - `id`：模块的唯一标识符，**只能包含英文字母、数字、下划线（_）、点号（.）和短横线（-），不能包含空格**。**相同 id 的 Magisk 模块不能共存。**
   - `name`：模块名称，可任意填写。
   - `version`：模块版本，可任意填写。
   - `versionCode`：模块版本代号，必须为整数型数值。该值用于版本比较。
   - `author`：模块作者，可任意填写。
   - `description`：模块描述，可任意填写。
   - 所有文本文件的行尾应以 **Unix 格式（LF）** 书写。

5. 将制作好的模块压缩包通过 Magisk 刷入，重启设备即可生效。

## 字重测试
 
[点击此处进入字重测试](https://font.yukonga.top/)，[@YuKongA](https://github.com/YuKongA/)（酷安 [@YuKong_A](http://www.coolapk.com/u/27385711)）制作提供。

## 注意事项

### 模块文件说明

1. **EmptyFont（空壳字体）**：位于 `/system/fonts` 目录内，为 Android 默认西文字体 Roboto 的空壳字体，主要用于提供字体度量和字重信息，**请勿删除**。

2. **Google Sans 覆盖**：`/system/product` 文件夹用于覆盖类原生 Android 系统内置的 Google Sans 字体，以实现所替换字体在类原生 ROM 上的全局覆盖。
   - **如需保留原生的 Google Sans 字体**，请将模块内的 `/system/product` 文件夹删除。
   - 当前版本采用空字体替换 Google Sans 的方式实现屏蔽，若遇到兼容性问题可尝试此调整。

3. **字体配置文件**：`/system/etc/fonts.xml` 为字体配置文件，已预先调整以调用空字体及自定义字体。
   - 经测试，该配置在 **Android 11 和 Android 12** 的部分 ROM 上可正常工作（测试机型：Redmi Note 5 / Pixel Experience 12.0；Redmi K20 Pro / crDroid 7.9）。
   - **但不保证所有 ROM 均能正常使用**，不同 ROM 调用字体的配置文件可能有所不同，请参阅下方 **「兼容性调整」** 章节。

### 制作与使用建议

4. **字体搭配注意**：添加字体时请留意各种语言字体的字重对应。
   - 若 CJK 字体已同时包含中文和韩文字形，则无需再单独添加韩文字体。
   - 若中文字体自带的西文字形已满足需求，则无需再单独添加英文字体。

5. **最低 Magisk 版本要求**：本模板最低支持 **Magisk 20.4**。

### ROOT 隐藏兼容性（针对 Android 12+）

6. 如需在 Android 12 及以上系统隐藏 ROOT 的同时使用字体模块，建议：
   - 使用 **Magisk 24.0+**，开启 Zygisk；
   - 配合 **Shamiko 0.2.0+**；
   - 在 Magisk 设置中取消勾选「遵守排除列表」，防止排除列表内的应用闪退。
   - **注意：** 请勿在已使用旧版 Magisk Hide 的 Android 12 系统上刷入本模板制作的字体模块，以免引发兼容性问题。
## 兼容性调整 <sub>仅供参考</sub>

>[!WARNING]
> 以下兼容性调整方法基于过往用户反馈整理，部分信息可能已过时，仅供参考，不保证在所有系统版本上有效。

为了使该模块模板更加适合您的手机，需要对模块模板内的配置文件进行调整：

- **OPPO/一加 ColorOS 13 及以下版本：** 将 `/system/etc/fonts.xml` 复制到 `/system/system_ext/etc/` *（若无该文件夹请先创建）* 目录并重命名为 `fonts_base.xml`。
- **OPPO/一加 ColorOS 14 版本：** 将 `/system/etc/fonts.xml` 复制两份到 `/system/system_ext/etc/` *（若无该文件夹请先创建）* 目录并重命名为 `fonts_base.xml` 及 `fonts_ule.xml`。
- **一加 HydrogenOS 11 及以上版本：** 将 `/system/etc/fonts.xml` 复制到相同文件夹，并重命名为 `fonts_base.xml。`
- **魅族 Flyme：** 将 `/system/etc/fonts.xml` 复制 3 份到相同文件夹，并重命名为以下 3 个文件： `fonts_flyme.xml`、`fonts_inter.xml` 和 `fonts_slate.xml`。
- **小米 MIUI 12.5：** 需刷入 [空字体模块 v4.4](https://yukonga.lanzoub.com/iSxAP07pu05i) / [v4.1](https://wwi.lanzoui.com/iEDyZt6a83g)。
- LG 手机的兼容性调整请参阅： https://github.com/lxgw/advanced-cjk-font-magisk-module-template/issues/2
- **Android 15 原生/类原生：** 根据 Android 官方变更，`fonts.xml` 已被弃用，相关配置需改写到 `font_fallback.xml` 中。请参考最新 Android 开发者文档调整模块配置。
- 如有其他设备的兼容性调整，请在 issue 提出。
- **已有用户测试，本模块模板不适用于 vivo/IQOO 手机。**

## 字体模块模板作者

基于 [Petit-Abba](https://github.com/Petit-Abba)（酷安 [@Kotch / 原名「阿巴酱」](https://www.coolapk.com/u/1132618)） 的 [Magisk-Modules-Template-ge20.4](https://github.com/Petit-Abba/Magisk-Modules-Template-ge20.4) 制作。采用 MIT License 开源发布。

- **Telegram：** @lxgwtg
- **微信公众号：** 霞鹜 *（ID: lxgwshare）*
- **酷安：** [@落霞孤鹜lxgw](https://www.coolapk.com/u/633884)
- **微博：** [@孤鹜先森](https://weibo.com/6624339726)
