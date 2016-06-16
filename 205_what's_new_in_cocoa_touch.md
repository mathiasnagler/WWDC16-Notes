## 205 - What's New in Cocoa Touch

* `UIGraphicsRenderer` new in iOS 10
* Accessibility Inspector audits to detect accessibility issues
* `SFSpeechRecognizer` for speech-to-text recognition
* Semantic tagging of text fields to get better quick type suggestions
* Dynamic Type Content size is now a trait
* `adjustsFontForContentSizeCategory` = full automatic support for Dynamic Type
* TabBar supports changing badge colors, tint colors, text attributes
* `UIPreviewInteraction` to create custom Peek and Pop UI(?) / Animations
* `UIRefreshControl` supported in `UIScrollView` (and thus in all subclasses)
* Automatic self-sizing cells without manually calculating estimated cell size
* Support for paging for `UICollectionView`
* Smooth scrolling for `UICollectionView` and `UITableView`
 * Cell prefetching (automatic when built with iOS 10 SDK)
 * Data prefetching through new protocol method for things like network requests or CoreData fetches
* `UIViewPropertyAnimator` is new animation APIs
 * Interruptible
 * Scrubbable
 * Reversible
 * Rich timing feature
 * Fully dynamic
 * Integrated in ViewController Transition System
* `openURL` is now asyncronous and completion block receives `didOpen`
* "Pin" `NSManagedObjectModel` in UI while its updated in background queue
* `CloudKit` now supports record sharing
* `UICloudSharingController` to manage `CloudKit` record sharing
* `NSUserActivity` now supports locations
* App can continue Spotlight searches through `CoreSpotlightContinuation`
* App can use `CoreSpotlight` to search indexed data
* User Notifications
 * Feature parity between remote and local notifications
 * unified code path for remote and local notifications
 * In-App presentation of notifications possible
 * React to notifications **before** user sees it
 * Custom views in Notifications (non-interactive)
