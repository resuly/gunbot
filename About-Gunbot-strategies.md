# Using and combining Gunbot strategies

Gunbot has 5 different main strategies that can be used to trade: these can be freely combined, where one strategy is being used for buying, and another for selling. Additionally, you can choose for the Emotionless or Ichimoku strategies - these cannot be combined with others.



| Strategy      | Description (short)                      |
| ------------- | ---------------------------------------- |
| `gain`        | Buy at a percentage below EMA, sell when your set gain is reached. |
| `stepgain`    | Like gain, but after hitting initial buy or sell level, a trend watcher will check if prices will further decrease or increase - making sure to only buy or sell when the trend reverses . |
| `bb`          | Buy and sell at configurable points between the lower and upper Bollinger Bands. |
| `pp`          | Set a fixed buy and sell price, perfect for coins that stay withing a predictable price range. |
| `tssl`        | Trailing Stop / Stop Limit: a moving range for buying and selling, trailing optimal buy and sell levels. |
| `emotionless` | "Just works" strategy. No configurable strategy parameters. Perfect for novice traders. |
| `ichimoku`    | Trading algorithm based on the Ichimoku cloud indicator. |



Settings for strategies are global, and apply to all pairs that you set to run on this strategy. When you need to make changes in the strategy settings for individual pairs, you can configure this using overrides in the pair setup (more on this below).



> **Contents:**
>
> 1. [All strategy combinations](#strategies-and-combining-them)
> 2. [Using Overrides](#using-overrides)



## Strategies and combining them

Each combination of strategies has its own section in the config file. If you want to use a combination of settings, pick the right one and proceed to configure the relevant parameters.

The following combinations can be used, each has its own section in the config file: 

| Strategy name   | Buy strategy               | Sell strategy              |
| --------------- | -------------------------- | -------------------------- |
| `bb`            | Bollinger Bands            | Bollinger Bands            |
| `gain`          | Gain                       | Gain                       |
| `pp`            | Pingpong                   | Pingpong                   |
| `stepgain`      | Stepgain                   | Stepgain                   |
| `tssl`          | Trailing stop / stop limit | Trailing stop / stop limit |
| `emotionless`   | Emotionless                | Emotionless                |
| `ichimoku`      | Ichimoku                   | Ichimoku                   |
| `tsslbb`        | Trailing stop / stop limit | Bollinger Bands            |
| `tsslpp`        | Trailing stop / stop limit | Pingpong                   |
| `tsslstepgain`  | Trailing stop / stop limit | Stepgain                   |
| `tsslgain`      | Trailing stop / stop limit | Gain                       |
| `bbrsitssl`     | Bollinger Bands + RSI      | Trailing stop / stop limit |
| `pptssl`        | Pingpong                   | Trailing stop / stop limit |
| `stepgaintssl`  | Stepgain                   | Trailing stop / stop limit |
| `gaintssl`      | Gain                       | Trailing stop / stop limit |
| `bbtssl`        | Bollinger Bands            | Trailing stop / stop limit |
| `bbgain`        | Bollinger Bands            | Gain                       |
| `gainbb`        | Gain                       | Bollinger Bands            |
| `bbstepgain`    | Bollinger Bands            | Stepgain                   |
| `stepgainbb`    | Stepgain                   | Bollinger Bands            |
| `bbpp`          | Bollinger Bands            | Pingpong                   |
| `ppbb`          | Pingpong                   | Bollinger Bands            |
| `gainstepgain`  | Gain                       | Stepgain                   |
| `stepgaingain`  | Stepgain                   | Gain                       |
| `gainpp`        | Gain                       | Pingpong                   |
| `ppgain`        | Pingpong                   | Gain                       |
| `stepgainpp`    | Stepgain                   | Pingpong                   |
| `ppstepgain`    | Pingpong                   | Stepgain                   |





## Using overrides

On pair level you can define exceptions for parts of a strategy. You could for example use a higher `TRADING_LIMIT` on a pair that you see particular potential in. The following example does just that.


```json
"BTC-ADA": {
	"strategy": "stepgain",
	"override": {
                "TRADING_LIMIT": 9000.00,
                 },
```



