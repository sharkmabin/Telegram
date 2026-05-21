## Telegram Android 客户端

[English](README.md) | [简体中文](README.zh-CN.md)

[Telegram](https://telegram.org) 是一款注重速度和安全性的即时通讯应用，快速、简单且免费。

本仓库包含 [Telegram Android App](https://play.google.com/store/apps/details?id=org.telegram.messenger) 的源码。当前项目是 Android/Gradle 工程，主要模块包括：

- `TMessagesProj`：核心 Android 工程与 Telegram 客户端源码
- `TMessagesProj_App`：主应用构建入口
- `TMessagesProj_AppHuawei`：Huawei 相关构建入口
- `TMessagesProj_AppHockeyApp`：HockeyApp 相关构建入口
- `TMessagesProj_AppStandalone`：独立构建入口
- `Tools`：辅助工具

当前仓库配置中的版本信息：

- `APP_VERSION_NAME=11.9.0`
- `APP_VERSION_CODE=5837`
- `APP_PACKAGE=org.telegram.messenger`
- Android Gradle Plugin: `8.4.2`

## 创建你自己的 Telegram 应用

Telegram 欢迎开发者使用 API 和源码在其平台上创建应用。请注意，所有开发者都需要遵守以下要求：

1. 为你的应用申请自己的 [api_id](https://core.telegram.org/api/obtaining_api_id)。
2. 不要直接使用 Telegram 名称作为你的应用名称；或者必须让用户清楚知道这是非官方应用。
3. 不要使用 Telegram 标准 logo，也就是蓝色圆形中的白色纸飞机，作为你的应用 logo。
4. 阅读并遵守 [MTProto 安全指南](https://core.telegram.org/mtproto/security_guidelines)，认真保护用户数据和隐私。
5. 按照许可证要求发布你自己的代码。

这些要求很重要。尤其在发布自己的 APK 前，请替换仓库中用于可复现构建的占位签名、Firebase 配置和构建变量。

## API 与协议文档

- Telegram API 文档：https://core.telegram.org/api
- MTProto 协议文档：https://core.telegram.org/mtproto

## 编译前准备

为了支持 [reproducible builds](https://core.telegram.org/reproducible-builds)，仓库中包含占位的 `release.keystore`、`google-services.json` 和已填充的 `BuildVars.java` 变量。发布你自己的 APK 前，务必替换为你自己的文件和配置。

你需要准备：

- Android Studio
- Android SDK
- Android NDK
- JDK 与 Gradle 兼容环境
- 你自己的 Telegram `api_id` 和相关 API 配置
- 你自己的 release keystore
- 你自己的 Firebase `google-services.json`

原英文 README 提到的历史构建环境是 Android Studio 3.4、Android NDK r20、Android SDK 8.1。当前仓库顶层 Gradle 配置使用 Android Gradle Plugin `8.4.2`，实际构建时请以当前 Gradle/Android Studio 对 AGP 8.4.2 的兼容要求为准。

## 编译步骤

1. 克隆源码：

   ```bash
   git clone https://github.com/sharkmabin/Telegram.git
   cd Telegram
   ```

2. 将你的 `release.keystore` 复制到：

   ```text
   TMessagesProj/config/release.keystore
   ```

3. 在 `gradle.properties` 中填写你的签名信息：

   ```properties
   RELEASE_KEY_PASSWORD=your_password
   RELEASE_KEY_ALIAS=your_alias
   RELEASE_STORE_PASSWORD=your_store_password
   ```

4. 打开 Firebase Console：

   https://console.firebase.google.com/

   创建两个 Android 应用，application ID 分别为：

   ```text
   org.telegram.messenger
   org.telegram.messenger.beta
   ```

   开启 Firebase Messaging，下载 `google-services.json`，并复制到：

   ```text
   TMessagesProj/google-services.json
   ```

5. 使用 Android Studio 打开项目。

   注意：应选择打开项目，而不是导入项目。

6. 填写构建变量：

   ```text
   TMessagesProj/src/main/java/org/telegram/messenger/BuildVars.java
   ```

   文件中每个变量附近通常会提示应从哪里获取对应数据。

7. 编译项目。

   可以在 Android Studio 中选择对应 variant 构建，也可以使用 Gradle wrapper。例如：

   ```bash
   ./gradlew assembleDebug
   ```

   如果你要生成发布包，请先确认签名、Firebase、API ID、包名、品牌名称、logo 和许可证合规要求都已处理完毕。

## 重要文件

| 文件或目录 | 说明 |
|---|---|
| `build.gradle` | 顶层 Gradle 构建配置 |
| `settings.gradle` | Gradle 模块声明 |
| `gradle.properties` | 应用版本、包名、签名变量和 Gradle 参数 |
| `TMessagesProj/build.gradle` | 核心 Android 模块构建配置 |
| `TMessagesProj/src/main/java/org/telegram/messenger/BuildVars.java` | Telegram API、推送和构建相关变量 |
| `TMessagesProj/config/release.keystore` | release 签名文件位置，发布前必须替换 |
| `TMessagesProj/google-services.json` | Firebase 配置文件位置，发布前必须替换 |

## 本地化

Telegram Android 的翻译已迁移到官方翻译平台：

https://translations.telegram.org/en/android/

如需参与本地化，请使用该平台。

## 合规提醒

如果你基于此仓库发布自己的应用，请至少确认：

- 已申请并使用自己的 `api_id`
- 已替换签名文件和 Firebase 配置
- 已替换应用名称、图标和品牌标识，避免让用户误认为是官方 Telegram
- 已审查安全与隐私处理
- 已按许可证要求公开你的修改源码

## 许可证

详见 [LICENSE](LICENSE)。
