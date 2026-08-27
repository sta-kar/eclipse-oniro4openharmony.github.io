# Debugging

DevEco Studio's debugger and profiler help you determine why an application behaves incorrectly.

## Starting a Debug Session

Select a run target (see [Emulator](emulator.md)), then click the **Debug** icon (bug shape) instead of **Run** in the navigation bar. The app launches the same way, but now stops at breakpoints and lets you inspect state.

## Breakpoints

* Click in the gutter to the left of a line number to set a line breakpoint (a red dot appears).
* Right-click a breakpoint to configure it further:
    * **Condition** — stop only when an expression evaluates to true, for example, `index == 3`. This is useful inside loops when you need to inspect one iteration.
    * **Log message** — print a message, optionally including expression values, without pausing execution. This provides temporary logging without recompiling or modifying the source.
    * **Suspend policy** — stop only the current thread or the whole process.

## While Paused

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

!!! note "Note"
    Instead of adding a temporary variable to inspect a computed value, pause at a breakpoint and use **Evaluate Expression** (`Alt+F8`). It can call methods and index into objects in the paused process, avoiding a source edit and restart.

## HiLog

The **Log** (HiLog) tool window streams the device/emulator's system log. Two filters make it usable on a busy device:

* **Tag filter** — match the tag used in your `hilog` calls (e.g. a per-module tag you define).
* **Log level** — restrict output to `WARN` and `ERROR` when diagnosing a crash, or `DEBUG` and `INFO` during normal development.

You can save a filter configuration instead of re-entering it in every session.

## Profiler

Once your app is up and running, **View → Tool Windows → Profiler** (or the toolbar icon) attaches CPU, memory, network, and energy profiling to the running app — reach for it when you actually have a performance problem to chase down, rather than as a first-app concern.
