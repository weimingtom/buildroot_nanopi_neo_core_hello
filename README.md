# buildroot_nanopi_neo_core_hello
Buildroot for NanoPi NEO Core hello project

## How to Build  
* For buildroot-2019.02.3, Ubuntu 14.04 32bit     
$ sudo apt-get update  
$ sudo apt-get install g++ git libncurses5-dev    
$ cd buildroot-2019.02.3    
$ make help  
$ make list-defconfigs    
$ make nanopi_neo_defconfig  
$ make menuconfig  
(Enable Toolchain->Enable C++ support)  
$ make  
(Get sdcard.img under output/images/)  
(Put hellocpp and helloworld to package/)  
(Modify package/Config.in)  
...  
menu "Miscellaneous"  
...  
source "package/helloworld/Config.in"  
source "package/hellocpp/Config.in"  
$ make menuconfig  
(Enable Package->Misc->helloworld, hellocpp)  
$ make  
(After modify hellocpp source)  
$ make hellocpp-dirclean && make  
(Get new sdcard.img under output/image/)  
(Flash sdcard.img to tf card using Win32DiskImager, over)  

## Pinout, gpio readall  
```  
 +-----+-----+----------+------+---+-NanoPi-NEO-Core--+------+----------+-----+-----+
 | BCM | wPi |   Name   | Mode | V | Physical | V | Mode | Name     | wPi | BCM |
 +-----+-----+----------+------+---+----++----+---+------+----------+-----+-----+
 |     |     |     3.3v |      |   |  1 || 2  |   |      | 5v       |     |     |
 |  12 |   8 |  GPIOA12 |  OFF | 0 |  3 || 4  |   |      | 5v       |     |     |
 |  11 |   9 |  GPIOA11 |  OFF | 0 |  5 || 6  |   |      | 0v       |     |     |
 | 203 |   7 |  GPIOG11 |  OFF | 0 |  7 || 8  | 0 |  OFF | GPIOG6   | 15  | 198 |
 |     |     |       0v |      |   |  9 || 10 | 0 |  OFF | GPIOG7   | 16  | 199 |
 |   0 |   0 |   GPIOA0 |  OFF | 0 | 11 || 12 | 0 |  OFF | GPIOA6   | 1   | 6   |
 |   2 |   2 |   GPIOA2 |  OFF | 0 | 13 || 14 |   |      | 0v       |     |     |
 |   3 |   3 |   GPIOA3 |  OFF | 0 | 15 || 16 | 0 |  OFF | GPIOG8   | 4   | 200 |
 |     |     |     3.3v |      |   | 17 || 18 | 0 |  OFF | GPIOG9   | 5   | 201 |
 |  64 |  12 |   GPIOC0 |  OFF | 0 | 19 || 20 |   |      | 0v       |     |     |
 |  65 |  13 |   GPIOC1 |  OFF | 0 | 21 || 22 | 0 |  OFF | GPIOA1   | 6   | 1   |
 |  66 |  14 |   GPIOC2 |  OFF | 0 | 23 || 24 | 0 |  OFF | GPIOC3   | 10  | 67  |
 +-----+-----+----------+------+---+----++----+---+------+----------+-----+-----+
 | BCM | wPi |   Name   | Mode | V | Physical | V | Mode | Name     | wPi | BCM |
 +-----+-----+----------+------+---+-NanoPi-NEO-Core--+------+----------+-----+-----+

 +-----+-----+----------+---- NanoPi-NEO-Core USB/Audio ----+----------+-----+-----+
 | BCM | wPi |   Name   | Mode | V | Physical | V | Mode | Name     | wPi | BCM |
 +-----+-----+----------+------+---+----++----+---+------+----------+-----+-----+
 |     |     |       5v |      |   | 25 || 26 | 0 |  OFF | GPIOA15  | 22  | 15  |
 |     |     |     USB1 |      |   | 27 || 28 | 0 |  OFF | GPIOA16  | 23  | 16  |
 |     |     |     USB1 |      |   | 29 || 30 | 0 |  OFF | GPIOA14  | 21  | 14  |
 |     |     |     USB2 |      |   | 31 || 32 | 0 |  OFF | GPIOA13  | 20  | 13  |
 |     |     |     USB2 |      |   | 33 || 34 |   |      | Mic      |     |     |
 |     |     |       IR |      |   | 35 || 36 |   |      | Mic      |     |     |
 |  17 |  19 |  GPIOA17 |  OFF | 0 | 37 || 38 |   |      | Audio    |     |     |
 |     |     |      I2S |      |   | 39 || 40 |   |      | Audio    |     |     |
 |     |     |      I2S |      |   | 41 || 42 | 0 | ALT5 | GPIOA5   | 18  | 5   |
 |     |     |      I2S |      |   | 43 || 44 | 0 | ALT5 | GPIOA4   | 17  | 4   |
 |     |     |      I2S |      |   | 45 || 46 |   |      | 5V       |     |     |
 |     |     |       0v |      |   | 47 || 48 |   |      | 0v       |     |     |
 +-----+-----+----------+------+---+----++----+---+------+----------+-----+-----+
 | BCM | wPi |   Name   | Mode | V | Physical | V | Mode | Name     | wPi | BCM |
 +-----+-----+----------+------+---+-NanoPi-NEO-Core--+------+----------+-----+-----+

 +-----+-----+----------+---- NanoPi-NEO-Core Network ----+----------+-----+-----+
 | BCM | wPi |   Name   | Mode | V | Physical | V | Mode | Name     | wPi | BCM |
 +-----+-----+----------+------+---+----++----+---+------+----------+-----+-----+
 |     |     |      Eth |      |   | 49 || 50 |   |      | Eth      |     |     |
 |     |     |      Eth |      |   | 51 || 52 |   |      | Eth      |     |     |
 |     |     |      Eth |      |   | 53 || 54 |   |      | Eth      |     |     |
 |     |     |       NC |      |   | 55 || 56 |   |      | NC       |     |     |
 |     |     |       NC |      |   | 57 || 58 |   |      | NC       |     |     |
 |     |     |       0v |      |   | 59 || 60 |   |      | 0v       |     |     |
 |     |     |     USB3 |      |   | 61 || 62 | 0 |  OFF | GPIOA7   | 24  | 7   |
 |     |     |     USB3 |      |   | 63 || 64 |   |      | GPIOE12  |     |     |
 |     |     |       5v |      |   | 65 || 66 |   |      | GPIOE13  |     |     |
 |     |     |       5v |      |   | 67 || 68 |   |      | 3.3v     |     |     |
 +-----+-----+----------+------+---+----++----+---+------+----------+-----+-----+
 | BCM | wPi |   Name   | Mode | V | Physical | V | Mode | Name     | wPi | BCM |
 +-----+-----+----------+------+---+-NanoPi-NEO-Core--+------+----------+-----+-----+
```  
