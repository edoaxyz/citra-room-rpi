## citra-room-rpi

<b>Before running it</b>, since it was compiled using GCC 8.1.0,
it uses libraries of GCC 8.1.0 and not libraries of previous version of GCC
that are installed by default on Raspbian; you need to link those libraries
to the binary file, so:

```bash
LD_LIBRARY_PATH=~/citra-room-rpi/lib:$LD_LIBRARY_PATH # ~/citra-room-rpi/lib can be another folder but it must contain data included inside lib repo's folder
export LD_LIBRARY_PATH
```

Now you can run it.

### Building procedure
Following citra's wiki it needed:
 - sld2 (which can be installed with a simple ```apt install libsdl2-dev```)
 - qt (which can be installed with a simple ```apt install qtbase5-dev libqt5opengl5-dev qtmultimedia5-dev```)
 - GCC <b>7+</b> (since the version installed in Raspbian is 6.3.0 it needs to be compiled but fortunately [there's someone that has already done it](https://solarianprogrammer.com/2017/12/08/raspberry-pi-raspbian-install-gcc-compile-cpp-17-programs/))
 - cmake <b>3.8+</b> (this needs to be built)
 
 After you had cloned citra's source code and installed all these stuff you do ```mkdir build && cd build``` and next 
 ```cmake .. -DCMAKE_BUILD_TYPE=Release -DENABLE_QT=OFF -DENABLE_SDL2=OFF -DENABLE_CUBEB=OFF -DENABLE_ASM=OFF -DCRYPTOPP_DISABLE_AESNI=ON -DCRYPTOPP_DISABLE_ASM=ON -DCRYPTOPP_DISABLE_CXXFLAGS_OPTI=ON -DCRYPTOPP_DISABLE_SSSE3=ON```
 disabling useless stuff.<br>
 
 <b>NOTE:</b> if you used the previous guide for installing GCC 8 
 you need to provide to cmake the new path for it so the entire command will be 
 ```cmake .. -DCMAKE_C_COMPILER=/usr/local/gcc-8.1.0/bin/gcc-8.1.0 -DCMAKE_CXX_COMPILER=/usr/local/gcc-8.1.0/bin/g++-8.1.0 -DENABLE_QT=OFF -DENABLE_SDL2=OFF -DENABLE_CUBEB=OFF -DENABLE_ASM=OFF -DCRYPTOPP_DISABLE_AESNI=ON -DCRYPTOPP_DISABLE_ASM=ON -DCRYPTOPP_DISABLE_CXXFLAGS_OPTI=ON -DCRYPTOPP_DISABLE_SSSE3=ON```
 
 And next ```make -j2```.
 At the end you will find you binary file in ```.../build/src/dedicated-room/citra-room```. 
 Before running remember to specify the new library path.
