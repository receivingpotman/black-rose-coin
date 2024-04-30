# BlackRoseCoin Project

Copyright (c) 2018-2019, BlackRoseCoin Project

Copyright (c) 2018-2019, The Geem developers

Copyright (c) 2016-2019 The Karbowanec developers

Copyright (c) 2018-2019, The Arqma Network

Copyright (c) 2018, The CryoNote Developers

Copyright (c) 2014-2018, The Monero Project

Copyright (c) 2011-2016 The Cryptonote developers
## Development Resources

- Web: [https://www.blackrosenetwork.space](https://www.blackrosenetwork.space)
- Mail: [blackrosecoin@tutanota.com](blackrosecoin@tutanota.com)
- Repo: [https://github.com/Camellia73/BlackRoseCoin.git](https://github.com/Camellia73/BlackRoseCoin.git)

## Coin Supply & Emission

- **Total supply**: **100,000,000** coins.
- **Premine**: **50%** for SWAP(13 000 000 old BR1 + 37 000 000 KSN).
- **Coin symbol**: **BR1**
- **Coin Units**:
  + 1 Nano-BlackRoseCoin &nbsp;= 0.000000001 **BR1** (10<sup>-9</sup> - _the smallest coin unit_)
  + 1 Micro-BlackRoseCoin = 0.000001 **BR1** (10<sup>-6</sup>)
  + 1 Mili-BlackRoseCoin = 0.001 **BR1** (10<sup>-3</sup>)
  + 1 BlackRoseCoin = 1 **BR1**
- **Hash algorithm**: CryptoNight (CN-Dark - Proof-Of-Work)
- **Emission scheme**: BlackRoseCoin's block reward uses "Linear Emission". Block reward will decrease over time.

## About this Project

This is the core implementation of BlackRoseCoin. It is open source and completely free to use without restrictions, except for those specified in the license agreement below. There are no restrictions on anyone creating an alternative implementation of BlackRoseCoin that uses the protocol and network in a compatible manner.

As with many development projects, the repository on Github is considered to be the "staging" area for the latest changes. Before changes are merged into that branch on the main repository, they are tested by individual developers in their own branches, submitted as a pull request, and then subsequently tested by contributors who focus on testing and code reviews. That having been said, the repository should be carefully considered before using it in a production environment, unless there is a patch in the repository for a particular show-stopping issue you are experiencing. It is generally a better idea to use a tagged release for stability.

**Anyone is welcome to contribute to BlackRoseCoin's codebase!** If you have a fix or code change, feel free to submit is as a pull request directly to the "master" branch. In cases where the change is relatively small or does not affect other parts of the codebase it may be merged in immediately by any one of the collaborators. On the other hand, if the change is particularly large or complex, it is expected that it will be discussed at length either well in advance of the pull request being submitted, or even directly on the pull request.

## License

Please view [LICENSE](LICENSE)

[![License](https://img.shields.io/github/license/Camellia73/BlackRoseCoin)](https://opensource.org/licenses/BSD-3-Clause)

## Compiling BlackRoseCoin from Source

### Dependencies

The following table summarizes the tools and libraries required to build.  A
few of the libraries are also included in this repository (marked as
"Vendored"). By default, the build uses the library installed on the system,
and ignores the vendored sources. However, if no library is found installed on
the system, then the vendored source will be built and used. The vendored
sources are also used for statically-linked builds because distribution
packages often include only shared library binaries (`.so`) but not static
library archives (`.a`).

| Dep            | Min. Version  | Vendored | Debian/Ubuntu Pkg  | Arch Pkg       | Optional | Purpose        |
| -------------- | ------------- | ---------| ------------------ | -------------- | -------- | -------------- |
| GCC            | 4.7.3         | NO       | `build-essential`  | `base-devel`   | NO       |                |
| CMake          | 3.0.0         | NO       | `cmake`            | `cmake`        | NO       |                |
| pkg-config     | any           | NO       | `pkg-config`       | `base-devel`   | NO       |                |
| Boost          | 1.58          | NO       | `libboost-all-dev` | `boost`        | NO       |                |
| OpenSSL      	 | basically any | NO       | `libssl-dev`       | `openssl`      | NO       | sha256 sum     |
| libminiupnpc   | 2.0           | YES      | `libminiupnpc-dev` | `miniupnpc`    | YES      | NAT punching   |
| GTest          | 1.5           | YES      | `libgtest-dev`^    | `gtest`        | YES      | test suite     |
| Doxygen        | any           | NO       | `doxygen`          | `doxygen`      | YES      | documentation  |
| Graphviz       | any           | NO       | `graphviz`         | `graphviz`     | YES      | documentation  |

[^] On Debian/Ubuntu `libgtest-dev` only includes sources and headers. You must
build the library binary manually. This can be done with the following command ```sudo apt-get install libgtest-dev && cd /usr/src/gtest && sudo cmake . && sudo make && sudo mv libg* /usr/lib/ ```

### Build instructions

BlackRoseCoin uses the CMake build system and a top-level [Makefile](Makefile) that
invokes cmake commands as needed.

#### On Linux and OS X

* Install the dependencies (see the list above)

    \- On Ubuntu 16.04, essential dependencies can be installed with the following command:

    	sudo apt install build-essential cmake libboost-all-dev libssl-dev pkg-config
    
* Change to the root of the source code directory and build:

        cd BlackRoseCoin
        make

    *Optional*: If your machine has several cores and enough memory, enable
    parallel build by running `make -j<number of threads>` instead of `make`. For
    this to be worthwhile, the machine should have one core and about 2GB of RAM
    available per thread.

* The resulting executables can be found in `build/release/src`

* **Optional**: to build binaries suitable for debugging:

         make debug

#### On the Raspberry Pi

Tested on a Raspberry Pi 2 with a clean install of minimal Debian Jessie from https://www.raspberrypi.org/downloads/raspbian/

* `apt-get update && apt-get upgrade` to install all of the latest software

* Install the dependencies for BlackRoseCoin except libunwind and libboost-all-dev

* Increase the system swap size:
```	
	sudo /etc/init.d/dphys-swapfile stop  
	sudo nano /etc/dphys-swapfile  
	CONF_SWAPSIZE=1024  
	sudo /etc/init.d/dphys-swapfile start  
```
* Install the latest version of boost (this may first require invoking `apt-get remove --purge libboost*` to remove a previous version if you're not using a clean install):
```
	cd  
	wget https://sourceforge.net/projects/boost/files/boost/1.62.0/boost_1_62_0.tar.bz2  
	tar xvfo boost_1_62_0.tar.bz2  
	cd boost_1_62_0  
	./bootstrap.sh  
	sudo ./b2  
```
* Wait ~8 hours

	sudo ./bjam install

* Wait ~4 hours

* Change to the root of the source code directory and build:

        cd blackrosecoin
        make

* Wait ~4 hours

* The resulting executables can be found in `build/release/src`

* You may wish to reduce the size of the swap file after the build has finished, and delete the boost directory from your home directory

#### On Windows:

Binaries for Windows are built on Windows using the MinGW toolchain within
[MSYS2 environment](http://msys2.github.io). The MSYS2 environment emulates a
POSIX system. The toolchain runs within the environment and *cross-compiles*
binaries that can run outside of the environment as a regular Windows
application.

**Preparing the Build Environment**

* Download and install Visual Studio 2015 or Visual Studio 2017.
* Use the Visual Studio installation wizard to install all the necessary tools.
* Download and install Cmake GUI
* Download and install [Boost libraries] (https://sourceforge.net/projects/boost/files/boost-binaries/1.69.0/) for your version of Visual Studio.
* Open Cmake and select the source folder
* Click the "configure" button. Select your version of Visual Studio and "x64" in the box below. After that, click "Finish".
* Wait for the process to finish and click "Generate".
* Click on "Open project".
* Change the configuration from "Debug" to "Release".
* Open the "Build" menu and select "Build solution".
* Wait for the process to finish and open the resulting exe in build/src/Release

### On FreeBSD:

* Update packages and install the dependencies (on FreeBSD 11.0 x64):
		
		pkg update; pkg install wget git pkgconf gcc49 cmake db6 icu libevent unbound googletest ldns expat bison boost-libs;

* Clone source code, change to the root of the source code directory and build:

        git clone https://github.com/Camellia73/BlackRoseCoin.git; cd BlackRoseCoin; make;
		
		