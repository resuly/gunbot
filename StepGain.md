# Stepgain

> [Info on EMA](https://en.wikipedia.org/wiki/Moving_average#Exponential_moving_average)

Stepgain is similar to gain, but here you set a minimum buy level below the lowest EMA at that moment, and a second, even lower buy level. Gunbot will buy when the price stops dropping after reaching the first buy level, or when it keeps dropping and reaches the second buy level. This way you can try to get a really good buy price. 

With selling, you define a minimum gain as a percentage compared to the bought price, and a second sell level at which you’d definitely want to sell. A sell order will be placed when the first level is reached and the price no longer increases, or when the second level is reached. This way you can get much higher gains then setting a single fixed gain.

It is no longer needed or possible to configure the trend watcher manually. Trends are calculated automatically, taking into account your settings for `PERIOD` and `SMAPERIOD`.

You can optionally use RSI as confirmation to only buy or sell when both a trend reversal and a specific RSI level occur.



> The aim is to get higher profits. How is that done? By defining different levels or steps of gain.


>[Stepgain tuner (thanks @allanster!)](https://gunthy.org/forum/index.php/topic,1788.0.html)




## Relevant indicators

![stepgain-strategy-detail](https://user-images.githubusercontent.com/2372008/31969235-2d6e0efe-b914-11e7-8531-39721fa35e33.png)



## Relevant settings

Following settings options are available for `stepgain`



| Parameter            | Default value | Description                              |
| -------------------- | ------------- | ---------------------------------------- |
| `TRADING_LIMIT`      | 0.001         | *Values: numerical – represent an amount in primary trading currency.* This value defines the trading limit for limit buy orders placed by Gunbot. The default value of 0.001 would place maximum orders of 0.001 BTC when used on a BTC_x pair. Only use whole numbers for fiat pairs. |
| `FUNDS_RESERVE`      | 0.001         | *Values: numerical – represent an amount in primary trading currency.* Sets an amount of base currency that will not be traded with. For a BTC_x pair, funds in BTC would be reserved, for an ETH_x pair the bot will keep the amount in ETH reserved, etc. It is recommended to use the same value for all pairs you run in this base currency. |
| `PERIOD`             | 15            | *Values: 1 / 5 / 15 / 30 / 60* – represents candlestick size in minutes. Only use periods that are available on the charts on your exchange. |
| `BUY_LEVEL`          | 0.6           | *Values: numerical – represent a percentage.* This setting can be used as protection against buying above EMA. The default value of 0.1% will prevent the bot from buying when the price is not at least 0.1 % under the lowest EMA. |
| `GAIN`               | 0.6           | *Values: numerical – represents a percentage.* Used as a security setting, defining the minimum gain of all your trades. |
| `EMA1`               | 16            | *Values: numerical – represents an amount of candlesticks.* Set this to the amount of candlesticks you want to use for your long EMA calculation. The closing price for each candle is used in the EMA calculation. For example: when you set PERIOD to 5, and want to have 2h for long EMA – you need to set EMA1 to 24 (24 * 5 mins). |
| `EMA2`               | 8             | *Values: numerical – represents an amount of candlesticks.* Set this to the amount of candlesticks you want to use for your short EMA calculation. The closing price for each candle is used in the EMA calculation. For example: when you set PERIOD to 5, and want to have 1h for short EMA – you need to set EMA2 to 12 (12 * 5 mins). |
| `HIGH_BB`            | 49            | *Values: numerical – represents a percentage.* This sets the target for selling with bb as selling strategy. The bot will sell when the price hits a point 40% from HIGH_BB. This is not used in stepgain strategy. |
| `LOW_BB`             | 49            | *Values: numerical – represents a percentage.* This sets the target for buying with bb as buying strategy. The bot will buy when the price hits a point 40% from LOW_BB. This is not used in stepgain strategy. |
| `STDV`               | 2             | *Values: numerical (recommended: between 1.9 and 2.1)* – represents a multiplier value used in the bollinger bands calculation. Relevant: when using bb as buying or selling strategy & when DOUBLE_UP is activated. This value defines the multiplier used for calculation of the lower and upper bollinger bands. This is only used for using `DOUBLE_UP `in stepgain strategy. |
| `SMAPERIOD`          | 50            | *Values: numerical – represents a number of candlesticks.* This parameter defines the amount of periods to be used for the simple moving average calculation. Set this value to the value used to chart on the exchange. If you want to use SMA 50 on the exchange charts, set this value to 50. This parameter (together with `PERIOD`) configures the trend watcher, and is used for `DOUBLE_UP` in stepgain strategy. |
| `BUYLVL1`            | 0.6           | *Values: numerical – represents a percentage.* Relevant: only when stepgain is used as buying strategy. This sets the level 1 target for buying with stepgain as buying strategy. |
| `BUYLVL2`            | 2             | *Values: numerical – represents a percentage.* Relevant: only when stepgain is used as buying strategy. This sets the level 2 target for buying with stepgain as buying strategy. |
| `BUYLVL3`            | 70            | *Values: numerical – represents a percentage.* Relevant: only when stepgain is used as buying strategy. This sets the level 3 target for buying with stepgain as buying strategy. |
| `SELLLVL1`           | 0.6           | *Values: numerical – represents a percentage.* Relevant: only when stepgain is used as selling strategy. This sets the level 1 target for selling with stepgain as selling strategy. |
| `SELLLVL2`           | 2             | *Values: numerical – represents a percentage.* Relevant: only when stepgain is used as selling strategy. This sets the level 2 target for selling with stepgain as selling strategy. |
| `SELLLVL3`           | 70            | *Values: numerical – represents a percentage.* Relevant: only when stepgain is used as selling strategy. This sets the level 3 target for selling with stepgain as selling strategy. |
| `BUYLVL`             | 2             | *Values: 1 / 2 / 3 – represents steps.* Relevant: only when stepgain is used as buying strategy. This sets which step should be considered when using stepgain as buying strategy. 1: Buy when price drops below BUYLVL1 and stops dropping or hits BUYLVL2. 2: Buy when price drops below BUYLVL2 and stops dropping or hits BUYLVL3. 3: Buy when price hits BUYLVL3 and stops dropping. |
| `SELLLVL`            | 2             | *Values: 1 / 2 / 3 – represents steps.* Relevant: only when stepgain is used as selling strategy. This sets which step should be considered when using stepgain as selling strategy. 1: Sell when price rises above SELLLVL1 and stops rising or hits SELLLVL2. 2: Sell when price rises above SELLLVL2 and stops rising or hits SELLLVL3. 3: Sell when price hits SELLLVL3 and stops rising. |
| `PANIC_SELL`         | false         | *Values: true or false.* When set to true, all coins will be sold at market value. This can incur losses! |
| `DOUBLE_UP`          | false         | *Values: true or false.* When set to true, DOUBLE_UP will try to get rid of bags by averaging down. Works on all strategies. Averaging down can use up a lot of balance, make sure you have enough of your base currency available. Gunbot will start averaging down a bag according to your setting for `DU_METHOD`. |
| `DU_METHOD`          | HIGHBB        | *Values: HIGHBB or RSI*. This sets the trigger for placing buy orders with Double Up. When set to **HIGH_BB** Gunbot will start averaging down a bag when the actual upper Bollinger Band drops below bought price (not the distance from it as set in `HIGH_BB`), and will then buy again when the upper Bollinger Band drops below the average buy price and the price is below last buy price, as set in `DU_BUYDOWN`. When set to **RSI** buy orders will only be placed when the set `RSI_BUY_LEVEL` is reached and the price is below last buy price, as set in `DU_BUYDOWN`. |
| `DOUBLE_UP_CAP`      | 1             | *Values: numerical - represents a ratio.* This defines the ratio to the pairs balance to be used for each consecutive buy when doubling up. Setting it to 0.5 would mean it uses a 0.5:1 ratio for averaging down. It is recommended to set this as high as you can afford, to increase your chance to actually average down and sell at profit. Example with ratio of 1: initial buy of 100 LTC, first double up buy order is 100 LTC, second will be 200 LTC, then 400 LTC, etc. Example with 0.5 ratio: initial buy of 100 LTC, first double up buy order is 50 LTC, then 75 LTC, then 112.5 LTC. |
| `DU_CAP_COUNT`       | 3             | *Values: numerical - represents a number.* Limits the amount of times a Double Up order can be placed for a pair. The default setting of 1 would limit Double Up to only 1 buy before it waits to sell. When you set this higher, the bot will invest more and will get a lower average bought price to get rid of your bags faster. |
| `DU_BUYDOWN`         | 2             | *Values: numerical, ranging between 0 and 100 - represents a percentage.* The minimum price drop compared to last bought price that needs to occur for Double Up buys to be placed. |
| `STOP_LIMIT`         | 60            | *Values: numerical – represents a percentage.* Sets a stop limit to sell a coin at a calculated loss. Setting a stop limit at 60 would cause that all balance for a coin are sold when the current price is >60% lower than bought price. After a stop limit sell order has been placed, the bot will go into buying mode after `TRADES_TIMEOUT` has passed and will buy again when market conditions meet your buying strategy. |
| `BUY_ENABLED`        | true          | *Values: true or false.* Set this to false to prevent Gunbot from placing buy orders. |
| `SELL_ENABLED`        | true       | *Values: true or false.* Set this to false to accumulate altcoins. Use `TRADES_TIMEOUT` to prevent fast consecutive buy orders.  |
| `RSI_BUY_ENABLED`    | false         | *Values: true or false.* Setting this to true will make sure Gunbot only buys when both strategy buying conditions and `RSI_BUY_LEVEL` are met. |
| `RSI_SELL_ENABLED`   | false         | *Values: true or false.* Setting this to true will make sure Gunbot only sells when both strategy selling conditions and `RSI_SELL_LEVEL` are met. |
| `RSI_BUY_LEVEL`      | 30            | *Values: numerical, ranging between 0 and 100.* Set the RSI to the level you want to allow the strategy to buy at. Additionally used as RSI level for Double Up buy orders. |
| `RSI_SELL_LEVEL`     | 70            | *Values: numerical, ranging between 0 and 100.* Set the RSI to the level you want to allow the strategy to sell at. Only acts as an added confirmation. |
| `MIN_VOLUME_TO_BUY`  | 0.001        | *Values: numerical – represents the total value of a coins holdings in base currency.* Sets a threshold for buy orders. If you own less than the set amount, buy orders will still be placed. This prevents owning very small quantities (dust) blocking buy orders. Only use whole numbers for fiat pairs. |
| `MIN_VOLUME_TO_SELL` | 0.001        | *Values: numerical – represents the total value of a coins holdings in market currency.* Sets a threshold for sell orders. If you own less than the set amount, sell orders will not be placed and the bot goes into buying mode again. Only use whole numbers for fiat pairs. |
| `TRADES_TIMEOUT`     | 600           | *Values: numerical – represent time in seconds.* This sets a timeout preventing any trades to be placed for a pair after the last order and after starting the bot. Use this to prevent double buys or fast consecutive buy orders when averaging down. Affects buy and sell orders. When the timeout is active you will see `Waiting to Trade - Safety Switch is on` in the logs. |
| `OKKIES_MODE`        | true          | *Values: true or false.* Setting this to true disables buy orders when there is too much price and volume pressure on BTC. Configurable with `BTC_MONEY_FLOW`. Only use this if BTC pumps have a significant effect on your trading pair. |
| `BTC_MONEY_FLOW`     | 35            | *Values: numerical, ranging between 0 and 100.* Sets the value on the Money Flow Index (MFI) you want `OKKIES_MODE` to disable buy orders. As soon as MFI hits the set value or drops below it, `OKKIES_MODE` will be enabled. |
| `TA_ALWAYS_ON`     | false         | *Values: true or false.*  When set to true, all indicators are updated each cycle. When set to false, indicators will get updated once every period. Only set this to true if you have unmetered data available.  |
| `RSI_DU_BUY `     | 30         | *Values: numerical, ranging between 0 and 100.* Use this to specify the RSI level for buying when `DU_METHOD` is set to RSI.  |



