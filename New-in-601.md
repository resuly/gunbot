# What's new in Gunbot XT Edition

Here's a quick overview of the most important changes introduced with Gunbot XT Edition (v6.0.1).



## New official GUI

Gunbot XT Edition includes a fully new browser based GUI. You no longer need to edit any configuration file to use Gunbot.



## New strategies

- **BB-RSI**: Trade on combined BB and RSI indicators, making sure buy orders are only placed on oversold market conditions, and sell orders are only placed when the market is overbought.
- **TSSL:** Introducing the concept of trailing stop - stop loss for buy and sell orders. Buy lower, sell higher! Maximize your gains by trailing price movements and only buy or sell when the trend has reached its tipping point.

The new strategies can be used as buying or selling strategy, Gunbot now has a total of 36 different trading strategies!

## New exchange: Bitfinex

Gunbot now supports trading at Bitfinex. Contact your reseller for a licence.

## Various

- **Much improved indicator calculation:** market info is now automatically pulled from Gunthy API when not available on the exchange, enabling fast and accurate calculation of indicators like Bollinger Bands. 

- **Predictable pair cycling:** Gunbot now cycles through your pairs in the same sequence as in your configuration. You can prioritize pairs by changing the order in your configuration.

- **New trend watcher for stepgain:** Xtreme Trend Watcher does what it's supposed to do and is configurable by setting `PERIOD` and `SMAPERIOD` to your desired timeframe.

- **Configurable ratio for averaging down:**  with `DOUBLE_UP_CAP`  you can set a ratio for each `DOUBLE_UP` buy order, compared to your current balance for your pair. Use this if you want to average down in a slower, more controlled way. 

- **New configurable trades timeout:** with `TRADES_TIMEOUT` you can define the minimum amount of time between trades for a pair, eliminating double buy orders during normal trading or fast consecutive buy orders when averaging down.

  ​

