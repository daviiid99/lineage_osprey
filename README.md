
Lineage 19.0 for Osprey
=======================

Current Status
--------------

What's working ?
 - It boots!
 - Audio
 - RIL
 - Mobile data
 - Wifi
 - Bluetooth
 - GPS
 - Camera
 - Camcorder

Not Working / Not Tested ?
 - VoLTE
 - SELinux Enforcing

Download
--------

It's not ready for public testing so no builds are availble to download at present.
Builds will available [here](https://chil360.github.io/) when it's ready for public testing.

Build Instructions
------------------
Create a build directory

	mkdir lineage
	cd lineage

Initialize your local repository using the LineageOS trees, use a command like this:

    repo init -u git://github.com/LineageOS/android.git -b lineage-19.0

Now create a local_manifests directory

	mkdir -p .repo/local_manifests
	curl https://raw.githubusercontent.com/Galaxy-J5-Unofficial-LineageOS/Manifest/main/LOS-19.0-Permissive-Manifest.xml > .repo/local_manifests/j5.xml

Then to sync up:
    
    repo sync -c --no-clone-bundle --no-tags --force-sync --optimized-fetch --prune
    source build/envsetup.sh

Apply required repopicks:

        curl https://raw.githubusercontent.com/daviiid99/lineage_osprey/lineage-19.0/repopick.sh  > repopick.sh
	chmod +x repopick.sh
	./repopick.sh
	
Apply any required patches:

	curl https://raw.githubusercontent.com/daviiid99/lineage_osprey/lineage-19.0/patch.sh > patch.sh
	curl https://raw.githubusercontent.com/daviiid99/lineage_osprey/lineage-19.0/0001-TEMP-Disable-ADB-authentication.patch > 0001-TEMP-Disable-ADB-authentication.patch
	curl https://raw.githubusercontent.com/daviiid99/lineage_osprey/lineage-19.0/0001-launcher-Add-support-for-themed-icons.patch > 0001-launcher-Add-support-for-themed-icons.patch
	curl https://raw.githubusercontent.com/daviiid99/lineage_osprey/lineage-19.0/0002-Launcher3-Import-more-themed-icons.patch > 0002-Launcher3-Import-more-themed-icons.patch
	 patch -d vendor/lineage -p1 < 0001-TEMP-Disable-ADB-authentication.patch
	 patch -d packages/apps/Trebuchet -p1 < 0001-launcher-Add-support-for-themed-icons.patch
	 patch -d packages/apps/Trebuchet -p1 < 0002-Launcher3-Import-more-themed-icons.patch
	 

Now start the build...

```bash
# Go to the root of the source tree...
$
# ...and run to prepare our devices list
$ . build/envsetup.sh
# ... now run
$ brunch j5nlte
```

Notes
-----

If you get stuck at the TWRP splash screen when rebooting to recovery:
```bash
$ adb shell rm /data/system/storage.xml
$ adb reboot recovery
```

Please see the [LineageOS Wiki](https://wiki.lineageos.org/) for further information.
