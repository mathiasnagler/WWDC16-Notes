# 705 - How iOS Security Really Works

- Attackers: Criminals, Business copetitors, Service Providers, Nation states, Partners (e.g. Family, ...)
- iOS Security Pillars:
    - iOS Platform Security
    - Users Upgrading their Software
    - Developer Building Secure Apps

## Platform Security

1. Secure Boot:
    - Trust built from silicon up (Boot ROM holds public key)
    - Every boot step (and in conclusion every software that is used during boot) is signed by Apples public key
    - All Keys are managed by Apples (No 3rd parties involved)
    - Software updates are authorized individually for each device (no installation of older / less secure versions possible)
    - Not possible to copy an old version of iOS to another device
2. Data Protection:
    - User data is encrypted at rest with keys derived from the users password
    - Entangled with hardware key in SEP (not possible to guess passwords offline, only on device, device can limit attempts)
    - SEP refuses to unlock after more than 10 incorrect password attempts
    - Core Crypto libs are public for review
3. Sandboxing
    - Isolating data between apps 
    - Reducing harm from developer mistakes (like an Airbag)
4. Code Signing
    - Prevents code execution from attackers
    - Covers not just the OS, but every app that runs
5. Touch ID
    - Average user unlocks device 80x per day
    - Fingerprint is directly transmited to the secure enclave via an encrypted link (never made available to the application processor)
    - Passcode Usage increased (from 50 to 90%)

## Users upgrading their Software

- Smaller install footprint with iOS 9
- Better UX (e.g. Update Dialog)
- 84% are on iOS 9

## Developers Building Secure Apps

- App-Transport-Security
    - Required by AppStore at end of 2016
    - TLS v1.2 (exceptio for already encrypted bulk data -> media streaming) 
- Touch ID
- "You are responsible for 3rd party code you include in your apps"
- Kepp 3rd party code current! (Example: AFNetworking SSL Pinning vulnerability)

## iOS Security Metrics

- No iOS malware at scale (since a decade)
- Recent Jailbreaks need to find 5-10 vulnerabilities (much higher as on any platform)
- $1M for untethered iOS jailbreak
