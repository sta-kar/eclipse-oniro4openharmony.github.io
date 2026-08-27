# Building & Running

## Core Workflow

The main development workflow consists of the following steps:

1. Generate a signing configuration if you have not already done so.
2. Build your application.
3. Connect to the emulator if it is not already connected.
4. Install your application.
5. Optionally, launch it remotely.

=== "Oniro IDE"

    Use buttons provided by the extension:

    <div style="text-align:center">
        <img src='../images/build.png'>
    </div> 

=== "Oniro App Builder"

    Use the following commands:

    1. `oniro-app sign`
    2. `oniro-app build`
    3. `oniro-app emulator connect`
    4. `oniro-app app install`
    5. `oniro-app app launch`

## HiLog

HiLog is the log system OpenHarmony apps use.

=== "Oniro IDE"

    Open the `HiLog viewer` tab. You can filter the log by:

    - Process ID
    - Severity
    - Tag
    - Message

    <div style="text-align:center">
        <img src='../images/hilog_viewer.png'>
    </div> 

    When choosing process ID, the extension will show you running apps.

    <div style="text-align:center">
        <img src='../images/pid_picker.png'>
    </div> 

=== "Oniro App Builder"

    `oniro-app watch` lets you collect HiLog lines. The available arguments are:

    | Argument | Description |
    | --- | --- |
    | `--log <pattern>` | Only log lines matching the given regex are displayed. |
    | `--for <ms>` | Duration to watch in milliseconds, defaults to 10000. |
    | `--bundle <bundle>` | Filter to a specific bundle. |
    | `--device <serial>` | Choose what device to listen to. |
    | `--no-dedup` | Oniro App Builder automatically hides consecutive duplicate lines. Use this argument to disable this behavior. |
    | `--json` | Emit the entries as JSON. |

## Additional App Builder Commands

Oniro App Builder provides other tools for debugging and working with AI agents:

| Command | Description |
| --- | --- |
| `oniro-app screenshot` | Takes a screenshot. |
| `oniro-app dump` | Dumps the device state as JSON. |
| `oniro-app lint` | Runs the OpenHarmony code linter. |
| `oniro-app gesture` | Simulates touch gesture. |
| `oniro-app input` | Simulates touch input. |
