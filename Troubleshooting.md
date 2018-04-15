# 常见问题

当你使用图形界面运行 Gunbot 时，机器人的运行日志会在控制台实时显示。同时日志文件会被储存在 out.log 文件中。 遇到错误请即使查看日志，寻找问题原因。

如果遇到问题，首先一个通用的解决方案就是：重启你的机器人。

### 目录
* [机器人的常见问题](Troubleshooting#bot-issues)
* [图形界面的常见问题](Troubleshooting#gui-issues)


### 机器人的常见问题

?>**INVALID LICENSE (...) Please contact Gunthar!**

`原因` 主密钥没有注册

`解决方案`
* 仔细检查密钥是否正确，确保前后没有空格
* 如果还是有问题请在社区联系我们 @

?>**Unable to check master key**

`原因` 未能成功验证您的密钥

`解决方案`
* 检查系统是否能够顺利联网，与 Gunbot 和交易平台是否能够顺利连接。
* 检查系统始终是否正确，建议与网络时间进行同步。
* 确保正确的配置密钥信息。
* 确保你的交易对输入正确，交易平台确实存在您所输入的交易对。



?>**Continuous messages about loading exchanges and configs**

`原因` 交易对产生的问题

`解决方案`
检查交易对是否拼写正确，交易对对大小写敏感。
* 验证交易对是否在交易市场上存在，如果Tradingview无法显示，一般即输入错误。


?>**...Safety Switch is on...**

`原因` 不允许机器人交易

`解决方案`

由于机器人被刚刚重启或启动，TRADES_TIMEOUT 。参数被激活，为了确保策略正确执行，一般会有短暂的安全期，在此期间不允许机器人交易。
* OKKIES_MODE 参数会阻止交易，原因是BTC-USD交易对高风险。
* WATCH_MODE 参数被激活，该模式即实验模式，并不会触发真实交易。

?>**Continuous heartbeat messages**

`原因`
无法获取相关指标数据

`解决方案`
确保你运行的是 Gunbot 最新稳定版本，包括配置文件 config.js 。
* 检查你的密钥是否正确，请不要留下任何空格
* 检查网络是否能正常连接（注：国内网络环境可能无法正常访问某些交易平台）
* 重新设置 PERIOD 参数，确保你选定的交易平台支持你选择的交易对
* 检查 config.js 文件是否存在异常，丢失一个逗号也会引起错误。

?>**Binance: error 1021**

`原因`
时间不同步

`解决方案`
检查系统时间是否正确，请将系统时间与 Internet 时间进行同步。

?>**Binance: error 400 / 401**

`原因`
请求币安数据失败

`解决方案`
检查系统时间是否正确，请将系统时间与 Internet 时间进行同步。
* 确保币安市场存在你选择的交易对，检查交易对名称与币安市场显示名称一致
* 尝试移除配置文件中重复的币安API配置，然后重试。
* 尝试重启路由器，或者刷新DNS缓存

?>**Binance: error 418 / 429**

`原因`
币安 API 交易频率限制

`解决方案`
暂停使用机器人，然后重新启动。
* 将 BOT_DELAY 参数的设置数值调高

?>**Poloniex: error 422**

`原因`
Poloniex API 交易频率限制

`解决方案`
暂停使用机器人，然后重新启动。
* 将 BOT_DELAY 参数的设置数值调高
* 如果问题还是存在，请联系我们注册一个新的 Poloniex API， 然后在仅一台设备上使用。

?>**TypeError: Cannot read property askprice of undefined**

`原因`
交易对设置出错

`解决方案`
检查交易对名称是否打错，以及市场是否支持您所输入的交易对。

?>**WARNING: we couldnt get a BOUGHT PRICE**

`原因`
买入价格未知

`解决方案`
为您的交易对额外单独添加 BOUGHT_PRICE 参数，您可以在图形界面中完成该操作。 


### 图形界面的常见问题

请先尝试一下重启你的机器人，看看能不能解决问题。

?>**Console screen flashes repeatedly after starting a setup**

`原因` 防火墙问题

`解决方案`
在防火墙中添加规则，确保为5000端口的进出流量放行。

?>**Error: bind EADDRINUSE null:5000**

`原因` 端口被占用

`解决方案`
有其他程序占用了5000端口，请尝试关闭所有其他在运行的 Gunbot，或者重启电脑。

?>**events.js:183 - Error: read ECONNRESET**

`原因` 图形界面不能从机器人获取数据

`解决方案`
图像界面暂时不能连接到机器人获取交易数据，一般并不影响机器人运行。

?>**Setups won't start. No error message is registered**

`原因` Gunbot 无法启动

`解决方案`
* Mac 系统: 确保从 terminal 启动 gunthy-gui-macos 程序，不要双击文件运行。
* 确保 gunthy 和 gunthy-gui 都可以被系统当前用户执行
* 删除或重命名 err.log 与 out.log 文件


