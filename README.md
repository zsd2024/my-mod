# Mindustry Java Mod 模板
一个适用于 Android 和 PC 的 Java Mindustry mod 模板。该模板的 Kotlin 版本可以在[这里](https://github.com/Anuken/MindustryKotlinModTemplate)查看。
 
## 桌面测试构建
 
1. 安装 JDK **17**。
2. 运行 `gradlew jar` [1]。
3. 你的 mod jar 文件将会在 `build/libs` 目录中。**仅使用此版本进行桌面测试。它不适用于 Android。**
要构建适用于 Android 的版本，你需要 Android SDK。你可以让 Github Actions 处理这个，或者自己设置。请参见以下步骤。
 
## 通过 Github Actions 构建
 
这个仓库已经设置好了 Github Actions CI，可以在每次提交时自动为你构建 mod。这需要一个 Github 仓库，原因很明显。
要获取一个适用于所有平台的 jar 文件，请执行以下操作：
1. 使用你的 mod 名称创建一个 Github 仓库，并将此仓库的内容上传到其中。进行任何必要的修改，然后提交并推送。
2. 在你的仓库页面中检查“Actions”标签。选择列表中最新的提交。如果它成功完成，应该在“Artifacts”部分有一个下载链接。
3. 点击下载链接（应该是你的仓库名称）。这将下载一个 **压缩的 jar 文件** - **不是** jar 文件本身 [2]！解压此文件并在 Mindustry 中导入包含的 jar 文件。此版本应同时适用于 Android 和桌面。
 
## 本地构建
 
本地构建需要更多时间来设置，但如果你之前做过 Android 开发，应该不会有问题。
1. 下载 Android SDK，解压并将其位置设置为 `ANDROID_HOME` 环境变量。
2. 确保你已经安装了 API 级别 30 以及任何最近的构建工具版本（例如 30.0.1）
3. 将一个 build-tools 文件夹添加到你的 PATH 中。例如，如果你安装了 `30.0.1`，那将是 `$ANDROID_HOME/build-tools/30.0.1`。
4. 运行 `gradlew deploy`。如果你一切都正确，这将在 `build/libs` 目录中创建一个可以在 Android 和桌面运行的 jar 文件。
 
## 添加依赖项
 
请注意，所有对 Mindustry、Arc 或其子模块的依赖 **必须在 Gradle 中声明为 compileOnly**。永远不要对核心 Mindustry 或 Arc 依赖使用 `implementation`。
 
- `implementation` **将整个依赖项放入 jar 文件中**，这在大多数 mod 依赖项中是非常不希望的。你不希望将整个 Mindustry API 包含在你的 mod 中。
- `compileOnly` 意味着依赖项仅在编译时存在，而不包含在 jar 文件中。
 
只有在希望将另一个 Java 库 *与你的 mod 一起打包*，并且该库在 Mindustry 中尚未存在时，才使用 `implementation`。
 
---
 
*[1]* *在 Linux/Mac 上是 `./gradlew`，但如果你使用的是 Linux，我假设你知道如何正确运行可执行文件。*  
*[2]: 是的，我知道这很愚蠢。这是 Github UI 的限制 - 虽然 jar 文件本身是未压缩上传的，但目前没有方法将其作为单个文件下载。*