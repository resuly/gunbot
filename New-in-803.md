# Gunbot XT v8.0.3 更新内容

Gunbot XT v8.0.3 更新一览


## Core changes核心功能的变化

- **新的交易所:** Gunbot 现在可以支持 CEX.io 交易平台
- **Telegram 自动交易通知:** 通过Telegram机器人自动发送 Gunbot 的每一笔买卖通知。 这项功能支持所有的交易所，并且自动计算每笔交易的收益（USD）、当前加倍购买次数等等。 [配置指南](Configuring Gunbot#telegram-settings-part-of-bot-section)
- **实时计算市场相关指数:** 如开启 `TA_ALWAYS_ON` 功能, 机器人每次查询币价时都会自动计算当前的相关指标，而以往都是在一定周期长度内计算。 开启这个功能会消耗更多的网络流量，不过一般没有太大影响。
- **为加倍购买（DU）单独设置 RSI 指标的选项:** 如开启 `RSI_DU_BUY` 功能，你可以设置一个单独的 RSI 指标，一但满足就会触发加倍购买（DU, Double Up）操作。

- **Timeout for order recalculation:** Gunbot在with `CANCEL_ORDERS_CYCLE_CAP` you can set the number of cycles to wait before Gunbot can cancel open oders.
<!-- - **订单出售增加了超时功能:** 如开启 `CANCEL_ORDERS_CYCLE_CAP` ，你可以设置一个查询次数，订单被最终出售前，会按照这个次数进行查询价格，决定是否取消。 -->

- **本金自动积累：**自动将您的利润增加到您的本金。
- **可选：提取BTC利润**您现在可以自动提取您的BTC利润。 使用这项功能需要您自担风险。
- **金字塔式购买（Pyramid buying）选项** TradingView 的附加组件现在支持金字塔式购买。



## 用户界面

- **支持运行多个实例:** 现在可以从用户界面运行多个配置文件，每个配置文件都拥有自己独立的机器人实例。
- **币安市场的 TradingView 图标:** 为币安市场的交易对添加对应的币安 TradingView 交易图。
- **在控制台（Dashboard）添加 TradingView 交易图:** 控制台上的每一个交易对都可以显示相应的 TradingView 交易图了，同时也包括基本的交易数据统计信息。
- **改进上手流程:** 现在的 Gunbot 比之前更容易上手了，通过简单几步即可配置运行。
- **众多微小改进:** 设置页面上操作变得更容易，去除PM2指标，改进交易策略参数的说明。



## 修复Bug

- 使用 PricePerUnit（实际价格）解析 Bittrex 历史交易记录
- 改进 Nodejs 中的 "promise rejections" 问题
- 修复没有近期交易记录的交易问题
- 修复bittrex 出现的"available of undefined" 问题
- 解决在Cryptopia下的出售方式问题
- 修复了一个会引发软件重启的问题。
- 允许在安全切换期间进行恐慌性出售操作
- 修复 TradingView 附加组件中的"Already bought enough"(已经买的足够多)问题
- 修复 Ichimoku 策略
- 修复部分出售情况下的加倍购买问题
- 修复订单的websocket的问题
- 改进了平均买入价格的计算方式
- 始终在控制台上输出平均购买价格
- 修复在Kraken上交易的问题
- 修复"waiting for open orders"（等待未结订单）问题
