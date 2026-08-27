# Project Structure

When a project is created from a template, many files are generated automatically. Understanding their purposes makes manual configuration easier when a wizard is not available.

## Stage Model vs. FA Model

OpenHarmony applications can be built using one of two application models:

* **Stage model** — the current, recommended model. Introduces `AbilityStage`, a shared context across components, and a clearer separation between the application and its abilities. All new projects created by recent IDE versions default to this model.
* **FA model** (Feature Ability model) — the legacy model, kept mainly for compatibility with older codebases.

!!! tip
    Unless you are maintaining an existing FA-model project, always choose the Stage model for new work — most current documentation, samples, and APIs assume it.

## Top-Level Layout

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

### AppScope

Settings that apply to the whole application, not just one module:

* `app.json5` — bundle name, vendor, version code/name, application icon, and application label.
* `resources/` — app-wide resources such as the app icon and label, shared across all modules.

### entry Module

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

!!! note "Note"
    If your app refuses to show up as a run target for a certain emulator, check `deviceTypes` in `module.json5`. HarmonyOS phone projects use `phone`; OpenHarmony projects use `default` (and can also list supported form factors such as `tablet`).

### Project-Level Files

* `build-profile.json5` (root) — declares products, SDK compatibility and compilation versions, signing configurations, build modes, and modules.
* `oh-package.json5` (root) — workspace-level dependency declarations and the `oh_modules` resolution behavior.
* `hvigorfile.ts` — the build script for **Hvigor**, OpenHarmony's build system (conceptually similar to a Gradle build script).

## Where the IDE Keeps Its Own State

The following IDE/tooling-generated paths should **not** be committed to version control:

| Folder | Contents |
|---|---|
| `.idea/` | Project-specific IDE settings (mostly machine-local) |
| `build/`, `.hvigor/` | Build outputs and Hvigor's cache |
| `oh_modules/` | Resolved dependencies (equivalent to `node_modules`) |

!!! tip
    A ready-to-use `.gitignore` can be found in the [Version Control](../environment-setup-guide/deveco-studio/version-control.md) section.
