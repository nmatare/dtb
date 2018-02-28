# DTB
Deployable Trading Bot (Interactive Brokers)

* Version 1.0.1

## Description
This Virtual Machine (VM) is set up to automate the execution of [quantstrat](https://github.com/braverock/quantstrat) trading strategies. The VM establishes a connection to either Interactive Brokers Trader Workstation or Gateway. The execution platform is fully automated and will start, stop, shutdown, restart, and handle exceptions. 

* Please note that this repo is the /home/algo/ directory of the accompanying [VM](https://www.dropbox.com/sh/3peps1nd1s79eds/AAAUr1GwEf0_FGJK9Dz7x1r7a?dl=0). The primary purpose of this repo is to serve as dev version control. One needs to launch the [VM](https://www.dropbox.com/sh/3peps1nd1s79eds/AAAUr1GwEf0_FGJK9Dz7x1r7a?dl=0) either on AWS or locally to use the functionality described hereinafter.

## Features
  - Hardened ArchLinux Virtual Machine;
  - [IBController](https://github.com/ib-controller/ib-controller) service controls IB Gateway and Trader Workstation start, shutdown, and restart; and
  - 'trade.R' R execution of trading strategies.

## Installation
1.  Download the latest version of the [VM](https://www.dropbox.com/sh/3peps1nd1s79eds/AAAUr1GwEf0_FGJK9Dz7x1r7a?dl=0);
2. 	Install the VM on an AWS server or;
3. 	Launch the VM locally using either VirtualBox or VM Ware;
4.	SSH **with X11 port forwarding enabled** into the VM; e.g., autossh -X algo@192.168.56.3; and
5.  Place your algorithm into the /home/algo/projects/ directory, making sure that
	/home/algo/projects/algorithm/lib has the RScript 'trade.R'.

* Default passwords are: {[user: root, password: root], [user: algo, password: algo]}

## Usage
From the user's (algo) home directoy first initialize the algorithm. 
```sh
cd /home/algo/
sudo ./init
```
This will initalize the VM for trading based upon specified arguments. See the below section 'Arguments' to see available parameters. It is **very important** to choose robust user and root passwords. Otherwise your passwords and intellectual property will be at considerable risk to otherwise preventable security vulnerabilities.

To manually start and stop the algorithm use start or stop, respectively.
```sh
sudo ./start --algo_name pair_trade --strategy GOOGL_and_AAPL
sudo ./stop
```

## Arguments
#### Required Arguments
| Argument | Description
| ---------------------------- | ------------------------------------------- |
| `--account`       | Interactive Brokers account name 						 |
| `--password`      | Interactive Brokers account password 				 	 |
| `--strategy`      | The specified name of the quantstrat strategy 		 |

#### Configurable Arguments
| Argument | Description
| ---------------------------- | ------------------------------------------  |
| `--mode`          | Either 'live' or 'paper' trading mode [default = 'paper']				 |
| `--port`          | API port number to connect to Interactive Brokers Gateway/TWS [default = '4003'] |
| `--algo_name`     | The specifed name of the algorithm [default = ""] |
| `--file`          | Either to print to terminal screen: ['stdin', 'stdout', 'stderr'] or whether to log messages to a specified file [default = 'stdin']|
| `--bars`          | The specified periodicity of OHLC price data; ['1week', '1day', '1hour', '30mins', '15mins', '5mins', '3mins', '1min', '30sec', '5sec']  [default = '1day']|
| `--back_fill`     | The amount of data to backfill when initalizing the algorithim. This is helpful when one has moving averages (or similar) that need 'n' number of periods to calculate averages. Backfill must be specified in the form 'nS' where the last character may be any one of 'S' (seconds), 'D' (days), 'W' (weeks), 'M' (months), and 'Y' (year). Interactive Brokers limits historical data requests up to 1 year. [default = '1Y']|
|`--market`         |The desired market exchange [default = NYSE]			|
|`--market_open`    |The (local) time of market open [default = "09:30:00"]	|
|`--market_close`   |The (local) time of market close [default = "16:00:00"]|
|`--exchange`      	|The desired market exchange [default = 'ib']			|

## Examples
```sh
sudo ./init 			\
--account john_doe 		\
--password pass123 		\
--algo_name momentum 	\
--strategy 60month		\
--mode paper
```

```sh
sudo ./stop
```

```sh
sudo ./start 			\
--algo_name momentum 		\
--strategy 60month 		\
--mode live
```

Author(s)
----
* Nathan Matare 

License
----

GNU 2

Copyright 2016-2018 Nathan Matare 
  
This file is free software: you may copy, redistribute and/or modify it  
under the terms of the GNU General Public License as published by the  
Free Software Foundation, either version 2 of the License, or (at your  
option) any later version.  

This file is distributed in the hope that it will be useful, but  
WITHOUT ANY WARRANTY; without even the implied warranty of  
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU  
General Public License for more details.  

You should have received a copy of the GNU General Public License  
along with this program.  If not, see <http://www.gnu.org/licenses/>.

[//]: # (These are reference links used in the body of this note and get stripped out when the markdown processor does its job. There is no need to format nicely because it shouldn't be seen. Thanks SO - http://stackoverflow.com/questions/4823468/store-comments-in-markdown-syntax)

   [dill]: <https://github.com/joemccann/dillinger>
   [git-repo-url]: <https://github.com/joemccann/dillinger.git>
   [john gruber]: <http://daringfireball.net>
   [df1]: <http://daringfireball.net/projects/markdown/>
   [markdown-it]: <https://github.com/markdown-it/markdown-it>
   [Ace Editor]: <http://ace.ajax.org>
   [node.js]: <http://nodejs.org>
   [Twitter Bootstrap]: <http://twitter.github.com/bootstrap/>
   [jQuery]: <http://jquery.com>
   [@tjholowaychuk]: <http://twitter.com/tjholowaychuk>
   [express]: <http://expressjs.com>
   [AngularJS]: <http://angularjs.org>
   [Gulp]: <http://gulpjs.com>

   [PlDb]: <https://github.com/joemccann/dillinger/tree/master/plugins/dropbox/README.md>
   [PlGh]: <https://github.com/joemccann/dillinger/tree/master/plugins/github/README.md>
   [PlGd]: <https://github.com/joemccann/dillinger/tree/master/plugins/googledrive/README.md>
   [PlOd]: <https://github.com/joemccann/dillinger/tree/master/plugins/onedrive/README.md>
   [PlMe]: <https://github.com/joemccann/dillinger/tree/master/plugins/medium/README.md>
   [PlGa]: <https://github.com/RahulHP/dillinger/blob/master/plugins/googleanalytics/README.md>
