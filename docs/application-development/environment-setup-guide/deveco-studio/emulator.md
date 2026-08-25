# Emulator

After verifying the UI in the Previewer (see [First App](first-app.md)), run the application on an emulator or physical hardware. The emulator works the same way on Windows and macOS. See [Previewer vs. Emulator](previewer-vs-emulator.md) if you're unsure which one you need at a given point.

The virtual devices downloaded through DevEco Studio's Device Manager are HarmonyOS images. Use them for a HarmonyOS project with a matching API and release type. To run a project configured with `runtimeOS: "OpenHarmony"`, use the [Oniro emulator](../oniro/setup.md#downloading-the-emulator) or an OpenHarmony device instead.

## Prerequisites

* **Hardware virtualization** must be enabled — Intel VT-x / AMD-V on Windows (usually a BIOS/UEFI setting). Apple Silicon Macs run the emulator natively; Intel-based Macs do not support emulation in DevEco Studio.
* The first time you download a virtual device image, DevEco Studio shows an additional **User Agreement** (HarmonyOS Software License and Service Agreement, plus the User Experience Improvement Program notice) that you need to accept.

<img src='../images/emulator_user_agreement.png' alt="User Agreement dialog with HarmonyOS Software License and User Experience Improvement Program checkboxes">

## Device Manager

Open **Device Manager** from **Tools → Device Manager** or from the device menu next to the Run and Debug buttons on the toolbar. It appears at the bottom of that menu.

<img src='../images/emulator_device_manager.png' alt="Run target dropdown with Device Manager listed under Huawei|Emulator">

Device Manager's **Your Devices** page lists existing emulators under the **Local Emulator** tab, along with their locations on disk.

<img src='../images/emulator_virtual_device_configuration.png' alt="Device Manager Your Devices page, Local Emulator tab, with the New Emulator button">

### Creating a Virtual Device

1. Click **+ New Emulator**.
2. On the **Select Virtual Device** screen, select a device type from the tree on the left (Phone, Foldable, WideFold, TripleFold, Tablet, 2in1, 2in1 Foldable, or TV) and a row that matches the target HarmonyOS and API version (see the version/API table in the [application development overview](../../index.md#openharmony-version-and-api-level-reference)).
3. If the system image has not yet been downloaded, click the download icon in the **Actions** column and wait for the download to finish. Allow approximately **2 GB** of free disk space for the image and approximately **12 GB** to run it.
4. Click **Next**.
<img src='../images/emulator_creating_new_device.png' alt="Select Virtual Device screen listing device types, API versions, and a download action per row">
5. On the **Virtual Device Configure** screen, confirm the device name and hardware profile, including the screen size, resolution, and DPI. Click **Customize** to change the screen profile. Choose a boot option as described below, then set the RAM and ROM allocated to the virtual device.
6. Click **Finish** to create it.
<img src='../images/emulator_virtual_device_configuration_2.png' alt="Virtual Device Configure screen with name, screen profile, boot options, RAM and ROM fields">

!!! tip "compileSdkVersion vs. compatibleSdkVersion vs. targetSdkVersion"
    These fields live in each module's `build-profile.json5` and are easy to mix up:

    * **`compileSdkVersion`** — the API level used to *compile* the app. It controls which APIs are available at build time and has no direct bearing on which emulator or device can actually run the app.
    * **`compatibleSdkVersion`** — the *minimum* API level the app can run on. This is the one that actually gates installation: if an emulator's API level is lower than `compatibleSdkVersion`, install/run will fail. In most OpenHarmony projects it's set to the same value as `compileSdkVersion`.
    * **`targetSdkVersion`** — the API level the app is designed and tested against; running on a higher level than this is fine, but the app won't opt into behavior changes introduced above it. This field is mainly a HarmonyOS (Huawei's downstream distribution) addition and isn't always present in plain OpenHarmony projects.

    In practice: keep at least one emulator matching (or above) your module's `compatibleSdkVersion`, so install/run never fails due to a version mismatch.

### Boot Modes

* **Cold boot** — starts the emulator from a clean state every time. Slower, but useful when you need to rule out state left over from a previous run.
* **Quick boot** — resumes from a saved snapshot, which is much faster for everyday iteration.

If an emulator becomes unresponsive or enters an invalid state, such as the "Unable to Find the BMS Service" problem described in [Common Issues and Solutions](first-app.md#common-issues-and-solutions), perform a cold boot or wipe its data.

## Running Your App on the Emulator

1. In Device Manager, start the emulator (or let the IDE boot it automatically the first time you target it).
2. Return to your project, open the run-target menu on the toolbar, and select the emulator under **Huawei|Emulator**. The menu also contains the **Huawei Simulator** entries (Wearable Simulator and Smart Vision Simulator) and the **Huawei Previewer**.
<img src='../images/emulator_device_run.png' alt="Run target dropdown with a created emulator selected under Huawei|Emulator">
3. Click **Run**. The app builds, installs, and launches automatically on the emulator.