<ShiftGrid release version 16.32 >


ShiftGrid automatic trading system welcomes you!

***This version fixes an error that occurs on some exchanges when
trading coins with a price of millionths or less of a dollar.
At the same time, it is sometimes impossible to place an order for too precise a number
of tokens (for example, you cannot buy 12984536.7 PEPE, but 500000.0 is possible). Now
the initiating transactions (purchase/sale for a given percentage of the deposit)
are made for a WHOLE number of lots in the volume closest to the calculated
one (for example, the system will buy not 15306703.8 coins, but 15000000.0 coins with a lot 
500000.0 coins, that is, exactly three lots. Of course, the lot value itself should 
be a fairly round number).***  




Before starting work, you should perform some preparatory operations.
Create a new folder on your desktop and put all the files contained
in the archive that you downloaded into it.
We recommend naming the folder with the name of the exchange where you trade, mentioning
a specific account or subaccount (for example, "Bybit" or "Bybit_sub_1"). Then you
won't get confused if you have several bots running on different exchanges and accounts.
For each instance of the bot, you need to create a separate subaccount so that the money at
the disposal of the bots does not mix:)
Next, you should take care of the continuity of the trading process in any conditions,
for example, loss of Internet connection, power outages, etc.
To do this, first of all, you need to place a shortcut
to the "Startup" folder on the desktop. This is how it is done: 

- press "Win+R";
- in the window that opens, type "shell:startup" and click "OK";
- click the "Properties" icon;
- in the window that opens, select "Location";
- copy the path using "Ctrl+C" and close all windows so as not to interfere;
- right-click on the desktop to create a shortcut ("Create" --> "Shortcut");
- press "Ctrl+V" and "Next";
- the name of the "Startup" shortcut --> "Done";
- if desired, you can change the label icon to a brighter and more noticeable one.

That's it, now we have an autorun folder at hand, in which we will place shortcuts
that launch the bot at Windows startup.
 
Next, you need to set the system start mode
when POWER ON in the BIOS / UEFI settings of the computer. This is necessary in case there are interruptions
mains power supply (times are hard now!). In addition, the Internet connection
must be restored after the loss and restoration of computer power: if
the connection is via a USB modem, router or iPhone, then everything will happen automatically,
The Android smartphone does not restore the modem mode after losing power
to the computer, so you need to take care of the backup gateway. This is so, just
in case, almost everyone has a fixed Internet connection, and there is nothing to worry about.
  
So, almost everything is ready "on the client side", it remains to provide access to the bot
to the trading account. To do this, on the exchange's website, go
to the "API Management" tab in the account settings and click "Create New Key". In the pop-up window
that opens, select "System-generated API Keys" and then follow the meaning. It is better to give maximum access rights to the keys
, except for the withdrawal of funds. We copy and save the API Key and Private Key.
The Private Key (or Secret Key) is shown only once, so you need to copy and save
it right here and now.
 
The keys have been created, and you can start configuring the robot. All settings are contained in the text
the settings.cfg file in the folder with our robot. Open it in Notepad.

As you can see, the settings are simple and almost intuitive. IT is IMPORTANT that all
settings values should be in QUOTATION MARKS without unnecessary spaces.
We tell you what's what here.


EXCHANGE:             "Bybit.com"
Our exchange is here. Currently available Bybit.com , Bitget.com , Gate.io
and HitBTC.com . The names should be exactly like here:

ACCOUNT_TYPE:       "CLASSIC" (CLASSIC, UTA)
Account type. This is recognized on the account page, most likely by default CLASSIC.
So far, this is only relevant for Bybit.com 

API_KEY: "Your API key"
SECRET_KEY: "Your secret key"
Keys. Everything is clear here.

PASSPHRASE: "***"
Passphrase. Relevant for Bitget.com . It is not applied to the rest yet,
we leave the asterisks. 

BASE: "USDT" (USDT, USD, USDC ...)
The base currency. By default, USDT. We leave it.

SYMBOL:                  "ARB"
Our tradable asset. Here we have an Arbitrum(ARB), we insert our own (for example, PEPE)

LOT_QUANTITY:       "280.0" (CRYPTO)
The size of a single lot. We calculate on the calculator how much money we have in the market
in dollars, for which part of them we will make transactions (no more than 1/10 is recommended)
and at the current price we approximately count the amount of the ASSET (not dollars).
For many tokens, there will be a very large number, for bitcoin - a very small one. 

TP_PERCENT:            "2.6" (%) TP %
The percentage of TakeProfit. We indicate what kind of winnings we want to receive in the transaction.

START_GRID:            "2.6 3.8 4.6 7.9 10.0" (%) grid step %
Here is the first step of the order grid or LIST (separated by a space!) grids in
the CUSTOM mode.

GRID_MODE: "ARITHMETIC" (ARITHMETIC/GEOMETRIC/EXPONENTIAL/CUSTOM)
Type of grid progression. Everything is clear here. For example, if you select GEOMETRIC
and the grid offset is 1, then the grid scale will be uniform (the same will happen when you select
ARITHMETIC and offset 0).

GRID_BIAS: "1.26" (% if ARITHMETIC/factor if GEOMETRIC/exponent if EXPONENTIAL)
Grid offset. The next value will be added to this number, multiplied
by it, or raised to this power. It is not used in CUSTOM mode.

INI_AMOUNT:         "30" (%)
Initial balancing. If you have 1000 USDT on your account and there is no or little asset,
then the asset will be bought at the market price for such a percentage.
On the contrary, if you have only an asset in your account and almost no USDT, then such a percentage
of the asset will be sold on the market. 30%-33% seems optimal to us, but other
traders can determine the optimum experimentally.

PING: "18" (seconds)
Ping. This is the interval between requests to the exchange server. The new kind and affectionate
exchanges allow 10 requests per second, but there is no need to be rude, and there is no 
of necessity. Every 20 years...60 seconds is quite enough, we work on pending
orders, there is no need for a special data update speed. Especially if the traffic
is not unlimited. 

SOUND: "ON" (ON/OFF)
Sound. A pleasant bell at an event (for example, a transaction)

DELTA:                          "2.0" (%) approximately equal TP % 
The percentage that we will withdraw from each transaction, that is, live profit.
It should be LESS than the takeprofit, since the exchange also takes a commission.
Well, how much should be left "for reproduction"

MIDDLE_MULTIPLIER:  "OFF"(ON/OFF)
An advanced feature. If it is enabled, then in a situation where the asset and dollars
are approximately equal (in dollars), then the transaction size is multiplied by the selected
coefficient. It is useful when the market is flat: it increases profits. 

MIDDLE_BAND: "20" (%)
The range in which multiplication works (a kind of "tropical zone":)

MIDDLE_FACTOR:        "1.2"  (1 ... 2)
Multiplier (coefficient). When exiting the tropics, the lot size returns
to the above value.

WITHDRAW:                 "ON" (ON/OFF)
Withdrawal of profits to an isolated account. If enabled, the profit is accumulated on
a separate "wallet" and withdrawn from circulation. This is what
we come to the stock exchange for.  

TIME_DELAY:                  "20" (seconds)
Time delay when making a transaction at a market price, for example, at the first
start. If the order has not been executed during this time, it is canceled and a new one is placed.
In my experience, 20 seconds is usually enough, you can increase it a little, you shouldn't decrease it.

MAKE_SURE:                  "1" (times)
How many times to check that the market order has been executed. Once is enough
enough, the function is written for one exchange, the server of which is slow to respond.

WATCHDOG_TIME:       "3" (minutes)
The system has advanced protection against all kinds of freezes. It includes built
-in and external watchdogs. This is especially necessary when several instances
of the robot are running and the processor is not too powerful. Therefore, a special program is assigned to each bot
, which monitors the operation of the main program. If the bot has stopped showing
signs of life, then the watchdog will restart the computer after a certain time
. This happens 2... 4 times a week.

WD_SWITCH:                "ON"  (ON/OFF)
It is recommended to enable an external watchdog.

WD_PORT: "9092" (9093, 9094 ... )
The port where the external watchdog connects to the bot. 
We allocate a separate bot instance for each instance. The same port is specified in the wd.cfg file

FAIL_ATTEMPTS:           "4"
The number of errors in the requests in a row, at which a reboot will be made. 
4 already indicates that something went wrong, and a restart is needed.

That's all with the configuration. It remains to put shortcuts to launch the bot and its watchdog
(wd.exe ) the "Startup" folder, we recommend renaming them, for example like this:
"Bybit-Shortcut", "Bybit_Sub_1- Shortcut", "WD_Bybit - Shortcut", so as not to get confused with a large
number of bot instances.


When the robot is first started, a tmp folder is created inside the main folder, which contains the
files necessary for operation and saving the state in case of a reboot. 
You don't need to touch them, except for the file log.txt in which the history of events
(transactions, etc.) is recorded, you can always view it. When switching, for example, to another coin or
if you need to start everything from scratch, the tmp folder should be deleted. The next time you run it
, it will be created again. When editing the settings.cfg file (for example, if you want
to change the lot size or grid pitch), the bot will need to be restarted.  

***
When Windows starts for the first time, it may display a message that "prevented the launch
of an unidentified application blah blah blah", click "More details" and "run". 
We do not keep viruses :) In general, it is best to allocate a separate computer with a clean
operating system for the robot. For example, our bots work on a machine with a dual-core Atlas, 
left over from the mining farm, you can buy some cheap
nettop, processor power does not matter much.


The setup of the Shift Grid automatic trading system has been completed. If there are no errors,
then by double-clicking on the bot and watchdog shortcuts in the "Startup" folder (we recommend
starting it this way), we will begin an endless trading process that will become your
reliable source of passive income for many years to come.

May the Force be with you!

***

©2024 ShiftGrid


