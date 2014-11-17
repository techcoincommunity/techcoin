UNIX BUILD NOTES
====================
Some notes on how to build TechCoin in Unix. 

Dependencies
---------------------

 Library     | Purpose          | Description
 ------------|------------------|----------------------
 libssl      | SSL Support      | Secure communications
 libdb5.1    | Berkeley DB      | Wallet storage
 libboost    | Boost            | C++ Library
 miniupnpc   | UPnP Support     | Optional firewall-jumping support
 qt          | GUI              | GUI toolkit
 protobuf    | Payments in GUI  | Data interchange format used for payment protocol
 libqrencode | QR codes in GUI  | Optional for generating QR codes

[miniupnpc](http://miniupnp.free.fr/) may be used for UPnP port mapping.  It can be downloaded from [here](
http://miniupnp.tuxfamily.org/files/).  UPnP support is compiled in and
turned off by default.  See the configure options for upnp behavior desired:

	--without-miniupnpc      No UPnP support miniupnp not required
	--disable-upnp-default   (the default) UPnP support turned off by default at runtime
	--enable-upnp-default    UPnP support turned on by default at runtime

Licenses of statically linked libraries:
 Berkeley DB   New BSD license with additional requirement that linked
               software must be free open source
 Boost         MIT-like license
 miniupnpc     New (3-clause) BSD license

System requirements
--------------------

C++ compilers are memory-hungry. It is recommended to have at least 1 GB of
memory available when compiling Dogecoin Core. With 512MB of memory or less
compilation will take much longer due to swap thrashing.

Dependency Build Instructions: Ubuntu & Debian
----------------------------------------------
Build requirements:

sudo apt-get update
sudo apt-get upgrade
sudo apt-get install build-essential pkg-config
sudo apt-get install libtool autotools-dev autoconf automake
sudo apt-get install libssl-dev libdb-dev libdb++-dev libqrencode-dev qt4-qmake libqtgui4 libqt4-dev git
sudo apt-get install libminiupnpc-dev libminiupnpc8 libboost-all-dev

Downloading Source
------------------
1. Create directories and clone git repository:
    
      cd ~ && mkdir -p ~/cryptos && cd ~/cryptos && git clone https://github.com/techcoincommunity/techcoin

Compiling daemon (Techcoind) from source
----------------------------------------   
1. Compile:

      cd ~/cryptos/techcoin/src && mkdir obj && make -f makefile.unix

2. Strip debug symbols (optional but recommended: reduces binary size):

      strip Techcoind
      
3. Allow daemon to be accessed from any path (optional: allows to use Techcoind <command> instead of using full path):
    
      sudo mv Techcoind /usr/local/bin

Compiling TechCoin-Qt from source
---------------------------------
1. Compile:

      cd ~/cryptos/techcoin && qmake techcoin-qt-linux.pro && make

2. Strip debug symbols (optional but recommended: reduces binary size):

      strip techcoin-qt
      
Updating
--------
1. Pull fresh code from git:

      cd ~/cryptos/techcoin && git pull
      
2. Repeat procedure for daemin or Qt (all steps)

Dependency Build Instructions: Fedora
-------------------------------------

Tested on Fedora 20:

	sudo yum install autoconf automake make gcc-c++
	sudo yum install openssl-devel
	sudo yum install miniupnpc-devel
	sudo yum install boost-devel
	sudo yum install libdb-cxx-devel
	sudo yum install libss-devel
	sudo yum install qrencode

Optional:

	sudo yum install miniupnpc-devel (see USE_UPNP compile flag)

