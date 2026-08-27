# Quick start

With DevEco Studio installed and its layout, project structure, and tooling covered in [IDE Basics](workflow.md), this page walks through creating an actual project, seeing it render, running it, and diagnosing anything that goes wrong along the way.

## Creating Your First Project

1. On the **Welcome** screen, click **New Project** (or, with a project already open, **File → New → New Project**).
2. Select a template. **Empty Ability** is the simplest starting point for a Stage-model application and is the best choice for a first project. Other templates add sample UI that is not needed at this stage.
3. Fill in the project details:
    * **Project name** — a human-readable label used only within DevEco Studio.
    * **Bundle name** — A reverse-domain-style identifier that follows the pattern `com.organisation_name.application_name`.
    * **Save location** — the directory on disk where the project is created.
    * **Compile/Compatible API** — match this to the OpenHarmony version you intend to run against (see the version/API table in the [application development overview](../../index.md#openharmony-version-and-api-level-reference)).
    * **Module name** — name of the default module DevEco Studio creates (usually `entry`); becomes both the module's folder name and its `name` field in `module.json5` (see [entry Module](../../create-your-first-app/project-structure.md#entry-module)).
    * **Device type** — the device types your application should target: **Phone**, **Tablet**, **2in1**, **Car**, **Wearable**, and **TV**. This sets the initial `deviceTypes` list in `module.json5`, which you can adjust later (see [Project Structure](../../create-your-first-app/project-structure.md)).
4. Click **Finish**. DevEco Studio generates the project and opens it; the first indexing pass can take a minute or two on a new machine.

!!! note "Note"
    Even if your application will need more structure, starting with **Empty Ability** and adding pages and modules yourself provides a clearer understanding of the project than removing content from a more comprehensive template.

### Targeting Oniro/OpenHarmony

Recent DevEco Studio versions create a HarmonyOS project by default. If your target is a HarmonyOS device, such as the HUAWEI WATCH 5, no further action is needed — use the SDK and runtime that already match that device. If your target is Oniro/OpenHarmony instead, retarget the generated project:

1. Open the project-level `build-profile.json5` file (next to the `entry` directory).
2. Ensure the selected product's entry uses the OpenHarmony SDK values. For OpenHarmony 6.1, for example:

    ```json
    "products": [
      {
        "name": "default",
        "signingConfig": "default",
        "compileSdkVersion": 23,
        "compatibleSdkVersion": 23,
        "runtimeOS": "OpenHarmony"
      }
    ]
    ```

    Keep any other product options DevEco Studio generated.

3. Click **Sync Now** after editing. If Sync Check offers to replace HarmonyOS-specific device types with OpenHarmony's `default` type, accept the change.

Once the project is open, `entry/src/main/ets/pages/Index.ets` is the default page rendered first. Open it to continue.

For committing, branching, and a starter `.gitignore`, see [Version Control](version-control.md).

## Running Your App

After verifying the page in the [Previewer](previewer.md), select a run target from the menu in the navigation bar and click **Run**. If no emulator or device is listed, follow [Emulator](emulator.md) to create an emulator with Device Manager or connect physical hardware.

For debugging, breakpoints, HiLog, and the Profiler, see [Debugging](debugging.md).

## Build Variants and Signing

To distribute an application outside DevEco Studio's Run and Debug workflow, you need a signed `.hap`. An `.app` file is a distribution archive that can contain multiple HAPs and HSPs; it is not installed directly with `hdc`.

### Debug vs. Release

By default, running or debugging from the IDE produces a **debug** build: automatically signed with a debug certificate so it can be installed on your own emulator/device, but not meant for distribution.

A **release** build is suitable for distribution or publication. It is optimized and signed with a certificate that persists across builds so that updates are trusted as coming from the same source.

Which variant gets built is controlled by the **Build Variant** selector, plus the products/targets declared in the project's `build-profile.json5` files (see [Project Structure](../../create-your-first-app/project-structure.md)).

### Signing Configurations

DevEco Studio supports two signing approaches:

#### Automatic Signing (recommended for getting started)

1. Go to **File → Project Structure → Signing Configs** (path may vary slightly by version).
2. Enable **Automatically generate signing configuration**.
3. Sign in with your Huawei/HarmonyOS developer account when prompted.

DevEco Studio then generates a keystore, certificate, and provisioning profile for you and wires them into `build-profile.json5` automatically. This is the fastest path and is sufficient for local testing and most individual development.

#### Manual Signing

Needed for CI pipelines, team-shared release certificates, or when a specific provisioning profile (with particular permissions/ACLs) must be used.

1. Generate a private key and CSR: **Build → Generate Key and CSR**, or via `keytool` directly if you need full control over the parameters.
2. Apply for/download a certificate and provisioning profile from the developer console using that CSR.
3. In **Project Structure → Signing Configs**, point to the `.p12`/keystore file, the certificate, and the profile, and supply the store/key passwords.
4. Reference this signing config from the relevant product entry in `build-profile.json5`.

!!! warning "Warning"
    Never commit a keystore file or its passwords. Store them in a secrets manager or CI-only environment variables, and keep only a *reference* (path/alias) in version control — see [Version Control](version-control.md) for a `.gitignore` starting point.

### Generating a Package

Once a signing configuration is in place:

* **Build → Build Hap(s)/APP(s) → Build Hap(s)** — produces a `.hap` for the current module/product.
* **Build → Build Hap(s)/APP(s) → Build APP(s)** — produces an `.app` bundle if your product is configured to build one (used for multi-HAP distribution).

Build output appears under the module's `build/` directory, and the **Build** tool window (`Alt+0`) shows progress and any failures.

With your first app created, run, debugged, and packaged, head to [Previewer](previewer.md) for a closer look at rendering your UI without an emulator, or back to [IDE Basics](workflow.md) for a closer look at the IDE itself.
