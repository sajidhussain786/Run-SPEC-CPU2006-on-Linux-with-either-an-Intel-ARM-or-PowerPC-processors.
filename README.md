Building and running SPEC CPU2006 on Linux
==========================================

This script is to automate building and running SPEC CPU2006 on Linux with either an Intel or ARM processor using gcc, g++, and gfortran.


Contents:
---------

+ [Structure](#structure)
+ [Usage](#useage)
+ [Troubleshooting](#troubleshooting)
+ [Optimizing GCC Process](#process-for-optimizing-gcc)


Structure:
----------

The assumed file structure is as follows:

```
/
├── arm/
│   ├── specsum_gnulib/
|   |   └── stdio.in.h
│   ├── specsum_win32/
|   |   └── stdio.h
│   ├── tar_gnu/
|   |   ├── stdio.h
|   |   └── stdio.in.h
│   ├── tar_mingw/
|   |   └── stdio.h
│   ├── makedepend.SH
│   ├── README.md
│   ├── README.txt
│   ├── setup.sh
│   └── unix.c
├── config/
│   ├── linux64-armv7-gcc.cfg
│   ├── linux64-c2750-gcc.cfg
│   ├── linux64-e5_1650-gcc.cfg
│   ├── lnx-arm-gcc.cfg
│   ├── lnx-i686-gcc.cfg
│   └── lnx-x86_64-gcc.cfg
├── SPECCPU.tar
│   ├── cpu2006-1.2.tar.xz
│   └── whatever custom binaries
└── benchmarking.sh
```

Usage:
------

Change to directory where files are, then start benchmarking by issuing the following 
command:

```bash
./benchmarking.sh
```


Workflow:
---------

1. CPU detection
2. Distribution detection
3. Using CPU and distribution detection, select config file
4. Install CPU2006, if needed
5. RUNSPEC using config file for GCC
6. Consolidate scores into simple sysout


Troubleshooting:
================

If you are getting a `Permission denied` response, make sure you're running as root. 
If you are still getting the message, try using the following command:

```bash
chmod +x benchmarking.sh
```


Process for optimizing GCC:
===========================

1. Get GCC capable flags: `gcc -march=native -Q --help=target` or `echo "int main {return 0;}" | gcc [OPTIONS] -x c -v -Q -`

2. For Intel processors, go to [MARK](http://mark.intel.com/) to get CPU information and fill in hw_* information. Else, search for the hardware information on the Web.

3. Check [SPEC CPU2006](http://www.spec.org/cgi-bin/osgresults?conf=rint2006) for submitted results.

4. Trial and error.
