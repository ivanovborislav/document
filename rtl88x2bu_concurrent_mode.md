##### [Realtek WiFi concurrent mode Introduction](https://github.com/ivanovborislav/document/blob/main/Realtek_WiFi_concurrent_mode_Introduction.pdf)

-----

## HOW TO

### Install

Download source:

```
git clone https://github.com/ivanovborislav/rtl88x2bu.git
cd rtl88x2bu
```

Download patch:

```
wget https://raw.githubusercontent.com/ivanovborislav/document/main/patch/rtl88x2BU_v5.13.1_concurrent_mode+virtual_interface_control.patch
```

Patch:

```
patch -p1 < rtl88x2BU_v5.13.1_concurrent_mode+virtual_interface_control.patch
```

Compile:

```
make
sudo make install
```

### Driver options

Driver virtual interface control, rtw_virtual_iface_num=
```
0:Disable (default)
1:Enable
```

-----
