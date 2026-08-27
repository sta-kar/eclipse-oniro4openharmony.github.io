# Build Variants and Signing

To distribute an application outside DevEco Studio's Run and Debug workflow, you need a signed `.hap`. An `.app` file is a distribution archive that can contain multiple HAPs and HSPs; it is not installed directly with `hdc`.

## Debug vs. Release

By default, running or debugging from the IDE produces a **debug** build: automatically signed with a debug certificate so it can be installed on your own emulator/device, but not meant for distribution.

A **release** build is suitable for distribution or publication. It is optimized and signed with a certificate that persists across builds so that updates are trusted as coming from the same source.

Which variant gets built is controlled by the **Build Variant** selector, plus the products/targets declared in the project's `build-profile.json5` files (see [Project Structure](../../create-your-first-app/project-structure.md)).

## Signing Configurations

DevEco Studio supports two signing approaches:

### Automatic Signing (recommended for getting started)

1. Go to **File → Project Structure → Signing Configs** (path may vary slightly by version).
2. Enable **Automatically generate signing configuration**.
3. Sign in with your Huawei/HarmonyOS developer account when prompted.

DevEco Studio then generates a keystore, certificate, and provisioning profile for you and wires them into `build-profile.json5` automatically. This is the fastest path and is sufficient for local testing and most individual development.

### Manual Signing

Needed for CI pipelines, team-shared release certificates, or when a specific provisioning profile (with particular permissions/ACLs) must be used.

1. Generate a private key and CSR: **Build → Generate Key and CSR**, or via `keytool` directly if you need full control over the parameters.
2. Apply for/download a certificate and provisioning profile from the developer console using that CSR.
3. In **Project Structure → Signing Configs**, point to the `.p12`/keystore file, the certificate, and the profile, and supply the store/key passwords.
4. Reference this signing config from the relevant product entry in `build-profile.json5`.

!!! warning "Warning"
    Never commit a keystore file or its passwords. Store them in a secrets manager or CI-only environment variables, and keep only a *reference* (path/alias) in version control — see [Version Control](version-control.md) for a `.gitignore` starting point.

## Generating a Package

Once a signing configuration is in place:

* **Build → Build Hap(s)/APP(s) → Build Hap(s)** — produces a `.hap` for the current module/product.
* **Build → Build Hap(s)/APP(s) → Build APP(s)** — produces an `.app` bundle if your product is configured to build one (used for multi-HAP distribution).

Build output appears under the module's `build/` directory, and the **Build** tool window (`Alt+0`) shows progress and any failures.
