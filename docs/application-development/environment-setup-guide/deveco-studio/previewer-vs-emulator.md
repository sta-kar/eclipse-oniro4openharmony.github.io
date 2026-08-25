# Previewer vs. Emulator

Both let you see and interact with your app without physical hardware, but they solve different problems and are not interchangeable.

## At a Glance

| | Previewer | Emulator |
|---|---|---|
| What it is | A live rendering of a single ArkUI page, inside the IDE | A full virtual HarmonyOS device |
| Startup time | Near-instant after the first compile | Seconds to a couple of minutes to boot |
| Update speed | Reflects most edits within a second or two on save | Requires a rebuild and reinstall to pick up changes |
| Scope | One page's `build()` method at a time | The whole app, including navigation between pages and abilities |
| Runs your `EntryAbility` lifecycle | No | Yes |
| Native code / platform APIs | Not available (sandboxed renderer) | Fully available |
| Network, filesystem, sensors | Not reliably reflected | Fully available |
| Multi-device comparison | Several device profiles side by side, in one view | One virtual device per running emulator instance |
| Disk/resource cost | Negligible | About 2 GB per downloaded system image, about 12 GB to run it |
| Covered in | [Using the Previewer](first-app.md#using-the-previewer) | [Emulator](emulator.md) |

## When to Reach for Each

**Use the Previewer** while iterating on layout and styling — adjusting padding, colors, component structure, or `@State` initial values. It gives feedback almost as fast as you can save the file, which makes it the right tool for the bulk of day-to-day UI work. See [Live Updates](first-app.md#live-updates) and [Multi-Device Preview](first-app.md#multi-device-preview).

**Use the Emulator** once you need to verify something the Previewer cannot simulate: navigation between pages, ability lifecycle callbacks, permission prompts, background tasks, real network/file/sensor access, or animations and gestures. It is also the only option for debugging or profiling, since only a running app process can be attached to — see [Debugging and Profiling](first-app.md#debugging-and-profiling).

## Interactive Preview Is Not an Emulator Substitute

The Previewer's **Interactive Preview** mode lets you click, tap, and scroll inside the rendered page, which can feel similar to running the app. It only exercises the current page's own state, though — it does not launch your `EntryAbility`, and it cannot represent flows that span multiple pages or abilities.

!!! warning "Don't skip real verification"
    As noted in [When to Stop Trusting the Previewer](first-app.md#when-to-stop-trusting-the-previewer), the Previewer is a productivity tool, not a substitute for testing on a real target. Always validate on an emulator or [physical device](real-device.md) before considering a feature done, especially anything touching permissions, sensors, background tasks, or performance.
