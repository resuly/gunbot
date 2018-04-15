# Ichimoku (beta)

>[Info on Ichimoku cloud](http://stockcharts.com/school/doku.php?id=chart_school:technical_indicators:ichimoku_cloud)


Using the Ichimoku cloud indicator, this strategy aims to find the optimal entry and exit points without notable configurable parameters. Timeframes are customizable by setting `PERIOD` to the candlestick size you prefer to trade on.

Entry and exit points consider tenkan sen, kijun sen and kumo sentiments. The exact algorithm will not be disclosed.

This strategy is not meant as a fast trading strategy at all. Don't be suprised about very long timeframes between buy and sell orders.





## Relevant settings

Following settings options are available for `ichimoku`



| Parameter            | Default value | Description                              |
| -------------------- | ------------- | ---------------------------------------- |
| `TRADING_LIMIT`      | 0.001         | *Values: numerical – represent an amount in primary trading currency.* This value defines the trading limit for limit buy orders placed by Gunbot. The default value of 0.001 would place maximum orders of 0.001 BTC when used on a BTC_x pair. Only use whole numbers for fiat pairs. |
| `FUNDS_RESERVE`      | 0.001         | *Values: numerical – represent an amount in primary trading currency.* Sets an amount of base currency that will not be traded with. For a BTC_x pair, funds in BTC would be reserved, for an ETH_x pair the bot will keep the amount in ETH reserved, etc. It is recommended to use the same value for all pairs you run in this base currency. |
| `PERIOD`             | 15            | *Values: 1 / 5 / 15 / 30 / 60* – represents candlestick size in minutes. Only use periods that are available on the charts on your exchange. |
| `STDV`               | 2             | *Values: numerical (recommended: between 1.9 and 2.1)* – represents a multiplier value used in the bollinger bands calculation.  This value defines the multiplier used for calculation of the lower and upper bollinger bands. This is only used for using `DOUBLE_UP `in this strategy. |
| `SMAPERIOD`          | 50            | *Values: numerical – represents a number of candlesticks.* This parameter defines the amount of periods to be used for the simple moving average calculation. Set this value to the value used to chart on the exchange. If you want to use SMA 50 on the exchange charts, set this value to 50. This is only used for using `DOUBLE_UP` in this strategy. |
| `PANIC_SELL`         | false         | *Values: true or false.* When set to true, all coins will be sold at market value. This can incur losses! |
| `DOUBLE_UP`          | false         | *Values: true or false.* When set to true, DOUBLE_UP will try to get rid of bags by averaging down. Works on all strategies. Averaging down can use up a lot of balance, make sure you have enough of your base currency available. Gunbot will start averaging down a bag according to your setting for `DU_METHOD`. |
| `DU_METHOD`          | HIGHBB        | *Values: HIGHBB or RSI*. This sets the trigger for placing buy orders with Double Up. When set to **HIGH_BB** Gunbot will start averaging down a bag when the actual upper Bollinger Band drops below bought price (not the distance from it as set in `HIGH_BB`), and will then buy again when the upper Bollinger Band drops below the average buy price and the price is below last buy price, as set in `DU_BUYDOWN`. When set to **RSI** buy orders will only be placed when the set `RSI_BUY_LEVEL` is reached and the price is below last buy price, as set in `DU_BUYDOWN`. |
| `DOUBLE_UP_CAP`      | 1             | *Values: numerical - represents a ratio.* This defines the ratio to the pairs balance to be used for each consecutive buy when doubling up. Setting it to 0.5 would mean it uses a 0.5:1 ratio for averaging down. It is recommended to set this as high as you can afford, to increase your chance to actually average down and sell at profit. Example with ratio of 1: initial buy of 100 LTC, first double up buy order is 100 LTC, second will be 200 LTC, then 400 LTC, etc. Example with 0.5 ratio: initial buy of 100 LTC, first double up buy order is 50 LTC, then 75 LTC, then 112.5 LTC. |
| `DU_CAP_COUNT`       | 3             | *Values: numerical - represents a number.* Limits the amount of times a Double Up order can be placed for a pair. The default setting of 1 would limit Double Up to only 1 buy before it waits to sell. When you set this higher, the bot will invest more and will get a lower average bought price to get rid of your bags faster. |
| `DU_BUYDOWN`         | 2             | *Values: numerical, ranging between 0 and 100 - represents a percentage.* The minimum price drop compared to last bought price that needs to occur for Double Up buys to be placed. |
| `BUY_ENABLED`        | true          | *Values: true or false.* Set this to false to prevent Gunbot from placing buy orders. |
| `SELL_ENABLED`        | true       | *Values: true or false.* Set this to false to accumulate altcoins. Use `TRADES_TIMEOUT` to prevent fast consecutive buy orders.  |
| `RSI_BUY_LEVEL`      | 30            | *Values: numerical, ranging between 0 and 100.* Set the RSI to the level you want to use for for Double Up buy orders. |
| `MIN_VOLUME_TO_BUY`  | 0.001         | *Values: numerical – represents the total value of a coins holdings in base currency.* Sets a threshold for buy orders. If you own less than the set amount, buy orders will still be placed. This prevents owning very small quantities (dust) blocking buy orders. Only use whole numbers for fiat pairs. |
| `MIN_VOLUME_TO_SELL` | 0.001         | *Values: numerical – represents the total value of a coins holdings in market currency.* Sets a threshold for sell orders. If you own less than the set amount, sell orders will not be placed and the bot goes into buying mode again. Only use whole numbers for fiat pairs. |
| `TRADES_TIMEOUT`     | 600           | *Values: numerical – represent time in seconds.* This sets a timeout preventing any trades to be placed for a pair after the last order and after starting the bot. Use this to prevent double buys or fast consecutive buy orders when averaging down. Affects buy and sell orders. When the timeout is active you will see `Waiting to Trade - Safety Switch is on` in the logs. |
| `TA_ALWAYS_ON`     | false        | *Values: true or false.*  When set to true, all indicators are updated each cycle. When set to false, indicators will get updated once every period. Only set this to true if you have unmetered data available.  |
| `RSI_DU_BUY `     | 30         | *Values: numerical, ranging between 0 and 100.* Use this to specify the RSI level for buying when `DU_METHOD` is set to RSI.  |
