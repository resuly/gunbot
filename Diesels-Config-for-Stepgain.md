**This page is community content**



# Diesel Stepgain for 4.0.5

OK peeps, just because it gets asked for constantly. Note that this config is for version 4.0.5 and that NO CONFIG will give unbelievable returns in every market for every coin on every day. This works for me and my trade style, your results and expectations are your own and will vary. 

It is designed to have an extremely short trend watch. This means that a buy or sell can be triggered by just a few reverse prices. My goal was just to get it selling for most coins. I like it selling fast. If you want to ride the trends higher, you will need to add more points and prices to the averages. You will also need to make adjustments for very high volume coins, as these settings just don't grab enough info for a coin that has a lot of price points per minute. I have no idea if EMA settings make any difference - I haven't seen it, but then again I can't stand analysis. 

This is NOT a complete config.js. Just the applicable sections. 

I make no guarantees, and no, I will not analyze your individual coins for peak performance. I do not sell configs.

Please do NOT PM me in Telegram - I freely answer question on the main channel if I am around. And someone else smarter than me will probably answer, so bonus! 

    "bot": {
    "debug": false,
    "period_storage_ticker": 500,
    "interval_ticker_update": 15000,
    "timeout_buy": 60000,
    "timeout_sell": 60000,
    "WATCH_MODE": false,
    "VERBOSE": false
    },
    "strategies": {
     "stepgain": {
     "BTC_TRADING_LIMIT": .1,    <-- Change this to your own amount! Don't leave this comment in the JSON either.
     "PERIOD": 5,
     "BUYLVL1": 1.5,
     "BUYLVL2": 1.6,
     "BUYLVL3": 70,
     "SELLLVL1": 1.5,
     "SELLLVL2": 1.6,
     "SELLLVL3": 70,
     "BUYLVL": 2,
     "SELLLVL": 2,
     "LASTPOINTS": 4,
     "AVGPOINTS": 20,
     "AVGMINIMUM": 0.00000001,
     "EMA1": 4,
     "EMA2": 2,
     "PANIC_SELL": false,
     "STOP_LIMIT": 60,
     "BUY_ENABLED": true,
     "MIN_VOLUME_TO_BUY": 0.001,
     "MIN_VOLUME_TO_SELL": 0.001
     },
     },


tips appreciated!

**BTC:** 1DiESeLca4RfbvoUTVUg7NSRn16T3G8YPd 

**ETH:** 0x4381adfb5e212f2ac2477075b866357b0b69c37b 

Help me AND get a 10% discount at **Cointracking referal:** [https://cointracking.info?ref=D416986](https://cointracking.info?ref=D416986)
