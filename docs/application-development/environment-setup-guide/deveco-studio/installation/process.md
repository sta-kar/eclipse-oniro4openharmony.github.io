# Process of Installation

**DevEco Studio** is an integrated development environment (IDE) based on IntelliJ IDEA, tailored for building OpenHarmony applications. It provides integrated tools for coding, debugging, and managing dependencies, making it easier to develop, test, and deploy apps for the OpenHarmony and Oniro platforms.

## Developer Account

!!! note
    For application development, developer verification is not required.

Before downloading DevEco Studio, you need a Huawei account. For details on registration and identity verification, see:
[HUAWEI ID Registration and Verification | HUAWEI Developers](https://developer.huawei.com/consumer/en/doc/start/registration-and-verification-0000001053628148)

In simple terms, anyone can register for an individual developer account, whether they choose to verify their identity or not. However, certain permissions reportedly require identity verification using an ID document.

According to information from the Huawei developer forum, verified developers gain access to more development resources, training materials, and market promotion. Moreover, only verified developers are allowed to publish applications.

Enterprise developers receive a broader range of services compared to individual developers. Here's a breakdown:

* Individual Developers: App Market, Themes, Product Management, Account, PUSH, New Game Pre-order, Interactive Comments, Social, HUAWEI HiAI, Watch App Market, etc.

* Enterprise Developers: App Market, Themes, Initial Release, Payment, Game Packages, App Market Promotion, Product Management, Games, Account, PUSH, New Game Pre-order, Interactive Comments, Social, HUAWEI HiAI, Watch App Market, Sports & Health, Cloud Testing, Smart Home, etc.

## Download

The latest version of DevEco Studio can be downloaded from the [official download page](https://developer.huawei.com/consumer/en/download/).

!!! info
    You need a Huawei account to download.

<img src='../../images/windows_download.png' alt="DevEco Studio download page listing the Windows, Mac (X86), and Mac (ARM) installers">

=== "Windows"
    Download the Windows installer (`.exe`, listed as "DevEco Studio for Windows").

=== "macOS"
    Download the build matching your Mac's chip: **Mac (X86)** for Intel Macs, or **Mac (ARM)** for Apple Silicon (M-series).

## Step-by-Step Installation

=== "Windows"
    After the download completes, run the installer.

    Keep clicking `Next` until the **Choose Install Location** step.
    Specify the desired installation path by clicking `Browse...` if necessary — the installer shows the space required alongside the space available on the selected drive — and then click `Next`.
    <img src='../../images/windows_setup1.png' alt="Choose Install Location step, showing space required and space available">

    >**Note:**
    Ensure that you delete all files from the previous installation path before proceeding if this is not your first installation.

    In the **Installation Options** step, keep `Create Desktop Shortcut` checked. Also check **Add "bin" folder to the PATH** if you want to invoke DevEco Studio's bundled command-line tools from any terminal; this option requires a restart to take effect. Adding **"Open Folder as Project"** to the Explorer context menu is optional.
    <img src='../../images/windows_setup2.png' alt="Installation Options step: desktop shortcut, PATH variable, and context menu checkboxes">

    In the **Choose Start Menu Folder** step, keep the default settings and click `Install`.
    <img src='../../images/windows_setup3.png' alt="Choose Start Menu Folder step with the Install button">

    DevEco Studio bundles its own OpenJDK, so no separate JDK install is required for basic use.

=== "macOS"
    Open the downloaded `.dmg` file, then drag **DevEco-Studio** into the **Applications** folder shown in the same window.
    <img src='../../images/macos_installation.png' alt="DMG window: dragging DevEco-Studio into the Applications folder">

    Wait for the copy to finish, then eject the mounted disk image.

    On first launch, macOS Gatekeeper may block the app since it was downloaded from outside the App Store — if so, go to **System Settings → Privacy & Security** and click **Open Anyway**.

## Environment Configuration

### OpenHarmony Version and API Level Reference

Before setting up your development environment, it's important to understand the relationship between OpenHarmony system versions and their corresponding API levels. This mapping helps you choose the right API version for your target OpenHarmony system.

<div style="width:100%;box-sizing:border-box; display:flex; justify-content:center;">
  <div style="width:100%; max-width:720px; box-sizing:border-box;">
    <table style="width:100%; table-layout:fixed; border-collapse:separate; border-spacing:0; border:1px solid #e6e6e6; border-radius:6px; overflow:hidden;">
      <thead style="background:#fafafa;">
        <tr>
          <th style="text-align:left;padding:12px 14px;white-space:normal;font-weight:600;border-right:1px solid #f0f0f0;">Version</th>
          <td style="text-align:center;padding:12px 10px;">4.0</td>
          <td style="text-align:center;padding:12px 10px;">4.1</td>
          <td style="text-align:center;padding:12px 10px;">5.0.0</td>
          <td style="text-align:center;padding:12px 10px;">5.0.1</td>
          <td style="text-align:center;padding:12px 10px;">5.0.2</td>
          <td style="text-align:center;padding:12px 10px;">5.0.3</td>
          <td style="text-align:center;padding:12px 10px;">5.1.0</td>
          <td style="text-align:center;padding:12px 10px;">5.1.1</td>
          <td style="text-align:center;padding:12px 10px;">6.0</td>
          <td style="text-align:center;padding:12px 10px;">6.1</td>
        </tr>
      </thead>
      <tbody>
        <tr>
          <th style="text-align:left;padding:12px 14px;white-space:normal;background:#fff;font-weight:600;border-right:1px solid #f0f0f0;">API Level</th>
          <td style="text-align:center;padding:12px 10px;">10</td>
          <td style="text-align:center;padding:12px 10px;">11</td>
          <td style="text-align:center;padding:12px 10px;">12</td>
          <td style="text-align:center;padding:12px 10px;">13</td>
          <td style="text-align:center;padding:12px 10px;">14</td>
          <td style="text-align:center;padding:12px 10px;">15</td>
          <td style="text-align:center;padding:12px 10px;">18</td>
          <td style="text-align:center;padding:12px 10px;">19</td>
          <td style="text-align:center;padding:12px 10px;">20</td>
          <td style="text-align:center;padding:12px 10px;">23</td>
        </tr>
      </tbody>
    </table>
  </div>
</div>

!!! tip "API Level Selection"
    When developing applications, select the API level that corresponds to your target OpenHarmony system version. For example, if you're targeting OpenHarmony 6.1, use API Level 23.

### DevEco Studio Initial Setup

When you run `DevEco Studio` for the first time, the setup wizard will appear. This first-run wizard is the same on Windows and macOS — the screenshots below are from Windows, but macOS shows the same dialogs (just with macOS-style window chrome instead of the Windows title bar).
<img src='../../images/deveco_welcome_screen.png'>

!!! note "macOS Gatekeeper / User Agreement"
    On macOS, before the wizard below appears you may first see a **User Agreement** dialog asking you to accept the "HarmonyOS Software License and Service Agreement" — accept it to continue. If macOS blocked the app from opening at all, see the Gatekeeper note in [Step-by-Step Installation](#step-by-step-installation) above.

Select `Do not import settings` (unless migrating from a previous install).
<img src='../../images/image8.png'>

!!! tip "Behind a proxy?"
    If your network requires a proxy, configure it now under **Settings → Appearance & Behavior → System Settings → HTTP Proxy** — otherwise the steps below may fail to download SDK components.

    === "Windows"
        Reach Settings via **File → Settings**.

    === "macOS"
        Reach Settings via **DevEco Studio → Settings** in the menu bar (or the `⌘,` shortcut).

The environment configuration is now complete.
<img src='../../images/image14.png'>

!!! note "Install Relevant APIs"

    <div style="display:flex;gap:20px;align-items:flex-start;flex-wrap:wrap;" markdown>
      <div style="flex:1 1 360px;font-size:0.9rem;line-height:1.9;" markdown>

      To run applications for OpenHarmony, you also need to install the relevant APIs.

      Open **DevEco Studio** and go to:
      `Settings` → `OpenHarmony SDK`, check the API version(s) you need and click **Apply** to download.

      You don't strictly have to do this ahead of time — if a project needs an API version you haven't installed yet, DevEco Studio will prompt you to download it automatically the first time you build or run the app.

      > 💡 If you're using **DevEco Studio 6.1**, select **API Version 23** for development.
      >
      > Refer to the version mapping table above to choose the appropriate API level for your target OpenHarmony system.

      </div>

    </div>

    ![OpenHarmony SDK settings page listing API versions 23, 20, 18, and 15 with their ArkTS/JS/Native/Previewer/Toolchains components](../../images/deveco_api_screen.png){: .center}

With the developer account set up, DevEco Studio installed, and the environment configured, you're ready to explore the IDE itself — continue to [Workflow](../workflow.md).
