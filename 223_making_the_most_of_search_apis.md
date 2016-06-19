# 223 - Making the Most of Search APIs

* Spotlight now present in Notification Center --> Faster to get to, access from within an app
* Spotlight now available on Lockscreen (Public results from internet)
* Spotlight results can support 3D Touch
* Query Suggestions in Quick Type based on past queries

## Search APIs
1. `CoreSpotlight` (any app content)
2. `NSUserActivity` (viewed app content)
3. Universal Links (app content on the web)

---
## New features

### Continue Search in App
* Option to present "Search in App" in Spotlight result list
* Tapping launches app and passes in search query, so search can be continued inside the app

### `CoreSpotlight` Search API
* Use Spotlight index for searches inside an app

### Differential Privacy
* Estimate popularity of deeplinks via differential privacy

### Visual Preview in Web Markup Tool

---
## Steps and best practices

### Indexing content

**CoreSpotlight**
* `CoreSpotlight` is on device and supports file protection
* Supports private data because of file protection
* App is in charge
* Use `CSSearchableItemAttributeSet`, `CSSearchableItem` and `CSSearchableIndex` to add data to the Spotlight index
* Deleting items from index is possible through
  * Unique identifier
  * Domain identifier (attribute shared across multiple items)
  * All items
* `indexDelegate`
  * can be used to start indexing after backup restore for example
  * Reindexing when item expires (expiration date)
  * `reindexAppSearchableItemsWithAcknowledgementHandler` for adding everything to index or full rebuild
  * `reindexSearchableItemsWithIdentifiers` for reindexing single items (ex: expired)
* Use client state for asynchronous updates
  * Allows to keep datastore and Spotlight in sync without blocking
  * Opaque token stored in Spotlight's index
  * Used with journals or database annotations
  * Create a named `CSSearchableIndex`
  * `index.beginBatch()`
  * Index our journal or database
  * `index.endBatch(withClientState: completionHandler:)`
  * store client state on your data items
  * fetch client state and check which items you need to index or update
* Use batching
* Don't block the main thread, index on background thread
* CoreSpotlight Extensions
  * Extension can index while app is not running (!)
  * Use shared app group to make app content available to extension
  * Other possiblities: Background fetch, silent remote notifications
* Set `contentURL` to Universal link web page URL to prevent duplicates


**NSUserActivity**
* Use NSUserActivity if the user *might* want to come back to what he does
* `userActivity.eligibleForSearch` to enable spotlight indexing
* `userActivity.relatedUniqueIdentifier` if user activity duplicates `CSSearchableItem` to prevent duplicate search results
* `weakRelatedUniqueIdentifier` new in iOS 10 to bind `NSUserActivity` weakly to a `CSSearchableItem`
* `domainIdentifier` now available to bulk delete `NSUserActivity`
* Set `webpageURL` to Universal link web page URL to prevent duplicates

**Universal Links**
* Index public content from the web
* Can be displayed without the app installed
* Steps
  1. Allow indexing by Applebot
  2. Support Universal Links and Smart App Banners
  3. Markup website with schema.org and Open Graph
  4. Update app to properly open deep Links
  5. Test URLs with App Search API Validation Tool

### Rich presentation
* Provide a good thumbnail
* Meaningful tilte
* suitable content description
* metadata (rating, dates, etc) when available

### Launching into app

* `application(_: continueUserActivity: restorationHandler)` will be called
* `userActivity.actionType` indicates wether user tapped on `CoreSpotlight`, `NSUserActivity` or Universal link result
* `userActivity.userInfo` contains all available properties
* For Universal links: `userActivity.wepPageURL`
* `CoreSpotlightContinuation` enables search continuing in app
* `userActivity.activityType == CSQueryContinuationActionType` --> Invoke apps own search UI

### `CoreSpotlight` Search API

* Uses data already indexed for `CoreSpotlight`
* Provides consistency
* Avoids overhead
* Powerful query syntax
* Escape query string (user input!)
* `CSSearchableQuery`
