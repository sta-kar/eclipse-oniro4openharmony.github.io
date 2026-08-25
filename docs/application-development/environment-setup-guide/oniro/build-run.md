# Building & Running

## Core Workflow

The main development workflow consists of the following steps:

- Generate a signing configuration if you have not already done so.
- Build your application.
- Connect to the emulator if it is not already connected.
- Install your application.
- Optionally, launch it remotely.

=== "Oniro IDE"

    Use buttons provided by the extension:

    <div style="text-align:center">
        <img src='../images/build.png'>
    </div> 

=== "Oniro App Builder"

    Use the following commands:

    - `oniro-app sign`
    - `oniro-app build`
    - `oniro-app emulator connect`
    - `oniro-app app install`
    - `oniro-app app launch`

## HiLog

HiLog is the log system OpenHarmony apps use.

=== "Oniro IDE"

    Open the `HiLog viewer` tab. You can filter the log by:

    - Process ID
    - Severity
    - Tag
    - Message

    > IMAGE HERE

=== "Oniro App Builder"

    `oniro-app watch` let's you collect HiLog lines. The passable arguments are:

    | Argument | Description |
    | --- | --- |
    | `--log <pattern>` | Only log lines matching the given regex are displayed. |
    | `--for <ms>` | Duration to watch in milliseconds, defaults to 10000. |
    | `--bundle <bundle>` | Filter to a specific bundle. |
    | `--device <serial>` | Choose what device to listen to. |
    | `--no-dedup` | Oniro-app autmatically hides consecutive dupliate line. Use this argument if you want to disable this behaviour.|
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
