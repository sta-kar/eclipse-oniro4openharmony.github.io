# Quick start

With DevEco Studio installed and its layout, project structure, and tooling covered in [Workflow](workflow.md), this page walks through creating an actual project, seeing it render, running it, and diagnosing anything that goes wrong along the way.

## Creating Your First Project

1. On the **Welcome** screen, click **New Project** (or, with a project already open, **File → New → New Project**).
2. Select a template. **Empty Ability** is the simplest starting point for a Stage-model application and is the best choice for a first project. Other templates add sample UI that is not needed at this stage.
3. Choose the device types that your application should target, such as Phone, Tablet, or Wearable. This sets the initial `deviceTypes` list in `module.json5`, which you can adjust later (see [Project Structure](workflow.md#project-structure)).
4. Fill in the project details:
    * **Project name** and **Bundle name** (reverse-domain style, e.g. `com.example.myapplication`).
    * **Save location** on disk.
    * **Compile/Compatible API** — match this to the OpenHarmony version you intend to run against (see the version/API table in [Process of Installation](installation/process.md)).
5. Click **Finish**. DevEco Studio generates the project and opens it; the first indexing pass can take a minute or two on a new machine.

!!! tip "Start from Empty Ability"
    Even if your application will need more structure, starting with **Empty Ability** and adding pages and modules yourself provides a clearer understanding of the project than removing content from a more comprehensive template.

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

## Using the Previewer

The **Previewer** renders ArkUI pages without an emulator or physical device, providing rapid feedback while you build the UI.

### Opening the Previewer

Open any page under `entry/src/main/ets/pages/` that contains an `@Entry @Component struct` declaration. The Previewer panel should appear automatically, usually docked to the right of the editor. If it does not:

1. Click inside the `.ets` file so it has focus.
2. Look for the **Previewer** tab along the tool window bar, or use **View → Tool Windows → Previewer**.

!!! note "First render can be slow"
    The first preview of a session compiles the module, so it can take noticeably longer than subsequent updates. Later edits generally re-render in a second or two.

### Live Updates

With the Previewer open, most changes to the page's `build()` method are reflected as soon as you save (or immediately, if **Auto-save** is enabled). This works for:

* Layout and styling changes (padding, colors, alignment).
* Adding/removing components.
* Changes to `@State` initial values.

It does **not** reliably reflect:

* Behavior driven by native code or platform APIs unavailable in the preview sandbox.
* Runtime logic that depends on a real network call, file system, or sensor.
* Some animations and gesture-driven interactions — verify those on an emulator or device.

### Multi-Device Preview

Click the device selector above the Previewer canvas to render the same page across several device profiles at once, such as phone, tablet, foldable, and wearable profiles. This helps you identify layout problems on smaller or larger screens before using an emulator.

!!! tip
    Keep at least one small-screen and one large-screen profile enabled for any page with a complex layout. Most responsive-layout problems appear immediately in this comparison view.

### Interactive Preview

By default, the Previewer is a static snapshot of the page's initial render. Switching to **Interactive Preview** mode (button above the canvas) lets you click, tap, and scroll inside the rendered page as if it were running on a device — useful for checking simple state changes (toggles, tab switches, list scrolling) without a full deploy.

### Previewer Settings

Under **Settings → Languages & Frameworks → ArkUI Previewer** (path may vary slightly by version) you can adjust:

* Which device profiles are shown by default.
* Whether the Previewer refreshes automatically or only on manual trigger.
* Rendering scale, useful on high-DPI displays where the default preview looks too large or small.

### When to Stop Trusting the Previewer

The Previewer is a productivity tool, not a substitute for testing on a real target. Always validate on an emulator or device (see [Emulator](emulator.md)) before considering a feature done, especially anything touching permissions, sensors, background tasks, or performance. See [Previewer vs. Emulator](previewer-vs-emulator.md) for a fuller comparison of what each one can and can't tell you.

## Running Your App

After verifying the page in the Previewer, select a run target from the menu in the navigation bar and click **Run**. If no emulator or device is listed, follow [Emulator](emulator.md) to create an emulator with Device Manager or connect physical hardware.

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

Which variant gets built is controlled by the **Build Variant** selector, plus the products/targets declared in the project's `build-profile.json5` files (see [Project Structure](workflow.md#project-structure)).

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

With your first app created, previewed, run, debugged, and packaged, head to [Emulator](emulator.md) if you haven't already set one up, or back to [Workflow](workflow.md) for a closer look at the IDE itself.
