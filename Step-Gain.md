Step-Gain
---------------------------------------
Introducing you STEP-GAIN strategy at its first commit: this is a modification of supergun algorythm as discussed in the Telegram group. You now have 3 levels of buy % to set and 3 levels of sell %. Any of these levels is reached (in the dump or in the pump), the bot performs the max possible % of profit.

*Examples:*

- BUYLVL1: 1, // first level margin to buy when currency decreases its value (example: buy when currency decreases 1% of EMA)
- BUYLVL2: 3, // second level margin to buy when currency decreases its value (example: buy when currency decreases 3% of EMA)
- BUYLVL3: 5, // third level margin to buy when currency decreases its value (example: buy when currency decreases 5% of EMA)
- SELLLVL1: 2, // first level margin to sell when currency increases its value (example: sell when currency increases 2% of paid)
- SELLLVL2: 5, // second level margin to sell when currency increases its value (example: sell when currency increases 5% of paid)
- SELLLVL3: 10, // third level margin to sell when currency increases its value (example: sell when currency increases 10% of paid)

 *You can decide to use one or more levels of step gains by using the following configs:*

- BUYLVL: 3, // buy level you want your gunbot to reach (example: i want my gunbot to buy when price reaches level 3)

- SELLLVL: 3, // sell level you want your gunbot to reach (example: i want my gunbot to sell when price reaches level 3)

Other fixes:

- No more pending and unfulfilled BUY orders: the bot deletes the not needed orders after a sell loopShowing up running version on consolecode cleanup

>BEWARE: the bot is backward compatible ONLY with 2.0.2b save.json files. Any previous versions OR if you want to be 100% sure of a smooth transition: place sell orders manually of all your holdings.

Usage 
---------------------------------------

>The aim is to get higher profits. How is that done? By defining different levels or steps of gain.

Practical situation:

Levels exist both for buying as for selling orders.

When buying, the Bot first will try to reach the stablished % at Lvl 1: 1.5% for instance. If Lvl 2 is set in 2%, the bot will try to reach this price, and will proceed with the order if favorable. But let's say price keeps going down and your Buy Lvl 3 is set at 5%. Bot will still try to reach this target. However, if it's not possible, it'll will try to buy in a price range between lvl 3 and lvl 2.
But suddenly there a spike in prices and bot couldn't place an order in time. In this situation, it'll try to buy until lvl 1 is reached. As usual, if price keeps above buy price, it'll wait.


The same for selling orders.

What defines how many steps the bot will try to reach prior to place an order? This is configured in "Buy Level" and "Sell Level", which can also b found in control panel. Choose from 1 to 3, define your gain %, save settings, start GunBot and have a great trade!

>*- Criptonauta*