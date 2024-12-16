# ts_xdma_archive


### XDMA

These are instructions for the deprecated XDMA gateware

1. Install the XDMA driver for [Linux](https://github.com/EEVengers/ts_xdma_archive/tree/main/xdma_driver_linux) or [Windows](https://github.com/EEVengers/ts_xdma_archive/tree/main/xdma_driver_win_src_2018_2)
   - On Windows, first run `Bcdedit.exe -set TESTSIGNING ON` in administrator powershell and restart your computer
      - Then use the [MSI installer](https://github.com/EEVengers/ts_xdma_archive/tree/main/xdma_driver_win_src_2018_2/Installers/Win10_x64_Release/XDMADriverInstaller.msi), when asked if you want to use polling, click no
   - On Linux, run `sudo make install` in the [xdma](https://github.com/EEVengers/ts_xdma_archive/tree/main/xdma_driver_linux/xdma) directory
      - Run `make` in the [tools](https://github.com/EEVengers/ts_xdma_archive/tree/main/xdma_driver_linux/tools) directory
      - Create a udev rule so you don't have to run everything acessing the hardware as root:
         - create `/etc/udev/rules.d/70-thunderscope.rules` file with the line `ACTION=="add", SUBSYSTEM=="xdma", TAG+="uaccess"`
      - With a TS connected, run `sudo ./load_driver.sh` in the [tests](https://github.com/EEVengers/ts_xdma_archive/tree/main/xdma_driver_linux/tests) directory
        - Output should be `The Kernel module installed correctly and the xmda devices were recognized.`  
2. Build TS.NET.Engine using the [build scripts](https://github.com/EEVengers/TS.NET/tree/main/build-scripts)
   - Dependences for build scripts on Debian/Ubuntu Linux: `sudo apt-get install -y dotnet-sdk-8.0 libgdiplus`
   - On Windows, should just need Visual Studio with the C# plugins
   - Copy [appsettings.json](https://github.com/EEVengers/TS.NET/blob/main/source/TS.NET.Engine/appsettings.json) and [thunderscope.yaml](https://github.com/EEVengers/TS.NET/blob/main/source/TS.NET.Engine/thunderscope.yaml) into the same directory as the TS.NET.Engine application
3. Install ngscopeclient, following the instructions in their [user manual](https://www.ngscopeclient.org/manual/GettingStarted.html)
4. Run TS.NET.Engine and ngscopeclient
5. Add ThunderScope in ngscopeclient under Add -> Oscilloscope with "thunderscope" Driver, "Twinlan" Transport and "Localhost:5025:5026" for the Path
