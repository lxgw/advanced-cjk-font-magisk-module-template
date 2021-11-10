# CJK Font Magisk Module Template <sup>ADVANCED</sup> </br> CJK 字体 Magisk 模块模板 <sup>高级版</sup>

> **重要提醒：**
>
> 刷机、刷入 Magisk 模块可能会导致系统无法正常启动，请在操作前审慎考虑，并建议备份重要数据。因操作不当导致的系统故障（包括卡开机动画、功能异常等）或效果异常与模块模板作者无关。

本项目为 **Magisk 字体模块模板**的 GitHub 发行项目。该模板用于制作 Magisk 字体模块，支持 9 个字重，可对西文、中文、日语、韩语字体各自进行自定义。在安装 Magisk 的手机上，使用该模板制作字体模块并刷入，更换字体或许会更简便。

有关套用模板的介绍和原理，请看：[为 Android 换上任意喜欢的字体，你可以试试这个 Magisk 模块（少数派）](https://sspai.com/post/58049)

## 使用方法

1. 在 [Release](https://github.com/lxgw/simple-cjk-font-magisk-module-template/releases/latest) 界面下载 zip 格式的模块模板 **FontTemplate-Magisk204.zip** *（不要直接选择 Download Zip）* 。
2. 利用压缩软件 *（电脑上如 7-zip，手机上如 MT 管理器）* 打开模块模板包内的 `/system/fonts` 文件夹，向里面添加 ttf 或 otf 格式的字体文件。字体文件的命名按照第 3 步的指示。
3. 要使加入的字体能够正常显示，**字体文件须遵循以下命名规则**：
   - 将喜爱的 TTF 格式字体按字重（粗细）及语言（或优先级）依次重命名为`fontxxwy.ttf`，复制到模块的「system/fonts」目录下刷入重启。**重命名方式如下：**
   
     - `xx`表示 TTF 格式字体的语言代号。本模块模板支持斜体西文。
   
       | 代号 | 语言         | 优先级                           |
       | ---- | ------------ | -------------------------------- |
       | en   | 西文（常规） | 最高优先级                       |
       | ei   | 西文（斜体） | 最高优先级（斜体时调用）         |
       | ch   | 中文         | 简体、繁体中文语言状态下优先调用 |
       | kr   | 韩文         | 韩语状态下优先调用               |
       | jp   | 日文         | 日语状态下优先调用               |
   
     - `wy`表示 TTF 格式字体的字重等级，从 1 至 9 由细到粗。**系统正文调用的基准字重（即 Regular 字重）**，`y` 数值为 4；**系统标题文本、加粗文本调用的粗字重（即 Bold 字重）**，`y` 数值为 7；Light、Medium 字重 `y` 分别为 3 和 5，`y` 越小则字重越细，越大则字重越粗。
   
     **例如：** `fontchw4.ttf`表示中文部分的正文字重，`fonteiw7.ttf`表示西文部分的粗斜体。
4. 模块根目录的 `module.prop` 用于存放模块信息，如模块的名称、版本号、作者等。
   - `id`：模块的代号，仅可包括**字母、数字及半角符号，不包含空格**。**相同 id 的 Magisk 模块不能共存。**
   - `name`：模块名称，可任意填写。
   - `version`：模块版本，可任意填写。
   - `versionCode`：模块版本代号，必须为整数型数值。该值用于版本比较。
   - `author`：模块作者，可任意填写。
   - `description`：模块描述，可任意填写。
   - 所有文本文件的行尾应以 **Unix 格式** 书写。
5. 使用 Magisk 刷入做好的模块，重启。

## 字重测试

[点击此处进入字重测试](https://font.yukonga.top/) （酷安 [@YuKongA / 原名「余空_YuK」](https://www.coolapk.com/u/680367) 制作提供）

## 注意事项

1. `/system/fonts` 目录内的 **EmptyFont** 为空字体文件，为 Android 默认西文字体 Roboto 的掏空字体，主要提供度量和字重信息，**请勿轻易删除。**
2. `/system/product` 文件夹内的内容用以覆盖类原生 Android 系统内置的 Google Sans 字体，实现所替换字体在类原生 ROM 上的全局覆盖。若想保留原生 ROM 内置的 Google Sans 字体，请将模块内的 `/system/product` 文件夹删除。
3. `/system/etc/fonts.xml` 为字体配置文件，已经过调整以调用空字体及自定义字体，经本人所持有的两部 Android 手机测试 *(Redmi Note 5, Pixel Expericence 12.0, Android 12; Redmi K20 Pro, crDroid 7.9, Android 11)* 均可正常使用，**理论上**可兼容 Android 12 和 Android 11，**但不保证所有 ROM 均能正常使用**。不同 ROM 调用字体的配置文件可能不同，请参阅下面的 **「兼容性调整」** 。
4. 添加字体时注意各种语言字体的字重对应。若有些 CJK 字体里既包含中文也包含韩文，则不必加韩文字体。若想使用中文字体自带的西文，则不必加英文字体。
5. **本模块模板最低支持 Magisk 20.4。**
6. 请不要在用过 Magisk Hide 或者 Zygisk 之后刷入任何字体模块，会导致被选中的应用闪退。

## 兼容性调整 <sub>仅供参考</sub>

为了使该模块模板更加适合您的手机，需要对模块模板内的配置文件进行调整：

- **OPPO/一加 ColorOS：** 将 `/system/etc/fonts.xml` 复制到 `/system/system_ext/etc/` 目录并重命名为 `fonts_base.xml`。
- **一加 HydrogenOS 11 及以上版本：** 将 `/system/etc/fonts.xml` 复制到相同文件夹，并重命名为 `fonts_base.xml。`
- **魅族 Flyme：** 将 `/system/etc/fonts.xml` 复制 3 份到相同文件夹，并重命名为以下 3 个文件： `fonts_flyme.xml`、`fonts_inter.xml` 和 `fonts_slate.xml`。
- **小米 MIUI 12.5：** 需刷入 [空字体模块](https://www.coolapk.com/feed/29518682?shareKey=NGU4ODM5Yjk3YjZmNjE4OTNiOTQ~&shareUid=633884&shareFrom=com.coolapk.market_11.4.3)。
- 如有其他设备的兼容性调整，请在 issue 提出。

## 字体模块模板作者

基于 [Petit-Abba](https://github.com/Petit-Abba)（酷安 [@Kotch / 原名「阿巴酱」](https://www.coolapk.com/u/1132618)） 的 [Magisk-Modules-Template-ge20.4](https://github.com/Petit-Abba/Magisk-Modules-Template-ge20.4) 制作。

- **Telegram：** @lxgwtg
- **微信公众号：** 霞鹜 *（ID: lxgwshare）*
- **酷安：** [@落霞孤鹜lxgw](https://www.coolapk.com/u/633884)
- **微博：** [@孤鹜先森](https://weibo.com/6624339726)
- **Email：** calxgw2018@gmail.com srtong2006@126.com lxgw1999@qq.com

