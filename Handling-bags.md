# Handling bags

Every trader will have to deal with the situation that sometimes after a buy order has been successfully placed, the price drops and you're stuck with assets that lost value and cannot be sold for profit soon. Such assets block further trade activity for that pair, and are commonly called bags.

There are several things you can do to prevent this from happening, or to deal with bags.



## Wait it out

Not the most appealing option, but a common way to deal with bags is to just wait it out for the market to reach a profitable price level again. This of course won't always work, but it often does.  Try to always keep enough base currency balance, to be able to keep on trading while you wait for one or more bags to recover.

Keep in mind that it is not possible to retrieve old bought prices from the exchange API. At some point, usually after 30 days, you have to provide `BOUGHT_PRICE` manually as an override for your pair. On Poloniex Gunbot is able to retrieve older bought prices than 30 days.



## Stop limit

A common way to prevent accumulating bags is to cut your losses fast. With Gunbot you can set a `STOP_LIMIT`  to sell a pair automatically after it loses x% of it's value. To prevent getting into a negative spiral of consecutive buy orders and stop limit orders, no further buy orders will be placed until the price reaches a point again that is above the level of that of the stop limit sell order.



## Averaging down

By buying more assets at a lower price than the initial price, you get a lower average buy price - this allows you to sell at a lower price than the price you initially bought for and get rid of your bags with profit. You can do this manually, or automatically by using `DOUBLE_UP`.

When averaging down, it is recommended to invest a lot more than your initial investment. The more you invest, the lower the average price to sell will be and the sooner you can get rid of your bags. Because of this, it is not recommended to enable `DOUBLE_UP` for many pairs at the same time. You can control how much funds is used to average down by configuring `DOUBLE_UP_CAP`.

This is how a typical trading history looks when `DOUBLE_UP` has been used:

![double-up](https://user-images.githubusercontent.com/2372008/32096078-95baa8ee-bb05-11e7-8f07-266a7a3952b1.jpg)



