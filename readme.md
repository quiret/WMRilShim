## Compilation

You must install the Windows 10 Driver Kit (WDK) to compile this application. It can be downloaded from Microsoft's website:

https://docs.microsoft.com/en-us/windows-hardware/drivers/download-the-wdk

*Latest compatible WDK version:* 10.0.18362.0

Just open the WMRilShim.sln file and compile for the ARM64 target.

## Binaries

Prebuilt binaries are included for mobile data collection purposes. If you want to improve the WoA cellular modem initialization layer of gus33000 then you can help by using the provided binaries.

## Logging of cellular data

During the runtime of the WoA OS this binary maintains a logfile at *C:\WMRilShim.log*.

You can contribute to the quality of gus33000's cellular modem initialization layer by publicly posting the (redacted off private details) logfile to [woaproject.net](https://www.woaproject.net/viewforum.php?f=17) or to the WoA-Project WMRilShim issues tracker.

Remember to uninstall the WMRilShim.dll file after you captured the required logfiles. It might clog-up your phone's system drive otherwise.

It is recommended to run the shim across multiple SIM configurations to collect the broadest-possible dataset. For each SIM configuration you should
* deleted any previous WMRilShim.log file,
* phone some SIM which has a number you will never-again use,
* get called by said number,
* text that same number, receive SMS from it aswell,
* browse the internet using the SIM,
* save the logfile after each test-run, correctly labelling it after SIM manufacturer, used network, performed tests during the test-run

If you happen to collect multiple log files it is recommend to pack them into a .zip file before uploading.

## Installation

We assume that you have WoA ARM64 (build 18908 or earlier) deployed and installed on your (preferably) Lumia 950/XL Smartphone. You need a Windows 10 desktop computer for which you plug the phone's USB into.

1) put your phone into UEFI Mass Storage Mode
2) connect your phone to the PC using USB
3) mount the MainOS partition
4) start regedit.exe on your PC and load the registry hive at *(drive letter of MainOS):\Windows\System32\config\SYSTEM* (you can load hives onto the HKLM node) with the name "W10A"
5) navigate to the registry key *Computer\HKEY_LOCAL_MACHINE\W10A\ControlSet001\Services\RILAdaptation\Parameters\0000*
6) change the property *RILPath* to: WMRilShim.dll
7) (optional:) unload the hive that is loaded at the W10A node
8) you can close regedit now.
9) download or compile the *WMRilShim.dll* ARM64 binary from this repository and put it into the *(drive letter of MainOS):\Windows\System32* folder
10) safely unmount the phone from your PC, unplug the USB and reboot it.

If you start Windows 10 ARM after this procedure, then a logfile located at *C:\WMRilShim.log* should be maintained for the runtime of the WoA OS.

## Uninstallation

The prerequisites are the same as for the installation.

1) shut down the WoA OS
2) connect your phone to the PC using USB
3) change back the RILPath registry property to: WMRil.dll
4) safely unmount the phone, unplug the USB and reboot it.