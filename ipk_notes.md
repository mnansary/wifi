# **IPK Creation Kit**

###  **The structure of an IPK**

IPK files are **archives** containing the following:

- **data.tar.gz**: contains data.tar:

  - **data.tar**: These are the files that will be installed to, or removed from, the file system. They are in their correct locations in the directory tree starting at the root of the firmware file system. For example:

    - **./**usr/sbin/package

    - ./tmp/package_config

    - ./etc/package_config *-> symbolic link* -> ../tmp/config_folder

    - ./tmp/package_config/package.conf

      >  NOTE: *the "." directory must be included in the path names*

- **control.tar.gz** : contains control.tar:

  - **control.tar**: These are files which give information about the package. For examples, it's name, version, and dependencies.
    - ./control : describes the package
    - ./conffiles : indicates which files in the package are used for config files once installed

- **debian_binary** : the reason this exists is unknown. It's perhaps some platform or format indicator. It is a text file that consists of "2.0".

**Using the IPK template**

The IPK template directory contained in the Firmware Modification Kit makes it particularly easy to create IPK files without having to manually create them each time.

## **Creating your own IPK**

**Step 1**:Copy or extract the IPK template directory to a new directory named after the package you are creating an IPK for. 

>  If you are copying, use "cp -r" to copy the entire directory and all its contents.

**Step 2**:In the new directory edit the "*control*" and "*conffiles*" text files appropriately. The fields in "control" are probably self-explanatory:

***control:***

```python
Package: somepackage 

Priority: optional 

Depends: libpcap libncurses 

Section: net 

Description: A minimal and secure package of great sorts. 

Maintainer: Junior Jim-Bob <juniorjim.bob.com> 

Source: N/A 

Version: 2.61-1 

Architecture: mipsel  
```



>  If you want to get fancy, the *Source* field can indicate a URL to download the data.tar.gz portion of the package. If instead the package files are included inside the PKG, leave "N/A" in this field.



***conffiles:***"conffiles" contains a listing of files in the package that are used for configuration storage. This is helpful to preserve the configuration of the package if it is updated, or if the configuration otherwise needs preserving. It might look something like this after editing:

* /etc/package_config/package.conf 
* /etc/package_config/moreconfig.conf  

**Step 3**: Copy the package files into the folder in the same relative directories to which they will be installed to the file system. Symbolic links are allowed. For example:

```bash
./usr/sbin/mypackage 

./tmp/etc/package_config/ 

./etc/package_config/ ---(symbolic link)---> ../tmp/etc/package_config/ 

./tmp/etc/package_config/moreconfig.conf  
```

 The above makes the **/etc/package_config/** directory a symbolic link to **/tmp/package_config/**.

 This would be useful for firmwares that have a read-only /etc file system. On these systems, the configuration files could reside on a ram disk and be emitted at boot-time based on input from some other store of configuration variables, like NVRAM.

**Step 4:**Build the IPK. You're done, now simply build the IPK file with the script provided. 

It's parameters are:

MAKE_IPK.SH OUTPUT_PACKAGE_IPK IPK_BASE_DIRECTORY

***OUTPUT_PACKAGE_IPK*** : The IPK file to output. If it already exists it will be over-written.
***IPK_BASE_DIRECTORY*** : The directory you created in step 1 and have been working with up until now.

Example:

```c
$ make_ipk.sh package.ipk ../package_ipk_dir  
```