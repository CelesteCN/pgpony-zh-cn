# PGPony 简体中文汉化包（开源贡献包）

## 这是什么

基于官方 PGPony Android v4.4.1 制作的简体中文汉化成果，包含：

1. **完整中文翻译**：官方翻译仓库全部 1390 条字符串的简体中文翻译（0 条遗漏）
2. **汉化版 APK**：`PGPony_4.4.1_汉化版.apk`（已打包签名，可直接安装）
3. **差分取证报告**：原版 APK 与汉化版的全量对比，证明仅改动语言相关部分

## 目录

- `android/values-zh-rCN/strings.xml` —— 官方翻译仓库格式的 PR 文件（1390 条全翻译）
- `PGPony_4.4.1_汉化版.apk` —— 汉化成品（自签名，安装需卸载官方版或同签名覆盖）
- `差分报告.md` —— 全量 diff 取证结果

## 改动清单（相对官方 v4.4.1）

| 类型 | 文件 | 改动 |
|---|---|---|
| 代码 | smali_classes2/i4/b.smali | 语言枚举 +1 个值（ZH），8 行 smali |
| 代码 | 其余全部 dex / so | **零改动**（smali 逐文件 diff + so 库 SHA256 验证） |
| 资源 | values-zh-rCN/strings.xml | 新增 1421 条中文翻译 |
| 资源 | xml/locales_config.xml | 语言白名单 + zh-CN |
| 资源 | drawable/ic_launcher_background.xml | 图标背景渐变改纯色（外观） |

## 许可证

PGPony = Apache-2.0（norsehorse-dev/PGPonyAndroid）。本汉化包同许可证，保留原作者版权。

## 如何提交给官方（推荐路线）

### 第一步：翻译 PR（PGPony-Translations 仓库）

在能访问 GitHub 的电脑上：

1. Fork `norsehorse-dev/PGPony-Translations`
2. 上传 `android/values-zh-rCN/strings.xml`（本目录已备好）
3. 提 Pull Request，标题建议：

```
Add Simplified Chinese (zh-rCN) translation for Android
```

正文建议：

```
Complete translation of all 1390 strings for Android, based on v4.4.1.
Also verified against the official app: every user-facing string is covered.
```

### 第二步：语言开关 Issue（PGPonyAndroid 主仓库）

翻译合入后，官方版还需要在代码里打开中文开关，给 `norsehorse-dev/PGPonyAndroid` 提 Issue：

```
Title: Add zh-CN to app language picker

The app's language picker hardcodes 7 languages in the AppLanguage enum
(compiled as class i4/b in v4.4.1) and in res/xml/locales_config.xml.
The zh-rCN translation exists (see PGPony-Translations), but users cannot
select it because:

1. AppLanguage enum has no ZH value (tag "zh-CN", display name "简体中文")
2. locales_config.xml lacks <locale android:name="zh-CN" />

Fix: add the ZH enum value + whitelist entry, and Simplified Chinese
becomes selectable in Settings → Language.
```

## 自己发 APK 到 GitHub（次选路线）

Apache-2.0 允许再分发，但建议做到：

1. **必放**：README（改动清单 + 差分报告 + 构建方法）、APK、SHA256 校验值
2. **必写**：基于官方 v4.4.1、Apache-2.0、非官方构建、签名非官方
3. **绝不**：上传签名 keystore（私钥泄露可被伪造签名）
4. **加分项**：附 smali 补丁文件，让洁癖用户自己构建验证

## 验证方法（任何人可复验）

```bash
# 解包两个 APK 后对比代码
diff -rq 官方解包/smali_classes3 汉化解包/smali_classes3   # 应为空（密码学代码零改动）
diff -rq 官方解包/smali 汉化解包/smali                     # 应为空
diff -rq 官方解包/smali_classes2 汉化解包/smali_classes2   # 仅 i4/b.smali 一处
```

## 备注

- 汉化版为自签名，官方出新版后无法直接覆盖升级，需备份密钥 → 卸载 → 装新版
- 一旦官方合入翻译并发布，就无需再使用本汉化包
