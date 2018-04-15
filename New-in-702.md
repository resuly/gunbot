# What's new in Gunbot XT v7.0.2

Here's a quick overview of the most important changes introduced with Gunbot XT Edition (v7.0.2).

v7.0.2 fixes reported issues with v7.0.1. 

**It is strongly recommended to upgrade from v7.0.1 to v7.0.2**!


***



### Upgrading

> **GUI:** all settings from v6x+ can be migrated just by copying db.sqlite to the v7.0.2 folder before first run.


It is recommended to do a clean install in a new folder when you are migrating from v6 or older, because of many new parameters in config.js and changed default values. 


Coming from v7.0.1 you can just overwrite the executables, there are no new configuration parameters between v7.0.1 and v7.0.2.




***



## Core changes

- **RSI:** Adding RSI to (almost) all strategies, as an optional extra trigger for buying and/or selling. The whole bbrsi strategy family is  removed, since it's functionality can be replicated in all strategies that support `RSI_BUY_ENABLED` and/or `RSI_SELL_ENABLED`.




## Bugfixes

- **TSSL:** many fixes, massively improving TSSL performance.
- **RSI**: fixing an issue where RSI would show as undefined. With RSI enabled for buys or sells, no orders will be placed when for some reason RSI is undefined in a cycle.
- **Emotionless**: fixing selling behavior.
- **TradingView:** fix for "undefined of available" error
- **Binance / Bitfinex:** various fixes regarding minimum lot sizes, errors on fiat pairs and selling behavior.
- **Stepgain:** Fixing selling behavior.
- **Double Up:** fixing `DU_CAP_COUNT` behavior.
- **Cryptopia:** fixing "Money Flow Index undefined" error.
- **Various:** graceful handling of various errors.




------



#### Archive

[[Changes in v7.0.1|New in 701]]

[[Changes in v6.0.2|New in 602]]

[[Changes in v6.0.1|New in 601]]