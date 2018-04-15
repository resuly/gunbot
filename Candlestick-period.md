# Candlestick period

>[Info on candlestick patterns](https://en.wikipedia.org/wiki/Candlestick_pattern)

The `PERIOD` you set for candlesticks in your strategy is very important, since it has a big effect on how `EMA1` and `EMA2` are calculated. This article provides a really quick overview of what the impact of `PERIOD` is. 

A single candlestick is a visualization of the opening, closing, high and low prices within a certain timeframe. The most common used values for this timeframe (`PERIOD`) are 5 minutes, 15 minutes and 30 minutes. The closing price of each candlestick is used for calculating `EMA1` and `EMA2`. 

Using shorter candlesticks results in more price movement around EMA, this can be great for trading, but also be risky because you are fixated on short term trends only.

In the image below, you can see the effect on EMA (the green and red lines) when using different candlestick sizes, while keeping other variables the same.

![ema](https://user-images.githubusercontent.com/2372008/32069470-900b0cd0-ba89-11e7-93f1-fbdfa80b3001.png)

> tl;dr: Set `PERIOD` low to trade on short trends, set it higher to trade on longer trends.









