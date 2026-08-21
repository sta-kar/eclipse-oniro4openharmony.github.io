# Connecting a Real Device

Physical devices generally provide more representative performance and let you test hardware features that the emulator cannot reproduce, such as real sensors, cellular and Wi-Fi conditions, and battery behavior.

1. On the device, enable **Developer Options** (usually by tapping the build number several times in system settings) and turn on **USB Debugging**.
2. Connect the device via USB.
3. Accept the debugging authorization prompt on the device the first time it connects.
4. The device should now appear in DevEco Studio's target device dropdown in the toolbar.

If the device is not detected, follow the USB-connection troubleshooting steps in [Common Issues and Solutions](first-app.md#common-issues-and-solutions). USB power management often causes unstable connections on Windows.

## Using `hdc` from the Terminal

**`hdc`** (HarmonyOS Device Connector) is the command-line counterpart to Device Manager and is bundled with the SDK. Use it to automate tasks or diagnose connection problems outside the IDE. Open the embedded **Terminal** tool window and try the following commands:

```bash
# List connected devices/emulators
hdc list targets

# Open a shell on the (single) connected target
hdc shell

# Push a file to the device
hdc file send ./local-file.txt /data/local/tmp/local-file.txt

# Pull a file from the device
hdc file recv /data/local/tmp/remote-file.txt ./remote-file.txt

# Install a HAP package directly
hdc install ./entry-default-signed.hap
```

!!! note "Multiple targets connected"
    If more than one device or emulator is connected, use `hdc -t <target-id> <command>`. Run `hdc list targets` first to get the identifier. The `-s` option selects an HDC server endpoint; it does not select a device serial number.

## Troubleshooting

* **Emulator does not start or displays a black screen** — confirm that virtualization is enabled in the BIOS or UEFI settings on Windows. Check whether other virtualization software, such as Hyper-V or VirtualBox, conflicts with it.
* **Slow performance** — close unused emulators, allocate more RAM/CPU cores to the virtual device in its configuration, and prefer a lower-resolution device profile for quick UI checks.
* **System image download stuck or failing** — verify your network/proxy configuration and that the selected image is available for your host platform and account region.
* **App fails to install on the emulator** — see the `compileSdkVersion`/permission-related entries in [Common Issues and Solutions](first-app.md#common-issues-and-solutions).

Next: run the app and diagnose problems in [First App](first-app.md#debugging-and-profiling).
