# TradingView add-on

TradingView is the most active social network for traders and investors. TradingView allows users to create and share technical analysis and advanced trading strategies on their interactive charts. 

With the Gunbot TradingView add-on you can trade on alerts sent from custom strategies at Tradingview, completely managing your strategy at Tradingview. Gunbot receives trade signals by e-mail and trades accordingly.

> This is a paid add-on.


> **Contents:**
>
> 1. [Setup video](#setup-video)
> 2. [Tradingview settings](#tradingview-settings)
> 3. [Imap listener settings ](#imap-listener-settings)
> 4. [Alert message contents](#alert-message-contents)



### Setup video

Before you start setting up your alerts, you need:

- the IMAP data for the email address you receive alerts from TradingView on

- a Pro subscription at tradingview.com (works with trial too)



[Watch on YouTube](https://www.youtube.com/watch?v=H2EybuYxc3Y)

[Script used in example: Finn's Microprofit Strategy](https://gunthy.org/forum/index.php/topic,1548.0.html)



### Tradingview settings

To run Gunbot with the TradingView add-on, the following are the only relevant settings. Normal Gunbot strategy and pair settings are not relevant and not used. Be sure to add one pair for the exchange you want to run TV on though (this can be any pair, it will not be used by the add-on)!



| Parameter                | Default Value | Description                              |
| ------------------------ | ------------- | ---------------------------------------- |
| `TV_GAIN`                | 0.6           | *Values: numerical – represent a percentage.* Set a minimum gain in % that trades initiated by Tradingview must comply to. When sell orders are being placed by Tradingview that would have a lower gain than this value, Gunbot will not place the order. Use this to prevent selling at loss. |
| `TV_TRADING_LIMIT_BUY`   | 0.001         | *Values: numerical – represent an amount in primary trading currency.* This value defines the trading limit for orders placed through Tradingview. The default value of 0.001 would place maximum orders of 0.001 BTC when used on a BTC_x pair. |
| `TV_PYRAMID`             | true         | *Values: true or false.* Setting this value to true enables the use of pyramid contracts for selling through Tradingview, allowing for stacked sell orders. Be sure to have checked your strategy and balances before trying this. Selling respects TV_TRADING_LIMIT_SELL, making it possible to sell an asset in multiple steps. |
| `PYRAMID_BUY`             | true         | *Values: true or false.* Setting this value to true enables the use of pyramid contracts for buying through Tradingview, allowing for stacked buy orders. This might possibly trigger a large amount of trades. Be sure to have checked your strategy and balances before trying this. Selling respects TV_TRADING_LIMIT_BUY, making it possible to buy an asset in multiple steps. |
| `TV_TRADING_LIMIT_SELL`  | 0.001         | *Values: numerical – represent an amount in primary trading currency.* This value defines the trading limit for limit sell orders placed through Tradingview, only applies when `TV_PYRAMID` is set to true. The default value of 0.001 would place maximum orders of 0.001 BTC when used on a BTC_x pair. |
| `TV_PROTECTION`          | true          | *Values: true or false.* When set to true Gunbot will check there is an overall profit before selling, as specified in TV_GAIN. When set to false, Gunbot will execute all TradingView without interfering with a custom strategy. |
| `TV_STOPLOSS_PERCENTAGE` | 60            | *Values: numerical – represents a percentage.* Percentage below averaged bought price at which a sell signal should override TV_PROTECTION and sell in a stop-loss manner. |
| `TV_TRADING_LIMIT_CAP`   | 0.9           | *Values: numerical – represents a price in BTC worth.* The maximum amount of BTC to be accumulated for a pair. |



## Imap listener settings 

You need the IMAP settings to configure Gunbot to listen to TradingView signals, which will arrive by e-mail.



| Parameter            | Default Value                 | Description                              |
| -------------------- | ----------------------------- | ---------------------------------------- |
| `enabled`            | false                         | Set this to true to enable the Tradingview plugin. You need to acquire a licence for this. |
| `authorized_froms`   | [\"noreply@tradingview.com\"] | Set the Tradingview sender email address that you want to use. |
| `user`               | YOUR_EMAIL_HERE               | Set your own email address here. This address listens for mails from Tradingview. |
| `password`           | YOUR_PASSWORD_HERE            | Input the password for your own email address. |
| `host`               | imap.gmail.com                | The address of the IMAP server that the plugin needs to connect to. |
| `port`               | 993                           | The port number for the IMAP server      |
| `tls`                | true                          | Defines if TLS encryption is used for the IMAP connection. |
| `rejectUnauthorized` | false                         |                                          |



## Alert message contents

The alerts messages have to be in the following format in order for Gunbot act on them. Alerts follow the same standardized pair syntax that also apply for normal Gunbot usage.

### **For Poloniex**

BUY_POLONIEX_BASEPAIR-TRADINGPAIR

Examples:

- BUY_POLONIEX_BTC-ETH would buy ETH using BTC		
- SELL_POLONIEX_USDT-BTC would sell BTC for USDT
- STOPLOSS_BITTREX_BTC-PIVX would sell PIVX for BTC if stoploss is triggered.





### **For Bittrex**

BUY_BITTREX_MAINPAIR-TRADINGPAIR

Examples:

- BUY_BITTREX_ETH-MYST would buy MYST using ETH

- BUY_BITTREX_BTC-XLM would buy XLM using BTC

- SELL_BITTREX_BTC-ETH would sell ETH for BTC

- BUY_BITTREX_USDT-NEO would buy NEO using USDT

  ​


### **For Bitfinex**

BUY_BITFINEX_MAINPAIR-TRADINGPAIR

Examples:

- BUY_BITFINEX_BTC-ETH would buy ETH using BTC	
- SELL_BITFINEX_BTC-ETH would sell ETH for BTC
- STOPLOSS_BITFINEX_BTC-ETH would sell ETH for BTC if stoploss is triggered.




### **For Binance**

BUY_BITFINEX_MAINPAIR-TRADINGPAIR

Examples:

- BUY_BINANCE_BTC-ETH would buy ETH using BTC	
- SELL_BINANCE_BTC-ETH would sell ETH for BTC
- STOPLOSS_BINANCE_BTC-ETH would sell ETH for BTC if stoploss is triggered.




### For Kraken:

* BUY_KRAKEN_DASH-EUR would buy DASH using EURO
* SELL_KRAKEN_BTC-LTC would buy LTC using BTC





More examples and syntax for exchanges available for Gunbot:
* BUY_POLONIEX_BTC-ETH
* SELL_POLONIEX_USDT-BTC
* STOPLOSS_BITTREX_BTC-PIVX 
* STOPLOSS_POLONIEX_BTC-XLM 