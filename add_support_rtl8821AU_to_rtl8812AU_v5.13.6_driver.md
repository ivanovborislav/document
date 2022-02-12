-----

## HOW TO

### Install

Download source:

```
git clone https://github.com/ivanovborislav/rtl8812au.git
cd rtl8812au
```

Download patch:

```
wget https://raw.githubusercontent.com/ivanovborislav/document/main/patch/add_support_rtl8821AU_to_rtl8812AU_v5.13.6_driver.patch
```

Patch:

```
patch -p1 < add_support_rtl8821AU_to_rtl8812AU_v5.13.6_driver.patch
```

Compile:

```
make
sudo make install
```

-----
