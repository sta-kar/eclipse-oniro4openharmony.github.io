# Connecting a Real Device

Physical devices generally provide more representative performance and let you test hardware features that the emulator cannot reproduce, such as real sensors, cellular and Wi-Fi conditions, and battery behavior. Connect over USB when the device has a data-capable port, or over Wi-Fi when it does not (or when a cable is inconvenient).

## Connecting via USB

1. On the device, enable **Developer Options** (usually by tapping the build number several times in system settings) and turn on **USB Debugging**.
2. Connect the device via USB.
3. Accept the debugging authorization prompt on the device the first time it connects.
4. The device should now appear in DevEco Studio's target device dropdown in the toolbar.

If the device is not detected, follow the USB-connection troubleshooting steps in [Common Issues and Solutions](first-app.md#common-issues-and-solutions). USB power management often causes unstable connections on Windows.

## Connecting via IP Address (Wi-Fi)

Some devices — wearables in particular, which often have no USB data connection — must be connected over Wi-Fi instead. The computer running DevEco Studio and the device must be on the same Wi-Fi network.

1. On the device, enable **Developer Options**, then turn on **HDC Debugging** and **Debugging via WLAN** (naming can vary slightly by device).
2. Note the IP address and port shown once WLAN debugging is enabled, for example `192.168.1.42:5555`.
3. In DevEco Studio, go to **Tools → IP Connection**, enter that IP address and port, and connect.
4. Once the connection succeeds, the device shows as **online** and appears in the target device dropdown, the same as a USB-connected device.

!!! note "Note"
    You can make the same connection from the Terminal with `hdc`, without opening the IP Connection dialog:
    ```bash
    hdc tconn 192.168.1.42:5555
    ```

If the connection fails, confirm the computer can reach the device (`ping` its IP address) and that both are on the same network segment — a guest Wi-Fi network with client isolation enabled will block it.

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

With DevEco Studio set up and a device connected, continue to [Create Your First App](../../create-your-first-app/index.md) to build and run your first Eclipse Oniro application.
