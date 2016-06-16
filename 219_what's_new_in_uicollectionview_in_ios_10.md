## 219 - What's New in UICollectionView in iOS 10

### Smooth scrolling

* Until now cells have been configured "just in time"
* `UICollectionView` had to load a whole row of cells in one frame (**in 16.67 ms!**)
* Load peaked in frames that needed new cells while nearly no load in between
* New API spreads work over time and flattens peaks
* Lifecycle **before** iOS 10
 * `prepareForReuse`
 * `cellForItemAtIndexPath`
 * `willDisplayCell` (same frame as cellForItemAtIndexPath)
 * `didEndDisplayingCell`
 * cell enters reuse queue
* Lifecycle on iOS 10
 * `prepareForReuse`
 * `cellForItemAtIndexPath` called earlier, spread over multiple frames for multi-cell rows
 * `willDisplayCell` in later frame than `cellForItemAtIndexPath`
 * `didEndDisplayingCell`
 * cell **does not** become reusable right away (in case user scrolls in other direction)
* Cell pre-fetching is free (no code change needed) and enabled by default
* `collectionView.isPrefetcingEnabled = false` to opt out of new behaviour
* Heavy lifting should be done in `cellForRowAtIndexPath`
* Do minimal work in `willDisplayCell` and `didEndDisplayingCell`
* For loading really heavy stuff (`NSManagedObjects`, `Image Decoding`, `Disk access`, etc) --> `UICollectionViewDataSourcePrefetching`
 * `collectionView(_: prefetchItemsAt:)`
 * `collectionView(_: cancelPrefetcingForItemsAt:)` (optional)
 * Provides hint for when to load content
 * Work should be done in background queue using GCD or NSOperationQueue
 * Pre-Fetching is an adaptive technology that does additional work in time with low load
 * If load is too high (for example while **very** fast scrolling) no prefetching will be done
 * Also available for `UITableView`

---
### Improvements to self-sizing cells

* Full support in `UICollectionViewFlowLayout` (already available in iOS 9)
 * set `estimatedItemSize`
 * Three options: Autolayout, `sizeThatFits()`, `preferredLayoutAttributesFittingAttributes()`
* Setting an `estimatedItemSize` can be difficult
* **New In iOS 10:** `estimatedItemSize = UICollectionViewFlowLayoutAutomaticSize`
 * `CollectionView` will calculate `estimatedItemSize` based on already displayed cells
 * Best when cells have similar `width` or `height`

---
### Interactive reordering

* Initially introduced in iOS 9
 * `beginInteractiveMovementForItem(at indexPath:)`
 * `updateInteractiveMovementTargetPosition(_ targetPosition:)` on each update
 * `endInteractiveMovement()` when reordering finishes successful
 * `cancelInteractiveMovement()` available
 * `installsStandardGestureForInteractiveMovement` makes this really easy for `UICollectionViewController`
* iOS 10 adds paging support
 * `isPagingEnabled` to control this
 * same APIs as in iOS 9
 * "Homescreen-Style" reordering experience

---
### UIRefreshControl

* Supported in `UIScrollView`
* `UITableViewController` no longer necessary for this --> `UITableView` is enough as it's a `UIScrollView` subclass
