# 配置 Gunbot 

> **注意**: 如果你选择使用 Gunthy 后台管理界面的话，就不必手动配置config.js文件了。

所有Gunbot的设置都在“config.js”文件中，你可以在这里设置你的交易API、交易对、交易策略等等。如果在机器人运行的时候更改配置文件，新的配置将会被自动加载。下面将介绍配置文件中的参数含义。

确保保存设置的时候所有参数的完整性，以及JSON格式的合法性。 你可以通过 https://jsonlint.com 来测试JSON语法是否正确，保证没有括号或者逗号丢失之类的情况。



> **目录**
>

> 1. [机器人（Bot）](#bot-settings)
> 2. [电报（Telegram）](#telegram-settings-part-of-bot-section)
> 3. [TradingView](#tradingview-settings-part-of-bot-section)
> 4. [IMAP 监听](#imap-listener-settings-for-tradingview-plugin)
> 5. [WebSockets](#websockets-settings-ws)
> 6. [交易所（Exchanges）](#exchanges)
> 7. [交易对（Pairs）](#pairs)
> 8. [交易策略（Strategies）](#strategy-settings)
> 9. [加倍（Double Up）](#double-up-part-of-strategy-section)




## 设置机器人（Bot）

这些设置将定义Gunbot的核心操作。
如果你是很确定这些参数的含义，我们推荐使用默认值即可。

| 参数                | 默认值 |            说明                              |
| ------------------------ | ------------- | ---------------------------------------- |
| `debug`                  | false         | *值: true 或 false*. 如果设为true，将显示调试信息，你可以在调试程序的时候打开此功能。  |
| `BOT_DELAY`              | 1             | *值: 数字 – 该值代表机器人的延迟系数。* 在处理下一个新的交易对之前，机器人将随机延迟一定的毫秒数。 因为交易接口有时候会提示请求次数过多，该参数用于减少交易市场的高频请求。公式: 一个介于200到400 ms的随机值 * BOT_DELAY. 推荐的最小值: Bittrex: 1, Binance: 3, Cex: 2, Bitfinex: 8.   |
| `BOT_CCLEAN`             | 2           | *值: 数字 – 表示小时。* 这个参数表示每过x小时，Gunbot会通过重启强制清除缓存。该设置不会导致`TRADES_TIMEOUT`（交易超时）。如果你发现在长时间使用之后，机器人的交易有问题，可以把这个值调低一点。 |
| `CANCEL_ORDERS_ENABLED`  | true          | *值: true 或 false。* 如果该值设为true, 机器人将删除所有未满足买卖价格条件的订单（买卖的过程中价格产生很大的变化，未能满足之前操作的条件）。如果你想手动设置交易对又想同时运行 Gunbot，可以把这个值设为false。 |
| `CANCEL_ORDERS_CYCLE_CAP`  | 1          | *值: 数字 – 表示周期。* 用于定义在取消有效订单之前，等待多少个周期。 |
| `RESERVE_PILE_UP`  | false          | *值: true 或 false。* 该值为true时, 交易的获利将自动加到储备资金(funds reserve)之中，储备资金不会用于交易。|
| `interval_ticker_update` | 25000         | *值: 数字 – 代表毫秒。* 这个参数为更新币价的频率，具体为多少毫秒值从交易所更新一次 (默认值是 25000，也就是 25 秒)。比如你想通过非常短的市场变化进行交易，你可以可以把这个值设低一点，让Gunbot可以更快速度的更新价格。该参数与“period_storage_ticker”有直接关系，因为“period_storage_ticker”决定了把新的价格加入价格队列的频率。 |
| `period_storage_ticker`  | 2000          | *值: 数字 - 代表一个数值。* 这个参数用于规定保存多少条历史价格信息（价格队列），这些信息将用于计算其他相关指标。请不要把这个值调的很低，不然没有足够的数据进行指标计算，比如趋势监控、 局部 EMA 值计算等等都会出问题。每次价格更新的时候，新的价格都会自动加入价格队列中。当你的交易对数量很少的时候，每循环一次所有的交易对时间可能小于“interval_ticker_update”时间，这时每次循环都会更新价格并加入价格队列。 |
| `timeout_buy`            | 60000         | *值: 数字 – 数字 – 代表毫秒。* 这是一个内部超时设置，防止机器人在买入后设定的毫秒内重复购买。 |
| `timeout_sell`           | 60000         | *值: 数字 – 数字 – 代表毫秒。* 这是一个内部超时设置，防止机器人在卖出后设定的毫秒内重复出售。 |
| `VERBOSE`                | true          | *值: true 或 false* 如果设置为true，控制台中将显示更详细的信息。 |
| `WATCH_MODE`             | false         | *值: true 或 false* 如果设置为true即开启测试模式，Gunbot 将处理配置好的交易对，但不会真的进行买卖操作。 |
| `withdraw_address`             | 你的比特币地址     |  当收益每次达到阈值时启用自动打款到你设置的BTC钱包地址当中，该功能相当于自动提取收益。|
| `withdraw_threshold`             | 0.5         |  *值: 数字 - 代表BTC的数量阈值* 在设置自动打款数量之前，你需要先设置 `RESERVE_PILE_UP` 参数来累积你的收益。  |




### 电报机器人设置 （Telegram settings）

如果你希望Gunbot每次发生交易的时候，都通过Telegram自动给你发送交易信息，你可以按照以下步骤配置一个交易通知的电报机器人。

1. 与 [@botfather](https://telegram.me/botfather) 对话，然后保存显示的机器人令牌（bot token）。输入 /newbot 命令创建一个新的机器人，然后给你的电报机器人取一个名字。
2. 与 [@myidbot](https://telegram.me/myidbot) 对话，然后查看你的 Telegram ID 并保存。
3. 在设置中开启 Telegram 通知功能，然后分别填写刚刚保存的机器人令牌（bot token）与 Telegram ID。
4. 与你刚刚创建的电报机器人开始对话，并点击开始按钮。


| 参数                | 默认值 | 说明                              |
| ------------------------ | ------------- | ---------------------------------------- |
| `TELEGRAM_ENABLED`       | true          | *值: true 或 false。* 开启该选项后，Gunbot将在每次买卖交易后，通过电报机器人为你自动发送交易信息。 |
| `TELEGRAM_NICK`          | Gunbot          | *值: 字符串。 * 每一条交易通知都会有个昵称，你可以为不同的机器人实例起不同的名字，以分辨不同的交易信息。 |
| `TOKEN`          | put_your_TOKEN_here          | *值: 字符串。 * 电报机器人令牌（bot token）|
| `chat_id`          | put_your_TELEGRAM_ID_here          | *值: 字符串。 * 电报机器人 ID，Telegram ID |



### Tradingview 设置

以下信息仅仅与购买过 Tradingview 插件的用户相关，如果你不打算使用该插件，使用默认值即可。


| 参数                | 默认值 | 说明                              |
| ------------------------ | ------------- | ---------------------------------------- |
| `TV_GAIN`                | 0.6           | *值: 数字 - 代表百分比。* 默认值为0.6%，由Tradingview发起的交易必须遵守此处的最低收益百分比。当Tradingview发出的卖出订单的收益低于此值时，Gunbot不会下单。 该参数用于防止在亏损的情况下卖出。|
| `TV_TRADING_LIMIT_BUY`   | 0.001         | *值: 数字 - 代表主交易币的数量。* 该值定义了通过Tradingview买入订单的交易最大限额。比如在比特币为基础的交易对（BTC_x）上使用时，默认值0.001代买每次最多买入 0.001 BTC x币。|
| `TV_TRADING_LIMIT_SELL`  | 0.001         | *值: 数字 - 代表主交易币的数量。* 该值定义了通过Tradingview卖出订单的交易最大限额。比如在比特币为基础的交易对（BTC_x）上使用时，默认值0.001代买每次最多卖出 0.001 BTC x币。|
| `TV_PYRAMID`             | true         | *值: true 或 false。* 将此值设置为true将启用金字塔出售，每个金字塔出售量由`TV_TRADING_LIMIT_SELL`定义。 |
| `PYRAMID_BUY`             | true         | *值: true 或 false。* 将此值设置为true将启用金字塔买入，每个金字塔买入量由`TV_TRADING_LIMIT_BUY`定义。|
| `TV_PROTECTION`          | true          | *值: true 或 false。* 该参数是一种保护性参数，设置为true时，Gunbot将在卖出前根据TV_GAIN检查总体利润。 当设置为false时，Gunbot将不会干预所有的自定义TradingView策略。 |
| `TV_STOPLOSS_PERCENTAGE` | 60            | *值: 数字 - 代表百分比。* Percentage below averaged bought price at which a sell signal should override TV_PROTECTION and sell in a stop-loss manner. 这是一个止损设置，该值为低于平均买入价格的百分比。低于此价格后，会以止损的方式卖出，并且无视TV_PROTECTION参数。|
| `TV_TRADING_LIMIT_CAP`   | 0.9           | *值: 数字 - 代表以 BTC 为基准的价值。* 在所有的交易对中，除了主交易币外的其他币种，其累积买入的价值换算成BTC均不会超过该设定值。|






## IMAP 监听设置 (用于 Tradingview 插件)

以下信息仅仅与购买过 Tradingview 插件的用户相关，如果你不打算使用该插件，使用默认值即可。

| 参数            | 默认值                | 说明                              |
| -------------------- | ----------------------------- | ---------------------------------------- |
| `enabled`            | false                         | 将其设置为true，即可启用Tradingview插件。 但你需要确认你购买的版本已授权该功能。|
| `authorized_froms`   | [\"noreply@tradingview.com\"] | 设置 Tradingview 的发送邮箱|
| `user`               | YOUR_EMAIL_HERE               | 设置你的接收邮箱地址 |
| `password`           | YOUR_PASSWORD_HERE            | 输入你自己邮箱的密码 |
| `host`               | imap.gmail.com                | 该插件需要连接的IMAP服务器地址 |
| `port`               | 993                           | IMAP 服务器端口      |
| `tls`                | true                          | IMAP 连接中是否启用 TLS 加密 |
| `rejectUnauthorized` | false                         | 无 |






## WebSockets 设置 (ws)

以下设置用于设置 WebSockets 的端口号和主机名。

如果你不是很确定你的操作，建议使用默认值。

| 参数    | 默认值 | 说明                              |
| ------------ | ------------- | ---------------------------------------- |
| `port`       | 5001          | WebSockets 端口 |
| `clientport` | 3000          | 网页端界面的客户端端口 |
| `hostname`   | 127.0.0.1     | WebSockets 服务的 IP 地址或者主机名，默认为本地地址。如果是在远程服务器上，应设置为服务器的IP地址。 |






## 交易所设置

在本节中，你可以添加你想要交易的交易所的API密钥和密码（API key 和 secret ）。

同时如果你暂时不想在某个交易所进行交易，也不必删除其API配置。

> 建议每个Gunbot实例只运行一个交易所的配置。 运行第二个实例时，应通过复制你的Gunbot文件夹并确保每个实例的 `port`（在ws部分中端口设置）设置不同。 Gunthy GUI的后台界面，在同一台计算机上只能运行一个，但你可以运行多个机器人实例。

如果你想使用不同的API密钥进行交易，并且不是你最初向我们注册的交易密钥，这没有任何问题！ 你可以在不联系客服的情况下使用新密钥，但请确保你保持最初注册的密钥处于活动状态。

The following options exist for each Exchange. Only fill in those that you actually need, and registered a Gunbot licence on. Gunbot requires all API permissions, except withdrawals.

每个交易所都可以设置以下相关参数。 只填写你需要的部分即可，并注册对应的Gunbot许可。 在创建API时请注意，Gunbot 需要交易所 API 除了提款之外的所有权限。


| 参数    | 默认值 | 说明                              |
| ------------ | ------------------- | ---------------------------------------- |
| masterkey    | YOURMASTERAPIKEY    | The exchange key used for your Gunbot purchase (or the last key support swapped). Used for authentication with the Gunbot license server. Not necessarily used for trading, key needs to exist at the exchange. |
| mastersecret | YOURMASTERSECRETKEY | The secret belonging to the key used for your Gunbot purchase (or the last key support swapped).  |
| key          | YOURAPIKEY          | The exchange API key you want to use for trading with Gunbot. Needs to be on the same exchange account as the masterkey. You can also enter the master key here again to trade with this key. |
| secret       | YOURSECRETKEY       | Change this value to the secret belonging to your API key that you want to use for trading.  |
| clientId       | YOURCLIENTID       | Enter your CEX client ID. Only relevant for CEX.  |



> ### YOU ARE RESPONSIBLE FOR YOUR OWN KEYS. DO NOT LOSE YOUR MASTER KEY AND MASTER SECRET. EVER.
>
> Make absolutely sure you safely keep a copy of your master key and secret. Never deactivate two factor authentication at your exchange when not strictly needed.





## Pairs

In the pairs sections you can configure which pairs to use, on which exchange and which strategy should be used, optional overrides are possible. You need to remove any example pairs in the config.js file that you are not planning to use. Pairs need to be written in CAPS.

The set base coin is the one you want to accumulate. You use the base coin to buy another asset, and sell it back for profit in the base currency. Gunbot will always sell all assets when selling, and will buy according to your set trading limit.

Gunbot normalizes pair notation, so all pairs for all exchanges follow the same logic:

**BASECOIN-MARKETCOIN**



All pairs with BTC as base currency are written like:

**BTC-ETH, BTC-OK, BTC-XLM**



All pairs with USDT as base currency are written like:

**USDT-BTC, USDT-ETH, USDT-XMR**



For a few coins on Bitfinex, the API display name is required. These are:

IOTA = **IOT**

DASH = **DSH**

QTUM = **QTM**

DATA = **DAT**

QASH = **QSH**




> **Warning:** Never trade on different pairs that cross-over on the same exchange account. You should not trade BTC-ETH and ETH-LTC in the same account, or any other two pairs where one coin is present in both pairs. This is not a Gunbot limitation, but an exchange wallet limitation.
>
> The issue is you only have one wallet for each coin in your exchange account. That results in a funds battle if you run pairs that cross each other. So for example, BTC-ETH and ETH-XMR are crossed. BTC-ETH will sell all your ETH, and leave ETH-XMR unfunded. 



Configuring a pair to use bb as strategy, and override the MIN_VOLUME_TO_SELL value set in the bb strategy would look like this in config.js:

`"BTC-DASH": { "strategy": "bb", "override": {"MIN_VOLUME_TO_SELL": 0.01}}`

If you want to override settings for pairs using the GUI, you can do this on the edit setup page too like shown below:

![override](https://user-images.githubusercontent.com/2372008/36449655-b4fc264c-168b-11e8-8eb8-10d3f05ca7ba.gif)





## Strategy settings

Strategies use a generic set of parameters, which are mostly the same for each strategy. Only the relevant parameters are being used to process the strategy. 

Below you'll find details on every parameter. At the pages for strategy descriptions you can find details on how to use these exactly, and which parameters are relevant for each strategy.



| Parameter            | Default value | Description                              |
| -------------------- | ------------- | ---------------------------------------- |
| `TRADING_LIMIT`      | Strategy dependent      | *值: 数字 - 代表 an amount in primary trading currency.* This value defines the trading limit for limit buy orders placed by Gunbot. The default value of 0.001 would place maximum orders of 0.001 BTC when used on a BTC_x pair. Only use whole numbers for fiat pairs. |
| `FUNDS_RESERVE`      | Strategy dependent         | *值: 数字 - 代表 an amount in primary trading currency.* Sets an amount of base currency that will not be traded with. For a BTC_x pair, funds in BTC would be reserved, for an ETH_x pair the bot will keep the amount in ETH reserved, etc. It is recommended to use the same value for all pairs you run in this base currency. |
| `PERIOD`             | Strategy dependent         | *Values: 1 / 5 / 15 / 30 / 60* – represents candlestick size in minutes. Only use periods that are available on the charts on your exchange. |
| `BUY_LEVEL`          | Strategy dependent       | *值: 数字 - 代表 a percentage.* Relevant: when gain is used as buying strategy – also acts as global protection against buying above EMA for other strategies. This setting can be used as protection against buying above EMA. The default value of 0.1% will prevent the bot from buying when the price is not at least >0.1 % under the lowest EMA. |
| `GAIN`               | Strategy dependent        | *值: 数字 - 代表s a percentage.* Relevant: when gain is used as selling strategy. This sets the target for selling with Gain as selling strategy. The bot will sell when the set percentage above last buying price is reached. Also used as a security setting in other strategies, defining the minimum gain of all your trades. |
| `EMA1`               | Strategy dependent      | *值: 数字 - 代表s an amount of candlesticks.* Set this to the amount of candlesticks you want to use for your long EMA calculation. The closing price for each candle is used in the EMA calculation. For example: when you set PERIOD to 5, and want to have 2h for long EMA – you need to set EMA1 to 24 (24 * 5 mins). |
| `EMA2`               | Strategy dependent      | *值: 数字 - 代表s an amount of candlesticks.* Set this to the amount of candlesticks you want to use for your short EMA calculation. The closing price for each candle is used in the EMA calculation. For example: when you set PERIOD to 5, and want to have 1h for short EMA – you need to set EMA2 to 12 (12 * 5 mins). |
| `HIGH_BB`            | Strategy dependent      | *值: 数字 - 代表s a percentage.* Relevant: when bb is used as selling strategy & when DOUBLE_UP is activated. This sets the target for selling with bb as selling strategy. The bot will sell when the price hits a point 45% from HIGH_BB. |
| `LOW_BB`             | Strategy dependent     | *值: 数字 - 代表s a percentage.* Relevant: only when bb is used as buying strategy. This sets the target for buying with bb as buying strategy. The bot will buy when the price hits a point 45% from LOW_BB. |
| `STDV`               | Strategy dependent       | *Values: numerical (recommended: between 1.9 and 2.1)* – represents a multiplier value used in the bollinger bands calculation. Relevant: when using bb as buying or selling strategy & when DOUBLE_UP is activated. This value defines the multiplier used for calculation of the lower and upper bollinger bands. |
| `SMAPERIOD`          | Strategy dependent      | *值: 数字 - 代表s a number of candlesticks.* This parameter defines the amount of periods to be used for the simple moving average calculation. Set this value to the value used to chart on the exchange. If you want to use SMA 20 on the exchange charts, set this value to 20. Also used for configuring the trend watcher in stepgain strategies. |
| `BUYLVL1`            | Strategy dependent      | *值: 数字 - 代表s a percentage.* Relevant: only when stepgain is used as buying strategy. This sets the level 1 target for buying with stepgain as buying strategy. |
| `BUYLVL2`            | Strategy dependent       | *值: 数字 - 代表s a percentage.* Relevant: only when stepgain is used as buying strategy. This sets the level 2 target for buying with stepgain as buying strategy. |
| `BUYLVL3`            | Strategy dependent       | *值: 数字 - 代表s a percentage.* Relevant: only when stepgain is used as buying strategy. This sets the level 3 target for buying with stepgain as buying strategy. |
| `SELLLVL1`           | Strategy dependent          | *值: 数字 - 代表s a percentage.* Relevant: only when stepgain is used as selling strategy. This sets the level 1 target for selling with stepgain as selling strategy. |
| `SELLLVL2`           | Strategy dependent           | *值: 数字 - 代表s a percentage.* Relevant: only when stepgain is used as selling strategy. This sets the level 2 target for selling with stepgain as selling strategy. |
| `SELLLVL3`           | Strategy dependent        | *值: 数字 - 代表s a percentage.* Relevant: only when stepgain is used as selling strategy. This sets the level 3 target for selling with stepgain as selling strategy. |
| `BUYLVL`             | Strategy dependent        | *Values: 1 / 2 / 3 – represents steps.* Relevant: only when stepgain is used as buying strategy. This sets which step should be considered when using stepgain as buying strategy. 1: Buy when price drops below BUYLVL1 and stops dropping or hits BUYLVL2. 2: Buy when price drops below BUYLVL2 and stops dropping or hits BUYLVL3. 3: Buy when price hits BUYLVL3 and stops dropping. |
| `SELLLVL`            | Strategy dependent          | *Values: 1 / 2 / 3 – represents steps.* Relevant: only when stepgain is used as selling strategy. This sets which step should be considered when using stepgain as selling strategy. 1: Sell when price rises above SELLLVL1 and stops rising or hits SELLLVL2. 2: Sell when price rises above SELLLVL2 and stops rising or hits SELLLVL3. 3: Sell when price hits SELLLVL3 and stops rising. |
| `PP_BUY`             | Strategy dependent    | *值: 数字 - 代表s a price*. Relevant: only when pp Is used as buying strategy. Set the exact price you want Gunbot buying for when using pp as buying strategy. A buy order will be placed as soon as this price point has been hit, or an even better price is available. Only use whole numbers for fiat pairs. |
| `PP_SELL`            | Strategy dependent    | *值: 数字 - 代表s a price.* Relevant: only when pp Is used as selling strategy. Set the excact price you want Gunbot buying for when using pp as selling strategy. A sell order will be placed as soon as this price point has been hit, or an even better price is available. Only use whole numbers for fiat pairs. |
| `PANIC_SELL`         | Strategy dependent      | *值: true 或 false。* When set to true, all coins will be sold at market value. This can incur losses! |
| `STOP_LIMIT`         | Strategy dependent          | *值: 数字 - 代表s a percentage.* Sets a stop limit to sell a coin at a calculated loss. Setting a stop limit at 60 would cause that all balance for a coin are sold when the current price is >60% lower than bought price. After a stop limit sell order has been placed, the bot will go into buying mode after `TRADES_TIMEOUT` has passed and will buy again when market conditions meet your buying strategy. |
| `BUY_ENABLED`        | Strategy dependent        | *值: true 或 false。* Set this to false to prevent Gunbot from placing buy orders. |
| `SELL_ENABLED`        | Strategy dependent       | *值: true 或 false。* Set this to false to accumulate altcoins. Use `TRADES_TIMEOUT` to prevent fast consecutive buy orders.  |
| `MIN_VOLUME_TO_BUY`  | Strategy dependent       | *值: 数字 - 代表s the total value of a coins holdings in base currency.* Sets a threshold for buy orders. If you own less than the set amount, buy orders will still be placed. This prevents owning very small quantities (dust) blocking buy orders. Only use whole numbers for fiat pairs. |
| `MIN_VOLUME_TO_SELL` | Strategy dependent        | *值: 数字 - 代表s the total value of a coins holdings in market currency.* Sets a threshold for sell orders. If you own less than the set amount, sell orders will not be placed and the bot goes into buying mode again. Only use whole numbers for fiat pairs. |
| `TSSL_TARGET_ONLY`   | Strategy dependent       | *值: true 或 false。* Setting this to true protects you from sell orders at loss when using tssl as strategy. When set to false, hitting the lower boundary of the range set directly after buying leads to a sell at loss. |
| `RSI_BUY_ENABLED`   | Strategy dependent      | *值: true 或 false。* Setting this to true will make sure Gunbot only buys when both strategy buying conditions and `RSI_BUY_LEVEL` are met.  |
| `RSI_SELL_ENABLED`   | Strategy dependent        | *值: true 或 false。* Setting this to true will make sure Gunbot only sells when both strategy selling conditions and `RSI_SELL_LEVEL` are met. |
| `RSI_BUY_LEVEL`      | Strategy dependent         | *Values: numerical, ranging between 0 and 100.* Set the RSI to the level you want to allow the strategy to buy at. Additionally used as RSI level for Double Up buy orders. |
| `RSI_SELL_LEVEL`     | Strategy dependent         | *Values: numerical, ranging between 0 and 100.* Set the RSI to the level you want to allow the strategy to sell at. Only acts as an added confirmation.  |
| `BUY_RANGE`          | Strategy dependent       | *值: 数字 - 代表 a percentage.* This sets the buy range for tssl. Setting a range of 0.5% at a current price of 0.1 would set a range between 0.0995 and 0.1005. Only used in tssl strategy. |
| `SELL_RANGE`         | Strategy dependent       | *值: 数字 - 代表 a percentage.* This sets the sell range for tssl. Setting a range of 0.5% at a bought price of 0.1 would set a range between 0.0995 and 0.1005. Only used in tssl strategy. |
| `BOUGHT_PRICE`       | Strategy dependent         | *值: 数字 - 代表 a price.* Only to be used as override for pairs, use this to manually enter the last (or average) bought price when Gunbot can no longer retrieve it from the exchange |
| `TRADES_TIMEOUT`     | Strategy dependent       | *值: 数字 - 代表 time in seconds.* This sets a timeout preventing any trades to be placed for a pair after the last order, after starting the bot or after applying config changes. Use this to prevent double buys or fast consecutive buy orders when averaging down. Affects buy and sell orders. When the timeout is active you will see `Waiting to Trade - Safety Switch is on` in the logs. |
| `OKKIES_MODE`        | Strategy dependent       | *值: true 或 false。* Setting this to true disables buy orders when there is too much price and volume pressure on BTC. Configurable with `BTC_MONEY_FLOW`. Only use this if BTC pumps have a significant effect on your trading pair. |
| `BTC_MONEY_FLOW`     | Strategy dependent         | *Values: numerical, ranging between 0 and 100.* Sets the value on the Money Flow Index (MFI) you want `OKKIES_MODE` to disable buy orders. As soon as MFI hits the set value or drops below it, `OKKIES_MODE` will be enabled. |
| `TA_ALWAYS_ON`     | Strategy dependent         | *值: true 或 false。*  When set to true, all indicators are updated each cycle. When set to false, indicators will get updated once every period. Only set this to true if you have unmetered data available.  |




## Double Up (part of strategy section) 

These settings are used for averaging down with Double Up. They are part of the strategy section, but do not apply to the normal buying and selling part of the strategy.


| Parameter       | Default value | Description                              |
| --------------- | ------------- | ---------------------------------------- |
| `DOUBLE_UP`     | Strategy dependent         | *值: true 或 false。* When set to true, DOUBLE_UP will try to get rid of bags by averaging down. Works on all strategies. Averaging down can use up a lot of balance, make sure you have enough of your base currency available. Gunbot will start averaging down a bag according to your setting for `DU_METHOD`. |
| `DU_METHOD`     | Strategy dependent        | *Values: HIGHBB or RSI*. This sets the trigger for placing buy orders with Double Up. When set to **HIGH_BB** Gunbot will start averaging down a bag when the actual upper Bollinger Band drops below bought price (not the distance from it as set in `HIGH_BB`), and will then buy again when the upper Bollinger Band drops below the average buy price and the price is below last buy price, as set in `DU_BUYDOWN`. When set to **RSI** buy orders will only be placed when the set `RSI_BUY_LEVEL` is reached and the price is below last buy price, as set in `DU_BUYDOWN`. |
| `DOUBLE_UP_CAP` | Strategy dependent             | *Values: numerical - represents a ratio.* This defines the ratio to the pairs balance to be used for each consecutive buy when doubling up. Setting it to 0.5 would mean it uses a 0.5:1 ratio for averaging down. It is recommended to set this as high as you can afford, to increase your chance to actually average down and sell at profit. Example with ratio of 1: initial buy of 100 LTC, first double up buy order is 100 LTC, second will be 200 LTC, then 400 LTC, etc. Example with 0.5 ratio: initial buy of 100 LTC, first double up buy order is 50 LTC, then 75 LTC, then 112.5 LTC. |
| `DU_CAP_COUNT`  | Strategy dependent             | *Values: numerical - represents a number.* Limits the amount of times a Double Up order can be placed for a pair. The default setting of 1 would limit Double Up to only 1 buy before it waits to sell. When you set this higher, the bot will invest more and will get a lower average bought price to get rid of your bags faster. |
| `DU_BUYDOWN`    | Strategy dependent             | *Values: numerical, ranging between 0 and 100 - represents a percentage.* The minimum price drop compared to last bought price that needs to occur for Double Up buys to be placed. |
| `RSI_DU_BUY `     | Strategy dependent         | *Values: numerical, ranging between 0 and 100.* Use this to specify the RSI level for buying when `DU_METHOD` is set to RSI.  |
