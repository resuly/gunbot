> **This page is about a legacy Gunbot version**

#  Current Issues:**

 - **1. Computer Disconnection**
  - If you are disconnected and GUNBOT Is running (had bought but couldn't sell due to disconnection), all you need to do is to write down the price GUNBOT was about to sell or take the price GUNBOT bought the pair at and multiply it by your gain percent then manually make the sell order in the exchange. Example: if your gain percent was 2% and your GUNBOT bought ETH at 0.015 and was disconnected you would then manuall sell it at 0.015 x 1.02 = 0.0153.

 - **2. Poloniex Error Status on GUNBOT**
   - '305': 'Use Proxy',
   - '307': 'Temporary Redirect',
   - '400': 'Bad Request',
   - '401': 'Unauthorized',
   - '402': 'Payment Required',
   - '403': The bot is not connecting to the server.  There are a couple potential issues
     - API keys are wrong or missing.
     - After adjusting your config settings, you did not save those settings.
     - IP restriction set but you did not actually save your IP to the list
   - '404': 'Not Found',
   - '405': 'Method Not Allowed',
   - '406': 'Not Acceptable',
   - '407': 'Proxy Authentication Required',
   - '408': 'Request Time-out',
   - '409': 'Conflict',
   - '410': 'Gone',
   - '411': 'Length Required',
   - '412': 'Precondition Failed',
   - '413': 'Request Entity Too Large',
   - '414': 'Request-URI Too Large',
   - '415': 'Unsupported Media Type',
   - '416': 'Requested Range Not Satisfiable',
   - '417': 'Expectation Failed',
   - '418': 'I\'m a teapot',
   - '422': If it is repeatedly and blocking the first start of the bot, make a new api key and send it to Gunthar. If it is occasionally or mixed with good cycles, it is just errors coming and the bot handling them in the correct way in the following cycles.

   - '423': 'Locked',
   - '424': 'Failed Dependency',
   - '425': 'Unordered Collection',
   - '426': 'Upgrade Required',
   - '428': 'Precondition Required',
   - '429': Temporary Ban from Exchange, because of too much API Requests by Bot.
     - Reduce the Bot Wait Time and Error Wait Time in config file if you use many coins to trade
     - Open less coin-pairs

   - '431': 'Request Header Fields Too Large',
   - '500': 'Internal Server Error',
   - '501': 'Not Implemented',
   - '502': 'Bad Gateway',
   - '503': 'Service Unavailable',
   - '504': 'Gateway Time-out',
   - '506': 'Variant Also Negotiates',
   - '507': 'Insufficient Storage',
   - '509': 'Bandwidth Limit Exceeded',