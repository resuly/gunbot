# 在 Mac 上安装 Gunbot

> 下载对应的 Gunbot XT 版本: https://github.com/GuntharDeNiro/BTCT/releases
>
> 像 node.js 和 pm2 这样的依赖组件已经被打包好，你无需手动安装。
>
> **[安装演示图](#installation-video)**




1. 解压 .zip 文件， 然后在命令行窗口（Terminal）执行以下命令，确保 Gunbot 和 Gunthy GUI 都可以执行：

   `chmod +x gunthy-macos`

   `chmod +x gunthy-gui`

2. 通过以下命令启动 Gunthy GUI，请保持命令窗口一直是开启状态：

   `./gunthy-gui`

3. 在系统浏览器中输入并访问 `localhost:5000`

   

> 你可能需要设置防火墙规则来允许 Gunbot 在5000端口的TCP进出流量，这取决于你的系统设置。


如果你不想启动图形界面，可以直接运行 Gunbot 的核心程序：
`./gunthy-macos`


> 还是有问题? 请尝试重启电脑，再次执行以上步骤。 更多信息请移步 [常见问题](Troubleshooting) 页面。

## 安装演示图
![macos-installation](./images/34313103-28a55d5e-e769-11e7-9be1-5ac2872c1d1f.gif)
