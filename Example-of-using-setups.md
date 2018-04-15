# 根据不同的市场条件进行配置的示例

> **注意:** 这仅仅是一个示例，Gunbot 需要根据实际情况具体配置使用。 应用配置的之前请再三确认，以防错误配置引起不必要的损失。

一个配置（setups），能够让你保存一系列交易对和对应的交易策略，然后交给Gunbot去执行你设置好的配置方案。你可以根据市场的变化，轻松的切换几种预设好的不同的配置方案。

下面将详细介绍如何根据市场变化创建不同的配置方案。



## 市场变化

假设我们有三种不同的市场情况：

1. 价格快速疯涨，几乎整个市场所有的币种都在涨。 (我们可以把这个配置命名为"牛市")

2. 价格平稳，市场存在一些波动，但没有剧烈的涨或跌。(我们可以把这个配置命名为"平常心")

3. 价格快速猛跌，整个市场都在跌。 ("熊市")

   ​
## 交易策略

针对以上三种不同的市场情况，我们使用先使用两种交易策略设置两种情况，最后一种用覆盖配置的方法设置。

|                   | 策略         | 逻辑      |
| ----------------- | ---------------------------------------- | ---------------------------------------- |
| **牛市** | 迅速、有闯劲的 `stepgain` | 市场情况很好，我们可以在价格迅速小跌的时候买入，然后在稳健上涨的时候卖出。 |
| **平常心**      | 速度更慢、更保守的 `bbstepgain` | 市场比较中立的情况下，我们可以更小心一点，只在 Bollinger Band 值比较低的时候买入，然后在稳健上涨的时候卖出。 |
| **熊市** | 速度更慢、只卖不买的`bbstepgain` + `BUY_ENABLED`| 市场一团糟的情况下，我们可以在 "平常心" 的基础上设置 BUY_ENABLED 参数，只卖不买。这样所有的币在达到预设的利润率的情况下会被卖出，机器人在该配置下不会买入任何币。|


让我们一起来设置一下这几种策略，在 Gunthy UI 界面找到下面的策略配置页面：

![ui-settings-example](https://user-images.githubusercontent.com/2372008/32149952-5ee24274-bd0c-11e7-8d24-81e5ac1ab4f4.png) 



## 创建配置（setups）

现在创建三种配置方案，并设置对应的交易策略。 点击 `+New Setup`（新建配置）, 命名为 `牛市`，然后添加交易对并选择`stepgain`作为策略。保存。

![ui-setup-example-bullish](https://user-images.githubusercontent.com/2372008/32149956-5fc94ae8-bd0c-11e7-9766-f728e7f14e00.png) 

第二个配置也是一样的，添加交易对并选择 `bbstepgain` 作为交易策略，保存。 


![ui-setup-example-sideways](https://user-images.githubusercontent.com/2372008/32149958-60803532-bd0c-11e7-8def-d8de5e79bb15.png) 

新建一个`熊市`配置，添加交易对并选择 `bbstepgain` 作为交易策略。此外，添加一个额外设置，将`BUY_ENABLED`设置为 false，确保该配置不会触发买入操作。


![ui-append-override](https://user-images.githubusercontent.com/2372008/32149962-6157d618-bd0c-11e7-811d-44147f2026ec.png) 


![ui-setup-example-bearish](https://user-images.githubusercontent.com/2372008/32149955-5f89230a-bd0c-11e7-89b9-9281c1d5432c.png) 


## 选择配置并运行 Gunbot

到控制台页面，选择你刚刚设置好的配置方案，点击 `Run Setup` （运行配置）启动 Gunbot。

当你意识到市场变化并且需要切换配置的时候，停止运行 Gunbot，然后选择其他的方案，点击运行即可。

![ui-setup-example-dashboard](https://user-images.githubusercontent.com/2372008/32149957-60289e76-bd0c-11e7-8432-c53530a20e1e.png) 