# Workflow

This page describes the IDE window layout, the files that DevEco Studio generates for a new project, and editor tools that streamline daily development.

## Interface Tour

DevEco Studio is built on the IntelliJ Platform, so if you have used Android Studio, WebStorm, or another JetBrains IDE, the layout will feel familiar.

### Welcome Screen

When no project is open, DevEco Studio shows the **Welcome** screen with:

* **New Project** – start a project from a HarmonyOS template (Empty Ability, Native C++, and more). Configure the generated project for OpenHarmony when that is the target runtime.
* **Open** – open an existing project directory.
* **Get from VCS** – clone a Git repository directly.
* A list of recently opened projects.
* A gear icon for **Settings/Preferences**, **Plugins**, and **SDK Manager** — useful because these are reachable even before a project is open.

### Main Window Layout

Once a project is open, the main window is split into the following regions:

| Region | Location | Purpose |
|---|---|---|
| Navigation bar | Top | Breadcrumb of the current file's path, run/debug configuration selector, run/debug/stop buttons |
| Project tool window | Left | File tree of the project (several views available, see below) |
| Editor | Center | Source files, resource files, previews |
| Tool window bar | Left/Right/Bottom edges | Icons to toggle tool windows such as Terminal, TODO, Problems |
| Status bar | Bottom | Encoding, line separator, current SDK/API level, background task progress |

!!! tip "Project view switcher"
    The dropdown at the top of the **Project** tool window (default label `Project`) lets you switch between several file tree presentations. The two used most often are:

    * **Project** – the raw directory structure on disk.
    * **Project Files** – filters out most build/IDE metadata so only source-relevant files remain.

### Essential Shortcuts

Before learning where every tool window lives, these are the five shortcuts worth memorizing on day one:

| Shortcut | What it does |
|---|---|
| `Ctrl+F` | Find text in the current file |
| `Ctrl+S` | Save all files |
| `Shift+F10` | Run the app |
| `Shift+F9` | Debug the app |
| `Ctrl+Z` | Undo the last change |

!!! note "Shortcuts differ per keymap"
    The shortcuts above use the default Windows/Linux keymap. macOS uses `Cmd` instead of `Ctrl` for most bindings. You can inspect or change any binding under **Settings → Keymap**.

### Essential Navigation Shortcuts

| Action | Shortcut |
|---|---|
| Search everywhere (files, classes, actions, settings) | `Shift` `Shift` (double Shift) |
| Go to declaration/definition | `Ctrl+B` or `Ctrl+Click` |
| Comment/uncomment line | `Ctrl+/` |
| Reformat code | `Ctrl+Alt+L` |
| Find usages | `Alt+F7` |

**Search Everywhere** (double `Shift`) can open files, jump to a settings page, or run an IDE action without navigating through menus.

## Project Structure

When DevEco Studio creates a project from a template, it generates many files. Understanding their purposes makes manual configuration easier when a wizard is not available.

### Stage Model vs. FA Model

OpenHarmony applications can be built using one of two application models:

* **Stage model** — the current, recommended model. Introduces `AbilityStage`, a shared context across components, and a clearer separation between the application and its abilities. All new projects created by recent DevEco Studio versions default to this model.
* **FA model** (Feature Ability model) — the legacy model, kept mainly for compatibility with older codebases.

!!! tip
    Unless you are maintaining an existing FA-model project, always choose the Stage model for new work — most current documentation, samples, and APIs assume it.

### Top-Level Layout

A typical Stage-model project looks like this:

```text
MyApplication/
├── AppScope/
│   ├── app.json5
│   └── resources/
├── entry/
│   ├── src/
│   │   └── main/
│   │       ├── ets/
│   │       │   ├── entryability/
│   │       │   │   └── EntryAbility.ets
│   │       │   └── pages/
│   │       │       └── Index.ets
│   │       ├── resources/
│   │       │   ├── base/
│   │       │   ├── en_US/
│   │       │   └── rawfile/
│   │       └── module.json5
│   ├── build-profile.json5
│   └── oh-package.json5
├── build-profile.json5
├── oh-package.json5
└── hvigorfile.ts
```

#### AppScope

Settings that apply to the whole application, not just one module:

* `app.json5` — bundle name, vendor, version code/name, application icon, and application label.
* `resources/` — app-wide resources such as the app icon and label, shared across all modules.

#### entry Module

`entry` is the default **module**. Most simple applications need only this module, while larger applications can add feature modules or shared libraries alongside it.

| File/Folder | Purpose |
|---|---|
| `src/main/ets/entryability/EntryAbility.ets` | The module's entry point (`UIAbility`); handles lifecycle callbacks like `onCreate`, `onWindowStageCreate` |
| `src/main/ets/pages/` | Your ArkUI page components (`.ets` files using `@Entry`/`@Component`) |
| `src/main/resources/base/` | Default resources (strings, colors, media) used when no more specific qualifier matches |
| `src/main/resources/en_US/`, `zh_CN/`, ... | Locale-specific resource overrides |
| `src/main/resources/rawfile/` | Raw assets bundled as-is, accessed by path rather than resource ID |
| `module.json5` | Module-level manifest: `deviceTypes`, abilities, requested permissions, module name/type |
| `build-profile.json5` | Module-level build configuration, including build options and module targets |
| `oh-package.json5` | Module's dependencies, similar in spirit to `package.json` |

!!! note "Where `deviceTypes` matters"
    If your app refuses to show up as a run target for a certain emulator, check `deviceTypes` in `module.json5`. HarmonyOS phone projects use `phone`; OpenHarmony projects use `default` (and can also list supported form factors such as `tablet`). This is the same issue documented in [Common Issues and Solutions](first-app.md#common-issues-and-solutions).

#### Project-Level Files

* `build-profile.json5` (root) — declares products, SDK compatibility and compilation versions, signing configurations, build modes, and modules.
* `oh-package.json5` (root) — workspace-level dependency declarations and the `oh_modules` resolution behavior.
* `hvigorfile.ts` — the build script for **Hvigor**, OpenHarmony's build system (conceptually similar to a Gradle build script).

### Where the IDE Keeps Its Own State

The following IDE/tooling-generated paths should **not** be committed to version control:

| Folder | Contents |
|---|---|
| `.idea/` | Project-specific IDE settings (mostly machine-local) |
| `build/`, `.hvigor/` | Build outputs and Hvigor's cache |
| `oh_modules/` | Resolved dependencies (equivalent to `node_modules`) |

The [Version Control](first-app.md#version-control) section in [First App](first-app.md) gives a ready-to-use `.gitignore` for these.

## Editor Features

DevEco Studio's editor is one of its strongest points — because it is built on the IntelliJ Platform, ArkTS/ArkUI code gets the same class of tooling that TypeScript and Java developers rely on daily.

### Code Completion

As you type, DevEco Studio suggests:

* Component names and their parameters (e.g. typing `Text(` shows the expected argument).
* Available `@State`/`@Prop`/`@Link` decorators for ArkUI component properties.
* Automatic import insertion when you accept a suggestion for a symbol that isn't imported yet.

!!! tip "Smart completion"
    `Ctrl+Shift+Space` narrows suggestions to those valid at the cursor, such as types assignable to the expected parameter. This is more useful than basic completion (`Ctrl+Space`) as a project grows.

### Navigating Code

Beyond `Ctrl+B` and `Alt+F7` from the Essential Navigation Shortcuts above, the **Structure view** (`Alt+7`) is worth knowing about — it shows an outline of the current file's declarations, handy for jumping around a large page.

### Refactoring

Refactoring tools rewrite code across the whole project consistently, not just in the current file:

* **Rename** (`Shift+F6`) — renames a symbol and updates every reference, including in resource files where applicable.
* **Extract Variable / Extract Function** — pulls a selected expression or block into a named variable/function.
* **Extract Component** — turns a chunk of ArkUI declarative UI code into its own reusable `@Component`, which is one of the most useful refactors once a page's `build()` method starts growing.
* **Safe Delete** — checks for remaining usages before deleting a declaration, refusing (or warning) if something still depends on it.

!!! warning "Review before committing a rename"
    Renames across resource strings or files referenced by relative paths are not always fully tracked. After a large rename, run a project-wide search (`Ctrl+Shift+F`) for the old name before committing.

### Inspections and Quick Fixes

The editor continuously analyzes your code and underlines potential issues:

* Red underline — compile errors (e.g. missing import, type mismatch).
* Yellow underline — warnings and style suggestions (e.g. unused variable).

Press `Alt+Enter` on a highlighted piece of code to see quick fixes — importing a missing symbol, adding a missing `@State`, or suppressing a specific inspection.

The **Problems** tool window provides an aggregated list of issues across the project, which is faster than inspecting every file after a large change.

### Live Templates

Live Templates are expandable code snippets. Type an abbreviation and press `Tab` to expand it into a boilerplate block you then fill in. You can inspect and add your own under **Settings → Editor → Live Templates**. This is worth doing for repeated ArkUI patterns you write often (a specific `@Component` skeleton, a common `Column`/`Row` layout, etc.).

### Formatting and Imports

Reformat with `Ctrl+Alt+L` (already listed above); enable **Reformat and optimize imports on save** under **Settings → Tools → Actions on Save** if you'd rather not think about it.

With the layout, project files, and editor covered, move on to [First App](first-app.md) to actually build and run something.
