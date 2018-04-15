# What's new in Gunbot XT Edition

Here's a quick overview of the most important changes introduced with Gunbot XT Edition (v6.0.2).

v6.0.2 fixes several issues reported for v6.0.1 and adds several new features. **It is strongly recommended to upgrade from v6.0.1 to v6.0.2**!

It is recommended to do a clean install in a new folder, because of several new settings in config.js and changed default values.





## Core changes



- **BTC pump protection**: automatically prevent buy orders from being placed when BTC price and volume are under high pressure. This is configurable per strategy or pair using `OKKIES_MODE` and `BTC_MONEY_FLOW`. 
- **Order recalculation:** Gunbot now automatically cancels unfulfilled orders when the current price moved away. This also affects manually placed orders - when you run the bot on the same pair.
- **Configurable cache cleaner**: some users reported cache issues after running Gunbot for a longer period, which prevented orders being placed. Gunbot can now be automatically restarted every x hours with `BOT_CCLEAN` - cleaning the cache every restart.
- **TSSL:** Various improvements and a new default value for `GAIN` to prevent possibly selling at loss due to exchange fees.


- **BBRSITSSL:** Added `GAIN` to the default strategy settings.
- **BBSRI:** fix to no longer cause the strategy to override stop limit.
- **TradingView:** several bugfixes and two new parameters: `TV_TRADING_LIMIT_CAP` and `TV_STOPLOSS_PERCENTAGE`. Unfulfilled orders are now automatically deleted.
- **TA library:** Tuning TA library to what we need. Cleaning up some deprecated stuff.
- **Reduced data usage:** fixed to decrease the amount of network traffic used by Gunbot.
- **Various:** fix an issue that would display wrong message "Safety switch is on..." when the `STOP_LIMIT` is hit.
- **Various:** fix pair cycling on Cryptopia.




## GUI changes

- **Pause logs**: logs can now be paused on the dashboard.
- **Improved dashboard performance:** fixing performance issues related to handling big log files.
- **Strategy sorting:** Strategies are now sorted logically in the strategy chooser dropdown.
- **Exchange keys:** trim blank spaces from input for API and secret.


------



#### Archive

[[Changes in v6.0.1|New in 601]]