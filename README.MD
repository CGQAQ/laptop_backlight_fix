# 1. 比较老的系统

对于比较老的系统，如我的CentOS 6.5，所有的显卡驱动配置都存在/etc/X11/xorg.conf这个文件中，文件分为不同的Section，分别定义不同的功能，亮度相关的功能在Device部分。

因此，在Section "Device"部分添加

```
Option    "RegistryDwords"    "EnableBrightnessControl=1"
Option    "NoLogo"    "True"
```

保存重启后，开机的nvidia图标就消失了，也可以用fn键调节亮度了。 

# 2. 比较新的系统

对于比较新的系统，如Linux Mint 17，不再存在/etc/X11/xorg.conf这个文件，显卡驱动配置在/usr/share/X11/xorg.conf.d/这个文件夹下，配置被分配在了不同的文件中，每个文件定义一部分的功能，自己也可以新建一个文件来定义一部分功能。

因此，新建一个配置文件

sudo vi /usr/share/X11/xorg.conf.d/10-nvidia.conf


```conf
Section "Device"
	Identifier "Device0"
	Driver "nvidia"
	VendorName "NVIDIA Corporation"
	Option "RegistryDwords" "EnableBrightnessControl=1"
	Option "NoLogo" "True"
EndSection
```

# CREDIT: https://blog.csdn.net/Lockvictor/article/details/49254485
