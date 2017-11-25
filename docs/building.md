Building MongoDB
================

To build MongoDB, you will need:

* A modern C++ compiler. One of the following is required.
    * GCC 5.3.0 or newer
    * Clang 3.4 (or Apple XCode 5.1.1 Clang) or newer
    * Visual Studio 2013 Update 2 or newer
* Python 2.7
* SCons 2.3

for the target x86, or x86-64 platform. More detailed platform instructions can be found below.

MongoDB Tools
--------------

The MongoDB command line tools (mongodump, mongorestore, mongoimport, mongoexport, etc)
have been rewritten in [Go](http://golang.org/) and are no longer included in this repository.

The source for the tools is now available at [mongodb/mongo-tools](https://github.com/mongodb/mongo-tools).

SCons
---------------

For detail information about building, please see [the build manual](http://www.mongodb.org/about/contributors/tutorial/build-mongodb-from-source/)

If you want to build everything (mongod, mongo, tests, etc):

    $ scons all

If you only want to build the database:

    $ scons

To install

    $ scons --prefix=/opt/mongo install

Please note that prebuilt binaries are available on [mongodb.org](http://www.mongodb.org/downloads) and may be the easiest way to get started.

SCons Targets
--------------

* mongod
* mongos
* mongo
* core (includes mongod, mongos, mongo)
* all

Windows
--------------

See [the windows build manual](http://www.mongodb.org/about/contributors/tutorial/build-mongodb-from-source/#windows-specific-instructions)

Build requirements:
* Visual Studio 2013 Update 2 or newer
* Python 2.7, ActiveState ActivePython 2.7.x Community Edition for Windows is recommended
* SCons

Or download a prebuilt binary for Windows at www.mongodb.org.

Debian/Ubuntu
--------------

NOTES:
* Building requires at least 2GB RAM and 8GB spare disk space.
* If GCC 5.3 is not in the stable release of your distribution, you will need to install unstable packages.
	In this case you will end up with Scons 3+, Python 3+ and GCC 7+ neither of which is supported.
	So make sure that your "alternatives" are pointing to GCC 5.3, Scons 2.3 and Python 2.7.
* The output executable will include debug symbols. Run the 'strip' command on the executables to significantly reduce the file size.


To install dependencies on Debian or Ubuntu systems:

    # aptitude install scons build-essential
    # aptitude install libboost-filesystem-dev libboost-program-options-dev libboost-system-dev libboost-thread-dev libssl-dev devscripts

To run tests as well, you will need PyMongo:

    # aptitude install python-pymongo

Then build as usual with `scons`:

    $ scons all
	or
	$ scons core -j 3 --ssl --link-model=object --opt=on --dbg=off --disable-warnings-as-errors --disable-minimum-compiler-version-enforcement CC=/usr/bin/clang CXX=/usr/bin/clang++

OS X
--------------

Using [Homebrew](http://brew.sh):

    $ brew install mongodb

Using [MacPorts](http://www.macports.org):

    $ sudo port install mongodb

FreeBSD
--------------

Install the following ports:

  * devel/libexecinfo
  * devel/scons
  * lang/gcc
  * lang/python

Optional Components if you want to use system libraries instead of the libraries included with MongoDB

  * archivers/snappy
  * lang/v8
  * devel/boost
  * devel/pcre

OpenBSD
--------------
Install the following ports:

  * devel/libexecinfo
  * devel/scons
  * lang/gcc
  * lang/python

Special Build Notes
--------------
  * [open solaris on ec2](building.opensolaris.ec2.md)

