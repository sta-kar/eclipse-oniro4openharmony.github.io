# Quick start

With DevEco Studio installed and its layout, project structure, and tooling covered in [IDE Basics](workflow.md), this page walks through creating an actual project, seeing it render, running it, and diagnosing anything that goes wrong along the way.

## Creating Your First Project

1. On the **Welcome** screen, click **New Project** (or, with a project already open, **File → New → New Project**).
2. Select a template. **Empty Ability** is the simplest starting point for a Stage-model application and is the best choice for a first project. Other templates add sample UI that is not needed at this stage.
3. Fill in the project details:
    * **Project name** — a human-readable label used only within DevEco Studio.
    * **Bundle name** — A reverse-domain-style identifier that follows the pattern `com.organisation_name.application_name`.
    * **Save location** — the directory on disk where the project is created.
    * **Compile/Compatible API** — match this to the OpenHarmony version you intend to run against (see the version/API table in the [Environment Setup Guide overview](../index.md#openharmony-version-and-api-level-reference)).
    * **Module name** — name of the default module DevEco Studio creates (usually `entry`); becomes both the module's folder name and its `name` field in `module.json5` (see [entry Module](../../create-your-first-app/project-structure.md#entry-module)).
    * **Device type** — the device types your application should target: **Phone**, **Tablet**, **2in1**, **Car**, **Wearable**, and **TV**. This sets the initial `deviceTypes` list in `module.json5`, which you can adjust later (see [Project Structure](../../create-your-first-app/project-structure.md)).
4. Click **Finish**. DevEco Studio generates the project and opens it; the first indexing pass can take a minute or two on a new machine.

!!! note "Note"
    Even if your application will need more structure, starting with **Empty Ability** and adding pages and modules yourself provides a clearer understanding of the project than removing content from a more comprehensive template.

### Targeting Oniro/OpenHarmony

Recent DevEco Studio versions create a HarmonyOS project by default. If your target is a HarmonyOS device, such as the HUAWEI WATCH 5, no further action is needed — use the SDK and runtime that already match that device. If your target is Oniro/OpenHarmony instead, retarget the generated project:

1. Open the project-level `build-profile.json5` file (next to the `entry` directory).
2. Ensure the selected product's entry uses the OpenHarmony SDK values — `compileSdkVersion` and `compatibleSdkVersion` matching your target OpenHarmony release (23 for OpenHarmony 6.1), and `runtimeOS` set to `"OpenHarmony"`. Keep any other product options DevEco Studio generated.

3. Click **Sync Now** after editing. If Sync Check offers to replace HarmonyOS-specific device types with OpenHarmony's `default` type, accept the change.

Once the project is open, `entry/src/main/ets/pages/Index.ets` is the default page rendered first. Open it to continue.

For committing, branching, and a starter `.gitignore`, see [Version Control](version-control.md).

## Running Your App

DevEco Studio gives you two ways to see your app running: the [Previewer](previewer.md), a live rendering of the current page inside the IDE without needing a device, and an [emulator](emulator.md) or physical device, which runs the actual compiled app.

1. Open the run-target dropdown in the navigation bar and select an emulator or a connected physical device. If none is listed, follow [Emulator](emulator.md) to create one with Device Manager, or connect [physical hardware](real-device.md).
2. Click **Run** (▶) or press `Shift+F10`. DevEco Studio builds the project, installs the resulting `.hap` on the selected target, and launches it automatically.
3. Watch the **Run** tool window for build progress and the app's console output — it's the first place to check if the build fails or the app crashes on launch.

For debugging, breakpoints, HiLog, and the Profiler, see [Debugging](debugging.md).

When you're ready to distribute a signed build instead of just running or debugging locally, see [Build Variants and Signing](build-variants-and-signing.md).

With your first app created, run, and debugged, head to [Previewer](previewer.md) for a closer look at rendering your UI without an emulator, or back to [IDE Basics](workflow.md) for a closer look at the IDE itself.
