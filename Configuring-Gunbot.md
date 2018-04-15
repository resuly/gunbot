# Configuring Gunbot 

> **Important**: you don't need to edit config.js manually when you are using Gunthy GUI



All Gunbot settings are done in a single file names “config.js”. This is where you set up your exchange API keys, add pairs and define your strategies. When the config file is overwritten while Gunbot is running, the changed settings will be loaded automatically. Below you'll find detailed explanations of all the options in the configuration file.

Make sure that no parameters are removed when setting it up. Make sure the JSON-formatting stays intact. Test for syntax errors on https://jsonlint.com, *always remove your API keys before testing!*



> **Contents:**
>

> 1. [Bot](#bot-settings)
> 2. [Telegram](#telegram-settings-part-of-bot-section)
> 3. [TradingView](#tradingview-settings-part-of-bot-section)
> 4. [IMAP listener](#imap-listener-settings-for-tradingview-plugin)
> 5. [WebSockets](#websockets-settings-ws)
> 6. [Exchanges](#exchanges)
> 7. [Pairs](#pairs)
> 8. [Strategies](#strategy-settings)
> 9. [Double Up](#double-up-part-of-strategy-section)




## Bot settings

These settings define the core behaviour of Gunbot.

It is recommended to use the default values unless you know what you are doing.



| Parameter                | Default value | Description                              |
| ------------------------ | ------------- | ---------------------------------------- |
| `debug`                  | false         | *Values: true or false*. Used to show debug messages in the bot, when set to true. Only use this if you really need to debug something.  |
| `BOT_DELAY`              | 1             | *Values: numerical – represents a multiplier value used in the formula to delay the bot.* Bot will delay processing a new pair for a random amount of milliseconds. Useful for when Poloniex complains about sending to many requests. Formula: random value between 200 and 400 ms * BOT_DELAY. Recommended mimimums: Bittrex: 1, Binance: 3, Cex: 2, Bitfinex: 8.   |
| `BOT_CCLEAN`             | 2           | *Values: numerical – represents time in hours.* This parameter forces the Gunbot cache to be cleaned by restarting the bot every x hours. This setting does not trigger `TRADES_TIMEOUT`. Only set this to a low value when your bot actually has problems not trading after a longer period of use. |
| `CANCEL_ORDERS_ENABLED`  | true          | *Values: true or false.* When set to true, the bot will remove unfulfilled orders when the price has moved away from the buy or sell price for unfulfilled orders. Set this to false if you trade manually on pairs you also run with Gunbot. |
| `CANCEL_ORDERS_CYCLE_CAP`  | 1          | *Values: numerical – represents a number of cycles.* Defines the number of cycles to wait before the bot is allowed to cancel open orders.  |
| `RESERVE_PILE_UP`  | false          | *Values: true or false.* When set to true, trading gains will be automatically added to the funds reserve.  |
| `interval_ticker_update` | 25000         | *Values: numerical – represents time in milliseconds.* This parameter defines after how many milliseconds new prices are being pulled from the exchange for each pair (default value of 25000 = 25 seconds). Set this to a lower value if you want Gunbot to retrieve prices faster, for example while you’re interested in following shorter trends.This value is related to "period_storage_ticker”, since it defines how often new prices are being added to the array. |
| `period_storage_ticker`  | 2000          | *Values: numerical - represent a number.* This parameter defines how many of the received prices from the exchange are being kept in the array for calculating other indicators. It is critical that you don’t set this value too low, otherwise you don’t have enough values for functions like the trend watcher or local EMA calculation. A new price gets added to this array every time the tickers are updated, or every time a new cycle starts faster than the set time for "interval_ticker_update" – the latter only happens if you run very little pairs in your bot. |
| `timeout_buy`            | 60000         | *Values: numerical – represent time in milliseconds.* This is an internal timeout that prevents the bot from buying again within the set amount of milliseconds after a buy order has been placed. |
| `timeout_sell`           | 60000         | *Values: numerical – represent time in milliseconds.* This is an internal timeout that prevents the bot from selling again within the set amount of milliseconds after a sell order has been placed. |
| `VERBOSE`                | true          | *Values: true or false*. Setting this to true will lead to more detailed information being shown in the console. |
| `WATCH_MODE`             | false         | *Values: true or false.* When set to true, Gunbot will process the configured pairs, but will not place actual buy or sell orders. Good for testing. |
| `withdraw_address`             | YOURBTCADDRESSHERE         |  Set a valid BTC wallet address to enable automatic withdraws each time the threshold is reached.  |
| `withdraw_threshold`             | 0.5         |  *Values: numerical - represents an amount of BTC.*  Set the amount of BTC to be accumulated with `RESERVE_PILE_UP` before an automatic withdraw will be executed.  |




### Telegram settings (part of bot section)

When you want Gunbot to send Telegram notifications of every trade placed, this is where you set that up.
Steps needed:
1. Talk to [@botfather](https://telegram.me/botfather) and save the bot token shown. Create a new bot with the command /newbot and choose a name and username for your bot.
2. Talk to [@myidbot](https://telegram.me/myidbot) to see your Telegram ID, save it.
3. Enable Telegram notifications for Gunbot, and enter the token and ID you've just gathered.
4. Start a chat with the username you've picked for your bot, and hit the start button. 


| Parameter                | Default Value | Description                              |
| ------------------------ | ------------- | ---------------------------------------- |
| `TELEGRAM_ENABLED`       | true          | *Values: true or false.* Enable this to have Gunbot send notifications through Telegram of every trade it makes.  |
| `TELEGRAM_NICK`          | Gunbot          | *Values: string * Each trade notification starts with the nickname set here. Use this to easily check from which bot instance the notifications have been sent.  |
| `TOKEN`          | put_your_TOKEN_here          | *Values: string * The Telegram token for your bot.  |
| `chat_id`          | put_your_TELEGRAM_ID_here          | *Values: string * The Telegram ID for your bot.  |



### Tradingview settings (part of bot section)

These are only relevant if you’ve bought the Tradingview plugin, just leave it on the default values if you are not planning to use the plugin.



| Parameter                | Default Value | Description                              |
| ------------------------ | ------------- | ---------------------------------------- |
| `TV_GAIN`                | 0.6           | *Values: numerical – represent a percentage.* Set a minimum gain in % that trades initiated by Tradingview must comply to. When sell orders are being placed by Tradingview that would have a lower gain than this value, Gunbot will not place the order. Use this to prevent selling at loss. |
| `TV_TRADING_LIMIT_BUY`   | 0.001         | *Values: numerical – represent an amount in primary trading currency.* This value defines the trading limit for orders placed through Tradingview. The default value of 0.001 would place maximum orders of 0.001 BTC when used on a BTC_x pair. |
| `TV_PYRAMID`             | true         | *Values: true or false.* Setting this value to true enables pyramid selling, the amount for each pyramid sell order is defined by `TV_TRADING_LIMIT_SELL`.  |
| `PYRAMID_BUY`             | true         | *Values: true or false.* Setting this value to true enables pyramid buying, the amount for each pyramid buy order is defined by `TV_TRADING_LIMIT_BUY`.  |
| `TV_TRADING_LIMIT_SELL`  | 0.001         | *Values: numerical – represent an amount in primary trading currency.* This value defines the trading limit for limit sell orders placed through Tradingview. The default value of 0.001 would place maximum orders of 0.001 BTC when used on a BTC_x pair. |
| `TV_PROTECTION`          | true          | *Values: true or false.* When set to true Gunbot will check there is an overall profit before selling, as specified in TV_GAIN. When set to false, Gunbot will execute all TradingView without interfering with a custom strategy. |
| `TV_STOPLOSS_PERCENTAGE` | 60            | *Values: numerical – represents a percentage.* Percentage below averaged bought price at which a sell signal should override TV_PROTECTION and sell in a stop-loss manner. |
| `TV_TRADING_LIMIT_CAP`   | 0.9           | *Values: numerical – represents a price in BTC value.* The maximum amount of BTC to be accumulated for a pair. |






## Imap listener settings (for Tradingview plugin)

These are only relevant if you’ve bought the Tradingview plugin, just leave it on the default values if you are not planning to use the plugin.



| Parameter            | Default Value                 | Description                              |
| -------------------- | ----------------------------- | ---------------------------------------- |
| `enabled`            | false                         | Set this to true to enable the Tradingview plugin. You need to acquire a licence for this. |
| `authorized_froms`   | [\"noreply@tradingview.com\"] | Set the Tradingview sender email address that you want to use. |
| `user`               | YOUR_EMAIL_HERE               | Set your own email address here. This address listens for mails from Tradingview. |
| `password`           | YOUR_PASSWORD_HERE            | Input the password for your own email address. |
| `host`               | imap.gmail.com                | The address of the IMAP server that the plugin needs to connect to. |
| `port`               | 993                           | The port number for the IMAP server.      |
| `tls`                | true                          | Defines if TLS encryption is used for the IMAP connection. |
| `rejectUnauthorized` | false                         |                                          |






## WebSockets settings (ws)

These settings are used to setup the port number and hostname for WebSockets. 

It is recommended to use the default values unless you know what you are doing.

| Parameter    | Default value | Description                              |
| ------------ | ------------- | ---------------------------------------- |
| `port`       | 5001          | You can change the port for WebSockets here. |
| `clientport` | 3000          | You can change the client port for third party web interfaces here. |
| `hostname`   | 127.0.0.1     | The IP address or hostname to be used for WebSockets. Defaults to your localhost. An external IP can also be set. |






## Exchanges

In this section you insert your API key and secret for the exchanges you want to trade on. 
You don’t need to remove the exchanges you do not want to trade on.

> It is recommended to run only one exchange per Gunbot instance. Run a second instance for your second exchange, by copying your Gunbot folder and making sure that the `port` (in the ws section) is set differently for each instance. Gunthy GUI can only run once on the same computer. 

If you want to use a different API key for trading than the one you initially registered with us, no problem! You can just use a new key without contacting support. Do make sure you keep the initially registered key active.

The following options exist for each Exchange. Only fill in those that you actually need, and registered a Gunbot licence on. Gunbot requires all API permissions, except withdrawals.



| Parameter    | Default value       | Description                              |
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
| `TRADING_LIMIT`      | Strategy dependent      | *Values: numerical – represent an amount in primary trading currency.* This value defines the trading limit for limit buy orders placed by Gunbot. The default value of 0.001 would place maximum orders of 0.001 BTC when used on a BTC_x pair. Only use whole numbers for fiat pairs. |
| `FUNDS_RESERVE`      | Strategy dependent         | *Values: numerical – represent an amount in primary trading currency.* Sets an amount of base currency that will not be traded with. For a BTC_x pair, funds in BTC would be reserved, for an ETH_x pair the bot will keep the amount in ETH reserved, etc. It is recommended to use the same value for all pairs you run in this base currency. |
| `PERIOD`             | Strategy dependent         | *Values: 1 / 5 / 15 / 30 / 60* – represents candlestick size in minutes. Only use periods that are available on the charts on your exchange. |
| `BUY_LEVEL`          | Strategy dependent       | *Values: numerical – represent a percentage.* Relevant: when gain is used as buying strategy – also acts as global protection against buying above EMA for other strategies. This setting can be used as protection against buying above EMA. The default value of 0.1% will prevent the bot from buying when the price is not at least >0.1 % under the lowest EMA. |
| `GAIN`               | Strategy dependent        | *Values: numerical – represents a percentage.* Relevant: when gain is used as selling strategy. This sets the target for selling with Gain as selling strategy. The bot will sell when the set percentage above last buying price is reached. Also used as a security setting in other strategies, defining the minimum gain of all your trades. |
| `EMA1`               | Strategy dependent      | *Values: numerical – represents an amount of candlesticks.* Set this to the amount of candlesticks you want to use for your long EMA calculation. The closing price for each candle is used in the EMA calculation. For example: when you set PERIOD to 5, and want to have 2h for long EMA – you need to set EMA1 to 24 (24 * 5 mins). |
| `EMA2`               | Strategy dependent      | *Values: numerical – represents an amount of candlesticks.* Set this to the amount of candlesticks you want to use for your short EMA calculation. The closing price for each candle is used in the EMA calculation. For example: when you set PERIOD to 5, and want to have 1h for short EMA – you need to set EMA2 to 12 (12 * 5 mins). |
| `HIGH_BB`            | Strategy dependent      | *Values: numerical – represents a percentage.* Relevant: when bb is used as selling strategy & when DOUBLE_UP is activated. This sets the target for selling with bb as selling strategy. The bot will sell when the price hits a point 45% from HIGH_BB. |
| `LOW_BB`             | Strategy dependent     | *Values: numerical – represents a percentage.* Relevant: only when bb is used as buying strategy. This sets the target for buying with bb as buying strategy. The bot will buy when the price hits a point 45% from LOW_BB. |
| `STDV`               | Strategy dependent       | *Values: numerical (recommended: between 1.9 and 2.1)* – represents a multiplier value used in the bollinger bands calculation. Relevant: when using bb as buying or selling strategy & when DOUBLE_UP is activated. This value defines the multiplier used for calculation of the lower and upper bollinger bands. |
| `SMAPERIOD`          | Strategy dependent      | *Values: numerical – represents a number of candlesticks.* This parameter defines the amount of periods to be used for the simple moving average calculation. Set this value to the value used to chart on the exchange. If you want to use SMA 20 on the exchange charts, set this value to 20. Also used for configuring the trend watcher in stepgain strategies. |
| `BUYLVL1`            | Strategy dependent      | *Values: numerical – represents a percentage.* Relevant: only when stepgain is used as buying strategy. This sets the level 1 target for buying with stepgain as buying strategy. |
| `BUYLVL2`            | Strategy dependent       | *Values: numerical – represents a percentage.* Relevant: only when stepgain is used as buying strategy. This sets the level 2 target for buying with stepgain as buying strategy. |
| `BUYLVL3`            | Strategy dependent       | *Values: numerical – represents a percentage.* Relevant: only when stepgain is used as buying strategy. This sets the level 3 target for buying with stepgain as buying strategy. |
| `SELLLVL1`           | Strategy dependent          | *Values: numerical – represents a percentage.* Relevant: only when stepgain is used as selling strategy. This sets the level 1 target for selling with stepgain as selling strategy. |
| `SELLLVL2`           | Strategy dependent           | *Values: numerical – represents a percentage.* Relevant: only when stepgain is used as selling strategy. This sets the level 2 target for selling with stepgain as selling strategy. |
| `SELLLVL3`           | Strategy dependent        | *Values: numerical – represents a percentage.* Relevant: only when stepgain is used as selling strategy. This sets the level 3 target for selling with stepgain as selling strategy. |
| `BUYLVL`             | Strategy dependent        | *Values: 1 / 2 / 3 – represents steps.* Relevant: only when stepgain is used as buying strategy. This sets which step should be considered when using stepgain as buying strategy. 1: Buy when price drops below BUYLVL1 and stops dropping or hits BUYLVL2. 2: Buy when price drops below BUYLVL2 and stops dropping or hits BUYLVL3. 3: Buy when price hits BUYLVL3 and stops dropping. |
| `SELLLVL`            | Strategy dependent          | *Values: 1 / 2 / 3 – represents steps.* Relevant: only when stepgain is used as selling strategy. This sets which step should be considered when using stepgain as selling strategy. 1: Sell when price rises above SELLLVL1 and stops rising or hits SELLLVL2. 2: Sell when price rises above SELLLVL2 and stops rising or hits SELLLVL3. 3: Sell when price hits SELLLVL3 and stops rising. |
| `PP_BUY`             | Strategy dependent    | *Values: numerical – represents a price*. Relevant: only when pp Is used as buying strategy. Set the exact price you want Gunbot buying for when using pp as buying strategy. A buy order will be placed as soon as this price point has been hit, or an even better price is available. Only use whole numbers for fiat pairs. |
| `PP_SELL`            | Strategy dependent    | *Values: numerical – represents a price.* Relevant: only when pp Is used as selling strategy. Set the excact price you want Gunbot buying for when using pp as selling strategy. A sell order will be placed as soon as this price point has been hit, or an even better price is available. Only use whole numbers for fiat pairs. |
| `PANIC_SELL`         | Strategy dependent      | *Values: true or false.* When set to true, all coins will be sold at market value. This can incur losses! |
| `STOP_LIMIT`         | Strategy dependent          | *Values: numerical – represents a percentage.* Sets a stop limit to sell a coin at a calculated loss. Setting a stop limit at 60 would cause that all balance for a coin are sold when the current price is >60% lower than bought price. After a stop limit sell order has been placed, the bot will go into buying mode after `TRADES_TIMEOUT` has passed and will buy again when market conditions meet your buying strategy. |
| `BUY_ENABLED`        | Strategy dependent        | *Values: true or false.* Set this to false to prevent Gunbot from placing buy orders. |
| `SELL_ENABLED`        | Strategy dependent       | *Values: true or false.* Set this to false to accumulate altcoins. Use `TRADES_TIMEOUT` to prevent fast consecutive buy orders.  |
| `MIN_VOLUME_TO_BUY`  | Strategy dependent       | *Values: numerical – represents the total value of a coins holdings in base currency.* Sets a threshold for buy orders. If you own less than the set amount, buy orders will still be placed. This prevents owning very small quantities (dust) blocking buy orders. Only use whole numbers for fiat pairs. |
| `MIN_VOLUME_TO_SELL` | Strategy dependent        | *Values: numerical – represents the total value of a coins holdings in market currency.* Sets a threshold for sell orders. If you own less than the set amount, sell orders will not be placed and the bot goes into buying mode again. Only use whole numbers for fiat pairs. |
| `TSSL_TARGET_ONLY`   | Strategy dependent       | *Values: true or false.* Setting this to true protects you from sell orders at loss when using tssl as strategy. When set to false, hitting the lower boundary of the range set directly after buying leads to a sell at loss. |
| `RSI_BUY_ENABLED`   | Strategy dependent      | *Values: true or false.* Setting this to true will make sure Gunbot only buys when both strategy buying conditions and `RSI_BUY_LEVEL` are met.  |
| `RSI_SELL_ENABLED`   | Strategy dependent        | *Values: true or false.* Setting this to true will make sure Gunbot only sells when both strategy selling conditions and `RSI_SELL_LEVEL` are met. |
| `RSI_BUY_LEVEL`      | Strategy dependent         | *Values: numerical, ranging between 0 and 100.* Set the RSI to the level you want to allow the strategy to buy at. Additionally used as RSI level for Double Up buy orders. |
| `RSI_SELL_LEVEL`     | Strategy dependent         | *Values: numerical, ranging between 0 and 100.* Set the RSI to the level you want to allow the strategy to sell at. Only acts as an added confirmation.  |
| `BUY_RANGE`          | Strategy dependent       | *Values: numerical – represent a percentage.* This sets the buy range for tssl. Setting a range of 0.5% at a current price of 0.1 would set a range between 0.0995 and 0.1005. Only used in tssl strategy. |
| `SELL_RANGE`         | Strategy dependent       | *Values: numerical – represent a percentage.* This sets the sell range for tssl. Setting a range of 0.5% at a bought price of 0.1 would set a range between 0.0995 and 0.1005. Only used in tssl strategy. |
| `BOUGHT_PRICE`       | Strategy dependent         | *Values: numerical – represent a price.* Only to be used as override for pairs, use this to manually enter the last (or average) bought price when Gunbot can no longer retrieve it from the exchange |
| `TRADES_TIMEOUT`     | Strategy dependent       | *Values: numerical – represent time in seconds.* This sets a timeout preventing any trades to be placed for a pair after the last order, after starting the bot or after applying config changes. Use this to prevent double buys or fast consecutive buy orders when averaging down. Affects buy and sell orders. When the timeout is active you will see `Waiting to Trade - Safety Switch is on` in the logs. |
| `OKKIES_MODE`        | Strategy dependent       | *Values: true or false.* Setting this to true disables buy orders when there is too much price and volume pressure on BTC. Configurable with `BTC_MONEY_FLOW`. Only use this if BTC pumps have a significant effect on your trading pair. |
| `BTC_MONEY_FLOW`     | Strategy dependent         | *Values: numerical, ranging between 0 and 100.* Sets the value on the Money Flow Index (MFI) you want `OKKIES_MODE` to disable buy orders. As soon as MFI hits the set value or drops below it, `OKKIES_MODE` will be enabled. |
| `TA_ALWAYS_ON`     | Strategy dependent         | *Values: true or false.*  When set to true, all indicators are updated each cycle. When set to false, indicators will get updated once every period. Only set this to true if you have unmetered data available.  |




## Double Up (part of strategy section) 

These settings are used for averaging down with Double Up. They are part of the strategy section, but do not apply to the normal buying and selling part of the strategy.


| Parameter       | Default value | Description                              |
| --------------- | ------------- | ---------------------------------------- |
| `DOUBLE_UP`     | Strategy dependent         | *Values: true or false.* When set to true, DOUBLE_UP will try to get rid of bags by averaging down. Works on all strategies. Averaging down can use up a lot of balance, make sure you have enough of your base currency available. Gunbot will start averaging down a bag according to your setting for `DU_METHOD`. |
| `DU_METHOD`     | Strategy dependent        | *Values: HIGHBB or RSI*. This sets the trigger for placing buy orders with Double Up. When set to **HIGH_BB** Gunbot will start averaging down a bag when the actual upper Bollinger Band drops below bought price (not the distance from it as set in `HIGH_BB`), and will then buy again when the upper Bollinger Band drops below the average buy price and the price is below last buy price, as set in `DU_BUYDOWN`. When set to **RSI** buy orders will only be placed when the set `RSI_BUY_LEVEL` is reached and the price is below last buy price, as set in `DU_BUYDOWN`. |
| `DOUBLE_UP_CAP` | Strategy dependent             | *Values: numerical - represents a ratio.* This defines the ratio to the pairs balance to be used for each consecutive buy when doubling up. Setting it to 0.5 would mean it uses a 0.5:1 ratio for averaging down. It is recommended to set this as high as you can afford, to increase your chance to actually average down and sell at profit. Example with ratio of 1: initial buy of 100 LTC, first double up buy order is 100 LTC, second will be 200 LTC, then 400 LTC, etc. Example with 0.5 ratio: initial buy of 100 LTC, first double up buy order is 50 LTC, then 75 LTC, then 112.5 LTC. |
| `DU_CAP_COUNT`  | Strategy dependent             | *Values: numerical - represents a number.* Limits the amount of times a Double Up order can be placed for a pair. The default setting of 1 would limit Double Up to only 1 buy before it waits to sell. When you set this higher, the bot will invest more and will get a lower average bought price to get rid of your bags faster. |
| `DU_BUYDOWN`    | Strategy dependent             | *Values: numerical, ranging between 0 and 100 - represents a percentage.* The minimum price drop compared to last bought price that needs to occur for Double Up buys to be placed. |
| `RSI_DU_BUY `     | Strategy dependent         | *Values: numerical, ranging between 0 and 100.* Use this to specify the RSI level for buying when `DU_METHOD` is set to RSI.  |
