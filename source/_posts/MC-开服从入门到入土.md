---
title: MC 开服从入门到入土
categories: 教程
tags:
  - 我的世界
  - 服务端
abbrlink: bda6a221
date: 2021-06-06 02:41:07
---
正如标题所言，这篇文章是一篇从入门到入土的开服教程，介绍了在 Windows 的开服方法，适用于想开服却无从下手的人，虽然阅读此教程并不需要任何基础，不过我依旧推荐先阅读一些相关信息后，再开始本篇教程。

以下是一些知识链接，可以对学习服务端搭建有所帮助：

*   理解 IP 和端口：[https://www.cnblogs.com/nzbbody/archive/2012/03/07/2383749.html](https://www.cnblogs.com/nzbbody/archive/2012/03/07/2383749.html)
*   什么是内网，什么是外网：[https://zhuanlan.zhihu.com/p/147282153](https://zhuanlan.zhihu.com/p/147282153)
*   服务端和客户端的区别：[https://www.zhihu.com/question/274332080](https://www.zhihu.com/question/274332080)
*   如何使用 Windows：[https://www.microsoft.com/zh-cn/windows/features](https://www.microsoft.com/zh-cn/windows/features)
*   什么是文件，目录，路径：[https://zhidao.baidu.com/question/44106194.html](https://zhidao.baidu.com/question/44106194.html)

## 快速开始

我现在假设你已经阅读了一些相关的基础文章，首先我们需要了解一些 MC 服务端基本的概念，在正常游玩单人游戏时，其实客户端就已经启动了一个隐藏的服务端，而通过这个服务端我们就能够实现最基本的局域网连接。

并且，通过端口转发或端口映射，外网玩家便可以通过你的公网 IP 加入你的局域网游戏。

### 创建局域网游戏

首先进入你的一个单人游戏世界，打开菜单并选择创建一个局域网世界，便可以成功的开启局域网服务端，而同样连接在你的局域网的用户，就可以从你的局域网 IP 地址加入你的游戏。

不过，该方法并不能作为长久的方案，因为一旦作为主机的你退出了游戏，那么你所开启的局域网服务端也会随之而关闭，所以我们需要创建一个专门的服务端供长久运行。

## Windows 10 设置服务端

在 Windows 10 下设置一个服务端时最基础且最简单的方式，因为你不需要学习使用任何的命令行命令，仅需要知道安装什么，以及哪里安装即可使用图形界面（GUI）完成配置。

我们需要一份 Java 的运行环境，你可以下载 JRE 或 JDK，JRE 是 Java 的运行环境，而 JDK 是 Java 的开发工具，其默认便自带了 JRE 因此有了 JDK 就等于有了 JRE 和 Java 的开发工具，并且 JDK 的版本往往会比 JRE 的版本要高，同时会有更好的性能，比如在 JDK 16 中优化了垃圾回收机制。

### 安装 JRE 环境

首先，访问 JRE 的下载页面，在浏览器中输入此地址：[https://www.java.com/download](https://www.java.com/download)

接着按照网站的提示完成下载，并找到下载的安装文件打开，继续按照提示完成安装。

安装完成后，JRE 环境便可以直接使用，按住 Win + R 输入 `cmd` 打开命令并输入 `java -version` 即可获得当前使用的 Java 版本以及其他的一些信息，如果没有显示则说明安装出现了问题，需要重启安装。

### 安装 JDK 环境

安装 JDK 环境可能会稍微困难一些，因为 Java并没有提供它的安装文件，而是一个压缩包，在下载完成后，需要用户自行完成后续设置才可以使用。

#### 下载 OpenJDK

访问 [https://openjdk.java.net/](https://openjdk.java.net/) 选择合适的 OpenJDK 版本下载并解压。

在解压后，你会发现目录中多了一个新的文件夹，该文件夹则是 JDK 以及 JRE 的储存目录，不过这个时候还没有结束，因为 Java 并没有自动地为我们设置环境变量，所以服务端并不能自动识别到 Java。

#### 设置环境变量

按以下步骤打开 Windows 的环境变量设置，控制面板 > 系统高级设置 > 找到虚拟环境点击，并在变量名下找到 PATH 并点击编辑，你可能会发现有用户变量和系统变量，不过这不要紧，选择其中之一即可。

在选择编辑后，点击添加，并将你的 JDK 解压目录下的 `bin` 文件夹的路径复制进去，之后回车保存并退出即可。

在设置完环境变量后，打开 `cmd` 并输入 `java -version` 便可以查看安装的 Java 版本。

### 设置原版服务端

原版服务端是最简单搭建的一种服务端，将来也可以基于原版服务端进行扩展设置。

访问 [https://mcversions.net](https://mcversions.net/) 找到你需要的版本点击下载后选择 Server Jar 下载即可。

在下载完成后，只需要将其移动到你希望服务端运行的路径，并运行即可，程序会自动地帮你配置好需要的文件。

在第一次运行时，程序可能会要求你同意 Eula 协议，使用任意文本编辑器在服务端运行路径下找到 eula.txt 打开，修改 `eula=false` 为 `eula=true`，之后再次运行服务端（你下载的 Server.jar 文件）即可运行。

### 修改 `server.properties` 文件

在成功运行完服务端后，我们需要在做一些最后的调整，这是一些常用的 `server.properties` 设置。

*   port：指定了服务端与客户端通讯的端口，默认为 25565
*   spawn-protection：出生点保护，默认为 16，推荐设置为 0
*   gamemode: 玩家加入服务器的游戏模式，默认为 survival
*   difficulty：游戏难度，默认为 easy
*   pvp: 是否开启玩家 pvp 伤害，默认为 true
*   enable-command-block: 是否允许在服务器内使用命令方块，默认为 false
*   max-players: 服务器允许的最大玩家在线数量，默认为 20
*   view-distance：允许的客户端最大视野范围，默认为 10，低配服推荐设置为 8
*   online-mode：是否开启正版验证，默认为 true

还有更多的设置可以参考 Minecraft 维基的地址：[https://minecraft.fandom.com/zh/wiki/Server.properties](https://minecraft.fandom.com/zh/wiki/Server.properties)

## 自动化安装服务端

对于那些希望能够自动安装服务端的人，可以查看该 GitHub 项目获取帮助：[我的世界服务器工具](https://actiniumcraft.github.io/mc-server-utils/#/server-installer)