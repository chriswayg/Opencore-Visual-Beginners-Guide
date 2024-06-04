# Use Debug Versions

## Switch to the Debug Version of OpenCore

* Launch OCAuxiliaryTools and open the relevant Config.plist.
* Modify the Config.plist debug settings as described here: [OpenCore Debugging | OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/troubleshooting/debug.html)

![](<../.gitbook/assets/Screenshot 2024-06-04 at 11.24.45 PM.png>)

* If you encounter problems during booting, you should utilize the _debug_ version of OpenCore. As explained previously in the _Misc_ section, make sure you have activated debugging and then _Select Menu -> Edit -> OpenCore DEBUG_

![](<../.gitbook/assets/image (3).png>)

<figure><img src="../.gitbook/assets/Screenshot 2024-06-04 at 11.29.52 PM.png" alt=""><figcaption></figcaption></figure>

* Next, select _Menu -> Edit -> Upgrade OpenCore and Kexts_ or click the _Upgrade OpenCore and Kexts_ button.
* Then click: _Get the latest version of OpenCore_

![](<../.gitbook/assets/Screenshot 2024-06-04 at 11.33.42 PM.png>)

* Then press the _Start Sync_ button.

![](<../.gitbook/assets/Screenshot 2024-06-04 at 11.33.42 PM (1).png>)

<figure><img src="../.gitbook/assets/Screenshot 2024-06-04 at 11.32.26 PM.png" alt=""><figcaption></figcaption></figure>

#### Back to release version

Once everything works, switch back to the _release_ version by taking essentially the same steps:

* Select _Menu -> Edit -> OpenCore DEBUG_ - This will uncheck _OpenCore DEBUG_ in the Menu.
* Select _Menu -> Edit -> Upgrade OpenCore and Kexts_ or click the _Upgrade OpenCore and Kexts_ button.
* Press the _Start Sync_ button.
* Also revert relevant debug settings in Config.plist:
  * `AppleDebug = NO`
  * `ApplePanic = NO`
  * `Target = 0`
* In order to remove any remaining effects of the debug session, also `Reset NVRAM` (then check the correct BIOS boot order and set your default boot volume in OpenCore)

![](../images/by-nc-license.svg) _Except where otherwise noted, content on this site is licensed under the_ [_Creative Commons — Attribution-NonCommercial 4.0 International — CC BY-NC 4.0_](https://creativecommons.org/licenses/by-nc/4.0/) _license. Attribution by link to_ [_chriswayg · GitHub_](https://github.com/chriswayg)_._
