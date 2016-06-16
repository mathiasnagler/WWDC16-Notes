## 406 - Optimizing App Startup Time

TL;DR
* Measure launch times with `DYLD_PRINT_STATISTICS`
* Reduce launch time by
 * Embedding fewer dylibs
 * Consolidating Objective-C Classes
 * Eliminating static initializers
* Use more Swift
* `dlopen()` is discouraged

---

* Launch should be faster than launch animation
* 400ms is a good target for launch time
* After **20s** the os will kill the application
* Test on slowest supported device
* Warm launch
 * App already in memory
* Cold launch
 * app not in kernel buffer cache
 * Cold launch is more important to Measurements
 * **Reboot** before measuring cold launch time
* `DYLD_PRINT_STATISTICS` environment variable to measure launch time
 * Available in Seed 2 of Xcode 8
 * Debugger time will be substacted (measured time will be shorter, but is correct)
* Embedded dylibs are expensive!
 * Use fewer dylibs
 * Merge existing dylibs
 * Use static archives
 * Lazy load via dlopen() (slower overall!)
 * ~ 6 dylibs is good target
* Reduce Objective C metadata (Classes, selectors and categories)
 * try to stay below 5000 classes and categories
 * Swift should launch faster (better inlining, fewer `__DATA` pointer fixups needed)
* Initializer time
 * `+load` --> replace with `+initialize`
 * Rewrite in Swift
 * Never call `dlopen()` in initializers --> turns on locking
 * Do not start threads in initializers
