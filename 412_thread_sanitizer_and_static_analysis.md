# 412 - Thread Sanitizer and Static Analysis

## Sanitizers

* Sanitizers find bugs at Runtime
* Low overhead at Runtime
* Address Sanitizer (**ASan**) introduced in Xcode 7
* Address Sanitizer has fill Swift support with Xcode 8
* Thread Sanitizer (**TSan**) new in Xcode 8
 * Detects use of unititialized mutex
 * Detects thread leaks
 * Detects multiple threads locating the same memory address (ex: Race conditions)
 * Enable in Scheme -> Run -> Diagnostics
 * Detected issues displayed beside build errors and warnings
 * **TSan** provides historical Stack Trace of time the issue occurred
 * Possibility to break on every issue or recording issues
 * **TSan** builds contain special instrumentation library
 * `xcodebuild -enableTrheadSanitizer YES` for command line builds
 * Supported on 64-bit simulators only
 * Instruments **every** memory access, so it can find (most) races
 * Run **all** tests with **TSan** turend on
 * Timing does not matter for **TSan**, so it can find hard to reproduce issues
* Do not build your own synchronization methods, instead use
 * GCD (preferred)
 * `pthread_mutex_lock()`
 * `os_unfair_lock` (instead of `OSSpinLock`)

---
## Static analyzer (new rules)

### Missing Localizibility
* Detects non-localized user-facing strings (enabled by default)
* Detects missing comments for localization (disabled by default)
* Can be configured in build settings

### Instance Cleanup
* Warns about over-releases in MRC code in `-dealloc`
* Warns about under-releases in MRC for retain or copy properties in `-dealloc`
* **Just use ARC instead**

### Nullability Violations
* Use nullablity annotations
* Detects nullability violations in Objective-C code
