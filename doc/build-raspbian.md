RASPBIAN BUILD NOTES
====================
Some notes on how to build TechCoin in Raspbian. 

Prerequisites
---------------------
* Raspberry Pi + Raspbian
* __RAM__
..* compilation could take up to 300MB of memory
..* model A with 256MB RAM - you will need bigger swap
--* model B and B+ with 512MB RAM - standard swap file (100MB) will do
--* maximize your RAM
----* _sudo raspi-config_ - Advanced Options -> Memory Split -> set GPU memory to minimum (16MB)
--* free as much RAM as possible (if you run other applications/servers close them for the time of compilation)
* __Disk space__
..* maximize your free space on SD card (min. 8GB card is recommended)
....* _sudo raspi-config_ - Expand Filesystem (expands disk space to take all available SD card capacity)
* Updated repositories
..* _sudo apt-get update_

Dependency Build Instructions: Ubuntu & Debian
----------------------------------------------
Build requirements (if you don't want the Qt app you can omit libqtgui4 and libqt4-dev):

	sudo apt-get update
	sudo apt-get upgrade
	sudo apt-get install build-essential pkg-config
	sudo apt-get install libtool autotools-dev autoconf automake
	sudo apt-get install libssl-dev libdb-dev libdb++-dev libqrencode-dev qt4-qmake libqtgui4 libqt4-dev git
	sudo apt-get install libminiupnpc-dev libminiupnpc8 libboost-all-dev

Downloading Source
------------------
Create directories and clone git repository:
    
	cd ~ && mkdir -p ~/cryptos && cd ~/cryptos && git clone https://github.com/techcoincommunity/techcoin

Compiling daemon (Techcoind) from source
----------------------------------------   
Compile:

	cd ~/cryptos/techcoin/src && mkdir obj && make -f makefile.unix

Strip debug symbols (optional but recommended: reduces binary size):

	strip Techcoind
      
Allow daemon to be accessed from any path (optional: allows to use Techcoind <command> instead of using full path):

	sudo mv Techcoind /usr/local/bin

Compiling TechCoin-Qt from source
---------------------------------
Compile:

	cd ~/cryptos/techcoin && qmake techcoin-qt-linux.pro && make

Strip debug symbols (optional but recommended: reduces binary size):

	strip techcoin-qt
      
Updating
--------
Pull fresh code from git:

	cd ~/cryptos/techcoin && git pull
      
Repeat procedure for daemon or Qt (all steps)
