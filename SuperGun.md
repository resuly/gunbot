**This page is about a legacy Gunbot version**

 # SuperGun

You can use the SUPERGUN strategy as an alternative to the 1000trades on. The SUPERGUN is easy to understand, but it can give you big profits during a pump. It uses the same watcher we use in the 1000trades for the pumps and dumps and overrides the %GAIN you set in configs.
​    
When there is a downtrend, the bot watches the price going down. When the price is at the bottom of the dump, it buys. The altcoins are now holding on your balance, and the bot starts to watch the trend, waiting for the pump. Soon as the pump starts, the bot waits for the highest possible price, and then it places a SELL order, a bit lower the highest price.
​    
The profit you get with this strategy depends on the spread between lowest and highest price in the pump/dump. The %GAIN you set in configs, becomes a "Minimum GAIN" we want. The bot won't SELL at lower GAIN. 
    Here is what I just got on NXC while I was writing this post: %GAIN is set at 1%, the bot got me over 3% in one single trade.

![](http://imgur.com/fVT9FXj.png)

Let's talk about the GUI now. As announced I started the refactor. I will push changes just-on-time which will not cause your bot to be restarted: you will be able to update the GUI while leaving your bot running Wink
I like this kind of development called RAD (rapid application development) because makes me feel very responsive to user's demands.

So in this first commit, besides the bot instances being docked with your dashboard, we got two interesting new features: the best currencies to trade analysis available BEFORE to start the bot and updating every hour on your dashboard, and some working and useful new buttons on the consoles. To start the currencies analysis, just press the "STATISTICS" button and then the $ symbol on your console (picture below explaining this step and describes all buttons)

![](http://imgur.com/hP1TYfx.png)