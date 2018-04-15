# Emotionless



The Emotionless strategy is fully tuned and ready to use, even for novice traders! It's meant to be a relatively safe strategy, with modest but steady gains.

With this strategy, you don't need to think about setting the right or best parameters: it's all there already. You only need to set the basics like your trading limit and choose on which pairs you want to trade. 

Behind the scenes, an advanced algorythm based on the Ichimoku cloud indicator does the hard work. The specifics will not be disclosed.

Even the best strategy will sometimes create a bag, you can enable automatically averaging down with Double Up - just like in every other Gunbot strategy.





## Relevant settings

Following settings options are available for `emotionless`



| Parameter            | Default value | Description                              |
| -------------------- | ------------- | ---------------------------------------- |
| `TRADING_LIMIT`      | 0.01         | *Values: numerical – represent an amount in primary trading currency.* This value defines the trading limit for limit buy orders placed by Gunbot. The default value of 0.001 would place maximum orders of 0.001 BTC when used on a BTC_x pair. Only use whole numbers for fiat pairs. |
| `FUNDS_RESERVE`      | 0.001         | *Values: numerical – represent an amount in primary trading currency.* Sets an amount of base currency that will not be traded with. For a BTC_x pair, funds in BTC would be reserved, for an ETH_x pair the bot will keep the amount in ETH reserved, etc. It is recommended to use the same value for all pairs you run in this base currency. |
| `PERIOD`             | 15             | *Values: 1 / 5 / 15 / 30 / 60* – represents candlestick size in minutes. Only use periods that are available on the charts on your exchange. |
| `BUY_LEVEL`          | 0.6           | *Values: numerical – represent a percentage.* This sets the target for buying, at a percentage below the lowest EMA at that moment. |
| `GAIN`               | 0.6           | *Values: numerical – represents a percentage.* This sets the minimum gain target for selling. |
| `EMA1`               | 16            | *Values: numerical – represents an amount of candlesticks.* Set this to the amount of candlesticks you want to use for your long EMA calculation. The closing price for each candle is used in the EMA calculation. For example: when you set PERIOD to 5, and want to have 2h for long EMA – you need to set EMA1 to 24 (24 * 5 mins). |
| `EMA2`               | 8             | *Values: numerical – represents an amount of candlesticks.* Set this to the amount of candlesticks you want to use for your short EMA calculation. The closing price for each candle is used in the EMA calculation. For example: when you set PERIOD to 5, and want to have 1h for short EMA – you need to set EMA2 to 12 (12 * 5 mins). |
| `HIGH_BB`            | 49            | *Values: numerical – represents a percentage.* This sets the target for selling with bb as selling strategy. Leave this settings as it is.  |
| `LOW_BB`             | 49            | *Values: numerical – represents a percentage.* This sets the target for buying with bb as buying strategy. Leave this settings as it is.  |
| `STDV`               | 2             | *Values: numerical (recommended: between 1.9 and 2.1)* – represents a multiplier value used in the bollinger bands calculation.  This value defines the multiplier used for calculation of the lower and upper bollinger bands. This is only used for using `DOUBLE_UP ` in this strategy. |
| `SMAPERIOD`          | 50            | *Values: numerical – represents a number of candlesticks.* This parameter defines the amount of periods to be used for the simple moving average calculation. Set this value to the value used to chart on the exchange. If you want to use SMA 50 on the exchange charts, set this value to 50. This is only used for using `DOUBLE_UP` in this strategy. |
| `PANIC_SELL`         | false         | *Values: true or false.* When set to true, all coins will be sold at market value. This can incur losses! |
| `DOUBLE_UP`          | false         | *Values: true or false.* When set to true, DOUBLE_UP will try to get rid of bags by averaging down. Works on all strategies. Averaging down can use up a lot of balance, make sure you have enough of your base currency available. Gunbot will start averaging down a bag according to your setting for `DU_METHOD`. |
| `DOUBLE_UP_CAP`      | 1             | *Values: numerical - represents a ratio.* This defines the ratio to the pairs balance to be used for each consecutive buy when doubling up. Setting it to 0.5 would mean it uses a 0.5:1 ratio for averaging down. It is recommended to set this as high as you can afford, to increase your chance to actually average down and sell at profit. Example with ratio of 1: initial buy of 100 LTC, first double up buy order is 100 LTC, second will be 200 LTC, then 400 LTC, etc. Example with 0.5 ratio: initial buy of 100 LTC, first double up buy order is 50 LTC, then 75 LTC, then 112.5 LTC. |
| `STOP_LIMIT`         | 60            | *Values: numerical – represents a percentage.* Sets a stop limit to sell a coin at a calculated loss. Setting a stop limit at 60 would cause that all balance for a coin are sold when the current price is >60% lower than bought price. After a stop limit sell order has been placed, the bot will go into buying mode after `TRADES_TIMEOUT` has passed and will buy again when market conditions meet your buying strategy. |
| `BUY_ENABLED`        | true          | *Values: true or false.* Set this to false to prevent Gunbot from placing buy orders. |
| `SELL_ENABLED`        | true       | *Values: true or false.* Set this to false to accumulate altcoins. Use `TRADES_TIMEOUT` to prevent fast consecutive buy orders.  |
| `MIN_VOLUME_TO_BUY`  | 0.001        | *Values: numerical – represents the total value of a coins holdings in base currency.* Sets a threshold for buy orders. If you own less than the set amount, buy orders will still be placed. This prevents owning very small quantities (dust) blocking buy orders. Only use whole numbers for fiat pairs. |
| `MIN_VOLUME_TO_SELL` | 0.001       | *Values: numerical – represents the total value of a coins holdings in market currency.* Sets a threshold for sell orders. If you own less than the set amount, sell orders will not be placed and the bot goes into buying mode again. Only use whole numbers for fiat pairs. |
| `TRADES_TIMEOUT`     | 600           | *Values: numerical – represent time in seconds.* This sets a timeout preventing any trades to be placed for a pair after the last order and after starting the bot. Use this to prevent double buys or fast consecutive buy orders when averaging down. Affects buy and sell orders. When the timeout is active you will see `Waiting to Trade - Safety Switch is on` in the logs. |
| `MICROTRADES`     | true           | Leave this settings as it is. |

