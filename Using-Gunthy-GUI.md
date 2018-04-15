# 开始使用 Gunthy GUI

新的界面让你能够直接管理交易策略和交易对，现在你能轻松修改、应用、导出你的配置（setup）。让我们先来熟悉一下基本的用户界面。


> **注意：导入配置文件config.js一定要注意软件版本，不同版本的Gunbot对应的config.js可能并不相同。**



1. **为你的后台设置一个密码** 当你第一次打开后台界面时，你需要设置一个保护密码。请牢记密码，暂时不支持找回功能，一旦丢失可能需要重新安装软件。

   ​

2. **添加交易平台账户中的交易 API key 和 secret** 你只需添加一次即可，这也是Gunbot可以顺利自动交易的基本条件。

   第一个添加的key是主key，一般使用主key进行交易即可。更多的key相关操作见 [配置 Gunbot](Configuring-Gunbot#Pairs)。

   ​


![masterkey](https://user-images.githubusercontent.com/2372008/34016571-b5eb853c-e122-11e7-87e5-bb13e0becb4f.png) 

   

3. **配置你的交易策略**. 所有的交易策略可以在一个页面上统一管理。


![ui-api-keys](https://user-images.githubusercontent.com/2372008/32149960-60d66b96-bd0c-11e7-975d-8e8e45d65cb0.png) 

   ​

4. **创建一个配置方案，然后保存** 这里就是你选择交易对和交易策略的地方。


![setup701](https://user-images.githubusercontent.com/2372008/34016572-b60de050-e122-11e7-9cab-8e274d871f35.png) 



**添加额外配置** 如果你想针对某一个交易对单独设置某些条件，你可以在该交易对的override中添加相应的规则。

![gui-override](https://user-images.githubusercontent.com/2372008/32993701-2b77d718-cd5c-11e7-9c5a-833a0b329974.gif)






5. **在控制台（Dashboard）预览你的配置并运行机器人** 点击预览按钮（preview），可以预览你所有的设置过的交易对和配置信息。如果没什么问题，可以点击运行，机器人就开始自动交易了。


  你可以设置多个配置（setup）方案，然后同时运行。比如以BTC为基础的一套配置（setup）方案，以ETH为基础一套配置（setup）方案等等。同时也可以配置不同的交易市，比如币安一套配置（setup）方案，bittrex一套配置（setup）方案等等。
  
  
  如果你修改了某些系统参数或者交易策略，保存配置后，可以在控制台直接点击应用配置，在不停止机器人的情况下直接加载新的配置方案。


 ![ui-dashboard](https://user-images.githubusercontent.com/2372008/32149963-61875064-bd0c-11e7-927e-8fe5a3b723a9.png)




> 如果你忘记了后台密码，请删除并创建一个新的 `db.sqlite` 文件，当然这么做也会同时丢失所有的配置数据。

