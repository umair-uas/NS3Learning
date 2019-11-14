## ns3 Installation 

### installation platform 
ns3 is installed on **Ubuntu 16.04** 

## Prerequisites for ns3 installation

On Ubuntu 16.04 gcc and g++ are already installed ,we can check the version 
```sh 
umair@umair-VM:~/work/ns3module$ g++ --version 
g++ (Ubuntu 5.4.0-6ubuntu1~16.04.9) 5.4.0 20160609

## Cloning the ns3 repo 
```sh 
umair@umair-VM:~/work/ns3module$ hg clone http://code.nsnam.org/ns-3-allinone
destination directory: ns-3-allinone
requesting all changes
adding changesets
adding manifests
adding file changes
added 61 changesets with 94 changes to 7 files
updating to branch default
7 files updated, 0 files merged, 0 files removed, 0 files unresolved
```
Once we have cloned it we change to [+ns-3-allinone+] destinition directory  and list the contents there.
```sh 
umair@umair-VM:~/work/ns3module$ cd ns-3-allinone/
umair@umair-VM:~/work/ns3module/ns-3-allinone$ la
total 48K
-rwxrwxr-x 1 umair umair 5,9K Jun 27 09:26 build.py
-rw-rw-r-- 1 umair umair  575 Jun 27 09:26 constants.py
-rwxrwxr-x 1 umair umair 6,5K Jun 27 09:26 dist.py
-rwxrwxr-x 1 umair umair 8,3K Jun 27 09:26 download.py
drwxrwxr-x 4 umair umair 4,0K Jun 27 09:26 .hg
-rw-rw-r-- 1 umair umair   71 Jun 27 09:26 .hgignore
-rw-rw-r-- 1 umair umair  924 Jun 27 09:26 README
-rw-rw-r-- 1 umair umair  561 Jun 27 09:26 util.py
```
Now we can build the ns3 version of our choice with the help of **download.py** and  **build.py** python scripts.Here we selected ns-3.28.

```sh 
umair@umair-VM:~/work/ns3module/ns-3-allinone$ ./download.py -n ns-3.28

    #
    # Get NS-3
    #
    
Cloning ns-3 branch
 =>  hg clone http://code.nsnam.org/ns-3.28 ns-3.28
requesting all changes
adding changesets
adding manifests
adding file changes                                                                                                                                             
added 13427 changesets with 64396 changes to 7880 files                                                                                                         
updating to branch default
3362 files updated, 0 files merged, 0 files removed, 0 files unresolved

    #
    # Get PyBindGen
    #
    
Required pybindgen version:  0.17.0.post58+ngcf00cc0
Trying to fetch pybindgen; this will fail if no network connection is available.  Hit Ctrl-C to skip.
 =>  git clone https://github.com/gjcarneiro/pybindgen.git pybindgen
Cloning into 'pybindgen'...
remote: Counting objects: 5985, done.
remote: Compressing objects: 100% (10/10), done.
remote: Total 5985 (delta 5), reused 6 (delta 3), pack-reused 5972
Receiving objects: 100% (5985/5985), 10.97 MiB | 4.19 MiB/s, done.
Resolving deltas: 100% (4080/4080), done.
Checking connectivity... done.
Fetch was successful.
 =>  git checkout cf00cc0 -q
 =>  python setup.py clean
running clean

    #
    # Get NetAnim
    #
    
Required NetAnim version:  netanim-3.108
Retrieving NetAnim from http://code.nsnam.org/netanim
 =>  hg clone http://code.nsnam.org/netanim netanim
requesting all changes
adding changesets
adding manifests
adding file changes
added 305 changesets with 1609 changes to 228 files
updating to branch default
195 files updated, 0 files merged, 0 files removed, 0 files unresolved

    #
    # Get bake
    #
    
Retrieving bake from http://code.nsnam.org/bake
 =>  hg clone http://code.nsnam.org/bake
destination directory: bake
requesting all changes
adding changesets
adding manifests
adding file changes
added 402 changesets with 873 changes to 63 files
updating to branch default
45 files updated, 0 files merged, 0 files removed, 0 files unresolved
```

```
## building with python 
The first time ns3 project should be built using allinone environment.This will configure the project in the user friendly mode. We change into the `ns-3-allinone `parent directory of mercurial repo and run the following command:
```sh 
./build.py 
# Build NetAnim
Entering directory `netanim'
 =>  qmake -v
QMake version 3.0
Using Qt version 5.5.1 in /usr/lib/x86_64-linux-gnu
qmake found
 =>  qmake NetAnim.pro
 =>  make
g++ -c -m64 -pipe -O2 -Wall -W -D_REENTRANT -fPIC -DNS3_LOG_ENABLE -DQT_NO_DEBUG -DQT_PRINTSUPPORT_LIB -DQT_WIDGETS_LIB -DQT_GUI_LIB -DQT_CORE_LIB -I. -Iqtpropertybrowser/src -isystem /usr/include/x86_64-linux-gnu/qt5 -isystem /usr/include/x86_64-linux-gnu/qt5/QtPrintSupport -isystem /usr/include/x86_64-linux-gnu/qt5/QtWidgets -isystem /usr/include/x86_64-linux-gnu/qt5/QtGui -isystem /usr/include/x86_64-linux-gnu/qt5/QtCore -I. -I/usr/lib/x86_64-linux-gnu/qt5/mkspecs/linux-g++-64 -o main.o main.cpp
--------------
```
After a lot of console output one can see some useful details;
```sh 
# Build NS-3
Entering directory `./ns-3.28'
 =>  /usr/bin/python waf configure --with-pybindgen ../pybindgen
Setting top to                           : /home/umair/work/ns3module/ns-3-allinone/ns-3.28 
Setting out to                           : /home/umair/work/ns3module/ns-3-allinone/ns-3.28/build 
Checking for 'gcc' (C compiler)          : /usr/bin/gcc 
Checking for cc version                  : 5.4.0 
------------------
------------------
------------------
---- Summary of optional NS-3 features:
Build profile                 : debug
Build directory               : 
BRITE Integration             : not enabled (BRITE not enabled (see option --with-brite))
DES Metrics event collection  : not enabled (defaults to disabled)
Emulation FdNetDevice         : enabled
Examples                      : not enabled (defaults to disabled)
File descriptor NetDevice     : enabled
GNU Scientific Library (GSL)  : enabled
Gcrypt library                : enabled
GtkConfigStore                : enabled
MPI Support                   : not enabled (option --enable-mpi not selected)
NS-3 Click Integration        : not enabled (nsclick not enabled (see option --with-nsclick))
NS-3 OpenFlow Integration     : not enabled (OpenFlow not enabled (see option --with-openflow))
Network Simulation Cradle     : not enabled (NSC not found (see option --with-nsc))
PlanetLab FdNetDevice         : not enabled (PlanetLab operating system not detected (see option --force-planetlab))
PyViz visualizer              : enabled
Python API Scanning Support   : not enabled (Missing 'pygccxml' Python module)
Python Bindings               : enabled
Real Time Simulator           : enabled
SQlite stats data output      : enabled
Tap Bridge                    : enabled
Tap FdNetDevice               : enabled
Tests                         : not enabled (defaults to disabled)
Threading Primitives          : enabled
Use sudo to set suid bit      : not enabled (option --enable-sudo not selected)
```
At the end of build process you can see the summmary ns3 modules build 
```sh 
Waf: Leaving directory `/home/umair/work/ns3module/ns-3-allinone/ns-3.28/build'
Build commands will be stored in build/compile_commands.json
'build' finished successfully (4m55.858s)

Modules built:
antenna                   aodv                      applications              
bridge                    buildings                 config-store              
core                      csma                      csma-layout               
dsdv                      dsr                       energy                    
fd-net-device             flow-monitor              internet                  
internet-apps             lr-wpan                   lte                       
mesh                      mobility                  mpi                       
netanim (no Python)       network                   nix-vector-routing        
olsr                      point-to-point            point-to-point-layout     
propagation               sixlowpan                 spectrum                  
stats                     tap-bridge                test (no Python)          
topology-read             traffic-control           uan                       
virtual-net-device        visualizer                wave                      
wifi                      wimax                     

Modules not built (see ns-3 tutorial for explanation):
brite                     click                     openflow                  

Leaving directory `./ns-3.28'
```
:heavy_exclamation_mark: Important 
Once the ns3 has been build ,we usually not use ns3-allinone scripts anymore.We interact with `waf` scripts and we run it under [+ns-3.28+] directory rather than [+ns-3-allinone+] directory.

## Configuring with Waf

we change into [+ns-3.28+] directory from where we can run the build with **./waf**.
we run  [+waf+] with the following options,the available options can be seen with `./waf --help`.
```sh 
mair@umair-VM:~/work/ns3module/ns-3-allinone/ns-3.28$ ./waf -d debug -j4  --enable-tests --enable-examples configure
Setting top to                           : /home/umair/work/ns3module/ns-3-allinone/ns-3.28 
Setting out to                           : /home/umair/work/ns3module/ns-3-allinone/ns-3.28/build 
Checking for 'gcc' (C compiler)          : /usr/bin/gcc 
Checking for cc version                  : 5.4.0 
Checking for 'g++' (C++ compiler)        : /usr/bin/g++ 
Checking for compilation flag -Wl,--soname=foo support : ok 
Checking for compilation flag -std=c++11 support       : ok 
Checking for program 'python'                          : /usr/bin/python 
Checking for python version                            : (2, 7, 12, 'final', 0) 
=================
--- Summary of optional NS-3 features:
Build profile                 : debug
Build directory               : 
BRITE Integration             : not enabled (BRITE not enabled (see option --with-brite))
DES Metrics event collection  : not enabled (defaults to disabled)
Emulation FdNetDevice         : enabled
Examples                      : enabled
File descriptor NetDevice     : enabled
GNU Scientific Library (GSL)  : enabled
Gcrypt library                : enabled
GtkConfigStore                : enabled
MPI Support                   : not enabled (option --enable-mpi not selected)
NS-3 Click Integration        : not enabled (nsclick not enabled (see option --with-nsclick))
NS-3 OpenFlow Integration     : not enabled (OpenFlow not enabled (see option --with-openflow))
Network Simulation Cradle     : not enabled (NSC not found (see option --with-nsc))
PlanetLab FdNetDevice         : not enabled (PlanetLab operating system not detected (see option --force-planetlab))
PyViz visualizer              : enabled
Python API Scanning Support   : not enabled (Missing 'pygccxml' Python module)
Python Bindings               : enabled
Real Time Simulator           : enabled
SQlite stats data output      : enabled
Tap Bridge                    : enabled
Tap FdNetDevice               : enabled
Tests                         : enabled
Threading Primitives          : enabled
Use sudo to set suid bit      : not enabled (option --enable-sudo not selected)
XmlIo                         : enabled
'configure' finished successfully (3.380s)
================
```

## Running Tests 
ns3 unit tests can be run by executing ./test.py 
```sh 
umair@umair-VM:~/work/ns3module/ns-3-allinone/ns-3.28$ ./test.py 
Waf: Entering directory `/home/umair/work/ns3module/ns-3-allinone/ns-3.28/build'
[   6/2742] Processing command (${PYTHON}): ../bindings/python/ns3modulegen-modular.py ../src/antenna/bindings/modulegen__gcc_LP64.py -> src/antenna/bindings/ns3module.cc src/antenna/bindings/ns3module.h src/antenna/bindings/ns3modulegen.log

===============
```
:mag: We will see the list of modules built successfully and ones which are not. 
```sh 
Build commands will be stored in build/compile_commands.json
'build' finished successfully (5m29.192s)

Modules built:
antenna                   aodv                      applications              
bridge                    buildings                 config-store              
core                      csma                      csma-layout               
dsdv                      dsr                       energy                    
fd-net-device             flow-monitor              internet                  
internet-apps             lr-wpan                   lte                       
mesh                      mobility                  mpi                       
netanim (no Python)       network                   nix-vector-routing        
olsr                      point-to-point            point-to-point-layout     
propagation               sixlowpan                 spectrum                  
stats                     tap-bridge                test (no Python)          
topology-read             traffic-control           uan                       
virtual-net-device        visualizer                wave                      
wifi                      wimax                     

Modules not built (see ns-3 tutorial for explanation):
brite                     click                     openflow  ```
 
Running tests might take a while ,the following output is given at the end 

```sh 
PASS: Example examples/wireless/mixed-wired-wireless.py
PASS: Example examples/tutorial/first.py
PASS: Example src/bridge/examples/csma-bridge.py
PASS: Example src/core/examples/sample-simulator.py
PASS: Example examples/wireless/wifi-ap.py
PASS: Example src/flow-monitor/examples/wifi-olsr-flowmon.py
PASS: Example src/wifi/examples/wifi-manager-example --wifiManager=Ideal --standard=802.11ax-5GHz --serverChannelWidth=160 --clientChannelWidth=160 --serverShortGuardInterval=1600 --clientShortGuardInterval=1600 --serverNss=4 --clientNss=4 --stepTime=0.1
PASS: Example src/wifi/examples/wifi-manager-example --wifiManager=Ideal --standard=802.11ax-5GHz --serverChannelWidth=160 --clientChannelWidth=160 --serverShortGuardInterval=3200 --clientShortGuardInterval=3200 --serverNss=4 --clientNss=4 --stepTime=0.1
587 of 590 tests passed (587 passed, 3 skipped, 0 failed, 0 crashed, 0 valgrind errors)
List of SKIPped tests:
    ns3-tcp-cwnd
    ns3-tcp-interoperability
    nsc-tcp-loss
umair@umair-VM:~/work/ns3module/ns-3-allinone/ns-3.28$ 
```
:white_check_mark: This completes the installation of ns3 .

References:

. [https://www.nsnam.org/docs/manual/html/new-modules.html](https://www.nsnam.org/docs/manual/html/new-modules.html) 

. [ns3 Installation](https://www.nsnam.org/wiki/Installation#Installation)

  Link to this repository  on **GitHub** [https://github.com/umairahmedshah/NS3Learning.git]    (https://github.com/umairahmedshah/NS3Learning.git)
