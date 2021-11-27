##### Samsung Galaxy S5

##### Versions: G900F (Europe)

##### Platform OS Android 6.0 (Marshmallow), TouchWiz UI

##### Kali NetHunter

##### Kernel Version

##### Linux version 3.4.0-nethunter-klte-eur-1.4

-----

### Compile the kernel

Download Kali NetHunter Kernel:

```
git clone https://github.com/jcadduono/nethunter_kernel_klte.git -b touchwiz-6.0
```

Download Cross compiler:

```
https://www.mediafire.com/file/9h19841nsm44z58/arm-cortex_a15-linux-gnueabihf-linaro_4.9.4-2015.06-build_2015_07_14.tar.xz/file
```

Edit:

`build.sh` (Ln54) - `TOOLCHAIN=/home/jc/build/toolchain/arm-cortex_a15-linux-gnueabihf-linaro_4.9.4-2015.06`.

`build.sh` (Ln69) - `VARIANT=eur` CAUTION: Edit line if needed.

`menuconfig.sh` (Ln8) - `TOOLCHAIN=$HOME/build/toolchain/arm-cortex_a15-linux-gnueabihf-linaro_4.9.4-2015.06`.

Run:

```
./menuconfig.sh
```

```
---Linux/arm 3.4.0 Kernel Configuration---

Enable loadable module support (y)
<Enter>
Forced module loading (y)
Module unloading (y)
Forced module unloading (y)
Module versioning support (y)
<Esc><Esc>
Device Drivers
<Enter>
Network device support
<Enter>
Wireless LAN
<Enter>
Realtek 8187 and 8187B USB support (M)
Atheros Wireless Cards (M)
<Enter>
Atheros 802.11n wireless cards support (M)
Atheros HTC based wireless cards support (M)
Linux Community AR9170 802.11n USB support (M)
Atheros mobile chipsets support (M)
Atheros ath6kl USB support (M)
<Esc><Esc>
Ralink driver support (M)
<Enter>
Ralink rt2500 (USB) support (M)
Ralink rt2501/rt73 (USB) support (M)
Ralink rt27xx/rt28xx/rt30xx (USB) support (M)
<Esc><Esc>
Realtek RTL8192CU/RTL8188CU USB Wireless Network Adapter (M)
ZyDAS ZD1211/ZD1211B USB-wireless support (M)
<Esc><Esc>
<Esc><Esc>
<Esc><Esc>
Save an Alternate Configuration File
<Enter>
<Tab>
< Ok >
<Enter>
<Tab>
< Exit >
<Enter>
Are you satisfied with these changes? Y/N: <y>
<Enter>
```

Run:

```
./build.sh
```

Now we have kernel zImage `/build/arch/arm/boot/zImage`, and we can load kernel module `insmod module_name.ko`.

### Compile the kernel module

Download:

```
git clone https://github.com/ivanovborislav/rtl8188eu.git
```

Edit:

`Makefile` (Ln143) - `CONFIG_PLATFORM_I386_PC = y` to `CONFIG_PLATFORM_I386_PC = n`

`Makefile` add line below (Ln143) - `CONFIG_PLATFORM_ANDROID_ARM = y`

`Makefile` add lines below (Ln1358) - 

```

ifeq ($(CONFIG_PLATFORM_ANDROID_ARM), y)
EXTRA_CFLAGS += -DCONFIG_LITTLE_ENDIAN
EXTRA_CFLAGS += -DCONFIG_IOCTL_CFG80211 -DRTW_USE_CFG80211_STA_EVENT
ARCH ?= arm
# edit line below
CROSS_COMPILE := /full/path/to/cross/compiler/arm-cortex_a15-linux-gnueabihf-linaro_4.9.4-2015.06/bin/arm-eabi-
# edit line below if needed, according to VARIANT= specified
KVER ?= 3.4.0-nethunter-klte-eur-1.4
# edit line below
KSRC := /full/path/to/folder/nethunter_kernel_klte/build
MODDESTDIR := /lib/modules/$(KVER)/kernel/drivers/net/wireless/
INSTALL_PREFIX :=
endif

```

Run:

```
make
```

Now we have kernel module `8188eu.ko`.

Make a folder and subfolder `/modules/3.4.0-nethunter-klte-eur-1.4` and copy `8188eu.ko` to `/modules/3.4.0-nethunter-klte-eur-1.4/`.

Drag and drop `zImage`, folder, subfolder and file(s) `/modules/3.4.0-nethunter-klte-eur-1.4/8188eu.ko` to `kernel-nethunter-klte-touchwiz-marshmallow-2017.11-18-1618.zip` (for example).

Now we have NetHunter image (zip file) with own kernel and kernel module(s).

-----
