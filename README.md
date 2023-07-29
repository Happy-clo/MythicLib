### 使用 MythicLib 作为依赖项
注册 PhoenixDev 仓库

```xml
<repository>
    <id>phoenix</id>
    <url>https://nexus.phoenixdevt.fr/repository/maven-public/</url>
</repository>
```

然后将 MythicLib-dist 添加为依赖项

```xml
<dependency>
    <groupId>io.lumine</groupId>
    <artifactId>MythicLib-dist</artifactId>
    <version>1.5.2-SNAPSHOT</version>
    <scope>provided</scope>
    <optional>true</optional>
</dependency>
```

### 编译 MythicLib
MythicLib 将 MMOItems 和 MMOCore 的所有版本相关代码进行集中，意味着它使用 NMS（net.minecraft.server）而不是常规的 Spigot API。由于 Minecraft 服务器构建现在使用了混淆的映射（自 1.17 版本开始），因此您需要首先为所有 1.17 以上版本设置 mojang-remapped 的 Spigot Jars。

以下是您可以使用的说明来生成所需的四个 mojang-remapped Jars（使用 BuildTools）。由于 Spigot 1.17 运行在 Java 16 上，而我的默认 Java 安装版本是 17，所以我不得不重新下载一个 Java 16 JDK，并让 BuildTools 在那个版本上运行，以便构建一个 remapped 的 Spigot 1.17。

```shell
"C:\Program Files\Java\jdk-16.0.1\bin\java" -jar BuildTools.jar --rev 1.17 --remapped
java -jar BuildTools.jar --rev 1.18 --remapped
java -jar BuildTools.jar --rev 1.18.2 --remapped
java -jar BuildTools.jar --rev 1.19 --remapped
java -jar BuildTools.jar --rev 1.19.3 --remapped
```

1.17+ 版本的版本包装器有单独的 Maven 模块。另一种选择是为一个特定版本构建 remapped 的 Spigot Jar，并删除所有其他模块。

自 MythicLib 1.3.4 版本开始，在编译 MMOItems 和 MMOCore 之前不再需要先编译 MythicLib，因为 PhoenixDevt 仓库现在包含了 MythicLib、MMOItems 和 MMOCore 的开发构件。