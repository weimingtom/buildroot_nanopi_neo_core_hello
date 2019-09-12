# buildroot_nanopi_neo_core_hello
Buildroot for NanoPi NEO Core hello project

## How to Build  
* For buildroot-2019.02.3 
$ sudo apt-get update  
$ sudo apt-get install g++ git  
$ cd buildroot-2019.02.3    
$ make help  
$ make list-defconfigs    
$ make nanopi_neo_defconfig  
$ make menuconfig  
(Toolchain->Enable C++)  
$ make  
(get sdcard.img under output/image/)  
(put hellocpp and helloworld to package/)  
(modify package/Config.in)  
...  
menu "Miscellaneous"  
...  
+	source "package/helloworld/Config.in"  
+	source "package/hellocpp/Config.in"  
$ make menuconfig  
(Enable Package->Misc->helloworld, hellocpp)  
$ make
(After modify hellocpp source)  
$ make hellocpp-dirclean && make  
