# apm disco manifest - workspace for building ArduPlane for Parrot Disco / C.H.U.C.K.

## Overview

[ArduPlane](http://ardupilot.org/plane/index.html) is an open source
autopilot. [Disco] is a consumer flying wing from Parrot and C.H.U.C.K. is it's
autopilot board.  
Although C.H.U.C.K. comes with it's own proprietary autopilot / software stack,
it is possible to use it with ArduPilot for a different flight experience or for
hacking.  
This README file explains how to prepare a workspace to build APM and other
handy software for C.H.U.C.K. and how to install it / update it.

**WARNING: The instructions described in this document are for advanced users
only.** They can lead to malfunction, crashes or a wide variety of problems and
a proficiency in working with embedded linux is recommended.

**Note: These instructions are for firmwares versions 1.1.0 and above.**
Versions 1.0.X can still use ArduPlane but it involves modifying the original
filesystem which can lead to problems **not recoverable with a reset factory**.
Upgrading to an 1.1.X+ firmware is strongly encouraged.

The Parrot company cannot be held responsible for any problem that following
these instructions can lead to.

This document is in markdown format and is best read with a markdown viewer. In
command line, one can use `pandoc README.md | lynx -stdin`.

## How to start / restart ArduPlane for Parrot Disco

Just press three times on the on/off button, the original autopilot will be
killed and ArduPlane will be launched instead.
If ArduPlane was already running, it will be restarted.
Now you can interact with ArduPlane the way you want, please refer to the
[ArduPlane documentation][ArduPlane] for more information.

## How to build ArduPlane for Parrot Disco (optional)

### Needed packages

For debian-based distributions (tested on debian 8):

        $ wget -c https://github.com/Parrot-Developers/toolchains/raw/master/parrot-tools-linuxgnutools-2016.02-linaro_1.0.0-2_amd64.deb
        # dpkg -i parrot-tools-linuxgnutools-2016.02-linaro_1.0.0-2_amd64.deb
        # apt-get install -f # if unmet dependencies are reported
        # apt-get install build-essential git curl pkg-config python3 autoconf

### The *arduplane disco* workspace uses google repo and parrot alchemy

        $ mkdir -p ~/bin
        $ export PATH=~/bin:$PATH
        $ curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
        $ chmod a+x ~/bin/repo

### Create an ArduPlane Disco workspace

        $ mkdir disco_arduplane
        $ cd disco_arduplane

        $ repo init -u https://github.com/Parrot-Developers/arduplane-disco-manifest.git
	or for a specific release,
       	$ repo init -u https://github.com/Parrot-Developers/arduplane-disco-manifest.git -m releases/1.1.0.xml

        $ repo sync
        $ ./build.sh all final -j5

## How to download the latest version of ArduPlane

The latest stable version can be downloaded from the ardupilot [website][Firmware]. Just download the file named *arduplane*.

## How to push an updated version of ArduPlane on a Disco

### Old Disco firmware ###

These instructions are for old version of Disco firmware.

First connect to the drone's wifi network, it's name as the form DISCO-XXXXXX.
It will give you an address on the 192.168.42.0/24 network, the address of the
drone is 192.168.42.1.

Then connect to the drone's ftp server, create the internal\_000/APM directory
and copy/paste the apm-plane-disco binary there. You will find in in
*Alchemy-out/linux-parrot-arm/final/usr/bin/apm-plane-disco*.

For users under Linux (or with an available ftp command), it's possible to
send apm-plane-disco in the right place by executing:

        $ ./update.sh

An error regarding the APM directory creation is normal and can be safely
ignored.

### Recent firmware ###

First connect to the drone's wifi network, named DISCO-XXXXXX. It will give you an address on the 192.168.42.0/24 network, the address of the drone is 192.168.42.1. Then connect to the drone's ftp server and upload the file arduplane into the folder internal\_000/ardupilot/.

## Troubleshooting

### wget-ing the toolchains fails with a security warning

        # apt-get install ca-certificates

[Disco]:https://www.parrot.com/fr/drones/parrot-disco-fpv#-parrot-disco-fpv
[ADB]:https://developer.android.com/studio/command-line/adb.html
[ArduPlane]:http://ardupilot.org/plane/
[Firmware]:http://firmware.ardupilot.org/Plane/stable/disco/