# Example of using setups for trading on different market conditions

> **Beware:** this is an example, not serious trading advice. Always check if you agree on the settings used before putting them to use for you.



With setups you can save a set of trading pairs and their trading strategy as presets for running Gunbot. You can use this to easily switch between setups to change the way Gunbot trades when you notice that market conditions change. 

In this article you'll read about an example of how to create setups for trading in different market conditions.



## Market conditions

Let's assume we have three different market conditions to create setups for:

1. Prices are going to the moon, all over the market. (let's call this setup "Super Bullish")

2. Prices are kind of flat, there are fluctuations, but nothing is going seriously down- or upwards. (let's call this setups "Sideways")

3. Prices are going down and fast, all over the market. (let's call this setup "Super Bearish")

   ​



## Strategies

To handle these market conditions, we'll use two different strategies, and one override.



|                   | Strategy                                 | Logic                                    |
| ----------------- | ---------------------------------------- | ---------------------------------------- |
| **Super Bullish** | Fast, aggressive `stepgain`              | Market is great, let's buy on small price drops at fast trends and sell for moderate to great gains. |
| **Sideways**      | Slower, conservative`bbstepgain`         | Market is kind of neutral, let's be more careful and only buy low on the lower Bollinger Band, sell for moderate to great gains. |
| **Super Bearish** | Slower, sell only with `bbstepgain` + `BUY_ENABLED` override | Market is a total disaster. Let's only sell our assets as soon as a profit is reached. Do not buy again until market improves and another setup is activated. |



So, let's set up these strategies. Go to Strategies in Gunthy UI and configure them as shown in the picture below.



![ui-settings-example](https://user-images.githubusercontent.com/2372008/32149952-5ee24274-bd0c-11e7-8d24-81e5ac1ab4f4.png) 



## Create setups

Now it's time to create three setups to work with these strategies. Go to `+New Setup`, name it `Super Bullish` and add your pairs with `stepgain` as strategy. Save it.



![ui-setup-example-bullish](https://user-images.githubusercontent.com/2372008/32149956-5fc94ae8-bd0c-11e7-9766-f728e7f14e00.png) 



For the second setup, create a new one and add the same pairs, now choosing  `bbstepgain` as the strategy to use. Save it.



![ui-setup-example-sideways](https://user-images.githubusercontent.com/2372008/32149958-60803532-bd0c-11e7-8def-d8de5e79bb15.png) 



To create your setup for bearish conditions, name a new one `Super Bearish`, add the same pairs again choosing `bbstepgain` as strategy. Additionally, append an override to to set `BUY_ENABLED` to false, and make sure that when you have this setup running, no buy orders will be placed.


![ui-append-override](https://user-images.githubusercontent.com/2372008/32149962-6157d618-bd0c-11e7-811d-44147f2026ec.png) 


![ui-setup-example-bearish](https://user-images.githubusercontent.com/2372008/32149955-5f89230a-bd0c-11e7-89b9-9281c1d5432c.png) 



## Choose your setup and run Gunbot

Go to the dashboard, choose the setup you want to run. Hit `Run Setup` to start Gunbot.

Anytime you notice market conditions changed and you need to run Gunbot with another setup, just stop your running setup on the dashboard, then run another one.


![ui-setup-example-dashboard](https://user-images.githubusercontent.com/2372008/32149957-60289e76-bd0c-11e7-8432-c53530a20e1e.png) 