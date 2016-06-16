# 401 - What's New in Xcode App Signing

- New: Automatic & Manual Signing (=> Xcode doesn't create Profiles)
- 3 Things to sign an app: Certificate, Profile, Entitlements
- Pre-Xcode 8: Develop account has a limit of one cert => Copying private key to other machines is necessary
- Xcode 8: Multiple certs (applies only to develop certs)
- Distribution Certificates still have a limit of 1
- Created through Xcode 8 or Develop Portal
- New Certificates are Backwards Compatible
- No more Fix-Issue Button
- **Automatic Signing:**
    - Can be enabled under "General" (On by default)
    - Creates signing Certificates automatic
    - Creates App IDs Profiles automatic
    - Prompts if new device should be registered
    - Signing Report (Log) is generated: Reports navigator
    - Select Team on creating new projects
    - Updates profiles automatic when capabilities change
    - Only for Develop Signing: Distribution is not modified by automatic signing
    - Works only with Xcode created Profiles
- **Customized Signing:**
    - Full Control over signign: Xcode never changes signing settings
    - Enabled by unchecking Automatic-Signing
    - Can completly configured under General-Tab
    - Useful if project uses CI
    - Error reporting under General-Tab (e.g. Problems with entitlements)
    - Limited to manually created profiles (e.g. over portal)
    - New build setting: `PROVISIONING_PROFILE_SPECIFIER`
    - Profiles referenced by name instead of unique id
    - No more project updates caused by Profile-Changes (!!!)
    - Safe-to-use capabilities tab: no changes