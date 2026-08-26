<!-- Staging file: merge into first-app.md, "Creating Your First Project" section, as a step after project creation (Click Finish). Source: create-your-first-app/create-template.md, step 6. -->

## Targeting Oniro/OpenHarmony

Recent DevEco Studio versions create a HarmonyOS project by default, even when the eventual target is Oniro/OpenHarmony. To retarget the generated project:

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

!!! note
    If the target is a HarmonyOS device, such as the HUAWEI WATCH 5, rather than an Oniro/OpenHarmony device, do not change `runtimeOS` to `OpenHarmony` — use the SDK and runtime that match that device.
