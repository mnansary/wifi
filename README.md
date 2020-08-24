
# DD-WRT NOTES

```c
    Version: 0.0.1   
    Author : Md. Nazmuddoha Ansary
```



**ENVIRONMENT**  

```c
OS          : Ubuntu 18.04.3 LTS (64-bit) Bionic Beaver        
Memory      : 7.7 GiB  
Processor   : Intel® Core™ i5-8250U CPU @ 1.60GHz × 8    
Graphics    : Intel® UHD Graphics 620 (Kabylake GT2)  
Gnome       : 3.28.2 
```

# Info
* **TP-LINK**: ```tl-wr841nd```
* **Requirements**: 
    * gcc 
    * g++ 
    * binutils 
    * patch 
    * bzip2 
    * flex 
    * bison 
    * make 
    * gettext 
    * unzip  
    * zlib1g-dev 
    * libc6 
    * subversion 
    * git

* From Website  : ```$ sudo apt install gcc g++ binutils patch bzip2 flex bison make gettext unzip  zlib1g-dev libc6 subversion git```
* From GitHub   : ```$ sudo apt install git build-essential zlib1g-dev liblzma-dev python-magic```

## DD-WRT- DEV:
For development of DD-WRT, we have two options:
* Use the Firmware Modification Kit. This kit gives the user the ability to make changes to a firmware image without recompiling the firmware sources. You need this option most of the time.
* Download DD-WRT source, make changes and compile it. This grants additional degree of freedom, but requires time, disk space and patience as it may not compile on first time

# Important links
* DD-Wrt Download:  ftp://ftp.dd-wrt.com/betas/

* [Firm-Wire-Mod-Kit](https://github.com/rampageX/firmware-mod-kit)

* [BitSum Forums](https://community.bitsum.com/forum/index.php/)

* [Open-Wrt Packages](https://openwrt.pkgs.org/19.07/openwrt-packages-x86_64/)

  


# Steps

### Extraction

* clone the repo:```git clone https://github.com/rampageX/firmware-mod-kit.git```

* Place Firmware file in the git repo (fw.bin)
* ``` $ ./extract-firmware.sh firmware.bin```
* Upon Success: files can be found at **/fmk/rootfs/** (change permissions if needed)

### Changing The firmware:
1. Adding Necessary files according to a general linux based distro

2. Creating Custom **.ipk** file 

3. Finding **.ipk** that suits our purpose

### Re-compile Firmware

1. Download the desired **.ipk**  
2. install    :```$./ipkg_install.sh path/to/package.ipk path/to/fmk/```
3. re-build :``` $ ./build-firmware.sh [-nopad] [-min]```

> The min option is to avoid errors (Size changes after recompilation)



### Success-Log:

- [x] Extraction

- [x] IPK install

- [x] Recompile

- [ ] Hard-wire upload 

  > Bricked  





# Local 

* **Modification Notes:** mod_notes.md
* **IPK Creation:** ipk_notes.md 










