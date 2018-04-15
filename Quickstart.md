# Gunbot 快速入门指南

> **目录**
>
> 1. [下载 Gunbot](#1-download-gunbot)
> 2. [安装](#2-unpack--install)
> 3. [运行](#3-run-gunthy-gui)
> 4. [可选: 手动编辑 config.js](#optional-manually-setup-the-json-configuration-file)
> 5. [学习 Gunbot 中的交易策略](#learn-about-gunbot-strategies)




## 1. 下载 Gunbot

从 Github 直接下载各类平台的 Gunbot XT: https://github.com/GuntharDeNiro/BTCT/releases



## 2. 解压与安装 

将下载好的文件解压到新的文件夹中，以下是各个平台的安装指南：

- [Windows](Windows-installation.md)
- [Mac OSX](Max-OSX-installation.md)
- [Linux](Linux-installation.md)
- [ARM](ARM-Installation.md)




## 3. 运行 

> Gunbot XT 支持一个全新的 Web 控制台，你可以在浏览器中：
>
> - 轻松配置所有的机器人参数
> - 全新的配置系统： 为多种不同的交易对提供不同的预设
> - 从控制台选择配置文件、直接停止或运行机器人


直接运行 gunthy-gui 可执行文件，然后在系统浏览器中输入 `localhost:5000` 即可(推荐 Chrome 或者 Firefox 等现代浏览器)。



[开始使用 Gunthy UI](Using-Gunthy-GUI.md)

[了解如何在 Gunbot 中运行交易对](Configuring-Gunbot#pairs)


## 可选: 手动配置 JSON 配置文件

如果你想并不需要运行GUI界面，你需要编辑 `config.js` 文件保证机器人能够顺利运行。这也是 Gunbot 的唯一配置文件，你需要这这里添加你的API密钥，编辑机器人配置、交易对以及交易策略等等。 


[了解更多的配置说明](Configuring-Gunbot.md)




## 学习 Gunbot 中的交易策略

研究配置不同的交易策略，是让机器人自动交易的核心。
Read up on the different strategies you can use to automatically trade with Gunbot. 
你可以使用我们提供的大量预设好的的策略，或者更改其中的某些特殊需求（比如止损比率，双倍购买等等）。

[了解更多交易策略信息](About-Gunbot-strategies.md)







