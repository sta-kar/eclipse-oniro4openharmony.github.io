# Quick start

With DevEco Studio installed and its layout, project structure, and tooling covered in [Work With IDE](workflow.md), this page walks through creating an actual project, seeing it render, running it, and diagnosing anything that goes wrong along the way.

## Creating Your First Project

1. On the **Welcome** screen, click **New Project** (or, with a project already open, **File → New → New Project**).
2. Select a template. **Empty Ability** is the simplest starting point for a Stage-model application and is the best choice for a first project. Other templates add sample UI that is not needed at this stage.
3. Fill in the project details:
    * **Project name** — a human-readable label used only within DevEco Studio.
    * **Bundle name** — the app's globally unique identifier, written in reverse-domain style (e.g. `com.example.myapplication`). It's stored as `bundleName` in `AppScope/app.json5` (see [AppScope](../../create-your-first-app/project-structure.md#appscope)), is how the OS and app stores tell your app apart from every other installed app, and is difficult to change once you've published — pick it deliberately rather than accepting a placeholder.
    * **Save location** — the directory on disk where the project is created.
    * **Compile/Compatible API** — match this to the OpenHarmony version you intend to run against (see the version/API table in the [application development overview](../../index.md#openharmony-version-and-api-level-reference)).
    * **Module name** — name of the default module DevEco Studio creates (usually `entry`); becomes both the module's folder name and its `name` field in `module.json5` (see [entry Module](../../create-your-first-app/project-structure.md#entry-module)).
    * **Device type** — the device types your application should target: **Phone**, **Tablet**, **2in1**, **Car**, **Wearable**, and **TV**. This sets the initial `deviceTypes` list in `module.json5`, which you can adjust later (see [Project Structure](../../create-your-first-app/project-structure.md)).
4. Click **Finish**. DevEco Studio generates the project and opens it; the first indexing pass can take a minute or two on a new machine.

!!! tip "Start from Empty Ability"
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

## Version Control

DevEco Studio includes the same built-in Git integration found across JetBrains IDEs, so you rarely need to leave the editor for everyday version control work.

### Enabling VCS for a Project

If a project wasn't cloned from Git, enable it via **VCS → Enable Version Control Integration** and choose Git. DevEco Studio then treats the project root as a Git repository and starts tracking file status.

### The Commit Tool Window

Open it with `Alt+9` or **View → Tool Windows → Commit**. It shows:

* Changed files, grouped by changelist (the default changelist is fine for most workflows).
* A diff preview for the selected file.
* A commit message box, plus **Commit** and **Commit and Push** buttons.

<img src='../images/deveco_version_control.png' alt="Version Control tool window's Git Log tab, showing the Local/master branch tree and a Commit local changes link">

<img src='../images/deveco_version_control_2.png' alt="Version Control tool window's Git Log tab, showing the Local/master branch tree and a Commit local changes link">

!!! tip "Review before committing"
    Review each changed file in the Commit window before committing. This is equivalent to reviewing `git diff` before `git add`, but the diff is displayed in the editor.

### Branch Management

The branch indicator in the lower-right status bar opens a menu for checking out, creating, renaming, or merging branches without a terminal. After you fetch, it also shows incoming and outgoing commit counts.

!!! note "Fetch vs. Update"
    **Update Project** (`Ctrl+T`) fetches and merges or rebases according to your configured settings. To inspect remote changes without modifying the working tree, use **Git → Fetch** instead.

### Resolving Conflicts

When a merge/rebase produces a conflict, DevEco Studio opens a three-pane merge tool: your version, the result, and the incoming version, with per-block **Accept Yours/Theirs** actions plus manual editing of the result pane. Resolve each conflicting file this way, then continue the merge/rebase from the VCS menu.

### `.gitignore`

Several folders under a DevEco Studio project are either machine-local IDE state or fully regenerable build output, and should not be committed:

=== "Default"
    <!-- TODO: replace with the .gitignore DevEco Studio actually generates for a new project -->
    ```gitignore
    /node_modules
    /oh_modules
    /.preview
    /build
    /.cxx
    /.test
    ```

=== "Recommended"
    ```gitignore
    # Build output
    build/
    .hvigor/
    .cxx/
    .test/

    # Previewer cache
    .preview/

    # Dependency cache (regenerated from oh-package.json5 / package.json)
    oh_modules/
    node_modules/

    # IDE metadata
    .idea/
    *.iml

    # Local, machine-specific config
    local.properties

    # Signing material — never commit real keystores or passwords
    *.p12
    *.jks
    *.cer
    *.p7b
    ```

!!! warning "Check history for secrets before pushing publicly"
    If a keystore or credentials file was committed before it was added to `.gitignore`, the ignore rule does not remove it from history. Purge it from history, for example with `git filter-repo`, and rotate the exposed credentials. Treat committed credentials as compromised.

## Running Your App

After verifying the page in the [Previewer](previewer.md), select a run target from the menu in the navigation bar and click **Run**. If no emulator or device is listed, follow [Emulator](emulator.md) to create an emulator with Device Manager or connect physical hardware.

## Debugging and Profiling

DevEco Studio's debugger and profiler help you determine why an application behaves incorrectly.

### Starting a Debug Session

Select a run target (see [Emulator](emulator.md)), then click the **Debug** icon (bug shape) instead of **Run** in the navigation bar. The app launches the same way, but now stops at breakpoints and lets you inspect state.

### Breakpoints

* Click in the gutter to the left of a line number to set a line breakpoint (a red dot appears).
* Right-click a breakpoint to configure it further:
    * **Condition** — stop only when an expression evaluates to true, for example, `index == 3`. This is useful inside loops when you need to inspect one iteration.
    * **Log message** — print a message, optionally including expression values, without pausing execution. This provides temporary logging without recompiling or modifying the source.
    * **Suspend policy** — stop only the current thread or the whole process.

### While Paused

The **Debug** tool window shows:

| Pane | Purpose |
|---|---|
| Frames | Current call stack; click a frame to inspect its local variables |
| Variables | Local variables and `this` in the selected frame, expandable for object/array contents |
| Watches | Expressions you pin so they're always visible while stepping |
| Evaluate Expression (`Alt+F8`) | Run arbitrary expressions against the current paused state, including calling functions |

Step controls:

| Action | Shortcut |
|---|---|
| Step over | `F8` |
| Step into | `F7` |
| Step out | `Shift+F8` |
| Resume program | `F9` |

!!! tip "Evaluate computed values"
    Instead of adding a temporary variable to inspect a computed value, pause at a breakpoint and use **Evaluate Expression** (`Alt+F8`). It can call methods and index into objects in the paused process, avoiding a source edit and restart.

### HiLog

The **Log** (HiLog) tool window streams the device/emulator's system log. Two filters make it usable on a busy device:

* **Tag filter** — match the tag used in your `hilog` calls (e.g. a per-module tag you define).
* **Log level** — restrict output to `WARN` and `ERROR` when diagnosing a crash, or `DEBUG` and `INFO` during normal development.

You can save a filter configuration instead of re-entering it in every session.

### Profiler

Once your app is up and running, **View → Tool Windows → Profiler** (or the toolbar icon) attaches CPU, memory, network, and energy profiling to the running app — reach for it when you actually have a performance problem to chase down, rather than as a first-app concern.

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

!!! warning "Keep release keys out of the repository"
    Never commit a keystore file or its passwords. Store them in a secrets manager or CI-only environment variables, and keep only a *reference* (path/alias) in version control — see [Version Control](#version-control) for a `.gitignore` starting point.

### Generating a Package

Once a signing configuration is in place:

* **Build → Build Hap(s)/APP(s) → Build Hap(s)** — produces a `.hap` for the current module/product.
* **Build → Build Hap(s)/APP(s) → Build APP(s)** — produces an `.app` bundle if your product is configured to build one (used for multi-HAP distribution).

Build output appears under the module's `build/` directory, and the **Build** tool window (`Alt+0`) shows progress and any failures.

With your first app created, run, debugged, and packaged, head to [Previewer](previewer.md) for a closer look at rendering your UI without an emulator, or back to [Work With IDE](workflow.md) for a closer look at the IDE itself.
