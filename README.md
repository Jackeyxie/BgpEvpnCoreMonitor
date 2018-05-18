# BgpEvpnCoreMonitor
An Arista EOS SDK Agent that Monitors the Status of BGP EVPN peers, and enables/disables ESI interfaces depending on the status of the said BGP EVPN Peers


## Installation
BgpEvpnCoreMonitor may be installed using the RPM provided or manually.

The RPM is installed using the usual steps for EOS extensions:

```
Arista#copy <source>/BgpEvpnCoreMonitor-<version>.rpm extension:
Copy completed successfully.

Arista#extension BgpEvpnCoreMonitor-<version>.rpm 
```
To verify that the extension is installed successfully: 

```Arista#show extensions```

Now just configure the BgpEvpnCoreMonitor daemon as below:

```
daemon BgpEvpnCoreMonitor
exec /mnt/flash/BgpEvpnCoreMonitor
no shut
```
Lastly, if it is desired that BgpEvpnCoreMonitor should be loaded automatically at boot time, the boot extensions must be modified accordingly:

```
Arista# show installed-extensions
BgpEvpnCoreMonitor-<version>.rpm 

Arista# show boot-extensions

Arista# copy installed-extensions boot-extensions
Copy completed successfully.

Arista# show boot-extensions
BgpEvpnCoreMonitor-<version>.rpm 
```


Alternatively, BgpEvpnCoreMonitor may be installed manually.  NOTE: This installation method does not Survice reboots!

The first step in doing so is to copy the BgpEvpnCoreMonitor script to the switch:

```
scp BgpEvpnCoreMonitor <user name>@<switch IP address>:/mnt/flash
```
Next, BgpEvpnCoreMonitor must be configured to interact with Sysdb by dropping into bash on the switch and executing	

```
sudo cp /usr/lib/SysdbMountProfiles/EosSdkAll /usr/lib/SysdbMountProfiles/BgpEvpnCoreMonitor
```
And then editing ```/usr/lib/SysdbMountProfiles/BgpEvpnCoreMonitor```, changing first line to be:

```agentName:BgpEvpnCoreMonitor-%sliceId```

Lastly, the BgpEvpnCoreMonitor daemon may be started using the conventional EOS daemon CLI:

```
configure 
daemon BgpEvpnCoreMonitor
exec /mnt/flash/BgpEvpnCoreMonitor
no shut
```
