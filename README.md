# $${\color{violet}Termux- ADB- and- Fastboot}$$
Install adb and fastboot in termux without root privilege.

© [nohajc](https://github.com/nohajc)
# $${\color{violet}Requirements}$$
- [Termux](https://github.com/termux/termux-app/releases/download/v0.118.2/termux-app_v0.118.2+github-debug_arm64-v8a.apk)
- [Termux-API](https://github.com/termux/termux-api/releases/download/v0.51.0/termux-api-app_v0.51.0+github.debug.apk)

# $${\color{violet}Auto- Install}$$
```
apt update && apt install wget -y && wget -qO- https://raw.githubusercontent.com/xiv3r/adb-fastboot-termux/refs/heads/main/install | bash
```
<details><summary>
  
## $${\color{cyan}ADB- Logs}$$
</summary>

```
~ $ adb
Android Debug Bridge version 1.0.41
Version 34.0.4-android-tools
Installed as /data/data/com.termux/files/usr/bin/termux-adb
Running on Linux 4.14.186-ge8369fee7-dirty (aarch64)

global options:
 -a                       listen on all network interfaces, not just localhost
 -d                       use USB device (error if multiple devices connected)
 -e                       use TCP/IP device (error if multiple TCP/IP devices available)
 -s SERIAL                use device with given serial (overrides $ANDROID_SERIAL)
 -t ID                    use device with given transport id
 -H                       name of adb server host [default=localhost]
 -P                       port of adb server [default=5037]
 -L SOCKET                listen on given socket for adb server [default=tcp:localhost:5037]
 --one-device SERIAL|USB  only allowed with 'start-server' or 'server nodaemon', server will only connect to one USB device, specified by a serial number or USB device address.
 --exit-on-write-error    exit if stdout is closed

general commands:
 devices [-l]             list connected devices (-l for long output)
 help                     show this help message
 version                  show version num

networking:
 connect HOST[:PORT]      connect to a device via TCP/IP [default port=5555]
 disconnect [HOST[:PORT]]
     disconnect from given TCP/IP device [default port=5555], or all
 pair HOST[:PORT] [PAIRING CODE]
     pair with a device for secure TCP/IP communication
 forward --list           list all forward socket connections
 forward [--no-rebind] LOCAL REMOTE
     forward socket connection using:
       tcp:<port> (<local> may be "tcp:0" to pick any open port)
       localabstract:<unix domain socket name>
       localreserved:<unix domain socket name>
       localfilesystem:<unix domain socket name>
       dev:<character device name>
       jdwp:<process pid> (remote only)
       vsock:<CID>:<port> (remote only)
       acceptfd:<fd> (listen only)
 forward --remove LOCAL   remove specific forward socket connection
 forward --remove-all     remove all forward socket connections
 reverse --list           list all reverse socket connections from device
 reverse [--no-rebind] REMOTE LOCAL
     reverse socket connection using:
       tcp:<port> (<remote> may be "tcp:0" to pick any open port)
       localabstract:<unix domain socket name>
       localreserved:<unix domain socket name>
       localfilesystem:<unix domain socket name>
 reverse --remove REMOTE  remove specific reverse socket connection
 reverse --remove-all     remove all reverse socket connections from device
 mdns check               check if mdns discovery is available
 mdns services            list all discovered services

file transfer:
 push [--sync] [-z ALGORITHM] [-Z] LOCAL... REMOTE
     copy local files/directories to device
     --sync: only push files that are newer on the host than the device
     -n: dry run: push files to device without storing to the filesystem
     -z: enable compression with a specified algorithm (any/none/brotli/lz4/zstd)
     -Z: disable compression
 pull [-a] [-z ALGORITHM] [-Z] REMOTE... LOCAL
     copy files/dirs from device
     -a: preserve file timestamp and mode
     -z: enable compression with a specified algorithm (any/none/brotli/lz4/zstd)
     -Z: disable compression
 sync [-l] [-z ALGORITHM] [-Z] [all|data|odm|oem|product|system|system_ext|vendor]
     sync a local build from $ANDROID_PRODUCT_OUT to the device (default all)
     -n: dry run: push files to device without storing to the filesystem
     -l: list files that would be copied, but don't copy them
     -z: enable compression with a specified algorithm (any/none/brotli/lz4/zstd)
     -Z: disable compression

shell:
 shell [-e ESCAPE] [-n] [-Tt] [-x] [COMMAND...]
     run remote shell command (interactive shell if no command given)
     -e: choose escape character, or "none"; default '~'
     -n: don't read from stdin
     -T: disable pty allocation
     -t: allocate a pty if on a tty (-tt: force pty allocation)
     -x: disable remote exit codes and stdout/stderr separation
 emu COMMAND              run emulator console command

app installation (see also `adb shell cmd package help`):
 install [-lrtsdg] [--instant] PACKAGE
     push a single package to the device and install it
 install-multiple [-lrtsdpg] [--instant] PACKAGE...
     push multiple APKs to the device for a single package and install them
 install-multi-package [-lrtsdpg] [--instant] PACKAGE...
     push one or more packages to the device and install them atomically
     -r: replace existing application
     -t: allow test packages
     -d: allow version code downgrade (debuggable packages only)
     -p: partial application install (install-multiple only)
     -g: grant all runtime permissions
     --abi ABI: override platform's default ABI
     --instant: cause the app to be installed as an ephemeral install app
     --no-streaming: always push APK to device and invoke Package Manager as separate steps
     --streaming: force streaming APK directly into Package Manager
     --fastdeploy: use fast deploy
     --no-fastdeploy: prevent use of fast deploy
     --force-agent: force update of deployment agent when using fast deploy
     --date-check-agent: update deployment agent when local version is newer and using fast deploy
     --version-check-agent: update deployment agent when local version has different version code and using fast deploy
     --local-agent: locate agent files from local source build (instead of SDK location)
     (See also `adb shell pm help` for more options.)
 uninstall [-k] PACKAGE
     remove this app package from the device
     '-k': keep the data and cache directories

debugging:
 bugreport [PATH]
     write bugreport to given PATH [default=bugreport.zip];
     if PATH is a directory, the bug report is saved in that directory.
     devices that don't support zipped bug reports output to stdout.
 jdwp                     list pids of processes hosting a JDWP transport
 logcat                   show device log (logcat --help for more)

security:
 disable-verity           disable dm-verity checking on userdebug builds
 enable-verity            re-enable dm-verity checking on userdebug builds
 keygen FILE
     generate adb public/private key; private key stored in FILE,

scripting:
 wait-for[-TRANSPORT]-STATE...
     wait for device to be in a given state
     STATE: device, recovery, rescue, sideload, bootloader, or disconnect
     TRANSPORT: usb, local, or any [default=any]
 get-state                print offline | bootloader | device
 get-serialno             print <serial-number>
 get-devpath              print <device-path>
 remount [-R]
      remount partitions read-write. if a reboot is required, -R will
      will automatically reboot the device.
 reboot [bootloader|recovery|sideload|sideload-auto-reboot]
     reboot the device; defaults to booting system image but
     supports bootloader and recovery too. sideload reboots
     into recovery and automatically starts sideload mode,
     sideload-auto-reboot is the same but reboots after sideloading.
 sideload OTAPACKAGE      sideload the given full OTA package
 root                     restart adbd with root permissions
 unroot                   restart adbd without root permissions
 usb                      restart adbd listening on USB
 tcpip PORT               restart adbd listening on TCP on PORT

internal debugging:
 start-server             ensure that there is a server running
 kill-server              kill the server if it is running
 reconnect                kick connection from host side to force reconnect
 reconnect device         kick connection from device side to force reconnect
 reconnect offline        reset offline/unauthorized devices to force reconnect

usb:
 attach                   attach a detached USB device
 detach                   detach from a USB device to allow use by other processes
environment variables:
 $ADB_TRACE
     comma-separated list of debug info to log:
     all,adb,sockets,packets,rwx,usb,sync,sysdeps,transport,jdwp
 $ADB_VENDOR_KEYS         colon-separated list of keys (files or directories)
 $ANDROID_SERIAL          serial number to connect to (see -s)
 $ANDROID_LOG_TAGS        tags to be used by logcat (see logcat --help)
 $ADB_LOCAL_TRANSPORT_MAX_PORT max emulator scan port (default 5585, 16 emus)
 $ADB_MDNS_AUTO_CONNECT   comma-separated list of mdns services to allow auto-connect (default adb-tls-connect)

Online documentation: https://android.googlesource.com/platform/packages/modules/adb/+/refs/heads/master/docs/user/adb.1.md
```
</details>

<details><summary>

## $${\color{cyan}Fastboot- Logs}$$
</summary>

```sh
~ $ fastboot
usage: fastboot [OPTION...] COMMAND...

flashing:
 update ZIP                 Flash all partitions from an update.zip package.
 flashall                   Flash all partitions from $ANDROID_PRODUCT_OUT.
                            On A/B devices, flashed slot is set as active.
                            Secondary images may be flashed to inactive slot.
 flash PARTITION [FILENAME] Flash given partition, using the image from
                            $ANDROID_PRODUCT_OUT if no filename is given.

basics:
 devices [-l]               List devices in bootloader (-l: with device paths).
 getvar NAME                Display given bootloader variable.
 reboot [bootloader]        Reboot device.

locking/unlocking:
 flashing lock|unlock       Lock/unlock partitions for flashing
 flashing lock_critical|unlock_critical
                            Lock/unlock 'critical' bootloader partitions.
 flashing get_unlock_ability
                            Check whether unlocking is allowed (1) or not(0).

advanced:
 erase PARTITION            Erase a flash partition.
 format[:FS_TYPE[:SIZE]] PARTITION
                            Format a flash partition.
 set_active SLOT            Set the active slot.
 oem [COMMAND...]           Execute OEM-specific command.
 gsi wipe|disable           Wipe or disable a GSI installation (fastbootd only).
 wipe-super [SUPER_EMPTY]   Wipe the super partition. This will reset it to
                            contain an empty set of default dynamic partitions.
 create-logical-partition NAME SIZE
                            Create a logical partition with the given name and
                            size, in the super partition.
 delete-logical-partition NAME
                            Delete a logical partition with the given name.
 resize-logical-partition NAME SIZE
                            Change the size of the named logical partition.
 snapshot-update cancel     On devices that support snapshot-based updates, cancel
                            an in-progress update. This may make the device
                            unbootable until it is reflashed.
 snapshot-update merge      On devices that support snapshot-based updates, finish
                            an in-progress update if it is in the "merging"
                            phase.
 fetch PARTITION OUT_FILE   Fetch a partition image from the device.
boot image:
 boot KERNEL [RAMDISK [SECOND]]
                            Download and boot kernel from RAM.
 flash:raw PARTITION KERNEL [RAMDISK [SECOND]]
                            Create boot image and flash it.
 --dtb DTB                  Specify path to DTB for boot image header version 2.
 --cmdline CMDLINE          Override kernel command line.
 --base ADDRESS             Set kernel base address (default: 0x10000000).
 --kernel-offset            Set kernel offset (default: 0x00008000).
 --ramdisk-offset           Set ramdisk offset (default: 0x01000000).
 --tags-offset              Set tags offset (default: 0x00000100).
 --dtb-offset               Set dtb offset (default: 0x01100000).
 --page-size BYTES          Set flash page size (default: 2048).
 --header-version VERSION   Set boot image header version.
 --os-version MAJOR[.MINOR[.PATCH]]
                            Set boot image OS version (default: 0.0.0).
 --os-patch-level YYYY-MM-DD
                            Set boot image OS security patch level.

Android Things:
 stage IN_FILE              Sends given file to stage for the next command.
 get_staged OUT_FILE        Writes data staged by the last command to a file.

options:
 -w                         Wipe userdata.
 -s SERIAL                  Specify a USB device.
 -s tcp|udp:HOST[:PORT]     Specify a network device.
 -S SIZE[K|M|G]             Break into sparse files no larger than SIZE.
 --force                    Force a flash operation that may be unsafe.
 --slot SLOT                Use SLOT; 'all' for both slots, 'other' for
                            non-current slot (default: current active slot).
 --set-active[=SLOT]        Sets the active slot before rebooting.
 --skip-secondary           Don't flash secondary slots in flashall/update.
 --skip-reboot              Don't reboot device after flashing.
 --disable-verity           Sets disable-verity when flashing vbmeta.
 --disable-verification     Sets disable-verification when flashing vbmeta.
 --fs-options=OPTION[,OPTION]
                            Enable filesystem features. OPTION supports casefold, projid, compress
 --unbuffered               Don't buffer input or output.
 --verbose, -v              Verbose output.
 --version                  Display version.
 --help, -h                 Show this message.
```
</details>
