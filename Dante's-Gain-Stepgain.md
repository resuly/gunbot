**This page is community content**

A configuration which tries to buy "safely", using a lot of values to avoid getting into pumps at the top. Modify LASTPOINTS and AVGPOINTS accordingly to your aggression.

     "stepgaingain": {
      "BTC_TRADING_LIMIT": 0.002,
      "PERIOD": 5,
      "BUYLVL1": 1.3,
      "BUYLVL2": 4,
      "BUYLVL3": 20,
      "BUYLVL": 1,
      "GAIN": 3,
      "LASTPOINTS": 30,
      "AVGPOINTS": 200,
      "AVGMINIMUM": 1e-8,
      "EMA1": 4,
      "EMA2": 2,
      "PANIC_SELL": false,
      "STOP_LIMIT": 30,
      "BUY_ENABLED": false,
      "MIN_VOLUME_TO_BUY": 0.001,
      "MIN_VOLUME_TO_SELL": 0.001
    }