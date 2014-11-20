RASPBIAN BUILD NOTES
====================
Some notes on how to build TechCoin in Raspbian. 

Prerequisites
---------------------
* Raspberry Pi + Raspbian
* __RAM__
	* compilation could take up to 300MB of memory
	* model A with 256MB RAM - you will need bigger swap
	* model B and B+ with 512MB RAM - standard swap file (100MB) will do
	* maximize your RAM
		* _sudo raspi-config_ - Advanced Options -> Memory Split -> set GPU memory to minimum (16MB)
	* free as much RAM as possible (if you run other applications/servers close them for the time of compilation)
* __Disk space__
	* maximize your free space on SD card (min. 8GB card is recommended)
		* _sudo raspi-config_ - Expand Filesystem (expands disk space to take all available SD card capacity)
* Updated repositories
	* _sudo apt-get update_

Setup
-----
Install dependencies:

	sudo apt-get install -y git build-essential libboost1.50-dev libboost-filesystem1.50-dev libboost-system1.50-dev libboost-program-options1.50-dev libboost-thread1.50-dev libssl-dev libdb5.1++-dev libminiupnpc-dev qt4-qmake libqt4-dev
	
Create directories and clone git repository:

	cd ~ && mkdir -p ~/cryptos && cd ~/cryptos && git clone git://github.com/techcoincommunity/techcoin

Compiling daemon (Techcoind) from source
----------------------------------------
Compile (takes some time, depending on CPU speed, ~2h on stock 700Mhz):
    
	cd ~/cryptos/techcoin/src && mkdir obj && make -f makefile.unix
	
Allow daemon to be accessed from any path (optional: allows to use Techcoind <command> instead of using full path:

	sudo mv Techcoind /usr/local/bin

Compiling TechCoin-Qt from source
---------------------------------
Compile (takes even more time, depending on CPU speed, 4-8 hours):

	cd ~/cryptos/techcoin && qmake techcoin-qt-linux.pro && make

Strip debug symbols (optional but recommended: reduces binary size):

	strip techcoin-qt
	
Create Desktop icon (optional but useful:

	wget https://raw.githubusercontent.com/techcoincommunity/techcoin/master/src/qt/res/icons/TechCoin-128.png -O ~/.TechCoin/icon.png && echo -e "[Desktop Entry]\nName=TechCoin\nType=Application\nComment=TECH rebuilt! \nCategories=Application\nExec=/home/pi/cryptos/techcoin/techcoin-qt\nIcon=/home/pi/.TechCoin/icon.png\nTerminal=false\nStartupNotify=true" > ~/Desktop/techcoin.desktop
      
Updating
--------
Pull fresh code from git:

	cd ~/cryptos/techcoin && git pull
      
Repeat procedure for daemon or Qt (all steps)
