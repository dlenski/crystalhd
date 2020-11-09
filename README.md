# Crystal HD Hardware Decoder Driver
## Broadcom BCM70012 & BCM70015

**1. Install required files**

    sudo apt-get update
    sudo apt-get install linux-headers-`uname -r` git autoconf build-essential subversion dpkg-dev fakeroot pbuilder build-essential dh-make debhelper devscripts patchutils quilt git-buildpackage pristine-tar git yasm zlib1g-dev minizip libzip-dev libx11-dev libxv-dev vstream-client-dev libgtk2.0-dev libpulse-dev libxxf86dga-dev x11proto-xf86dga-dev git automake libtool libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev python-appindicator

**2. Ge the source**

Get the driver source code from the git repository.

    git clone https://github.com/spear1403/crystalhd.git

_The original repo source is available at git://git.linuxtv.org/jarod/crystalhd.git_

**3. Compile driver, install libraries, and load driver**

Use make command to compile driver. If you have multiple core processor then use the “-j2″ or “-j4″ option (2 or 4 is the number of cores). This will speed up the make process.

    cd crystalhd/driver/linux
    autoconf
    ./configure
    make -j2
    sudo make install

**4. Install the libraries.**

    cd ../../linux_lib/libcrystalhd/
    make -j2
    sudo make install

**5. Load the driver.**

    sudo modprobe crystalhd

**6. Reboot your system** , then check if 'crystalhd' is listed in the output of the following commands.

    lsmod
    dmesg | grep crystalhd

 Then you should see something like this:

    [  886.604511] Loading crystalhd v3.10.0
    [  886.604588] crystalhd 0000:03:00.0: Starting Device:0x1615

 Then let's try VLC with its `crystalhd` codec:

    vlc --codec=crystalhd video_1080p.mkv


 If it's able to use the CrystalHD module properly, you should see these additional messages in the `dmesg` log:

    [ 1234.123456] crystalhd 0000:03:00.0: Opening new user[0] handle
    [ 5678.308567] crystalhd 0000:03:00.0: Closing user[0] handle via ioctl with mode 10200

## History

See [HISTORY.md](HISTORY.md) for a rough history of the various versions of this driver floating around the web.
