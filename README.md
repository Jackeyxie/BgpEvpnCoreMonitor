# BgpEvpnCoreMonitor
An Arista EOS SDK Agent that Monitors the Status of BGP EVPN peers, and enables/disables ESI interfaces based on the status of the BGP EVPN Peers


## Installation
BgpEvpnCoreMonitor may be installed using the SWIX provided or manually.

The RPM is installed using the usual steps for EOS extensions:
```
Arista#copy <source>/BgpEvpnCoreMonitor-<version>.rpm extension:                                                               Copy completed successfully.
Arista#extension BgpEvpnCoreMonitor-<version>.rpm 
```
To verify that the extension is installed successfully: ```Arista#show extensions```
No just configure the BgpEvpnCoreMonitor daemon as below:
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
